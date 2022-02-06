# Chapter 5 - Designing Software Architectures

*Architecture design processes* provide guidance to software architects
to ensure that a design satisfies requirements, quality attribute scenarios,
and constraints.

## Software architecture design

Software architecture design involves making decisions in order to satisfy
functional requirements, quality attributes, and constraints.

It comprises defining the structures that will make up the solution
and documenting them.

The design allows you to undestand how the elements behave and interact with
each other. Private implementations of the elements are not architecturally
significant.

### Making design decisions

The set of software requirements consists of a series of design issues that
must be solved.

The result of the design is a set of decisions that shape your software
architecture. The design is documented in artifacts that can be used for the
implementation of a solution.

A decision that is made for one design issue may affect another one.
Each decision for a design issue may not be optimal for another issue,
but the overall solution must be acceptable by satisfying all of the requirements.

### Software architecture design terms

#### Structure

Structures are grouping of, and relations between, elements.

Anything that is complex and made up of elements can be referred to as a
structure.

An architecture is made up of the structures, their elements,
and the relationships of those elements with each other.

#### Element

A generic term that can be used to represent any of the following terms:
system, subsystem, module, or component.

#### System

The software system represents the entire of the project, including all of its
subsystems.

#### Subsystem

Subsystems are logical groupings of elements that make up a larger system.

Subsystem can represent standalone software applications, but don't have to.

#### Module

Modules, like subsystems, are logical groupings of elements. Each module
is contained within a subsystem and consists of other modules and/or components.

Modules are typically focused on a *single logical area of responsibility*.

#### Component

Components are execution units that represent some well-defined functionality.
They typically encapsulate their implementation and expose their properties
and behaviours through an interface.

Components are the smallest level of abstraction and typically have a relatively
small scope.

## The importance of software architecture design

### Making key decisions

During software architecture design key decisions are made that will determine
whether requirements, including quality attributes, can be satisfied.

Software architecture enables or inhibits quality attributes.

### Avoid design decisions can incur technical debt

There is a cost to either delaying a decision or not making one at all.

*Technical debt* is the cost and effort for the additional work that will be
necessary later due to decisions that are made now, or because decisions have not been made.

A decision may be made knowing that it will cost some amount of technical debt.
You may decide to take an easier route to a solution, incurring in tecnical debt,
even though there is a better solution. Technical debt is not always a bad thing.

### Communicating the architecture to the others

The result of the *architecture design* allows you to communicae the software
architecture to the others (documentation?).

### Providing guidance to developers

A software architecture design imposes implementation constrations.
Knowing the design helps developers be aware of the implementation choices
available to them, and minimizes the possibility of making an incorrect
implementation decision.

### Influencing non-technical part of the project

Design decisions affect aspects of the software project other than the architecture. E.g. certain architecture design decisions could affect the purchasing of tools and licenses, the hiring of team members, etc.

## Top-down versus bottom-up design approaches

### Top-down approach

A *top-down* aproach starts witht the entire system at the hightest level, and then a process of decomposition begins to work downward toward more detail.
As decomposition progresses, the design becomes more detailed,
until the component level is reached
(that is, the *public interfaces* of the components).

A design using top-down approach is typically performed iteratively.

It is particularly effective if the domain is well understood.
It can handle large and complex projects and the method of design is planned.

#### Advantages of the top-down approach

It is a systematic approach to design and breaks the system down into smaller parts. On larger projects with multiple teams, work can be divided among
the teams.

Gives *ability to plan*: as further decomposition takes place, tasks
can be created for individual team members.

It can be particularly useful or large projects.

#### Disadvantages of the top-down approach

Strict top-down runs the risk of a *big design up front* (**BDUF**),
sometimes also referred to as *big up-front design* (**BUFD**).
It can be difficult to create the entire architecture up front.
Design flaws or missing functionality may not be uncovered until later in
the process.

A top-down approach works best when the domain is well understood,
which is not always the case. Even then, stakeholders and users can sometimes
be unclear as to what the software should do, and how it should work.

Knowledge sharing and reuse can be difficult with this approach.
Each team can work indipendently from each other. But this does not facilitate
the sharing of code or knowledge.

### Bottom-up approach

The *bottom-up approach* begins with the components that are needed for
the solution, and then the design works upward into higher level
of abstraction.

There is no upfront architecture design. The architecture *emerges* as more
work is completed. Sometimes this approach is refered to as
*emergent design* or *emergent architecture*.

