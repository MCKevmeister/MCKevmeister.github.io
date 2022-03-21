---
layout: encrypted 
title: Project Kickoff 
date: 2022-2-25 20:22 
category: PRJ701 
image: assets\\images\\concept-development-device-flat.jpeg 
featured: true 
hidden: false 
permalink: /:categories/:title
---

## Summer Internship

My initial foray into the company was with a summer internship. Another inter and I were tasked with creating a simple
web application that would be used as a sign-in board for the office. The application was to utilize RFID hardware that
the company is producing. The software stack was PHP and more specifically the laravel framework, using
[Jetstream](https://jetstream.laravel.com/2.x/introduction.html) to handle login and registration. For the templating
engine, we used [Inertia](https://inertiajs.com/) and [Vue](https://vuejs.org/).

The purpose of the application was to allow the company to know for health and safety purposes, who was in the office at
a given time. It was a requirement that it had a user interface, and that some consideration was given to other users of
the system such as Fire Wardens.

As the stack suggested was new to me, I followed a tutorials at [laracasts](https://laracasts.com), specifically
[Laravel 8 from scratch](https://laracasts.com/series/laravel-8-from-scratch)
and [Build Modern Laravel Apps using Inertia.js](https://laracasts.com/series/build-modern-laravel-apps-using-inertia-js)
. This took me from having no understanding of the framework, to having 2 weeks of learning and having built 2
applications. While these applications were not intended to be used in production, they were a good learning experience.

Although not a specific requirement of the project, we were also encouraged to look into the use of Test Driven
Development (TDD)and modular development.

Modularization was a key part of the project. Modules (or packages in php) are managed by
composer. [Composer](https://getcomposer.org/) is a package dependency manager for PHP, similar to npm in Node.js or
Nuget in .NET. By creating the key parts of the application in a package, I learned to manage dependencies and to use
the package manager.

Modularization also allowed me to learn about testing. I was able to learn about the testing
framework [PHPUnit](https://phpunit.de/). This did create problems though, as classes in the parent application where
the package were developing could not be accessed. This was resolved by creating stubs and mock objects, to mimic the
classes in the parent application without implementing them.

To gain an understanding of the hardware requirements, we met with members of the hardware team. Their solution for
sending and receiving messages was to use the MQTT protocol. [MQTT](https://www.mqtt.org/) is a protocol for publishing
and subscribing, intended to be used for IoT applications. The MQTT protocol is a lightweight and efficient, which is
beneficial for lowering power and memory consumption of the RFID device. It works via a 'publish and subscribe' model,
where clients can publish messages to topics, and other clients can subscribe to those topics. A broker mediates the
messages between the clients, in a similar way to a server. I found a book on the topic,
[MQTT Essentials - A Lightweight IoT Protocol](https://www.packtpub.com/mqtt-essentials-a-lightweight-iot-protocol/book)
, which was very helpful in gaining a better understanding of the protocol, including different types of software
solutions for the parts of the protocol.

Below is a diagram showing the MQTT protocol implementation that we came up with. [Mosquitto](https://mosquitto.org/)
was selected as the broker, as it was the most popular and easy to
install. [MQTT.js](https://www.npmjs.com/package/mqtt) was used to create the client. The client would subscribe to a
topic, and on receiving a message, a put request would be sent to an API endpoint. The API would the process the request
and update the status of an employee in the database.

![MQTT](/assets/images/mqtt.png)

In the end, the project taught me a lot about

* PHP
* Laravel
* MQTT
* Test Driven Development
* Modular Development

I enjoyed the internship and was keen to learn more about the technologies that I had not used before. Following a
summer internship at SnapIT, I enquired the company about the possibility of working on a project for my capstone
project at NMIT. They were very interested in retaining me within the company, and I have chosen to do complete a work
based project with them.

## Project

The project that I have proposed is somewhat of a follow on from the internship. The company is interested to move away
from Monolithic development, and instead use a combination of Microservices and Modular development. They also want to
ensure that modules are well-designed before coding beings, and that the modules are well tested before they are
released.

I have made my project proposal to the NMIT project committee based around these areas of work within the company. I
will be drawing on my academic experience with systems analysis and design, as well as my programming experience. My
project meets the needs of the business, as they are looking to develop strategies and systems to improve the
modularization of the software that they develop, and to ensure that the software developed is well tested, using Test
Driven Development.

During the week I have been gathering research on Test Driven Development and Modular software development. While there
is a plethora of resources on Test Driven Development, I could find little about modular development. That was, until I
stumbled upon the article by Martin Fowler on [Microservices](https://martinfowler.com/articles/microservices.html) and
[Laravel Package Development](https://laravelpackage.com/).

## Person in Need

John is a 23-year-old male living in central Nelson. He works part-time as a labourer, but is struggling to pay his
weekly bills. Often he needs to make a choice between paying his weekly bills and buying quality food for himself. He
has enquired with the citizens' advice bureau, and they have suggested that he should buy food. They gave him the
contact details of several food bank services. He goes to the library and uses a computer to find out about the Nelson
food bank. He goes to the home page and reads the description of the food bank. He then goes to the contact page and
reads the contact details. After this he understands that to be eligible for food packages, he needs to exchange tokens
for food parcels. He signs up for an account on the website and gets tokens. He exchanges his tokens for a food package.

## Single Parent of 2 children

Mary is a single mother of 2 children. She is currently living in Richmond with her partner, and has been living there
for the past few years after separating from her ex-partner in Christchurch. Due to having to care for her children
during covid, she is struggling to find a stable job. This is a time of great stress, and she is looking for a job that
will allow her to provide for her children long term.

One of her friends has been working in the food bank for the past few months, and has suggested that Mary should use the
services provides to help her children. She asked the friend to help her as she isn't that technical. She has been able
to create an account on the website with the friends help. She exchanges tokens for food parcels, and is able to feed
her family.

## Producer with too much Food

Micheal owns a salad factory in Stoke. He is currently working on a project to increase the number of contracts he has
in the region. This has required him to ensure that he has enough product to meet the demand. There has been a down turn
in the market, and he is looking to increase his sales. He has been able to find a suppliers of produce, and has been
able to sell some of his product. He is looking for ways to increase his sales and considers the possibility of
partnering with a food bank to help him improve the brand image of the company. He reaches out to the food bank and
arranges a meeting with them to discuss establishing an ongoing relationship whereby he can provide seconds and old
product to the food bank in exchange for promotion of his brand on the website and in their social media. He reaches out
to the local newspaper and writes a story about the partnership. The newspaper publishes the story and the food bank
receives praise for its commitment to the community. Michaels company is now in the spotlight, and the food bank is          