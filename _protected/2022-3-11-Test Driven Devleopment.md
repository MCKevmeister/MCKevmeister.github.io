[//]: # "@formatter:off"
---
layout: encrypted
title: Test Driven Development
date: 2022-03-11 13:10
category: PRJ701
image: assets\\images\\tdd-cycle.png
featured: true
hidden: false
permalink: /:categories/:title
---
[//]: # "@formatter:on"

# Test-Driven Development

Test Driven Development is a software development process that uses a series of tests to validate the correctness of the
software under development. The goal of which is to ensure that the software project is able to grow sustainably, and to
ensure that the code avoids software entropy(Software entropy, 2022).

The process of testing is a key part of the software development process. It is the process of verifying that the
software is working as intended. In TDD, the process of adding code follows a cycle: Red, Green, Refactor.

### Red

When a new behaviour has been identified to be build, a unit test is written to test the new behaviour. Without having
first written the code, the unit test will fail when the test suite is run. This is expected, and if the test does not
fail then it identifies a problem. Most test runners will display this failure with red text in the console, hence the
name.

### Green

With a failing test, the goal now becomes to pass the test and turn the red text into green text. The goal at this point
is to write the smallest possible code that will pass the test. It does not matter how well the code is written, as long
as it passes the test.

### Refactor

With a passing test the goal now is to refactor the code to make it more efficient. Any refactoring should be followed
by rerunning the tests. If any tests fail, then the code should be reverted to the previous version. This process
ensures that the system is still functional and that the tests are still passing.

## Common Mistakes

There are several common mistakes that can be made when writing TDD. Often the test runner will provide some output on
the amount of code that has been covered by the tests. A mistake that can occur is that developers will see that number
and intend to try to maximise it ie. achieve 100% coverage. This is short-sighted and will not produce the best code.
Having high test coverage does not ensure that the System Under Test (SUT) is performing well. It is possible that tests
cover all lines of code, but that the tests are written in a way that the tests are not testing the SUT, and will pass
regardless.

Simply, Test Coverage does not equal quality code. If coverage is low it's an indication that there are not enough
tests. If coverage is high, it does not ensure that the system is tested well. A better metric to use, but still not
perfect is branch coverage. Again though, coverage metrics are only an indicator of poor code, not a positive indicator
if the coverage is high. It is best to have high coverage numbers, but there should not be a requirement to have 100%,
or else developers will game the outputs to ensure the desired coverage, and quality tests will not be produced.

Another issue lies with code that is difficult to tests. This indicates that the code is not well written, or has been
poorly designed. To remedy this, it is best to write tests that are easy to write code for.

Another big question relates to a question, "What is a 'unit' of code?"

### What is a Unit?

The name of 'unit' imply some conceptual boxing around a piece of code, but what exactly is that unit? There are 2
schools of thought here.

### London/Chicago Style

The London Style states that a unit is a unit of code, such as a class or function. From the perspective of
Object-Oriented Programming (OOP) this makes a lot of sense. In OOP classes are the build blocks of code, and functions
are the ways in which they interact with other objects. Therefore, logically, a test should be written to test a class
or method of an object.

In this way when tests are written, they should be isolated from other classes. When the class being tested needs to
interact with another class, or several tests have shared dependencies, a test double should be created. This follows an
outside-in approach, building all the higher level tests and objects first that set expectations of the system, doubling
each collaborator until a class structure is built. Implementing doubled classes can be done later.

The benefit of this approach is that there is a high level of granularity in the tests. It is easy to test the
interactions with other classes, as the behaviour of the collaborated will be known from the test double. Also if a test
fails, then it is clear in exactly which class or method there is a bug or regression.

The negatives of this approach are that the tests become tightly coupled to the implementation detials of the classes.
If a collaborator is needed then its double must be build, which adds time to development. If requirements change and
classes need to be changed, then not only will the tests need to be rewritten but the all the test doubles will, as well
as the actual code being tested. Additionally, tests are not testing for behaviours of the system, but the
implementation details of the classes and test doubles.

## Classical Style

In the Classical Style, a unit is a unit of behaviour. A test should be written to test a part of that behaviour which
comes from the higher level requirements of the system. Each unit test should be tested in isolation from other units.

In this way, the system is build inside-out, starting at the domain model and adding additional functional layers on top
of it until the system is usable by the end user.

The benefit of this approach is that the tests focus on the behaviours of the system, which can be defined more easily
in the business requirements. Building in this way, a behaviour being tested is more easily traced back to business
value that it adds to the system.

The negatives of this approach are that if a bug or regression is introduced in the system, then many tests can fail.
However, if the developer is running the tests regularly in developing new features then it should be easy to identify
the regression. In this way, it encourages the developer to use the test suite as a safety tool rather than to treat it
as an annoyance only used at the end of development.

From reading about the two different types, my preference is towards the Classical style as it promotes better value for
the end user and a better development process. The test suite should be a useful tool used often not just a check that
is done at the end of a TDD cycle.

This preference is also supported by research paper titled "A Dissection of the Test-Driven Development Process" (Fucci
et al., 2017), where the authors found that the quality of code improved based on the cadence and uniformity of cycles
writing tests and writing production code. Taking steady small uniform steps(time spent on tests and code being close to
even) the better quality the code.

## Structure of a Unit Test

Structuring a unit test in a consistent manner allows for the test suite to be more readable and maintainable. The best
way to structure a unit test is to follow the arrange, act, assert pattern.

### Arrange Act Assert (AAA)

**Arrange**

The arrange section of a test is used to bring the System Under Test (SUT) into a known and desired state.

**Act**

In the act section of a test, the SUT is exercised in a way that is expected to result in a desired outcome. The output
values are stored in variables.

**Assert**

Verify outputs, make assertions on outputs

With TDD, when writing tests using the test first approach, writing the assert statement for the expected behaviour that
is being covered by the test. When writing the test last, start with arranging first as the code already exists.

## Thing to Avoid when writing unit test:

For each unit test, only do one set of AAA. A single test that has many AAA cycles is not a unit test, and more
resembles an integration or feature test, or several unit tests. In such a case, refactor the unit test into single
cycles, or move to an integration test suite.

Having multiple actions inside a single unit test is also a mistake. Split up that unit test, so that only 1 action
occurs per test. Optimizing tests by refactoring them together (DRY - Don’t repeat yourself) should not apply in unit
tests (to a point), but rather in slow integration tests.

Tests should not contain if statements. Refactor a test with if statements into several tests for all the branches or
cases. If statements make tests hard to read and increase the cost of time in maintainability.

## Size of each section

The ‘Arrange’ will be the biggest. However, extract arrangements into private methods if they get too big or are
repeated in several tests. If some unit tests have the same arrangement, then it is better to extract it into a private
method. If all the unit tests have the same arrangement, then it is better to extract it into a setup method called
before each test.

The ‘Act’ should be a single line. Multiple actions or lines of code indicate a problem with the SUT public API. The
underlying code may need better encapsulation.

‘Assert’ all behaviors of the test. One assertion may not be enough. Too many assertions also may be an issue, and may
require creating an equality object then comparing the object to the expected value of SUT.

## Formatting

To improve the readability of tests, have consistent formatting. 2 common conventions are separating by comments
//Arrange //Act //Assert) or line space/s. If using line spaces, avoid empty lines in each section.

When Arranging the SUT, consider naming it ‘sut’ as a variable, as to improve readability. Actions are taken on/with the
‘sut’ variable and assertions are made against ‘sut’

## References

Fucci, D., Erdogmus, H., Turhan, B., Oivo, M., & Juristo, N. (2017). A Dissection of the Test-Driven Development
Process: Does It Really Matter to Test-First or to Test-Last? IEEE Transactions on Software Engineering, 43(7),
597–614. https://doi.org/10.1109/tse.2016.2616877

Software entropy. (2022, January 25). Wikipedia. https://en.wikipedia.org/wiki/Software_entropy

Vladimir Khorikov. (2020). Unit testing : principles, practices, and patterns. Manning.