This approach does not require that the domain be well-understood,
as the team focuses on a small piece at a time.
The system grows incrementally as the team learns more about the
problem domain.

#### Advantages of the bottom-up approach

Greater level of simplicity. The team only has to focus on individual pieces.

Works well with agile methodologies. In each iteration refactoring can take
place. Each iteration ends with a working version of the software.

Avoids the possibility of a big design up front, which can lead to
overdesigning a solution.

Allows to get feedback earlier, as coding and testing can begin very early
in the process.

Facilitates code reuse.

#### Disadvantages of the bottom-up approach

Bottom-up works well if change is cheap. However, refactoring software
architecture design can be very costly.

Can lead to lower levels of maintainability. With refactoring issues can arise.

Makes it more difficult to plan and estimate the entire project, as the entire
scope of work may not be known.

### Which approach should I use?

Use top-down if more than one of the following is true:

* The project is large in size
* The project is complex
* Enterprise software is beign designed for an organization
* The team is large, or there are multiple teams
* The domain is well-understood

Use bottom-up if more than one of the following is true:

* The project is small in size
* The project is not very complex
* Enterprise software for an organization is not beign designed
* The team is small, or there is only a single team
* The domain is not well-understood

Taking an extreme approach is not ideal. Software architects should
consider usign a combination of these two approaches.

The design of a *high-level architecture* provides some structure
that can be leveraged for further design and development.
It can be used to define and organize the teams and for resource
allocation, scheduling, and budget planning.

Focus on architecturally significant design issues. Once an high-level
architecture is established, you can employ a bottom-up approach.

## Greenfield versus brownfield software systems

### Greenfield systems

A *greenfield software system* is a completely new application, one in which
you can start with a clean state. A greenfield system can be designed for
a well-understood domain or for a novel domain.

A *well-understood domain* is mature, and the possibilities for innovation are
very limited. There are existing frameworks, tools and sample architectures
for the software that you need to build.

A *novel domain* requires a lot more innovation. You will find yourself spending
time building prototypes to test out your solutions.
It may beneficial to design a throwaway prototype initially.

### Brownfield systems

A *brownfield software system* is an existing software system.
If architecture changes are required, architecture design will be needed.

One of the crucial first steps is to gain an understanting of the existing
architecture. You need to understand the overalll structure, the elements,
and the relationships between those elements.

## Architectural drivers

*Architectural drivers* are considerations that need to be made
for the software system that are architecturally significant.
They describe what you are doing and why you are doing it.
They are inputs to the design process.

* Design objectives
* Primary functional requirements
* Quality attribute requirements
* Constraints
* Architectural concerns

### Design objectives

*Design objectives* focus on the purpose of the specific architecture design.
Whate are the reasons behind why the software is being designed?

A common design objective is to design a n architecture for a solution,
prior to development. The overall objective is to facilitate
the implementation of a solution that satisfies requirements.

Another example is for pre-sales activities, such as project proposals.
The design objective may focus on coming up with the software's capabilitiesm
the possible timeframe for delivery, a breakdown of work tasks,
and the feasibility of the proposed project.

Similarly, software architects may need to create a prototype (e.g. for
project proposal, to test out a new technology framework,
to create a proof of concept, or to explore how a certain quality
attribute might be effectively met).

### Primary functional requirements

*Primary functional requirements* are those that are critical to the
organizations's business goals.

Some of the primary functionality will come from the core domain.
It is what differentiates the organization from competitors.

While some functionality is highly affected by the architecture,
other functionality can be delivered qeually as well with different
architectures.

### Quality attribute scenarios

Quality attribute are measurable properties of the system.
They are one of the main drivers for software architecture design.
Quality attributes are tipically described in the context of a particular
scenario.

A *quality attribute scenario* is a short description of how the software
system should respond to a particular stimulus.

Scenarios make quality attributes measurable and testable.
Example: *When the user selects the Login option, a Login page is
displayed whitin two seconds*.

#### Prioritizing quality attribute scenarios

Prior to the start of the architecture design process, the quality attribute
scenarios should be prioritized.

Quality attribute scenarios can be prioritized by ranking them based on two
criteris: their *business importance* and the *technical risk* associated with
the scenario. A ranking scale of *high*, *medium* and *low* can be used.

One can assign a number to each quality attribute scenario
and put them in a table as this:

