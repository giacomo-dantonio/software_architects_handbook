# Chapter 7 - Software architecture patterns

A *software architecture pattern* is a solution to a recurring problem that is
well understood, in a particular context.

Each pattern consists of a **context**, a **problem** and a **solution**.
Patterns codify knowledge and experience into a solution that we can reuse.

Software architecture patterns are similar to design patterns, except that they
are broader in scope and are applied at architecture level.

Software architecture ptterns provide the structure and main components
of the software system being built. They introduce design constraints, which
reduce complexity and help to prevent incorrect decisions.

## Architecture styles vs. patterns

An *architecture style* is a set of elements, and the vocabulary to be used
for those elements, that is available to be used in an architecture.
It constraints an architecture design by restricting the available design choices.

For example the microservice architecture style comes with the constraint that
each service should be independent of the others.
A system that follows a microservice architecture style will be able to deploy
services independently, isolate faults for a particular service, and use a
technology of the teams's choosing for a given service.

A *software architecture pattern* is a particular arrangement of the available
elements into a solution for a recurring problem given a certain context.
Given a particular architecture style, we can use the vocabulary of that style
to express how we want to use the elements available in a certain way.

## Layered architecture

In a *layered architecture* the software application is divided into various horizontal layers, witch each layer located on top of a lower layer.
Each layer is dependent on one or more layers below it, but is independent of the layers above it.

### Open vs. closed layers

With a closed layer, requests that are flowing down the stack form the layer above
must go through it and cannot bypass it.

Closed layer provide layer of isolation, which makes code easier to change, write
and understand. Change made to one layer of the application will not affect
components in the other layers.

If the layer are open, maintanability is lowered because multiple layer can now
call into another layer.

There may be situations in which it is advantageous to have an open layer.
E.g. when unnecessary traffic can result when each layer must be passed
even if one or more of them is just passing requests on to the next layer.

### Tiers vs. layers

**Layers** are logical separations of a software application and **tiers** are
physical ones.

Layers are a way to organize functionality and components. Different layers do
not necessarily have to be located on different physical machines.

Tiers concern themselves with the physical location of the functionality
and components.

### Advantages of layered architectures

This pattern reduces complexity by achieveing a *Separation of Concerns* (*SoC*).
Each layer is independent and can be understood on its own without
the other layers.

Dependencies between layers can be minimized, which further reduces complexity.

Layered architectures can make development easier. The way that the architecture
separates the application logic matches up well with how many organizations
hire their reources and allocate tasks during a project
(e.g. UI developers for the presentation layer,
and backend developers for the business and data layers).

This pattern increases testability.

When an application usign a layered architecture is deployed to different tiers,
there are additional benefits:

* Increased scalability (more hardware can be added to each tier).
* Greater level of availability when multiple machines are used per layer.
* Enhances security (firewalls can be placed in between the various layers).
* Physical tiers can be reused, just like logical ones.

### Disadvantages of layered architectures

Although the layers can be designed to be independent, a requirement change may
require changes in multiple layers (coupling).
For example, adding a new field will require changes to multiple layers.

More code will be necessary to provide the interfaces and other logic for
the communication between layers.

If you are designing a high-performance application, you should be aware
that there can be inefficiencies in having a request go through multiple layers.

Disadvantages when deploying to multiple tiers:

* Deploying to separate tiers has an additional performance cost.
* Greater monetary cost.
* An internal team will be needed to manage the physical hardware (or use
  a cloud solution instead).

### Client-server architecture (two-tier architecture)

In a distributed application that uses a client-server architecture,
clients and server communicate with each other directly.
There can be multiple clients connected to a single server.

The client part of the application contains the user interface code and
the server contains the database.

When the client contains a significant portion of the logic and is handling
a large share of the workload, it is known as a **thick** or **fat client**. 
When the server is doing that instead, the client is known as a **thin client**.

If a team isn't diligent, business logic might be duplicated on the client and the server, violating the DRY principle.

#### Using stored procedures for application logic

If application logic exists *in the database* it is commonly found in stored
procedures.

A *stored procedure* is a grouping of one or more SQL statements that forms
a logical unit to accomplish some task. It can be used to do a combination
of retrieving, inserting, updating, and deleting data.

##### Benefits

The use of stored procedures redues the amount of network traffic between
the client and the server.

Store procedures are compiled the first time they are executed,
at which time an execution plan is created that a database's query engine
can use to optimize its use on subsequent calls.

