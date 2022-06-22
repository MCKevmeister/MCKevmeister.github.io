---
layout: post
title: Review of Develop Assignment
date: 2022-06-21 16:36
category: WEB701
image: assets/images/develop-image.jpg
featured: true
hidden: false
permalink: /:categories/:title


Deploying the website to Heroku was possibly the most challenging part of the project. While there are numerous guides
on how to do this for a Laravel application, the challenge occurred when trying to deploy both a Laravel and Svelte
application with an attached database. After adding the procfile to the repository, I had to change the database config.
Using Heroku made for interesting commits; I chose to directly commit to Heroku as a git source rather than GitHub and
create interactions there. Fortunately, in doing so, each commit to Heroku provided full feedback on the build scripts
that had been set up. This allowed me to understand what was occurring on the server and adjust the build scripts such
that the assets would be generated for production and that both the Laravel app and Vue application were started.
 
Some things don’t make sense about the Heroku deployment. For example, when visiting the ‘/account’ route while not
logged in, the controller logic states that the user should be redirected to the ‘/login’ route, but no such redirecting
occurs. This behaviour does not happen on a local deployment; the redirect occurs as it should.

I would be happy to work further on a Laravel Svelte project; I just found the requirements for the project to be a
little confusing. I’m overall happy enough with the quality of the website. However, I don’t think a project like this
would ever be completed, only abandoned. 

I have allowed myself to work further on this project by adding the contact form to the bottom of the homepage, but it
is a feature that has not been implemented.

Styling the code for the project was somewhat simple. I have applied the use of PHPStorm and the reformatting that it
provides, editing the configuration so that all files are formatted on save. PHPStorm’s TODO feature was helpful
throughout the project as well. As I would find myself wanting to come back to something later, I would leave a comment
in code with TODO included. PHPStorm index’s all the TODOs into a single tab, and this became my source of tasks and
little reminders of things to connect throughout the project.