| business importance/technical risk | Low           | Medium     | High |
| ---------------------------------- | ------------- | ---------- | ---- |
| Low                                | 6, 21         | 7, 13      | 15   |
| Medium                             | 3, 10, 11     | 14, 16, 17 | 1, 5 |
| High                               | 4, 18, 19, 20 | 2, 12      | 8, 9 |

Quality attribute scenarios located toward the bottom-right side
of the table will be of higher importance.
Initial design iterations can focus on those first.

### Constraints

*Constraints* are decisions imposed on a software project that must
be satisfied by the architecture.

Examples include being required to use a certain technology,
having the ability to deploy to a particular type of target environment,
or using a specific programming language.

Non-technical constraints could be to abide by a certain regulation,
or that the project must meet a paricular deadline.

*Internal* constraints originate from within the organization and you
may have some control over them.

### Architectural concerns

*Architectural concerns* are interests of the software architect
that impact the software architecture. Just as the other drivers,
architectural concerns are design issues important to the software architect.

They need to be considered part of the design, but are not captured
as functional requirements.
The architetural concern may lead to a new quality attribute.

For example a software architect may have concerns related to software
instrumentation or logging.

## Leveraging design principles and existing solutions

The design issues facing a project may have already been solved by others.
Those solutions can be leveraged in your architecture design.
These architecture design principles and solutions are sometimes referred to as
*design concepts*.

### Selecting a design concept

There are many design concepts, so a software architect needs to know
hich ones ar suitable for a particular problem,
and then select the one that is most appropriate.

Some of the design concepts available to you include

* Software architecture patterns
* Reference architectures
* Tactics
* Externally developed software

### Software architecture patterns

*Software architeture patterns* provide solutions fo recurring
architecture design problems.

You shouldn't try to force the use on one. You should only use
an architecture pattern if it truly sovles the design issue that you have
and if it is the best solution given your context.

Chapter 7 is dedicated to software architecture patterns.

### Reference architectures

A *reference architecture* is a template for an architecture
that is best suited to a **particular domain**.
It is composed of design artifactes for a software architecture that provides recommended structures, elements, and the relationships between the elements.

#### Benefits of reference architectures

Reference architectures provide a tested solution to a problem domain,
and reduce some of the complexities involved in designing
a software architecture.

Re-using an architecture provides advantages such as quicker delivery of a
solution, reduces design effort, reduces costs, and increases quality.

#### Refactoring a reference architecture for your needs

Using a refernce architecture will require multiple iterations.
Design decisions will need to be made regarding the reference
architecture.

Refactoring can take place to meet the specific needs of the software application.

If a reference architecture deals with a particular design issue,
you will need to make design decisions about that issue, even if
you don't have a specific requirement related to it.
The decision might very well be to exclude something from your architecture
that is in the reference architecture.

#### Creating your own reference architecture

When an organization needs to create new software apoplications,
perhaps as part of a software product line,
it can use the architecture of an existing product as a reference architecture.

The added advantage (in comparison to any other reference architecture)
is that the reference architecture would be likely to already be
suited to your particular domain.

### Tactics

*Tactics* are proven techniques to influence quality attribute scenarios.
They focus on a single quality attribute.

* Satisfy maintenability by *increasing cohesion* and *reducing coupling*.
* Increase usability by providing friendly and informative messages
  to the user.
* Improve availability by implementing a retry strategy to handle
  a possible transient fault.
* Satisfy portability by ensuring that a software update properly
  cleans up the older version.

### Externally developed software

#### Buy or build?

You must first make sure that you understand the problem that you are
trying to solve, and the scope of that problem.
You will need to research whether externally developed software exists
that will solve the design problem.

##### Advantages/disadvantages of building

Advantages:

* The solution will be tailored to your organization.
  If a need arises to make changes or add functionality,
  the organization will be able to do in full authority.
* There could be a competitive advantage.

Disadvantages:

* It will require time and resources.
* The end result may not have as robust a set of features
  as an externally developed solution.

##### Advantages/disadvantages of buying

Advantages:

* It will save time.
* May be of higher quality. Feedback from other users may have exposed
  problems that have already been solved.

Disadvantages:

* Cost (if commercial).
* You may not have access to the source code.
* You may be limited in how the solution can be used.
* The solution's functionality may not exactly fit your needs.

#### Researching external software

Things to consider:

* Does it solve the design problem?
* Is the cost of the software acceptable?
* Is the type of license compatible with the project's needs?
* Is the software easy to use?
* Can the software be integrated with other technologies used in the project?
* Is the software stable/mature?
* Does it provide support?
* Is the software widely known, such that the organization can easily
  hire resources familiar with it?