There are security advantages to using store procedures as users and applications
do not need to be granted permission to the underlying database objects.

##### Drawbacks

There are limited coding constructs, as compared with high-level
programming languages, that are available for use in application logic.

Having some of your business logic located in stored procedures also means
that your business logic isn't centralized.

Application logic should not be placed in stored procedures.
It belongs outside the data layer, independent and decoupled from the
mechanism used to store the data.

For complex queries and queries requiring multiple statements and large amounts of data the performance advantages of stored prcedures can be useful.

### N-tier architecture

With and *n-tier* or *multitier architecture* there are multiple tiers in an
architecture.

See pic on page 226.

One of the most widely used variation of this arcitecture is the *three-tier architecture*, most commen in web applications. With web applications rich client applications containing buisness logic were not ideal.

The three-tier architecture speartes logic into *presentation*, *business* and *data* layers.

#### Presentation tier

The *presentation tier* provides functionality for the application's UI.
Data is presented to the user and input is received from users.

Aspects of the *usability* quality attribute should be concern of
the presentation tier.

The tier should contain logic to render the user interface. It should also
provide some basic validation to help users avoid or minimize mistakes.
Developers should be careful not to introduce business logic into the validation,
which should be handled by the business tier.

The presentation tier should provide users with useful feedback.

Software architects should strive to design thin clients that minize the
amount of logic that exists in the presentation tier.

#### Business tier

The *business tier* (sometimes referred to as the *application tier*) provides the
implementation for the business logic of the application, including such things
as business rules, validations, and calculation logic.

The business tier serves as an intermediary between the presentation and
data tiers. It provides the presentatoin tier with services, commands,
and data that it can use, and it interacts with the data tier to retrieve
and manipulate data.

#### Data tier

The *data tier* provides functionality to access and manage data.
The data tier constaina a data store for persistent storage, such as an RDBMS.

## Event-driven architecture

An **event** is the occurrence of something deemed significant in a software
application.

An example is the placement of a purchase order or the posting of a letter grade
for a course that a student is taking.

An **event-driven architecture** (**EDA**) is a distributed, asynchronous
software architecture pattern that integrates application and component through
the production and handling of events.

By tracking events we don't miss anything of significance realted to the
business domain.

EDAs are *loosely coupled*. The producer of an event does not have any knowledge
of the event subscribers.

SOA can complement EDA because service operations can be called
based on events being triggered.

EDAs can be relatively complex. Issues may occur due to a lack of responsiveness,
performance issues, or failures with event mediators and event brokers.

### Event channels

Event messages contain data about an event and are created by event producers.
These event messages use **event channels**, which are streams of event messages,
to travel to an event processor.

#### Message queues

Message queues ensure that there is *one, and only one receiver* for a message.
This means that only one event processor will receive and event from an event
channel.

##### The point-to-point channel pattern

The point-to-point channel pattern is a messaging pattern used when we want
to ensure that there will be exactly one receiver for a given message.

If more than one receiver attempts to consume a message, the event channel will
ensure that only one of them succedds. Since the event channel is handling that,
it removes any need for coordinatin between the event processors.

#### Message topics

Message topics allow multiple event consumer to receive an event message.

##### The publish-subscribe pattern

The pulish-subscribe pattern, sometimes referred to as *pub/sub*, is a
messaging pattern that provides a way for a sender (publisher) to broadcast
a message to interested parties (subscribers).

The messages can be sent without any knowledge of the subscribers or even if there
are no subscribers. Similarly, it allows subscribers to show interest in a
particular message without any knowledge of the publishers or even if there are
no publishers.

### Event-driven architecture topologies

#### The mediator topology

A *mediator topology* for EDAs uses a single event queue and an event mediator
to route events to the relevant event processors.

This topology is commonly used when multiple steps are required to process
an event.

[see picture on page 230]

Event producers send events into an **event queue**.
These events are referred to as *initial events*.
There can be many event queues in an EDA.

Event queues are responsible for sending event messages on to the
**event mediator**.
The event mediator the performs any necessary orchestration.

After the event mediator orchestrates each event from the event queue,
it creates one or more asynchronous *processing events* based on the
orchestration.

These processing events get sent out to an **event channel**, which can
either be a message queue or a message topic.
Message topics are more commonly used.

**Event processors** listen in on event channels to pick up events
and process them.

##### Implementations

An event mediator can be implemented in a number of different ways.

For simple orchestrations, an integration hub can be used.
These typically allow you to define mediaton rules using a
*domain-specific-language* (**DSL**) for the routing of the events.

