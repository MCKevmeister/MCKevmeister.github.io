[//]: # "@formatter:off"
---
layout: encrypted
title: Project review so far
date: 2022-03-28 16:18
category: PRJ701
image: assets/images/review-image.jpg
featured: true
hidden: false
permalink: /:categories/:title
---
[//]: # "@formatter:on"

As I am into my 6th week of my project, I am going to do a review of the work that I have done so far. My project plan
was set out a week or so in to the project. It is below

| Activity                   | Deliverables                                                                                                                          | Time Frame / Dates                                                 |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| Initial Research           | - List of research questions <br/> - Gain an understanding of what Snap wants from my project - Conduct initial information gathering | 2 weeks finishing 4 March                                          |
| Test Driven Development    | - Define a set of best practices <br/> - Document work flows from requirements to tests to code                                       | 6 weeks finishing 15 April                                         |
| Scope of Modules           | - Practices and guidelines for designing modules                                                                                      | 3 weeks finishing 6 May                                            |
| Encompass Skeleton Package | - Build a template package skeleton based on internal requirements for Encompass Modules (Snap Opinionated)                           | 3 weeks 27 May                                                     |
| Dependency Management      | - Provide options for providers                                                                                                       | 1 week 3 June                                                      |
| Report and Poster          | - Write project report <br/> - Present poster board                                                                                   | 3 weeks Report <br/> due 12 June <br/> Poster Presentation 16 June |

For questions raised in each activity:

- Provide a problem statement
- Discuss the background
- Offer options to solve with pros/cons
- (Optional)Provide a Proof of concept

As of now, I feel as though my original time frames are fine. My exploration into TDD and BDD means that I have a much
better understanding of the Scoping of modules. As such, I think that the application of BDD withs its benefits of being
able to gather the requirements from users and documentation them in a non-technical way achieves the goal of better
scoping modules to meet the needs of the end user.

Knowing how to test and what packages to include into a skeleteon package is a important deliverable as part of my
project. It makes sense to know what packages to include into the skeleton package. Going through learning about TDD
first and BDD second, I have a much better understanding of how to test and what packages to include into the skeleton.

With another 11 weeks left in my project, I feel comfortable that I will have all the deliverables completed. I'm
looking forward to the coming weeks of learning Cypress, further into BDD and building out the skeleton package.

On a side note, writing this blog took me a little longer than I expected. There were issues in the gulp script that
needed updates, which led into more issues that took a while to resolve. The original person who wrote the script didn't
think that anyone would put a markdown table in a blog file, as the text of a table is similar to the front matter text
in '---' lines. The script looks for those and replaces them where necessary. The table really doesn't work with that.
Anyway I added a line break to the front matter delimiter. Annoying but it works now again. Due to the amount of time I
have spent on this particular problem, I'm considering releasing the improved code on github.