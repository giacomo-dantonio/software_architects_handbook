# Chapter 4 - Software Quality Attributes

## Quality attributes

*Quality attributes* are properties of a software system and a subset
of its non-functional requirements. They should be *measurable* and
*testable*.

Software quality attributes are *benchmarks* that describe the
software system's quality and measure the fitness of the system.

Software quality attributes can affect each other, and the
degree to which one is met can affect the degree to which others
can be met. It's important to identify *conflicts* between
quality attributes.

### External or internal

*Internal* quality attributes can be measured by the software system itself
and are visible to the development team.
Examples are lines of code, level of cohesion, readibility of the code,
and the degree of coupling between modules.

*External* quality attributes are properties that are externally visible.
They are noticeable to the end users. A working version of the software
must be deployed so that it can be tested.
Examples are performance, reliability, availability, and usability of the system.

### Quality attributes and the SDLC

Quality attributes should be considered throughout the software development
life cycle (SDLC).

The process begins during requirements engineering by ensuring that they
are captured completely and correctly.

During testing, quality attributes must be verified to ensure that
the software system satisfies the requirements.

### Testing quality attributes

Example:

* Manually testing the software usability
* Creating benchmarks and using tools for performance testing
* Performing code reviews and calculating code metrics to test for maintainability
* Executing automated unit tests to ensure the system behaves as expected

A balance needs to be reached between the amount of testing and the time available.
Automating as much of the testing as possible is the key.

## Maintainability

*Maintainability* focuses on the ease with which a software system can be maintained.

Maintenance of a software system takes place as changes are made to it after
the software is in operation. It is necessary to preserve the value of the software
over time.

When a developer is writing code, he or she has to take into consideration
not just the end user of the software, but also those who will be maintaing it.

### Types of software maintenance

#### Corrective maintenance

Corrective maintenance is the work involved in analyzing and fixing defects
in the software.

The severity and priority of the defect vary depending on the nature of the bug.

Severity represents the level of impact the bug has on the operation of the software
(e.g. critical, high, medium and low).

The priority of a defect is the order in which it will be fixed (e.g. high, medium, low).

Maintainability can be measured by the time it takes to analyze and fix a particular
defect.

#### Perfective maintenance

Perfective maintenance is necessary when the software needs to implement new
of updated requirements.

#### Adaptive maintenance

Adaptive maintenance is defined as the work required to adapt a software system
to changes in the software environment.

#### Preventive maintenance

The goal of preventive maintenance is to prevent problems in the future,
by increasing quality. Example: refactoring a software component
to make it less complex.

### Modifiability

Modifiability is the ease with which changes can be made to the software
without introducing defects or reducing quality.

The time required from when a change is specified until it is deployed
is an indication of the modifiability of the system.

### Extensibility and flexibility

Related to modifiability. The level of *extensibility* reflects how easy
it is to enhance or extend the software system.
Take the future growth into consideration by anticipating the need to add
new functionality.

*Flexibility* focuses on how easy it is to change a capability so that
it can be used in a way that wasn't originally designed.

### Designing for maintainability

You must reduce the difficulty in implementing changes. This means reducing
the complexity of the architecture and its components.

* Reduce size

    Your design should seek to reduce the size *of individual modules*.
    E.g. by splitting up a module into multiple ones.

* Increase cohesion

    *Cohesion* represents how interrelated the elements in a particular
    module are. Increase cohesion by not allowing a particular
    module to have too many disparate elements.
    High cohesion often correlates with loose coupling.

* Reduce coupling

    *Coupling* refers to how dependent different modules are on each other.
    Design should seek loose coupling, such that different modules are indepent
    of each other or almost indepenent.

### Measuring maintainability

There are *software metrics* that can provide insights about the maintainability
of the software.

**Lines of code (LOC)**

Represents the size of a software system by determining the number of lines
in its source code.

**Cyclomatic complexity**

Measures the number of linearly independent paths through a module
or detailed design element. (??)

Given a control flow graph of the code, we have:

    CC = E - N + 2 * P

where E is the number of *edges* in the graph, *N* is the number of nodes
of the graph and *P* is the number of connected components of the graph.

