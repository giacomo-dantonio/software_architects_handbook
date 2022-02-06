# Chapter 12 - Documenting and Reviewing Sotware Architectures

## Uses of software architecture documentation

### Communicating your architecture to others

During software architecture design, we identify all of the structures that make
up the architecture and how they interact with each other.
Documentation allows us to communicate those structures and interactions.

Different types of architecture view can help to cmmunicate the architecture to
everyone who needs to understand it.

### Assisting the development team

Learning about the structures and elements of the architecture and how they
interact with each other, will allow developers to understand how they should
be implementing their functionality.

### Educates team members

Developers who are unfamiliar with the system can use it as a guide to become
familiar with the architecture.

### Providing input for software architecture reviews

Architecture documentation is useful during this process because it
contains details that will allow a review team to analyze an architecture
and make these types of determination.

### Allowing for the reuse of architectural knowledge

The design decisions made, the design rationale that formed the decisions, and
any lessons learned can be leveraged when other sofware systems need to be created
or maintained.

### Help the software architect

It supports software architects to fulfill some of their responsibilities
by providing artifacts with whhich to communicate the architecture to others.

## Creating architecture descriptions (ADs)

An *architecture description* is a work product used to express and communicate
an architecture.

ADs identify the stakeholders of the software system and their concerns.
ADs consist of one or more architecture views, with the views addressing
the different concerns of the stakeholders.

### Software architecture views

*Architecture views* are used to ease understanding, as each one focuses on a
specific structure or structures of the architecture. This allows a software
architect to document and communicate only a small piece of the architecture
at a time.

Different views will focus on different aspects of the architecture, so the
intended usage of the architecture documentation will dictate the types of
view that you create.

### Software architecture notations

#### Informal software architecture notations

Informal notations are view of the architecture that are often created
with general-purpose tools, using whatever conventions the team deems appropriate.

Software architectes may consider using this notation for artifacts created for
the project's management team.

#### Semiformal software architecture notations

A semiformal notation in views is a standardized notation that can be used in
diagrams. However, fully-defined semantics are not part of a semiformal notation.

UML is an example of a semiformal notation.

#### Formal software architecture notations

Views of the architecture that use formal notations have precise semantics,
usually mathematically based. This allows for formal analysis of both the
syntax and the semantics.

Some formal notations are *Architecture Analysis and Design Language* (**AADL**)
and *System Modeling Language* (**SysML**).

### Including design rationales

Without documenting the design rationale the reasons that a design decision
has been made will not be known.

It is not necessary (or pratical) to record every design decision that is made
but any decisions that are important to the architecture are candidates
to be documented.

## Overview of the Unified Modeling Language (UML)

### Types of modeling

In UML there are two main types of modeling: *structural modeling* and
*behavioral modeling*.

Some structure diagrams in UML include:

* Class diagrams
* Component diagrams
* Package diagrams
* Deployment diagrams

Some of the behavior diagrams in UML include:

* Use case diagrams
* Sequence diagrams
* Activity diagrams

#### Class diagrams

Class diagrams show us the structure of a software system by allowing us to see
the classes and their relationships.

A rectangle is used in a class diagram to graphically represent a class and
each one can have up to three sections in it: *name*, *attributes*
and *operations*.

**Visibility** dictates the accessibility of a member (attribute or operation).

* `+` *public*
* `#` *protected*
* `~` *package*
* `-` *private*

An **association** is a broad term that refers to a semantic relationship between classes. It is shown on a class diagram as a solid line.

When there are no arrowheads at the end of the line, the navigability of the
association is unspecified. However sometimes this notation is used for
bidiretional associations.

**Aggregation** is a relationship in which a child object can exist
independently of the parent (e.g. car - tire). It is graphically
represented by a hollow diamond shape.

**Composition** is a relationship in which an object cannot exist independently
of another object (e.g. building - room). It is graphically represented by a
filled diamond shape.

A **dependency** is a type of relationship between UML elements in which one
element requires, needs, or depends on another element.
The dependency is sometimes referred to as a supplier/client relationship.

In an association one class may have a reference to the other as a member
variable. A dependecy relationship is slightly weaker. For example, a dependency
may exist because a return type or paramater for a method in one class
references another class.

A dependency is graphically represented by a dashed line with an open arrowhead.
Example: `FileImport --> StreamReader`.

**Generalization** (inheritance) is the process of abstracting common attributes
and opertions into a base class.
Generalization is graphically represented with a hollow triangle on the part
of the connecting line that is closest to the base class.

**Realization** denotes a relationship in which one element realizes or implements
the behaviour that another element specifies. An example is when a class
implements an interface.
Realization is graphically represented with a hollow triangle at the end of a dashed line.

A class can be designed as an interface using a **stereotype**.
Stereotypes are one of the extensibility mechanisms available in UML, which
allow you to extend vocabulary and introduce new wlements.
Stereotypes are graphically represented by enclosing the name in
guillemetes (« »).

#### Component diagrams

Component diagrams detail the structural relationship between
components of a system.
They are needed with complex software systems that consist of many components.
They are sometimes referred to as *wiring diagrams*.

Components communicate with each other through interfaces, and component
diagrams allows us to see system behavior as it relates to an interface.

Components are graphically represented as a rectangle with a component symbol
(a rectangluar block with two smaller rectangles on the left side).