For a more complex orchestration of events, *Business Process Execution
Language* (**BPEL**) can be used in conjunction with a BPEL engine.
BPEL is frequently used with SOA and web services.

Large software applications with complex orchestration needs,
which may even include human interactions, may opt to implement
an event mediator that uses a *Business Process Manager* (**BPM**).

Business process management involves modeling,
automating and executing business workflows.
Some business process managers use *Business Process Model and Notation*
(**BPMN**) to define business processes.

Software architects need to understand the needs of the software application in order to select an appropriate implementation.

#### The broker topology

In a broker topology the event messages created by event producers enter an event broker (sometimes referred to as *event bus*).

The event broker contains all of the event channels udes for the event flow.
The event channels may be message queues, message topics or some combination
of the two.

There is no event queue with the broker topology. The event processors are
reponsible for picking up events from an event broker.

[see picture on page 232]

This topology is ideal when the processing flow is fairly simple and there is no
need for centralized event orchestration.

Event flow to the *event processor* from the *event broker* and, as part of the processing, new events may be created.

### Event processing styles

*Event processors* are components that have a specific task and contain logic
to analyze and take action on events. Each event processor should be independent
and loosely coupled with other event processors.

#### Simple event processing (SEP)

In SEP notable events are immediately routed in order to initiate some type
of downstream action.

This type of processing can be used for real-time workflows. It also includes
functionality such as transforming event schemas from one form to another,
generating multiple events based on the payload of a single event,
and supplementing an event payload with additional data.

#### Event stream processing (ESP)

ESP involves analyzing streams of event data and the taking any necessary
action based on that analysis.
Events are screened based on various conditions and then either an action
may be taken for the event or the event may be ignored.

Example: stock trading system in which an event takes place and enters an event
stream when a stock ticker reports a change in price.

#### Complex event processing (CEP)

In CEP, analysis is performed to find patterns in events to determine
whether a more complex event has occurred.

Events may be correlated over multiple dimensions, such as casual,
temporal or spatial.

CEP can take place over a longer period of time as compared to the other
types of event processing.
This might be used to detect business threats, opportunities, or other anomalies.

Example: a credit card fraud engine.

### Types of event-driven functionality

#### Event notification

An architecture that provides *event notification* is one in which
the software system sends a message when an event takes place.
The mediator and broker topologies allow us to implement event notifications.

There is a loose coupling between the event producer and any event consumers
as well as between the logic that sends event messages and logic that responds
to the events.

The drawback is that it can be difficult to see the logical flow
of event notifications.
This makes it more difficult to debug and maintain.

#### Event-carried state transfer

Event-carried state transfer is a variation on event notification.

When an event consumer receives an event notification, it may need more information from the event producer in order to take an action.
This requires the event processor to query the event producer in some way,
such as through an API, for this information.

The subscriber is coupled to the producer.

Callbacks increase network load and traffic. One way to resolve this is to add
state information to the events so that they contain enough information
to be useful for potential consumers.

#### Event-sourcing

With event-sourcing the events that take place in a system, such as state changes,
are persisted in an event store. Having a complete record of all the events
that took place allows it to server as a source of truth.

Events should be immutable as they represent something that has already taken
place.

Event-sourcing introduces some added complexity into a software system.
Multiple instances of an application and multithreaded applications might be
persisting events to an event store.

Consideration must be given to ensure that older events, possibly with different
event schemas, can still be replayed with the current logic.

## The Model-View-Controller pattern

The Model-View-Controller (*MVC*) pattern is widely used for the UI
of an application. It is particularly well suited to web applications.

[See picture on page 237]

### Model

The model manages the application data and the state.

Among its responsibilities is the processing of data to and from a data store, such as a database.

A model is independendent of the controllers and the views, allowing them to be
reused with different user interfaces.

Models receive directives from controllers to retrieve and update data.

### View

The view is responsible for the presentation of the application.

As users manipulate a view, such as providing input or providing some
user action, the view will send this information to a controller.

### Controller

As users navigate a web application, requests are routed to the appropriate
controller based on routing configuration. A controller acts as an intermediary
between the model and the view.

A controller executes application logic to select the appropriate view
and sends it the information that it needs to render the user interface.

View notify controllers of user actions.
Controllers will update the model based on user actions.

### Advantages of the MVC pattern

It allows for a separation of concerns. It make it easier to change the presentation without affecting the data, and viceversa.
It also makes each part easier to test.

