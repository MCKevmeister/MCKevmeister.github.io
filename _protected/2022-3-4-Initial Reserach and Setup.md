---
layout: encrypted
title: Initial Research and Setup
date: 2022-03-4 9:27 
category: PRJ701
image: assets\\images\\initial-research.jpg
featured: true
hidden: false
permalink: /:categories/:title
---

## Setup

Snap stores all code on github. To ensure security, there is an organizational policy that requires that all access to
the code be through SSH. The company has provided me with a Mac mini, so configuration of the SSH keys is not a problem.

Fortunately with Mac, I have access to brew. [Brew] is a package manager that is used to install and manage software and
call's itself
"The missing package manager for macOS". Brew runs in the command line and works similar to linux package managers. To
install brew I ran the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### PHP

The main language that I have been specified by the business to focus on is PHP. With brew installed, PHP can be
installed with the following command:

```bash
brew install php
```

Composer is the dependency manager for PHP applications. Again install done though the command line following the
instructions on the [Composer website](https://getcomposer.org/download/).

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

Moving composer to PATH allows global access to the composer command.

```
sudo mv composer.phar /usr/local/bin/composer
```

Laravel is a PHP framework that is used to build web applications. It is an opinionated framework, and provides simple
starter kits for scaffolding an application. To install laravel I ran the following command:

```bash
composer global require "laravel/installer"
```

To create a new laravel application I ran the following command:

```bash
cd ~/sites
laravel new my-app
```

[Jetstream](https://jetstream.laravel.com/2.x/introduction.html) provides implementation for login, registration, email
verification, and session management. The [inertia](https://inertiajs.com/) stack uses Vue as the templating language.
It offeres the power of Vue but removes the complexity of front end routing, and uses Laravel routes to handle the
routing. To add inertia to the laravel app, I ran the following command:

```bash
composer require laravel/jetstream
php artisan jetstream:install inertia
npm install
npm run dev
php artisan migrate
```

This will install the Jetstream package, install the inertia package, install the dependencies for the front end, and
run the migrations for the database.

[Laravel Valet](https://laravel.com/docs/9.x/valet) is used to run Laravel application on a local server. All laravel
applications can be stored in the same directory, and served via:

```bash
cd ~/sites
valet park
```

The laravel application can be accessed via [http://my-app.test](http://my-app.test). The test TLD is used to indicate
that the service is running locally.

At this point, any changes done in PHP will be reflected in the front end. However, changes to the vue files will not
be. To view any changes on the front end rerunning ```npm run dev``` will refresh the front end,
else ```npm run watch``` will watch for changes and recompile the front end.

For writing PHP and Javascript code, I used the [PHPStorm IDE](https://www.jetbrains.com/phpstorm/). I have become
familiar with the JetBrains IDE features over the last few years with different projects and languages. I have found the
IDE to be very useful, and at points I have found it to be a useful learning tool.

For example, learning some git commands at first felt daunting, but the git tab makes understanding commands more
intuitive. When merging changes from different branches, the IDE has a feature that allows me to see the changes in the
files that are being merged, and resolve conflicts. While it would be better to use the command line for git, I have
found the IDE to take a lot of the complexity of getting the commands to work out of the way. Thus, I feel more
comfortable moving forward using git commands as I have a better understanding of what they do.
![git-phpstorm](/assets/images/git-phpstorm.png)

## Research

The company has asked me to figure out how to best implement test practices. As an initial step, I will be conducting
research into testing frameworks and practices that are used in Test Driven Development (TDD). As well, I will be
creating a list of questions for asking internal stakeholder to find out what they are exactly wanting.

Additionally, the company is interested in Modular development, and I will be conducting research into the different ways
of doing this.