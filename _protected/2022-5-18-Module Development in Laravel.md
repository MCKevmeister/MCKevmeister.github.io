---
layout: encrypted
title: "Module Development in Laravel"
date: 2022-05-18 19:36
category: PRJ701
image: assets/images/modular-monolith.png
featured: true
hidden: false
permalink: /:categories/:title
---

To develop a large-scale application, with the possibility of different user interfaces for different customers, SnapIT is looking for a modular approach to building their applications. The modularization allows for customization for individual customers of the products that will be built, such as calling specific endpoints and passing data to an API in a specific structure. Currently, there is no way to handle adding these changes without adjusting the overall system.

Management at Snap have decided that building another Monolithic application (as 2 of their current products are) is not beneficial and in line with the business strategy, which is moving towards being a software vendor rather than selling directly to the end user. To achieve this strategy, a decomposition strategy must be adopted. There are 2 major decomposition strategies that can be applied in breaking apart a monolith (Newman, 2020):
Migration to microservices
Migration to a modular monolith

Migrating directly into microservices proposes some large challenges, including sending data over a network, managing and deploying several services and building a well abstracted system to perform information hiding through encapsulation. An option is to have microservices as an eventual goal, but use a stepwise approach by first decomposing the system to a modular monolith (Faustino et al., 2022). Sam Newman suggests that migrating to a ‘Modular Monolith’ before further migrating to microservices if necessary is a “Highly underrated option”(Newman, 2020).

Developing Modules in Laravel does not seem to be a new concept. In fact, there are many repositories that are no longer being currently maintained and only work with older version of Laravel. However, I have found 2 possible solutions for modularizing a modern laravel application.