A *POC* to ensure that it is a workable solution is a wise idea.

## Documenting the software architecture design

Sketching the architecture *views* and documenting the *design rationale*.

### Sketching the architetcture design

*Architecture views* are representations of a software architecture that
are used to document it and communicate it to various stakeholders.
Multiple views of an architecture are typically required.

Formal documentation of a software architecture to views is not typically
done as a part of the design process. That type of documentation
comes afterward.

Informal documentation, in the form of sketches, should take place during
the architeture design. Sketches can record the *structures*,
the *elements*, the *relationship between the elements*, and the
*design concept* used.

Sketches can be used to explain how requirements and quality attributes
were satisfied by the architecture design.

### Documenting the design rationale

A *design rationale* explains the reasons, and justification,
behind the decisions that are made during the design of the software architecture.
They can also include documentation on decisions that were *not made*,
as well as alternatives that were considered for decisions that were made.

The design rationale should refer to the specific structures that were designed
and the specific requirements that they intended to meet.

## Using a systematic approach to software architecture design

Software architects need to ensure that the architecture they are designing
will satisfy the architectural drivers, and a systematic approach
can assist in accomplishing that goal.

Using an established *architecture design process* will provide you
with guidance on how to go about designing an architecture that will
satisfy functional requirements and quality attribute scenarios.

### A general model of software architecture design

Paper:

Christine Hofmeister, PhilippeKruchten, Robert L. Nord, Henk Obbink,
Alexander Ran and Pierre America.
*A general model of software architecture design derived from five
industrial approaches*

The most architecture design processes involve

* analyzing architectural driver,
* designing candidate solutions that will satisfy the architectural drivers,
* and then evaluating the design decisions and candidate solutions
  to ensure that they are correct.

There are three main design activities (see picture on page 146).

#### Architectural analysis

During *architectural analysis* the problems that the architecture
is trying to solve are identified.

These are sometimes referred to as *architecturally significant
requirements* (*ASR*s). Not all the design issues that must be
considered are requirements though. We must adress all the
architectural drivers.

The output of this activity is a set of architectural drivers
that will server as the input to architectural synthesis.

#### Architectural syntesis

The *architectural syntesis* is where solutions are designed on the basis
of the set of architectural drivers that were identified in the
architectural analysis activity.

During this activity we leverage design concepts such as
architecture patterns, reference architectures, tactics
and externally developed software.

We combine them with the design of structures, elements and relationships
between the elements.

This produces *candidate solutions* for the set of architectural
drivers.

#### Architectural evaluations

In the *architectural evaluation* the candidate solutions that were
designed during architectural synthesis are evaluated to ensure
that they solve the problems and that all of the design
decisions are correct.

This will be the topic of Chapter 12.

### Architecture design is an iterative process

The design of the architecture occurs over multiple iterations until all architectural drivers have been addressed.

Each iteration starts by selecting the architectural drivers that will
be considered for that iteration.

If a candidate solution has been validated, that design decision is integrated
into the overall architecture.

### Selecting an architecture design process

To compare different design prcesses we can examine the activities and
the artifacts of the design process:

* What are the activities and the artifacts of the process?
* Are there any activites or artifacts that you think are not needed?
* Are there any activites or artifacts that you feel are lacking?
* What are the techniques and tools of the design process?

You should have an understanding of what each design process entails,
along with their strenghts and weaknesses.

## Attribute-driven Design (ADD)

*Attribute driven design* is an iterative, organized step-by-step method
that can be followed during architectural design iterations.

It pays particular attention to *software quality attributes* during
the design process. You need to consider quality design attributes
early in the design process.

The ADD process is focused on architecture design and doesn't cover
the entire architectural life cycle. It doesn't include the gathering
of architectural drivers, documenting the architecture or evaluating
the architecture.

There are eight steps (see figure on page 150).

### Step 1 - Reviewing inputs

The first step is to review the inputs into the attribute-driven design.
We want to ensure that we are clear on the overall design problem we are solving.

The inputs are as before:

* Design objectives,
* Primary functional requirements,
* Quality attribute scenarios,
* Constraints,
* Architectural concerns.

If there is some part of an architecture already in place (browfield or
greenfield in some later iteration) the existing architecture
must be considered as part of the inputs.

### Step 2 - Establishing the iteration goal and selecting inputs

Iterations always begin with Step 2 (Step 1 is preliminary).