The MVC pattern makes presentation objects and models more reusable.

It allows developers to specialize in either frontend or backend development.

### Disadvantage of the MVC pattern

If your team is made of full stack developers, they need to be skilled
in multiple technologies.

If a model is providing notifications directly to views, frequent
changes may result in excessive updates to views.

## The Model-View-Presenter pattern

Each view in the *MVP* pattern typically has a corresponding interface
(view interface). Presenters are coupled with the view interfaces.

Compared with the MVC pattern, the view is more loosely coupled to the model
because the two do not interact with each other directly.

[See picture on page 239]

### Model

As in the MVC pattern, the model interacts with the database to retrieve
and update data.

The model receives messages from the presenter for updates and reports
state changes back to the presenter.

Models in the MVP pattern do not interact directly with views.

### View

Each view in the MVP pattern implements an interface (view interface).

As the user interacts with the view, the view will send messages to the presenter to act on the events and data.

Views are more passive in the MVP model and rely on the presenter to provide
information on what to display.

### Presenter

The presenter is the intermediary between the model and the view.
It interacts with both of them.

A presenter will receive data from the model and format it for the view
to display, taking an active role in the presentation logic.

In the MVP pattern each presenter typically handles one, and only one, view.

## The Model-View-ViewModel

The *MVVM* pattern separates the UI from the rest of the application.

[See picture on page 240]

There is typically a significant amount of interaction between views and
ViewModels, facilitated by data binding.

The MVVM pattern works well for rich desktop applications.
An example is *Windows Presentation Foundation* (*WPF*).

### Model

Same as in MVC and MVP: the model uses the database to retrieve and update
data.

In MVVM applications there may be direct binding with model properties.
Models commonly raise property changed notifications.

### View

The view is responsible for the user interface. In the MVVM pattern,
the view is active. Views are aware of the model and ViewModel.

While views handle their own events, they do not mantain state.
They must relay unser actions to the ViewModel, which can
be done through a mechanism such as data binding or commands.

A goal of the MVVM pattern is to minimize the amount of code in views.


### ViewModel

The ViewModel in the MVVM pattern is similar to the controller and presenter
objects of the other patterns in that they coordinate between the view and
the model.

ViewModels provide data to views for display and manipulation, and also contain
interaction logic to communicate with views and models.

The ViewModel contains navigation logic to handle moving to a different view.

## The Command Query Responsibility Segregation pattern

Command Query Responsibility Segregation (**CQRS**) is a pattern in which
the model that is used to read information is separated from the model
that is used to update information.

In a more traditional architecture, a single object model is used for both
reading and updating data. The same represetnation of an entity 
must support all of the *create*, *read*, *update*, and *delete* (**CRUD**)
operations, making them alrer than they need to be in all circumstances.

This can also make managing security and authorization more complex as each class
is used for both read and write operations.

Multiple operations may be taking place in parallel on the same set of data.
There is a risk of data contention if records are locked, or update conflicts
due to concurrent updates.

### The query model and the command model

CQRS separates the object models for queries and commands.
The **query model** is responsible for reads and the **command model**
is responsible for updates.

Query objects only return data and do not alter state, while command objects
alter state and do not return data.

If taken to the next level, the query and command models can be made to
utilize separate databases.
The two databases must be kept in sync.

### Using event-sourcing with CQRS

CQRS and events complement each other, so it is common for system that use
CQRS to leverage the use ove events.

Event-sourcing involves persisting events that take place in a system such that
the event store can serve as the record of truth.

### Advantages of CQRS

CQRS is well suited to complex domains and provides a separation of concerns
that helps to minimize and manage the complexity.

Development teams can be organized so that one team focuss on the query model
while another focuses on the command model.

Performance can be improved by optimizing the schema specifically for each model.
Data in the query model's data store can be denormalized in order to increase
the performance of queries that the application needs to execute.

Security improves with CQRS because it makes it easier to ensure that only
the right classes can update data.

### Disadvantages of CQRS

For systems that simply need basic CRUD operations, implementing a CQRS system
may introduce unnecessary complexity.

CQRS is not applicable to all situations. CQRS does not have to be applied to
the entiriety of a software system.

The software system will follow an *eventual consistency* model where if
no new updates are made to a given item, eventually all access to that item
will acquire the latest data.

This is in constrast with a *strong consistency* model, in which all data changes
are atomic and a transaction is not allowed to complete until all of the changes
have been completed successfully or, in the case of a failure, everything has
been undone.

## Service-oriented architecture

