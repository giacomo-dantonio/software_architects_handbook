# Chapter 6 - Software Development Principles and Practices

## Designing orthogonal software systems

Software that is well designed is orthogonal in that its modules are independent
of each other. Ideally, changes to one module in a software system should
not require changes to another module.

The benefits include increased productivity for those who work on them and
lowered risk of introducing defects when changes are made.

Orthogonal systems are designed so that their elements are *loosely coupled*
and *highly cohesive*.

### Loose coupling

Coupling is the degree to which a software module depends on another
software module.
It is a measure of how closely connected they are. It can be loose
(low, weak), or tight (high, strong).

Tight coupling makes modifying the code more difficult because a change
in a tightly cooupled module will likely require changes in other modules.
This introduces a higher degree of risk as there is a greater likelihood
that a new defect could be introduced if a software module is modified.

It is also easy to engage in parallel development if the code is loosely coupled.

Tight coupling also reduces reusability.

Now we see the types of coupling in order of the tighest (least desirable)
to loosest (most desirable).

#### Content coupling

*highest*

Is the highest type of coupling. It is bad. Also referred to as
*pathological coupling*.

It occurs then one module directly references the internal or private
information in another module.

If modules have content coupling thy should be refactored so that
there is a proper level of abstraction. The modules should not
directly rely on the internal workings of each other.

#### Common coupling

*high*

Also known as *global coupling*. It is highly undesirable although sometimes
is unavoidable.

It occurs when modules share the same global data, such as a global variable.

It is acceptable to share configuration data throughout an application.
For other types of global data, it is better to use something that has a fixed
value, such as a constant.

#### External coupling

*high*

It exists when multiple modules share the same part of an environment that is
external to the software. For example by having to use an external data format,
interface, communication format, tool, or device.

External dependencies are unavoidable, but we should seek to limit the number
of modules that have those dependencies. If the external dependency changes,
only a limited number of modules are affected.

#### Control coupling

*moderate*

It happens when one module controls the internal logic of the other by passing it information. For example when a module passes a control flag to another module,
which uses it to control its flow.

This may be acceptable, but an effort should be made to make it known
that the coupling exists, so that the modules can be tested together.

#### Stamp coupling (data-structured coupling)

*low*

It occurs when modules share a composite data structure. Composite means that
it is data that has some internalstructure to it, such as a record.

It is similar to data coupling, except that tha data is a composite data type
and that not all values shared may be used.

#### Data coupling

*low*

It occurs when two modules share some data which are just primitive data values.
For example when a module calls a method on anothre module,
and inputs and outputs are shared in the form of method parameters and return
value.

This is a common and acceptable type of coupling.
All of the parameters in data coupling are used. If any parameters are not needed,
they should be removed.

#### Message coupling

*lowest*

It is when one modle calls a method on another module and does not send
any parameters.

#### No coupling

This is when two modules have no direct communication at all.

#### The Law of Demeter (LoD) / principle of least knowledge

It is a design principle. It follows the *only talk to your friends* idiom.

Ideally, a method should only call other methods

* in the same object,
* in objects that were passed into it,
* in direct component objects,
* in objects that it created/instantiated,
* or in objects in a global variable that are accessible.

A software module should know as little as possible about other modules.

#### Designing for loose coupling

During designs and implementations modules should be designed to be
as independent as possible.

For any coupling that must exists, it should be the lowest type that is
necessary.

### High Cohesion

*Cohesion* is the degree to which the elements inside a module belong together.

A higher level of cohesion is preferable. Highly cohesive modules have a single,
well-defined purpose.

If a module contains multiple unrelated functions, changes to it are more likely
to require changes in other modules.

The extra complexity in modules with low cohesion make it more likely that
defects may be introduced when modified. They may also be harder to understand,
making them more difficult to modify.

#### Coincidental cohesion

*lowest*

Occurs when elements in a module are grouped arbitrarily.
There is no relationship among the different elements, making it the lowest
(worst) type of cohesion.

It is often the case of *utilities* or *helper* classes.

#### Logical cohesion

*low*

Elements are grouped together because they are related in some logical way.

Even though the functionality of logically cohesive modules might be of the same
general category, they may differ in other ways.

While better than coincidental cohesion, these types of modules
are not very cohesive.

An example would be a module that contains a set of functions that handles
I/O for the application. They would be more cohesive if each type of I/O
was handled by a separate module.

#### Temporal cohesion

*low*

It is when the elements of a module are grouped together based on when
they are processed. Different elements are grouped together
simply because they need to be executed at a single moment in time.

