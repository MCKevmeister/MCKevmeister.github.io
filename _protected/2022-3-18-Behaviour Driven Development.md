---
layout: encrypted title: Behaviour Driven Development date: 2022-03-18 11:35 category: PRJ701 image:
assets\\images\\bdd-double-loop.png featured: true hidden: false permalink: /:categories/:title
---

# Behaviour Driven Development

Behaviour Driven Development (BDD) is an extension on Test Driven Development (TDD) which was originally conceived by
Dan North. Dan was teaching developers how to utilize TDD to write better code. However, developers did not know:

* where to start testing
* what to test
* how much to test
* and overall why to test at all.

All this confusion he found led to developers writing poorly written tests, or worse not testing at all. To resolve
this, Dan established BDD as a framework of development methodologies and practices to make TDD easier and to focus on
delivering better code and value to the customer of the product that developers are building(North, 2006).

BDD closes the gap between business people and technical people by:

* Encouraging Collaboration Providing a shared understanding of the systems desired behaviour
* Produces documentation that guides development and is automatically checked against the system behaviour
* Work in small iterative cycles which increase feedback and delivers value faster

BDD conceptually has 3 main phases in a cycle. BDD has names for each phase: Discovery, Formulation and Automation

### Discovery - What it could do

A small new change to the system is required i.e. a User Story. A conversation is held to explore, discover and agree on
behaviour with concrete examples.

The goal of BDD isn’t to make documentation and automated tests, rather it's to create valuable working software. BDD
proposes that the fastest way to do so is through conversations between the people who are involved in imagining and
delivering the software. This logically extends on the principles of Agile, favouring "interactions over processes and
tools"(Agile Manifesto).

BDD uses structured conversations called discovery workshops to minimise meeting time and maximise code output. The
focus is around real-world concrete examples of the system from the user's perspective. This grows the teams shared
understanding of the users needs, the rules of the systems' functionality, and scope of work.

Three different perspectives are required in the discovery workshop, which is aptly named “The Three Amigos”. More or
less than 3 people can contribute, but an understanding of the types of questions and perspectives aids discovery. Often
the tester and developer can be the same person.

A perspective of the product from the client, customer or product owner is required. They bring domain knowledge,
business perspective and the problem the team should be trying to solve.

A perspective from the developer is required. They understand how to build a solution around the problem, and technical
limitations of the solution.

A perspective from a tester is required. They ask questions such as “what if” and identify edge cases that may be a
problem if unhandled.

If gaps in understanding are identified, more information is needed to be sourced before moving on from Discovery.
Discovery of unknowns is useful at this point - Known unknowns indicate that writing code shouldn’t yet happen.
Discovery resolves incorrect assumptions being made.

User stories and business requirements are useful to have before discovery but not necessary. User stories can be
placeholders for conversations, and are often the starting point of the conversations.

### Formulation - What it should do

Once a valuable concrete example is identified, it can be documented in Gherkin. This confirms the shared understanding
of what to build.

Gherkin can be read by both computers and humans which allows for feedback from all stakeholders about the shared
vision. It captures the problem-domain language/terminology into a shared language for talking about the system. This
captured language is used in the code for the naming of classes and methods. This eliminates the cost of translation
when discussing the system with non-technical stakeholders.

Simply, Gherkin is a business readable, domain specific language. It is living documentation which can become the basis
for a user manual. It is user stories with a narrative and contains at least 1 concrete scenario with acceptance
criteria. It is a language that is easy to read and understand.

The examples will be able to be automated to guide the development (behat for PHP and godog for Go are examples of this)
.

### Automation - What it does Code is written, implementing the behaviour described.

Once the behaviour is written into a testable piece of code, it can be run to test the system. This then builds a test
suite than can be run anytime in the future when a change is made to the system. In doing so, the system is verified to
work as expected in the defined behaviours.

BDD is an approach that collaboratively specifies the system's desired behaviour. Each time a behaviour is agreed on,
that specific behaviour is used to drive the development of the code that will implement the behaviour.

## Real world examples

Below are some repos in which there is a ‘feature’ folder, containing all the feature tests for the project.

* [Jekyll](https://github.com/jekyll/jekyll/tree/master/features)
* [Time Flies By](https://github.com/esambo/TimeFliesBy/tree/master/features)

## Studies

When building many modules as Snap plans to do, how is it best to manage the BDD tests? This study suggests a model
whereby all BDD tests are stored in a single repository. It may be best for this example to store the integration
feature tests in a separate repository, while storing all the feature tests for a single module in the repository with
the code.(Rahman & Gao, 2015)

## References

Agile Manifesto. (2001). Manifesto for Agile Software Development. Agilemanifesto.org. https://agilemanifesto.org/

Cucumber. (n.d.). Behaviour-Driven Development - Cucumber Documentation. Cucumber.io. https://cucumber.io/docs/bdd/

North, D. (2006, September 20). Introducing BDD. Dan North & Associates. http://dannorth.net/introducing-bdd/

Rahman, M., & Gao, J. (2015, March 1). A Reusable Automated Acceptance Testing Architecture for Microservices in
Behavior-Driven Development. IEEE Xplore. https://doi.org/10.1109/SOSE.2015.55