Interfaces hat a component provides are graphically represented by a small circle
at the end of a line, which is also sometimes referred to as the
*lollipop* symbol.

Interfaces that a component requires are represented by a half circle at the end
of a line, which is also referred to as a *socket*.

#### Package diagrams

Packages logically group elements together and provide a namespace for the groups.
Package diagrams show the dependencies between packages in a software system.

A *package import* dependency is a relationship between an importing namespace
and an imported package. Thi allow us to reference package members from other
namespaces without fully qualifying them.

A *package merge* dependency is a relationship between two packages in which
one package is extended by the contents of another package.

A package is graphically represented by a symbol which looks like a file folder
with a name.

#### Deployment diagrams

Deployment diagrams represent the physical deployment of artifact on nodes.
An *artifact* is a physical piece of information, such as a source code file,
binary file, script, table in database or document.

A *node* is a computational resource.
A **device node** represents a physical computation resource (hardware).
An **execution environment node** is a software container that resides in a
device (e.g. operating system, JVM, Docker container).

Nodes are represented by a three-dimensional box.

#### Use case diagrams

Use cases are text that describes a software system's behavior as it responds
to requests from the system users, known as *actors*.

*Actor generalization* is a relationship between actors in which one actor
(descendant) inherits the role and properties from another actor (ancestor).

Actor generalization is represented with a hollow triangle on the part of
the connecting line closest to the ancestor.

A use case diagram is a graphic representation of a use case, the relevant actors
and their relationships.

Actors are represented by a stick figure with the name of the actor's role
appearing underneath it.
Use cases are graphically represented with a horizontally shaped oval.

#### Sequence diagrams

Sequence diagrams (also referred to as *event diagrams* or *event scenarios*)
model how components in a software system interact
and communicate. They describe a sequence of events from the software system.

An object is graphically represented by a rectangle with its *lifeline*
descending from the center of its bottom.
The **lifeline** is represented by a vertical dashed line.

The rectangle can show both the name of the object and the class
(`objectname:classname`). An object can be left unnamed.

**Activation boxes** on the lifelines show when an object is completeing a task.

Arrows are use to graphically represent **messages** that are passed between
objects.
*Synchronous* messages are shown as a solid line with a solid arrowhead.
*Asynchronous* messages are represented by a solid line with a line arrowhead.
*Reply/Return* messages are represented by a dashed line with a line arrowhead.

In order to model a **loop** in a sequence diagram a box is placed over the
part of the diagram that is iterating through a loop.

An **optional control** is represented with a box. An inverted tab at the top-left
corner of the box is labeled with **opt**.
Alternative (conditional) fragments are labeled with **alt**.

#### Activity diagrams

An activity diagram represents a seres of action in the form of a *workflow*.

An activity diagram begins with an initial state, or start point, which is
graphically represented by a small solid circle (**Start/Initial node**).
The diagram ends with a final state that is graphically represented by a small
filled circle inside another circle (**End/Final node**).
A **Flow final node**, which is a circle with and X inside, can be used
to represent the end of a specific process flow. Unlike the end node,
it only ends a single control flow and not the complete activity.

## Reviewing software architectures

### Software architecture analysis method (SAAM)

The original purpose of SAAM was to asses the modifiabilty of a software system,
altought it has been extended to review a software architecture for a variety
of quality attributes.

SAAM is a **scenario-based** review method.

A *scenario* is a description of the interaction between some source, such as
a stakeholder, and a software system.
*Software quality attribute scenarios* can be used to test software
quality attributes.

A software quality attribute scenario consists of the following parts:

* *Source of stimulus*: some entity, such a stakeholder or another software
    system.
* *Stimulus*: some condition that require a response from the software system.
* *Artifact*: the software that is stimulated.
* *Environment*: the set of conditions under which the stimulus occurs.
* *Response*: the activity that takes place when the stimilus arrives at the
    artifact.
* *Response Measure*.

#### Step 1 - Develop scenarios

Using requirements we can identify the different types of functionality that the
software system is supposed to support and the qualities it is expected to have.

It is often useful to take an iterative approach when developing scenarios.

#### Step 2 - Describe the architecture

In this step the software architect describes the architecture to the review team.

#### Step 3 - Classify and prioritize scenarios

Scenarios can be either *direct* or *indirect*.
If the software system does not require any modifications to perform the
scenario, it can be classified as direct scenario. If the scenario is not
directly supported, then it is an indirect scenario.

Classified scenarios should be prioritized based on importance.

#### Step 4 - Evaluate scenarios

For each scenario the software architect demonstrates how the architecture can
execute it.
The team should estimate the level of effort necessary to change the system so
that it can execute indirect scenarios.

#### Step 5 - Access scenario interaction

In this step the reviewers analyze the interaction of the scenarios.
If multiple *related* scenarios interact with the same component this may be
acceptable.
If multiple *unrelated* scenarios do that, this could be and indication of a
poor design. The component may be lacking a clear separation of responsibilities.

#### Step 6 - Create an overall evaluation

At this point the team shoudl have a list of scenarios that have been classified,
prioritized, and evaluated.

The review team must make a decision as to whether the architecture is viable and
can be accepted as is or if it has to be modified in some way.

[Skipping the other review methods..]