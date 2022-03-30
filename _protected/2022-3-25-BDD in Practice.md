[//]: # "@formatter:off"
---
layout: encrypted
title: BDD in Practice
date: 2022-03-25 10:0
category: PRJ701
image: assets/images/bdd_practice.jpg
featured: true
hidden: false
permalink: /:categories/:title
---
[//]: # "@formatter:on"

After having spent time to learn some theory of BDD, I wanted to apply it in practice in the way in which SnapIT are
looking at moving towards, that being modular. As such, I wanted to first try to install a BDD framework for PHP in a
monolith then, move it into a module.

## PHP BDD Frameworks

I have identified 2 PHP BDD frameworks that I have attempted to install

* [Behat](https://behat.org/)
* [Codeception](https://codeception.com/)

### Behat

I followed the installation instructions at the behat website, and on initial running of the installation command, I ran
into the following issue:

![behat issue 1](/assets/images/behat_install_issue_1.png)

Composer is rather intelligent and will not install packages if there are dependency conflicts or other issues with
packages that are attempting to be installed, and will however roll back to before the installation command is run and
provide feed back to the user as to what happened and to possible fixes/workarounds.

Reading through the output, I though that I may be able to install the dev-master branch in an attempt to get behat to
work, albeit possibly not the best to use in a production environment. On running the installation command, I ran into
another issue:

![img.png](/assets/images/behat_install_issue_2.png)

This proposes an insurmountable issue, due to a major semantic version change to the psr/container package. In searching
the behat github repository, I came across [this pull request](https://github.com/Behat/Behat/pull/1380) of which one of
the creators of symfony made to support psr/container 2.0. At the time of writing, the pull request was open but was not
yet merged. I downloaded the branch that the pull request included and pointed the behat dependency in the composer.json
to the local instance of behat from that pull request branch:

```json
{
  "require": {
    "behat/behat": "dev-master"
  },
  "repositories": [
    {
      "type": "path",
      "url": "../behat"
    }
  ]
}
```

This installed fine, but in when i ran the Initialize command ```vendor/bin/behat --init``` that is in the behat
documentation, and nothing ran. I created the files that the init command was going to make manually, and tried to
execute behat again with the command ```vendor/bin/behat``` but there was no output to the console.

Since this all felt very hacky, and not likely to work for a production environment, I decided to try and install
codeception.

### Codeception

In another laravel installation, I followed the installation instructions
at [Codeception’s website for laravel](https://codeception.com/for/laravel) and again ran into another issue:

![img.png](/assets/images/codeception_issue_1.png)

There were several issues here, the biggest that wouldn’t be able to be resolved is that the PHP version that I am using
currently is 8.1.2 which is incompatible
with [laravel’s minimum PHP version of 8.0.2](https://packagist.org/packages/laravel/laravel). It seemed like there was
no possibility to use a PHP BDD framework in the development lifecycle.

After having these issues, I reached out to the senior developer Isaac, and he offered to jump on a Google meet call to
discuss. I explained the problems that I had encountered and the road blocks that I ran into. While he had no solution
for me, he did discuss a test framework that he had been looking into over the last few weeks
called [Cypress](https://www.cypress.io/).

As we were talking, I looked into the possibility of using cypress for the testing framework with the laravel
application. It seemed entirely possible that it would work, due to
the [Jetstream](https://jetstream.laravel.com/2.x/introduction.html#inertia-vue) stack we were using Vue as a front end.
I look further and wonder if there were BDD frameworks or libraries that I could utilize, and came
across [cypress-cucumber-preprocessor](https://github.com/TheBrainFamily/cypress-cucumber-preprocessor) which took
features written in gherkin and converted them into step definitions which could be written in cypress.

I ended the call and attempted to install Cypress and the cypress cucumber preprocessor into a laravel application, and
it worked. While I did not create any features or write any cypress tests, I felt like I finally had some success.

The next steps will be to see if cypress can work in laravel modules and how to write and cypress tests.