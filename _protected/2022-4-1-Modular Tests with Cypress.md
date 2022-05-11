[//]: # "@formatter:off"
---
layout: encrypted
title: "Modular Laravel Packages with Cypress Testing"
date: 2022-03-30 19:36
category: PRJ701
image: assets/images/cypress_laravel.png
featured: true
hidden: false
permalink: /:categories/:title
---
[//]: # "@formatter:on"

After discovering Cypress last week, I am excited to continue to use it to test my Laravel packages. While I was able to
quickly add it into a monolith last week and run some basic tests, I still needed to confirm weather I could use it in
packages.

So the initial test would be composed of 2 parts

* A Module that would contain tests
* A Laravel application in which I would pull the package into

As much as a test first approach would be best, I wanted to build something quickly as a proof of concept rather than
having the same issues that I ran into last week. The only module that I have worked with and have familiarity with is
the employee module that I built during my internship. I figured that I could use that as the proof of concept.

![employee module](/assets/images/encompass_employee_module.png)

To get started, I needed the Laravel application in which I would pull the package into

```
laravel new test
composer require laravel/jetstream
php artisan jetstream:install inertia
npm install
npm run dev
```

At this point I needed to set the environment variables of the Laravel app to a database that I could use. Once set up I
could then run the migrations.

```bash
createdb test
php artisan migrate
```

The laravel application would also require cypress so that it could run the tests.

```bash
npm install cypress --dev
```

In searching 'cypress laravel', in order to discover if someone else had come across issues or a guide on what to do I
found the [laracasts/cypress](https://github.com/laracasts/cypress) repository. It provides some useful helpers for
testing a laravel application. To set it up I ran:

```bash
npm install cypress --save-dev && npx cypress open
```

This installs cypress and opens the cypress browser, which adds the cypress directory to the project and adds a
cypress.json configuration file. With cypress installed I then ran:

```bash
composer require laracasts/cypress --dev
php artisan cypress:boilerplate
```

The boilerplate command moves the cypress directory into the test directory and adds a bit more boilerplate code. I set
the baseUrl in the cypress.json to the name of the application `https://test.test`. Having previous set up Laravel
valet, I wouldn't need to run anything for the application to hosted locally.

With the laravel application set up, I could then install the module into it. I worked on a new git branch of the module
that I could install in the application, as is best practice with a new feature. I imported the module into the
application and updated the dependencies in the composer.json file.

```composer.json
 "require": {
        ...
        "snapithd/encompass-employee-module": "dev-behaviour-tests"
    },
    "repositories": [
        {
            "type": "path",
            "url": "../encompass-employee-module"
        }
    ],
```

I then downloaded the module into the vendor directory with `composer update`.

With the package in the vendor directory, I still needed to set a few things up. I knew that there would be a problem
with running the tests in the module as it didn't have laravel to act as a server. Additionally, I didn't have the tests
in the test app. So as part of the modules install command, I created symlinks between the modules' cypress test folder
and the test app's cypress test folder.

```php
$this->installSymbolicLinkAfter(
    "public_path('storage') => storage_path('app/public'),",
    "resource_path('js/Pages/Encompass/EmployeeModule') => base_path('vendor/snapithd/encompass-employee-module/resources/vue'),
    base_path('tests/cypress/integration/EmployeeModule') => base_path('vendor/snapithd/encompass-employee-module/tests/cypress/integration'),
    base_path('app/Models/EmployeeModule') => base_path('vendor/snapithd/encompass-employee-module/src/Models'),"
);
```

With the test folders symlinked, I could then run the tests that were in the module from the test app. Then it occurred
to me as I accidentally ran the tests in the module instead of the test app, does the base application even need
cypress? So I removed cypress from the base application and the test still ran. To confirm my theory, I made a new
laravel application and installed the module into it. This lead me down a rabbit hole....

On installing the module I ran into a problem. As part of the procedure that we had produced to install the module, it
required adding a line to the `webpack.config.js` file. Here is what I had written in the procedure to add the line:

[//]: # "@formatter:off"
```markdown
10. Then install the package resources php artisan encompass-employee-module:install

11. Set symlinks to false in base app webpack.config.js

    module.exports = { 
        resolve: { 
            alias: {
                '@shd-employee-module': path.resolve('vendor/snapithd/encompass-employee-module/resources/vue'),
                '@': path.resolve('resources/js'), 
            }, 
        symlinks: false 
        }, 
    };
```
[//]: # "@formatter:on"

However, on running the installation command gave me the following error:

![encompass install issue](/assets/images/encompass-install-issue.png)

In the laravel application there was no webpack.config.js file. This seemed odd, and I thought that maybe I had done
something wrong during the installation. So I deleted the application and started again. Yet again, there was no
webpack.config.js file. This was a problem. I knew I needed to set the variable `symlinks: false`, and it was done in
the config file. Initially I thought, why don't I just add the file back and carry on. However, I knew the config would
be loaded somewhere, and I didn't want to sweep the issue under a quick fix.

I decided to search through the repositories of the packages that I had used to build the application at that point to
find where the config file was created, and why it was no longer being created. The 3 packages I had to search through
were:

* [laravel/laravel](https://github.com/laravel/laravel)
* [laravel/jetstream](https://github.com/laravel/jetstream)
* [inertia/inertia](https://github.com/inertiajs/inertia)

The laravel repo was my first choice, as it contained the most code. However, since it had no javascript out of the box,
I realized that it couldn't possibly be the problem repository.

I then searched through both the jetstream and inertia repositories to find the config file, or at least where it had
been. I searched through the issues and pull requests using 'webpack' as the search term. I found
a [closed pull request](https://github.com/laravel/jetstream/pull/1011)
in the jetstream repository that mentioned webpack.config.js. It referred
to [another pull request](https://github.com/laravel/jetstream/pull/1009), which specifically states "This PR removes
the webpack.config.js". The reason became apparent when I looked at the code in the pull request. The webpack.config.js
file wasn't doing that much and there was a fluent helper function provided
by [laravel-mix](https://github.com/laravel-mix/laravel-mix) that was being used instead. I checked to see if there was
a fluent assertion in that repo for symlinks, however there was not.

So I turned to google. Using the search term `set symlinks false laravel mix` the third result led me
to [a](https://stackoverflow.com/questions/52206917/get-laravel-mix-to-transpile-js-from-different-path)
stackoverflow question. The second answer with 0 votes to the question
contained [a link to a github issue](https://github.com/laravel-mix/laravel-mix/issues/1327) which
had [a comment](https://github.com/laravel-mix/laravel-mix/issues/1327#issuecomment-352244762) that led me to solving my
problem:

![github comment webpack](/assets/images/github_comment_webpack.png)

So I added `mix.webpackConfig({ symlinks: false })` to the mix.js file in the laravel application. However, it still
didn't work.

![webpack.config.js error](/assets/images/webpack.config_error.png)

In the end I messed around with a lot of different things, tweaking things and trying again. I eventually found a
stackoverflow question with a solution:

```js
mix.js('resources/js/app.js', 'public/js').vue()
    .postCss('resources/css/app.css', 'public/css', [require('postcss-import'), require('tailwindcss'),])
    .alias({
        '@': 'resources/js',
        '@shd-encompass-employee-module': path.resolve('vendor/snapithd/encompass-employee-module/resources/vue'),
    })
    .webpackConfig({
        resolve: {
            symlinks: false
        }
    });

if (mix.inProduction()) {
    mix.version();
}
```

I didn't bother rewriting the installation script yet because I'm not sure that this is the exact solution.

Anyway, where was I oh testing cypress without installing it in laravel. When I went to run the cypress tests from the
module, they failed to open and run. From what I can gather this is due to the fact that the module does not have all
the necessary elements to run the test, due to it being only part of a full application.

I discussed these findings with the software team during a stand-up the next day. They mentioned that there were some
high level talks about where to run the tests and how to get them to work in the future. My input and feedback was
appreciated and their decisions are yet to be made exactly on what implementation to use.

Overall, the week has been a great one. I learned a lot about dependencies changing their implementation, and how to
resolve those issues. I also learned how to use Cypress to test an application. I'm sure that I could improve some of my
implementations of the tests that I have written, and will endeavour to learn more about Cypress and how to use it to.