*Service-oriented architecture* is an architectural pattern
for developing software systems by creating loosely coupled,
interoperable services that work together to automate business processes.

A *service* is a part of a software application that performs a specific task.
Service *consumers* can be web applications, mobile applications,
desktop applications, and others.

SOA decomposes application logic into smaller units that can be reused
and distributed.

Services can vary in size and one service can be composed of multiple
other services to accomplish its task.

SOA does not require web services, although they happen to be a perfect
technology to implement with SOA.

### Benefits of using a SOA

#### Increases alignment between business and technology

Business logic, in the form of business entities and business processes,
exists in the form of physical services with an SOA.

SOA provides organizational agility through service abstraction and loose
coupling between business and application logic.
When changes are required, they can more easily be made so that the business
remains in alignment with the technology.

#### Promotes federation within an organization

Federation in an organization is an environment in which the software
applications and resources work together while simultaneously
mantaining their autonomy.

As long as ther is a common, open, and standardized frameworks,
legacy and non-legacy applications can work together.

#### Allows for vendors diversity

In addition to allowing organizations with potentially disparate vendors
to work together, an organization can use different vendors interally
to achieve best-of-breed solutions.

#### Increases intrinsic interoperability

SOA allows for the sharing of data and the reuse of logic. It can allow
an existing software system to integrate with others through web services.

#### Works well with agile development technologies

The fact that complex software systems are broken down into services
with small, manageable units of logic fits well with an iterative process
and how tasks are allocated to resources.

### Cost-benefit analysis of SOA

Adopting a SOA can be a gradual, evolutionary process.
Because a contemporary SOA promotes federation, creating an SON
does not have to be an all-or-nothing rocess.
An organization does not have to replace all existing systems at once.
Legacy logic can be encapsulated and can work with new application logic.
As a result, the adoption of SOA and its related costs can be spread out
over time.

Adopting SOA leads to reduced integration expenses. A loosely coupled SOA
should reduce complexity and therefore will reduce the cost to integrate and
manage such systems.

SOA can increase asset reuse. By creating business processes by reusing
existing services, costs and time to market can be reduced.

Adopting an SOA reduces business risk and exposure. SOA facilitates
the controll of business processes, allows fo the implementation of security
and privacy policies, and provdes audit trails for data, which can all reduce
risk.

### Challenges with SOA

SOA solutions can cause enterprise architectures to grow larger in scope
and functionality as compared to the legacy systems.

In an SOA new layers may be added to software architectures, providing
more areas where failure can occur and making it more difficult to pinpoint
those failures.

People can be a challenge to SOA-adoption because there are still technical
and business professionals who are not familiar with SOA and do not know what
it means.

### Key principles for service orientation

#### Standardized service contract

Each service should have a standardized *service contract*,
consisting of a technical interface and service description.

Services have to adhere to a common agreement.

#### Service loose coupling

Services should be loosely coupled and independent of each other.
Service contracts should be designed to have independence from
service consumers and from their implementation.

#### Service abstraction

Service contracts should only contain information that it is necessary to
reveal.
Service implementations should also hide their details.

#### Service reusability

Services should be designed with reusability in mind, with their service
logic being independent of a particular technology or business process.

#### Service autonomy

Services should be designed to be autonomous, with more independence
from their runtime environment.
The design should seek to provide services with increased control over
their runtime environments.

#### Service statelessness

Service design should strive to minimize the amount of state management that
takes place, and separate state data from services.

#### Service discoverability

Services need to be discoverable.
By including consistent and meaningful metadata with a service,
the purpose of the service and the functionality it provides can be communicated.
Service developers are required to provide this metadata.

#### Service composability

Services should be designed so that they are composable.
This is the ability to use a service in any number of other services,
and those services may themselves be composed of other services.

Service composition is heavily related to service reusability.

### SOA delivery strategies

#### The top-down strategy

The top-down strategy begins with analysis. IT centers on the organization's
business logic. When done properly, results in a high quality SOA.

This approach requires many resoureces, in terms of time and money.

#### The bottom-up strategy

The bottom-up approach begins with the web services themselves.
They are created on an *as-needed* basis.

Integration with a legacy system is a common motivation for using the bottom-up
strategy.

This is not a valid approach to achieving SOA.

#### The agile strategy

Sometimes referred to as meet-in-the-middle approach.
Analysis can occurr concurrently with design and development.

Pairs well with an iterative, agile software development methodology.

### Service-oriented analysis