An example is grouping elements together because they are all related to system
startup, shutdown or the handling of a system error.

#### Procedural cohesion

*moderate*

Elements are grouped together because they always execute
in a particular sequence.

Example: payment processing for an order might involve

* Gathering payment information
* Validating payment method details
* Checking whether funds are available or whether there is enough
  available credit
* Persisting the order in a database
* Checking inventory levels
* Creating a back order or canceling an order based on inventory
* Sending the order for fulfillment
* Sending an email confirmation to the customer

The various parts are all related by the order of execution, but some
of the activities are quite distinct from each other.

Although it is an acceptable level of cohesion, it is not ideal.
If possible should be refactored.

#### Communicational cohesion

*moderate*

Parts of a module are grouped together because they use the same set
of inputs and outputs. Elements have been grouped together because
they access and modify the same data structure.

For example a data structure that represents the contents of a customer's
shopping basket may be used by a variety of elements in a single module.
The elements might calculate discounts, shipping, and taxes.

#### Sequential cohesion

*moderate*

Different parts of a module are grouped together because the output
of one part serves as input for another part.

Example: a module for formatting and validating a file. The output of an
activity that formats a raw record becomes the input for an activity
that the validates the fields in that record.

#### Functional cohesion

*high*

Elements of a module are grouped together because they are united
for a single, well-defined *purpose*.
All of the elements in the module work together to fulfill that purpose.

#### Designing for high cohesion

Each module should have a single, well-defined purpose.
The elements contained in the module should be related and contribute
to that purpose.

If there are auxiliary elements contained in a module that are not directly
related to the main purpose, consider moving them to either a new module or an
existing module that has the same purpose of the lement being moved.

## Minimizing complexity

The problems facing software engineering can be divided in two categories.

*Accidental* difficulties are problem that are just inherent to the production
of software in general. Improvements in programming languanges,
frameworks, design patterns, IDEs, and software development methodologies
are some examples of progress eliminating or reducing accidental difficulties.

*Essential* difficulties are the core problems that you are trying to solve
and they can't be simply be removed to reduce complexity.

We try to manage and minimize complexity, whether it is accidental or essential.
Complexity has a direct relationship with the quality of the software.

### KISS principle - Keep it simple, stupid

Systems generally work best if they are kept simple.
A development team should strive to not overcomplicate their solutions.

Some ways to follow the KISS principle in software include:

* Eliminating duplication as much as possilbe (DRY).
* Eliminating unnecessary features (YAGNI).
* Hiding complexity and design decisions.
* Following known standards when possible.

We cannot oversimplify a design or implementation though.
If we reach a point that it negatively affects the ability to deliver
on required functionality or quality attributes, we have gone too far.

### DRY - Don't repeat yourself

DRY strives to reduce duplication in a codebase.
Duplication makes a codebase unnecessarily larger and more complex.
It makes maintenance more difficult.

Code duplication often results from **copy-and-paste** programming.

**Magic strings** are strings that appear directly in your code.
Sometimes they are needed in multiple places and are duplicated,
violating DRY. Declare *constants* instead or use a *resource file*.

If you find yourself copying and pasting code, or simply writing code
that is identical or similar to existing code, think about what
you are trying to accomplish ad how it can be made reusable.

Duplication in logic can be eliminated by abstraction. This is the
**abstraction principle**. The code that is needed in multiple places
should be abstracted out.
Some refactoring may be necessary to make ti generic enough to be reused.

If there is **duplication in a process**, it may be possible to reduce it
through *automation*. Manual tests, build and integration processes can be
eliminated automating them.

#### Don't make thinkg overly DRY

Be careful not to consolidate disparate items that just happen
to be duplicates in some way. It may be that tehy are just *coincidentally
repetitive*.

### Information hiding

*Information hiding* is a principle that advocates for software modules
to be designed such that they hide implementation details
from the rest of the software system.

The details of a module that do not need to be revealed
should be made inaccessible.

Only exposing the details that need to be known reduces complexity
and improves maintainability.

Another reason for information hiding is to hide design decisions
from the rest of the software system.
If the decision needs to be changed, it minimizes the amount and extent
of the modifications that will be necessary.

You should think about the properties and behaviours that need to be
exposed for a module. Everything else can be hidden.

The public interface defines a contract that the implemenatin must follow,
and allows other to know *what* is available.
It is up to the implementation to decide *how* it is accomplished.

### YAGNI - You Aren't Gonna Need It

*YAGNI* is a principle from the software development methodology
*extreme programming* (*XP*).

You should only implement functionality when you need it and not just because
you think you may need it some day.