* [nWidart/laravel-modules](https://github.com/nWidart/laravel-modules) (Widart, 2022)
* [spatie/package-skeleton-laravel](https://github.com/nWidart/laravel-modules) (Spatie, 2022)

There is also a website that documents the creation of laravel package (Braun, n.d.). Braun has detailed steps for creating many parts of a laravel module, and includes details for creating these modules with tests. It provides many links to external resources, including the orchestral testbench package, which is the de-faco package writing tests in laravel packages (Laravel Testing Helper for Packages Development, 2022). Laravels own documentation on package creation is available but limited in comparison (Laravel - the PHP Framework for Web Artisans, n.d.-b)

## nWidart/laravel-modules

This repository allows building of modules inside a large laravel application. Each module in this context would have a vertical slice of the system, containing routes, controllers, models, views, and business logic. This stops all the logic being bundled into a single application, leading to a mess of an application(Widart, 2016).

By building inside an existing laravel application, the developer has access to the powerful command line tool, artisan (Laravel - the PHP Framework for Web Artisans, n.d. -a). This package includes it own artisan commands which allow for the creation of new modules, migrating the database migrations in a single module, seeding of the database from a module, among many other useful commands (Artisan Commands - Laravel Modules Docs, n.d.).

After a module is created, it can be published as a php package. These modules can then be installed via the accompanying package [joshbrw/laravel-module-installer](https://github.com/joshbrw/laravel-module-installer) (Brown, 2022), which identifies the packages created with the laravel-module package.

To make a module that would work with the stack that Snap wants to implement, it would make sense to create a custom module generator. This can be done by creating new stub files from which the module generates new modules. The documentation provided by the package outlines the process by which this is done, with explanation of how the command that generates new packages works (Build Your Own Module Generator - Laravel Modules Docs, n.d.)

The only issue with this package is that it would require modification to work with the Inertia/Vue frontends. Out of the box, this package only works with blade template files. There is some discussion in the github issues, with one specifically discussing how to use the inertia/vue stack with this module. Without more community support, Snap would need to commit resources to making this package work with the desired stack.

# spatie/package-skeleton-laravel

This package provides a scaffold for building laravel packages. It includes a configuration script which replaces placeholders in the files of the package to that of the inputs provided by a user. As a github repository, it can be used as a template repository for new packages. Snap could utilize the Spatie laravel package skeleton as a starting point, and only need to modify, remove and add some files and dependencies, specifically for the Vue Inertia stack.

To simplify development, github allows for users to create template repositories. Repositories made from the template include the same directory and file structure. Documentation by github about:

* [Creating a template repo](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository)
* [Creating a repo from template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)

### Foreseen Issues
If Snap created its own package skeleton, dependencies in the skeleton package will need to be kept up to date. A possible solution to this, to watch for changes in the dependencies of these packages and reflect any version bumps to the snap package skeleton. Otherwise, Dependabot could be provided access to the skeleton to keep dependencies up-to-date. (Dependabot S Private Dependencies, 2021).

### Modifications
The skeleton package includes a configuration script, which could be modified to be explicitly for Snap as the vendor, removing unnecessary features of the script and adding additional options. Additional options may include asking the user whether the package would have views or not. Such a feature would allow for selectively installing dependencies, and creating files on an as needed basis, and would remove unnecessary files if not needed.

The installation script in the package skeleton is currently empty. It would make sense to complete this as much as possible. This script would need to include the creation of symbolic links, and publishing any config files, publishing migrations and loading routes.

### Additions

[inertia](https://www.npmjs.com/package/@inertiajs/inertia) - For packages that have views, to incorporate with an inertia/laravel server side the package would require the client-side adapters. The additional configuration files would also be necessary and could be optional as part of the configuration script.

[cypress](https://www.npmjs.com/package/cypress) - For packages that have views, adding support for cypress tests would benefit the creation of those views to ensure they are well tested. Addition of this dependency could be made optional as part of the configuration script, as well as the following cypress dependencies.

[cypress-cucumber-preprocessor](https://www.npmjs.com/package/cypress-cucumber-preprocessor) - This package adds support for “.feature” files that can be used to define the behaviours of the package for cypress tests. This would benefit the ‘double loop’ work flow of behaviour testing and unit testing.

[laracasts/cypress](https://github.com/laracasts/cypress) - This composer package provides helper functions to cypress that are useful such as creating models, refreshing the database, and calling artisan commands. It would be useful to add this to the skeleton package if the package has views, and could be made optional when running the configuration script. As well, this package restructures the organisation of the cypress tests from the root directory, into the test's folder for better file structure.

(possible, but may be unnecessary) [orchestra/canvas](https://packagist.org/packages/orchestra/canvas) - Provides commands for generating code that would normally be provided by artisan commands.

### Removal

[spatie-package-tools](https://github.com/spatie/laravel-package-tools) - This package is too tightly coupled to blade file. Removing this however would require a complete rewrite of the Service Provider, as the package service provider completely relies upon it. A solution to this would be to add a package service provider to the package that could be configured.

[spatie/laravel-ray](https://github.com/spatie/laravel-ray) - While the debug features offered by ray are useful, it may be hard to justify the cost of $71/year if not fully utilized in development. Adds bloat to the package.

## References

Artisan commands - Laravel Modules Docs. (n.d.). Docs.laravelmodules.com. Retrieved May 18, 2022, from https://docs.laravelmodules.com/v9/artisan-commands

Braun, J. (n.d.). Introduction | Laravel Package Development. Laravelpackage.com. Retrieved May 18, 2022, from https://laravelpackage.com/

Brown, J. (2022, May 13). Laravel Module Installer. GitHub. https://github.com/joshbrw/laravel-module-installer

Build your own module generator - Laravel Modules Docs. (n.d.). Docs.laravelmodules.com. Retrieved May 18, 2022, from https://docs.laravelmodules.com/v9/custom-module-generator

Dependabot s private dependencies. (2021, March 15). The GitHub Blog. https://github.blog/2021-03-15-dependabot-private-dependencies/

Faustino, D., Gonçalves, N., Portela, M., & Silva, A. R. (2022). Stepwise Migration of a Monolith to a Microservices Architecture: Performance and Migration Effort Evaluation. ArXiv:2201.07226 [Cs]. https://arxiv.org/abs/2201.07226

Laravel - The PHP Framework For Web Artisans. (n.d.-a). Laravel.com. Retrieved May 18, 2022, from https://laravel.com/docs/9.x/artisan

Laravel - The PHP Framework For Web Artisans. (n.d.-b). Laravel.com. https://laravel.com/docs/9.x/packages

Laravel Testing Helper for Packages Development. (2022, May 17). GitHub. https://github.com/orchestral/testbench

Newman, S. (2020, May 5). Monolith Decomposition Patterns. InfoQ. https://www.infoq.com/presentations/microservices-principles-patterns/

Spatie. (2022, May 18). :package_description. GitHub. https://github.com/spatie/package-skeleton-laravel

Widart, N. (2016, January 7). Writing modular applications with laravel-modules | Nicolas Widart. Nicolaswidart.com. https://nicolaswidart.com/blog/writing-modular-applications-with-laravel-modules

Widart, N. (2022, May 18). Laravel-Modules. GitHub. https://github.com/nWidart/laravel-modules