Service oriented analysis is used to decide what services should be built
and what logic should be encapsulated by each service.
It is an iterative process which takes place for each business process.

Three steps to service-oriented analysis.

#### Defining business automation requirements

The first step is to define the business automation requirements for the
business process being analyzed.

The business process can be documented at a high level (the details
are used in the third step).

#### Identifying existing automation systems

The next step involves identifying what parts, if any, of the business
process logic are already automated.

#### Modeling candidate services

The final step consists of identifying service operation candidates and grouping
them into candidate services.

Modeling candidate services should be a collaborative process between technical
and business resources.

#### Service layers and service models

Enterprise logic consists of both business and application logic.

Business logic is an implementation of the business requirements and includes
an organization's business processes.
These requirements include things such as constraints, dependencies,
preconditions and postconditions.

Application logic is the implementation of business logic in a technology
solution. It can be a purchased solution, a custom developed solution,
or some combination of the two.

Service-orientatin principles can be applied to both business and
application logic.

A service layer in a software architecture is typically placed between
the business and the application layers. This allows services to represent
business logic and abstract application logic.

During service modeling, it becomes apparent that there are some common types
of services. These types are **service models**, which can be used to classify
candidate services. Those candidate services can be grouped together based
on their service model into a **service layer**.

Three common service models and layers.

##### Task service

This type of servie has a **non-agnostic functional context**:
it contains business process logic and was created for a specific business
task or process.

Task services do not have a gread deal of reuse protential.

##### Entity service

This service model has an **agnostic functional context**: its logic is not
bound to a single business process and is reusable.

Entity services are business-centric services that are associated with
one or more business entities.

##### Utility service

Like entity services, they have an agnostic functional context.
They contain multi-purpose logic and are highly reusable.

Utility services are not associated with a business entity or business
logic. Examples include logging, caching, notification, authentication,
and authorization (cross-cutting concerns).

### Service-oriented design

The service-oriented design phase begins once the analysis is complete,
using the service models from the analysis stage.

The service-oriented design phase uses the *logical candidate services* that were defined during analysis and creates the *physical service designs*.

The first step is to desig the physical service interfaces.
Once the service contracts have been established, the logic and implementation
of the service can be designed.
We should fully focus on the serice contracts first,
independent of their implementations.

#### Service-interface design

Service interface design is significant because the design phase is the first
time that real technology is identified.

One of the key principles for service orientation is that service contracts
need to be standardized with each other and within a service inventory.

Service interface design identifies *internal* and *external* exposure
of the services. Each interface to the service may expose different operations
and will require different levels of security and authentication.

#### Service-interface granularity

Granularity can have a significant impact on performance and other concerns.
Usually a service interface contains more than one operatione. The operations should be semantically related.

### Service registries

A *service registry* contains information about the available services.

As an orgranization begins to publish and use more and more web services, the need
for a centralized registry becomes more apparent.

Service registries can either be private or public.

One of the challenges of implementing a truly useful and reliable
registry service is the administration of the registry. This includes keeping it
up to date by adding new services, removing obsolete services, and updating
versions, service descriptions, and web service locations.

### Service descriptions

Service descriptions provide information about the available services
so that potential consumers can decide whether a particular service will
satisfy their needs.

Dependencies between services are minimized as services can work together simply
through the awareness they have of each other through their service descriptions.

Service descriptions typically have both abstract and concrete information.
The abstract part details the service interface without getting into the
details of the specific technologies being used. The abstract description
typically includes a high-level overview of the service interface, including what 
operations it can perform.

The concrete part of the service description provides details about the
physical transport protocol. This includes the binding, port, and service
(a group of related endpoints).

### Structuring namespaces

A namespace is a unique *Uniform Resource Locator* (**URL**).
They are used to group related services and element together and to
differentiate between different ones that share the same name.

An appropriate namespace should provide meaning to the service
or element, so that someone who is looking at it can gain an understanding
of the service.

### Orchestration and choreography

Service orchestration and service choreography are approaches to assembling
multiple service so that they can work together.

In service orchestration, there is a centralized process containing fixed logic.
An orchestrator controls the process by deciding which services to invoke
and when to invoke them.
In a SOA, orchestrations themselves are services.

Choreographies define message exchanges and can involve multiple participants,
each of which may assume multiple roles.
There is no centralized process that is controlling it.
There is an agreed upon set of coordinate interactions that specify the
conditions in which data will be exchanged.
Each service acts autonomously to execute its part based on the conditions
and the actions of the other participants.