The problem with implementing a feature that you think might eventually be needed
is that quite often the feature ends up not being needed or the requirements
for it change.

YAGNI applies to presumtive features, as in functionality that is not currently
needed.
It does not apply to code that would make the software system easier
to mantain and modify later.

### Separation of Concerns (SoS)

*Concerns* are the different aspects of functionality that the software system provides.

*Separation of Concerns* is a design principle that manages complexity
by partitioning the software system so that each partition is responsible
for a separate concern.

It involves decomposing a larger problem into smaller, more manageable concerns.

When the DRY principle is followed, and logic is not repeated, a SoC is usually a natural result.

An architecture pattern that separates concerns is the *Model-View-Controller* (*MVC*) pattern.

## Following SOLID design principles

Software architects should be familiar with SOLID principles and apply them
in their design and implementations. They should realize though,
that the principles are guidelines.
While you should strive to follow them, you may not always be able to
accomplish that.

### Single responsability principle (SRP)

The *Single Responsibility Principle* states that each class hould have only one responsibility. A resposibility is a reason to change, so each class should have
only one reason to change.

### Open/Closed Principles (OCP)

The *Open/Closed Principle* states that software components, such as classes,
should be **open for extensions, but closed for modification**.

When requirements change, the design should minimize the amount of changes
that need to occur on the existing code.
Whe should be able to extend a component by adding new code
without having to modify existing code that already works.

You can use inheritance but using abstraction through interfaces is better.
Using interfaces we can change implementations as needed. This way,
we can change behavior without having to modify existing code
that relies on the interfaces.

### Liskov Substitution Principle (LSP)

The *Liskov Substitution Principle* states that subtimes must be substitutable
for their base types without having to alter the base type.

Subtypes extending a base class should do so without changing the behaviour
of the base class.

### Interface Segregation Principle (ISP)

Interfaces define a contract, and clients can use them without concerning
themselves with their impelmentation details.
The implementation can change and as long as a breaking change is not
made to the interface, the client does not need to change their logic.

The *Interface Segregation Principle* states that clients should not be forced
to depend on properties and methods that they do not use.

Prefer smaller, more cohesive interfaces. If an interface is too large,
we can logically split it up into multiple interfaces.

If a developer of a class that is implementing an interface finds
themselves having to mark properties and methods as not supported/not implemented,
perhaps the interface needs to be segregated.

### Dependency Inversion Principle (DIP)

The *Dependency Inversion Principle* describes how to handle dependencies
and write loosely coupled software.

    The high-level modules should not depend on low-level modules. Both should depend on abstractions.

    Abstractions should not depend upon details. Details should depend upon abstractions.

Rather than high-level calsses being dependent on lower-level classes,
they should depend on abstractions through an interface.
The interfaces do not depend on their implementations.
Instead, the implementations depend on the interfaces.

#### Inversion of Control (IOC)

*Inversion of Control* is a design principle in which a software system
receives the flow of control from reusable code, such as a framework.

In traditional procedural programming, a software system would call into
a reusable library. The IOC principle invert this flow of control,
by allowing the reusable code to call into the software system.

DI containers are frameworks tha provide DI functionality.

#### Dependency injection

With *dependency injection* dependencies are passed (injected) to a client
that need it.

The following are some of the benefits of DI.

* DI removes hardcoded dependencies and allow them to be changed,
  at either runtime (late binding, or runtime binding) or compile-time.
* DI allows us to write loosely coupled code.
* Testability increases in software applications that use DI.
  Loosely coupled code can be tested more easily.
  We can inject mock objects for the dependencies by using the interface
  and writing unit tests.
* Parallel development is made easy with DI.

There are different patterns available that can be used for DI.

##### Constructor injection

*Constructor injection* is a technique in ehich dependencies are passed
through a class's constructor.

The dependencies are made explicit: the object cannot be instantiated without
its dependencies (which is good).

##### Property injection

*Property injection* allows clients to supply a dependency through a public property.

If you need to provide callers with the ability to provide an instance
of a dependency, such as to override the default behaviour,
you can use this injection pattern.

The property injection pattern provides dependencies in an implicit way.

If you are going to use this pattern over an explicit one, a default instance
should be provided in some way.

##### Method injection

*Method injection* is similar to property injection, except a dependency
is provided through a method rather than a property.

##### Service locator

The *service locator* pattern uses a locator object that encapsulate
logic to determine and provide an instance of the dependencies that are
needed.

    var cache = ServiceLocator.GetInstance<ILogger>();