Cyclomatic complexity values greater than 10 typically indicate modules that are complex.

**Depth of inheritance tree (DIT)**

Measures the maximal length between a node and the root noe in a class hierarchy.
A higher DIT means there is code reuse through inheritance but it may make it
more difficult to predict behaviour.
A lower DIT indicates tell complexity but it also may mean that there is
less code reuse through inheritance.

## Usability

Usability describes how easy it is for users to perform the required tasks
using the software system.

Increasing usability can be one of the easiest and cheapest ways to imrpve
the quality of the system.

### Learnability

Learnability is the degree to which new users can learn how to effectively
use the software system. Learnability also includes how easy it is
for experienced users to learn new functionality that is added to the system.

### Accessibility

Accessibility is the aspect of usability which provides features
that make it easier for people with disabilities or impairments
to effectively use the software.

Examples:

* Make the software usable when only using a keyboard
* Provide support for assistive technologies (screen readers, etc.)
..

### Appealing visual design

The visual appearance of a software system is a component of usability.

* Place emphasys on readability (headers, proper spacing, readable fonts,
  attractive colors, appropriately formatted text).
* Use well thought page layouts.
* Avoid excessive text.
* Avoid complicated navigation and menus.
* Provide tooltips.
* Be consistent with colors, icons, fonts and captions/terms.
* Display progress indicators when the user hast to wait for a response.

### Providing a good help system

A thorough and up-to-date help system makes an application easier to learn.

### Software must be useful, not just usable

In addition to being usable, the software must probide the functionality
that its users need.

## Availability

*Availability* describes the degree to which the software system will work
as required when it is needed. It is the probability that the software
system is operating properly when needed by a user and is not experiencing
unplanned downtime due to failure and repair.

It is tipically measured in term of *nines* (99.9%, 99.99%, or 99.999%).

### Calculating availability based on time

    Availability = MTBF / (MTBF + MTTR)

*MTBF* is the mean time between failures (average time between two failures
of the system). *MTTR* is the mean time to repair, which is the average
time to troubleshoot and repair the system back to its operational state.

High availability is considered five nines 99.999%. It means
only 5:15 minutes downtime in a whole year.

Each additional nine requires a whole magnitude improvement of availability.
The user won't be able to tell the difference between 99.99% and 99.999%.

The benefits of higher availability needs to be weighted against the increased
costs of providing them.

### Calculating availability based on request success rate

    Availability = Successful requests / Total requests

### Faults, errors, and failures

Availability involves how a software system can handle and overcome faults,
so that the duration of an unplanned outage does not exceed the specified
value over a particular amount of time.

* A system *fault* is a characteristic of a software system, that can lead to
  a system failure. A system fault exists somewher in the code.
* An *error* is an erroneous state of the software system, caused by one or more 
  faults.
* A *system failure* is an event experienced by a user, in which the system
  does not behave as expected. System failures are caused by one or more faults.

You want to *detect* faults, *recover* from faults or *prevent* faults.

### Detecting faults

* **Ping/echo reply**: Internet Control Message Protocol (ICMP).
* **Heartbeat**: like the numbers in lost.
* **Timestamp**
* **Voting**: triple modular redundancy (TMR). It utilizes three components
  to perfom the same process. If all three componentes produce the same output,
  the everything work as expected.
* **Sanity test/sanity checking**: uses a test to evaluate if a result from a
  process is reasonable and possible.
* **Condition monitoring**: conditions are checked in a software system
  in order to detect a fault or a situation in which a fault may develop.
* **Self-test**: built-in self-test (BIST).

### Recovering from faults

* **Exception handling**
* **Retry strategy**
  *Transient faults* are error that occur due to some temporary conditions.
  Retry strategies can be used to attempt to retry an operation when it
  encounters a transient fault.
* **Varying levels of redundancy** Have a failover mechanism.
  - *active/hot spare* environment: each component has another one that performs
  the same processes.
  - *passive/warm spare* environment: only active components perform processes
    from input, but the active components provide the backup components
    with periodic state updates (backup).
  - *cold spare*: redundant components are kept out of service until they are
    needed.