At the start of each iteration we need to establish the *goal* for that
iteration. It should answer the question *What design issure are we trying
to solve in the iteration*?

Each goal will be associated with one or more inputs.

### Step 3 - Choosing one or more elements of the system to refine

Based on the iteration goal and the architectural drivers that we want to
create a solution for, we must seelct the various elements
that we want to decompose.

In the first iteration of a greenfield system you begin at the highest level
and start by decomposing the system itself.

In the next iterations the system has already been decomposed to some
degree and you select one or more existing elements to focus on.

### Step 4 - Choosing one or more design concepts that satisfy the inputs

Once elements have been selected for decomposition we need to select
one or more design concepts (architecture patterns, references architectures,
tactics and externally developed software) that can be used to satisfy
the inputs (architectural drivers).

### Step 5 - Instatiating architectural elements, allocating responsibilities, defining interfaces

Based on the design concepts choosen at step 4, analysis is performed
so that details can be provided regarding *responsabilities* for the
element being decomposed, along with *public interfaces* of the
elements being exposed.

Each element beign decomposed (parent element) may yield one or more child
elements. The responsibilities of the child elements will be a subset
of the responsibilities of the parent element.

### Step 6 - Sketching views and recording design decisions

In this step, all of the design decisions that were made during this iteration
are documented. The documentation should also include the design rationale.

The artifacts creates in this step can simply be sketches and do not have
to be the formal, detailed software architecture views.

### Step 7 - Performing analysis of current design and reviewing the iteration

In the final step of the iteration the design decisions are analyzed
to ensure that they are correct and sstisfy the iteration goal and architectural
drivers that were established for the iteration.

### Step 8 - Iterating if necessary

If more iterations are needed, the process go back to *Step 2*.

## Microsoft's technique for architecture and design

Like ADD, it is an iterative, step-by-step method.

See picture on page 154.

### Step 1 - Identifying architecture objectives

The purpose of this step is to ensure that the design process has clear
objectives so that the solution focuses on the appropriate problems.

The various architectural drivers, such as design objectives, primary
functional requirements, quality attribute scenarios, constraints,
and architectural concerns all combine to form the architecture
objectives.

Step 1 will occur only once. Each design iteration will start with Step 2.

### Step 2 - Identifying the key scenarios

A scenario is defined as a more encompassing user interaction with the
software system, not just a single use case.

Key scenarios are the most important that are required
for the success of the application.

Scenarios could be an issue, an architecturally signifcant use case (one
that is business critical and has a high impact), or involve an intersection
between functional requirements and quality attributes.

### Step 3 - Creating an application overview

An application overview is what the architecture will look like
when it is complete. It is intended to connect an architecture design
with real-world decision.

Creating an application overview consists of the following steps.

#### Determining your application type

The software architect must determin what type of application is appropriate
based on the objectives and key scenarios. Examples are web, mobile, service
and Windows desktop application.

#### Identifying your deployment constraints

You may be required to follow particular policies of the organization.
The infrastracture and target environment of the software application may be
dictated by the organization. Such constraints may be something you will
have to work around.

#### Identifying important architecture design styles

Usign an architecture style (pattern) promotes reuse by leveraging
a known solution to a recurring problem.

#### Determining relevant technologies

The decisions are based on the type of application, the architectural styles,
and the key quality attributes.

In addition to technologies specific to the application type (e.g. a web
server for a web application), technologies will be needed for categories such as
application infrastracture, data access, database server, development tools,
and integration.

### Step 4 - Identifying key issues

This step involves identifying the important issues you may be facing
in the architecture. These issues may require additional focus because
they are areas where mistakes are most likely to be made.

Key issues typically map to either *quality attributes* or
*cross cutting concerns*. Analyzin quality attributes and cross-cutting
concerns closely based on the issues you identify will alow you to know
which areas ot give extra attention to in your design.

### Step 5 - Defining candidate solutions

Depending on wheter or not this is the first iteration, either an initial
architecture is created, or the existing architecture is refined to include
the solutions that were designed in the current iteration.

Once candidate solutions are integrated into the architecture design for the
current iteration, the architecture can be reviewed and evaluated.

## Architecture-centric design method

The *architecture-centric design method* is a lightweight method with a product
focus and seeks to ensuse that the software architecture mantains a balance between businees and technical concerns.
It attemps to make the software architecture the intersection between
requirements and the solution.

It is not a complete development process. It can be used in conjunction
with other methods to cover activities ooutside of architecture.

See picture on page 158.