It is considered an anti-pattern by some people because it hides a class's
dependencies. As opposed to constructor injection, where we can see
the dependencies in the public constructor, we would have to look at
the code to find dependencies being resolved through the service locator.

#### DI containers

A *Dependency Injection container* (a.k.a *DI container* or *IoC container*)
is a framework that helps with DI. It creates and injects dependencies
for us automatically.

Leveraging a DI container eliminates the repetitive grunt work of handling
dependencies manually.


## Helping your team succeed

### Unit testing

*Unit testing* is the practice of testing the smallest testable units
of a software system, such as methods, to ensure that they are working
properly.

Unit tests can be automatically executed as part of a build process.

Unit tests should be atomic, deterministic, automated and repeatable,
isolated and independent, easy to set up and implement, and fast.

#### Atomic

Unit tests should only test a single assumption about a small piece of
functionality. The assumption should focus on a behaviour of the unit
being tested. Multiple tests are necessary to check all of the assumptions
for a given unit.

#### Deterministic

If no code changes are made, unit tests should yield the same result
every time they are executed.

#### Automated and repeatable

This will allow unit tests to be executed as part of a build process.

#### Isolated and independent

Each unit test should have the ability to be run independently of other
tests and in any order.

Unit tests should not depend on anything except the class we are testing.
It should not rely on other classses, nor should it depend on things such as
connecting to a database, using a hardware device,
accessing files on a file system, or communicating across a network.

With a testing framework and a DI framework, we can mock dependencies
for our unit tests.

#### Easy to set up and implement

Unit tests shold be easy to set up and implement. If they are not, this is a
*code smell*. The problem could be in the way the unit being tested is designed
or in the way the test is being written.

#### Fast

The execution of unit tests should not slow down development or build processes.

### The AAA pattern

The *AAA pattern* is a common unit testing pattern. It consists of separating
each unit test method into three sections: *Arrange*, *Act* and *Assert*.

#### Arrange

In this section of the unit test method, you arrange any preconditions
and inputs for the test.

#### Act

The act section is where you *act* on the unit that is being tested.
Logic should invoke the method being tested, passing in values that were
previously arranged.

#### Assert

In this part you assert that the results are what you expect.

### Naming conventions for unit tests

You should follow a naming conevtion for units tests. This provides not just
consinstency, but allows your tests to be a form of documentation.

If meaningful names are provided, everyone can know something about
the purpose of the test class and its methods just by looking at the names.

### Keeping unit tests up to date

As requirements change or new functionality is added, unit tests need
to be changed or added.

If a bug is found, the unit tests did not cover that particula scenario.
One or more unit tests should be created that incorporate the situation 
into the tests to ensure it remains fixed. *Bugs should only be found once*.

### Pair programming

*Pair programmin* is an agile software development technique where two developers
work together on the same deliverable. The person who is coding is the *driver*
while the other person, is the *navigator*.

Pair programming can improve code quality.

It is a good practice to rotate pairs and not just have the same two people
always pair up.

### Reviewing deliverables

Completed deliverables hould be reviewed to ensure that they are correct and
to identify any potential problems.

#### Code reviews

*Code reviews* are evaluations of code, typically conducted by peers.

It may be helpful to use a checklist during code reviews.
The checklist can serve as a reminder of issues to look out for that have been
found to be problematic in the past.

#### Formal inspections

*Formal inspections* is a group review method. They are meetings in which
deliverables (design or code) are reviewed in order to find defects.

In a formal inspection ivited participants are assigned a role that they
will play.

*Leader/moderator*: Facilitates the meeting and is responsible for obtaining
a productive review.

*Author*: The person who created the design or wrote the code that is being
reviewed. They may be required to explain anything that is unclrar or to provide
reasons why something that appears to be a defect is actually not one.

*Reviewer*: One or more individuals, who server as reviewers for the inspection.
They can prepare for the inspection by reviewing the deliverables before
the meeting takes place.

It may be helpful for the reviewers to have a checklist of items that they want
to focus on for the review.

*Recorder/scribe*: Is responsible for taking notes during the meeting.
They should record any defects found as well as action items.

#### Inspection meetings and follow-up

During the actual inspection meeting, reviewers should focus on identifying
defects and not on solutions. After the meeting, an inspection report is produced
summarizing the results of the inspection.

Defects should be placed in a backlog and assigned to someone for resolution.
Follow-up should take place to ensure that any action items were completed.

#### Walkthroughs

A *walkthrough* is an informal method of review. The author of a design
or code seliverable hosts a meeting in which they guide reviewers
through the deliverable.

Participants are not assigned specific roles.