* **Rollback**
* **Graceful degradation**
  Some functionality is made unavailable in order to prevent the entire system
  from becoming unusable.
* **Ignoring faulty behaviour**

### Preventing faults

* **Removal from service** A software component can be removed from operation
  in anticipation of faults.
* **Transactions**
* **Increasing competence sets**
  The *competence set* for a given component determines what state and
  conditions it can handle. A component can be modified so that it handles
  more cases, reducing the exceptions that are thrown.
* **Exception prevention**

## Portability

*Portability* describes how efficiently and effectively a software system can be
transfered from one environment to another.

### Adaptability

*Adaptability* is the degree to which a software system can be adapted for
different environments, such as different hardware, operation systems,
or other operational characteristics.

Functional testing must be conducted to ensure that the software system
can perform all of its tasks in all target environments.

### Installability

*Installability* is the easse with which a software system can be installed
on uninstalled in a specific environment.

Another aspect is how the software handles update/upgrade processes.

### Replaceability

*Replaceability* is the capability of a software system to replace another
software system for the same purpose, in the same environment (e.g. upgrade).

All relevant functionality should be tested to verify that it works as expected.

### Internationatilization and localization

*Internationalization* and *localization* consist of adapting a software system
for use with different languages, taking into consideration cultural differences,
and meeting other requirements for various locales.

The software should be designed so that adapting it to different locales
will not require modifications to the code.

## Interoperability

*Interoperability* is the degree to which a software system can exchange and use
information from another software system.

Two software system muse be able to communicate with each other
(*syntactic* interoperability) as well to interpret the information exchanged
in a meaningful and correct way (*semantic* interoperability).

Another term for interoperability is *integration*.

Even when a software system follows a particular standard, interoperability
may not be met due to the two systems interpreting the standard specifications
in different ways.

### Locating and exchanging information with another system

In order for the two systems to exchange information, interoperability tactics,
such as orchestration and the management of interfaces, are used.

*Orchestration* involves direction and managing the services thar are called
and ensuring that the necessary steps take place in the correct sequence.

A capability may be added to an interface specifically to enable data exchange
(e.g. buffering of data). Capabilities may be removed from an interface
if we do not want those capabilities to be exposed to other systems
(e.g. functionality to delete certain data).

### Interoperability standards

One way to achieve interoperability is to follow a common standard.

Another aspect is using a common technology, such as a data interchange protocol
(e.g. JSON) or a communication protocolo (e.g. HTTPS).

### Interoperability testing

Test must be conducted to ensure that the consumer can *locate* the other system
and that they can *exchange* information properly.

## Testability

*Testability* is the degree to which a software system supports testing in its
given context.

If a component is not easy to test it might indicate that the design is not ideal,
leading to an implementation that is unnecessary complex.

### Controllability

*Controllability* represents the level to which it is possible to control
the state of the component being tested.

Controlling the state of a component involves being able to dictate the inputs
of the component as well as the level to which those inputs exercise its
capabilities.

### Observability

*Observability* represents the level to which it is possible to observe
the state of the component being tested.

This includes being able to observe inputs and outputs so that we can determine
if the component is working correctly.

### Isolability

*Isolability* is the degree to which a component can be isolated.

The goal is to have tests that can focus on specific pieces of functionality
(e.g. unit tests) that do not have dependencies on other components.

We want to avoid the situation that we have to write a great deal of code
before any of it can be tested since it is desiderable to get feedback
as quickly as possible.

### Automability

*Automability* is the level to which a process or action can be automated.

### Complexity of the software

Reducing dependencies and isolating modules decreases the complexity of
the software.

Reduce the number of lines of code in modules, increase cohesion and
reduce coupling.

#### *Structural* complexity vs *behavioural* complexity

Deterministic algorthims are less complex. Non-deterministic code is more
difficult to test.

Refactor the logic to make it deterministic or allow the logic
to be mocked as deterministic.

Use dependency injection for that.

### Importance of test documentation

An aspect of testability is the ease with which tests can be executed,
including testers who did not originally write the test cases.
*Reusability* and *maintainability* of tests are improved with the existence
of quality test documentation.