### Step 1 - Discovering architectural drivers

The first step is to meet with the stakeholders to determine
the architectural drivers. The priorizatiopn of quality attribute scenarios
also takes place in this step.

### Step 2 - Establishing project scope

In this step the architectural drivers are reviewed.

First, consolidation of the information gathered takes place,
to remove duplicate architectural drivers.

Next, if any of the architectural drivers are unclear, missing, or incomplete,
additional information will be needed. The same is true for any requirements
or quality attribute scenarios that are not measurable or testable.

### Step 3 - Creating notional architecture

Using the architectural drivers, the initial representations of the
structures that make up the architecture are created and documented.

Not a lot of time is spent on the notional architecture. The idea is that
the architecture will be refined through multiple iterations.

### Step 4 - Architectural review

A review is conducted on the architecture as it currently exists.

The purpose of this review is to ensure that all of the design decisions
are correct and to uncover any potential issues or problems with the
architecture.

### Step 5 - Production go/no-go

Once the architectural review is complete, a decision is made as to whether
the architecture is complete and ready for production.

Production refers to implementation, including using the architecture in
the detailed design of elements, coding, integration, and testing.

It is possible that only parts of the design require further refinement,
in which case a portion of the design can move to production.

In the production decision is a go, the process can skip ahead to production
planning. Otherwise the process moves on to Step 6.

### Step 6 - Experiment planning

Any experiment that the team feels are necessesary are planned.

The purpose of an experiment may be to resolve an issue uncovered during
the architectural review, to gain a greater understanding of one or more
architectural drivers, or to improve elements and modules of the design.

Experiment planning includes solidifying the goals of the experiment,
estimating the level of effort, and assigning resources.

### Step 7 - Experimenting with and refining the architecture

Experiments are executed, ther results of the experiments are recorded.
If the architecture needs to be refined, it is done during this step.

The process goes back to step 4, so thate another architectural review
can take place.

### Production planning and production

Once the architecture is complete, production planning is conducted.
*Production* in this context refers to using the architecture in implementation.

The project management creates plans for the work and bases them, in part,
on the architecture.

## Architecture development method (ADM)

The *architecture development method* is a step-by-step software architecture
design approach specifically made for enterprise architectures.

The process as a whole is iterative, but it is also iterative between
phases and within a single phase.

### The Open Group Architecture Framework (TOGAF)

ADM is a part of TOGAF, which is a framework for enterprise architecture.

Four architecture domains are defined by TOGAF (*BDAT domains*):

* business,
* data,
* application,
* and technology domains.

### Phases of the ADM

There is a preliminary phase in which the organization prepares for a
successful software architecture implementation. After this there are
eight phases.

See picture on page 163.

[...] *skipping because not interesting*

## Tracking progress of the software architecture's design

Keeping track of progress enables you to know how much of the design work
is complete, and how much of it remains. The remaining work can be
prioritized.

If you are using an agile methodology, you may be using product and
sprint backlogs to track progress.

### Using a backlog

A *product backlog* contains a complete list of the features and bugs
of the product.

You should consider creating a product backlog that is specific to th
software architecture of the project, which is separate
from the other product backlog.

Prior to each sprint, sprint planning takes place. Items from the product
backlog that get selected for a sprint are then moved to the sprint
backlog. Once an item is completed, it can be removed from the backlog.

### Prioritizing the backlog

Product backlog items should be linearly ordered based on criteria.
One possible set of criteria is called *DIVE*.
It stands for **D**ependencies, to **I**nsure against risks,
business **V**alue, and estimated **E**ffort.

#### Dependencies

If item *A* depends on item *B*, *B* would be prioritized higher than item *A*.

#### Insure against risks

Includes both business and technical risks. Taking potential risks into
consideration may lead the team to prioritize a backlog item higher or lower.

#### Business value

Product backlog items with greater levels of business value may be deemed
a higher priority.

#### Estimated effort

The estimated effort for a product backlog item may be a factor when
prioritizing work. There may be a case where a product backlog item
has a large estimated effort, and the team wants to tackle the
item sooner rather than later to ensure that it will be completed in time.

### Active and dynamic architecture backlogs

The architecture backlog is not static and will evolve as the architecture
design takes place.

As architecture design iterations are completed, new architectural drivers
may be uncovered, necessitating the need for new items to be added to the
backlog.

When the design is reviewed a problem may become appartent, requiring
further work to be done.

Changes to the architecture backlog may prompt you to revisit the priorities
of the backlog items.