# Chapter 9 - Cross-Cutting Concerns

In a software system, a *concern* os a grouping of logic and functionality that the application is providing.
The concerns of the system reflect the requirements.

**Core concern**
    It represents functionality that is fundamental to the system and is
    a primary reason as to why the software is being written.
    The logic for each core concern is typically localized to particular
    components.

**Cross-cutting concern**
    It is an aspect of the application that relies on and affects other concerns.
    It is functionality that is used in multiple areas. Examples include
    security, logging, caching, and error handling.

## General guidelines for cross-cutting concerns

### Identifying cross-cutting concerns

By recognizing common functionality across modules and layers of the system,
we can consider how concerns can be abstracted so that they are not duplicated.

### Using open-source and third-party solutions

Once cross-cutting concerns have been identified, implementations must
be provided for them. Software architects should consider solutions that have
already been developed, such as open-source or third-party solutions.

### Maintaning consistency

When satisfying the needs of cross-cutting concerns, software achitects should
ensure that each concern is implemented consistently.

### Avoid scattered solutions

When implementing cross-cutting concerns, we want to avoid simply adding the
functionality to each consuming class that needs it.
This approach is called *scattering*.

As a software architect, you will want to ensure that developers are not simply
copying and pasting logic that they need in multiple places.

### Avoid tangled solutions

When the logic for a cross-cutting concern is mixed with logic for a different
concern, it is known as *tangling* because the logic for disparate concerns
is tangled together.

An implementation that is tangled is likely in violation of the separation of concerns principle and tends to suffer from low cohesion.

We want to avoid tangling. Part of accomplishing that is to make the logic for
the cross-cutting concern loosely coupled with the code that needs it.

Another principle that we should follow in order to avoid a tangled solution is the *Single Responsibility Principle* (**SRP**).

## Implementing cross-cutting concerns

### Using dependency injection (DI)

The DI pattern can be used to inject cross-cutting dependencies into classes
that need them. This allows us to write loosely coupled code and avoid scattering.
The logic for the cross-cutting concern will not be duplicated in multiple places.

See example at page 307.

We may want to use a different implementation for a cross-cutting concern
at runtime based on something such as configuration setting. This approach will
allow us to change the implementation without having to recompile and redeploy
the application.

Although this approach eliminates scattering, it does not eliminate tangling.
If you take this approach, you will have cross-cutting logic mixed in with
your other logic.

### Using the decorator pattern

The **decorator pattern** can add behaviors dinamically to an object, including
behaviors for cross-cutting concerns. It is essentially like creating a wrapper to handle a cross-cutting conern around some other object.

[See picture at page 309]

A DI container can handle dependency chains for you so that when you want
a concrete instance of `IAccountService`, you will receive one that has been
decorated with all of the cross-cutting concerns, without having to do the
wiring up yourself.

Using the decorator pattern in conjunction with DI will allow you to write logic
for the cross-cutting concerns thatare neither scattered, nor tangled with other
logic. However, it does require you to create the decorator classes.

## Aspect-oriented programming

Aspect-oriented programming (**AOP**) is a paradigm that was created t handle the scattering and tangling of boilerplate code in object-oriented programming.

**Aspect**
    It is the logic for the cross-cutting concern itself, such as logging
    or caching.

**Join point**
    Is a location between logical steps of your program, such as after
    your program starts, before/after creating an object, etc.

**Pointcut**
    Is a set of join points. E.g. before/after any object is created.

**Advice**
    Is the code that actually performs the cross-cutting concern.

### Types of advice

**Before advice (on start)**
    Executes before a joint point. It cannot prevent the flow of logic
    proceeding on to the join point.

**After returning advice (on success)**
    Executes after a join point has completed successfully.

**After throwing advice (on error)**
    Executes if an exception occurred in the method.

**After advice (finally)**
    Executes after a join point exits, whether the methode completed successfully
    or an exception occurred.

**Around advice**
    Surrounds a join point, so that it can execute logic before and after
    a method is invoked.
    It also has the ability to prevent a method from executing by either
    returning its own value or throwing an exception.

### Weaving

Weaving is the process of applying the advice (logic for the
cross-cutting concern) to the logic of the core concern.

#### Compile-time weaving

AOP tools that employ compile-time weaving perform an additional step to attach
aspects after a program is compiled. This process is handled by a post-processor
that is provided with an AOP tool.

The post-processor takes the DLL or EXE and adds aspects to it.

#### Runtime weaving

Runtime weaving does not take place until after the application starts executing.
The advice for an aspect and the code that it will be applied to are both
instantiated at runtime.

Runtime weaving works similarly to the decorator patter. The AOP tool can generate
the decorator classes at runtime without requiring developers to manually create
them beforehand.

## Types of cross-cutting concerns

### Caching

A reusable caching service should provide the ability to perform operations,
such as putting data in a cache, getting data out of a cache,
and setting policies on how and when cached data will expire.

The two main types of server-side caching are in-process cache and distributed
cache.

### Configuration management

Configuration management involves deciding what options for a software application
should be made configurable and how that configuration will be stored, protected,
and modified.

A software application needs to be deployed and used in multiple environments,
such as development, testing, staging, and production.
In addition, it may use a number of different infrastructures and third-party
services. Different environments may require different configuration values
for these various services.

### Auditing

There may be requriements to maintain an audit trail that includes information
about a data change, such as the date/time that it occurred and the identity of
the individual who made the change.

### Security

Will be the topic of chapter 11.

### Exception management

An exception is a type of error that occurs during a program exeution that we
expect may happen. They are issues that re known to occur and an application can
be designed to recognize them.

Exception management should be treated as a cross-cutting concern and
a centralized exception management approach should be designed
for the application.

A software application should have consistency in terms of how exceptions and
errors are handled.

A good exception management strategy should also take into consideration
unhandled exceptions and design a way to deal with them.
Failures in the application should not leave it in an unstable
state or corrupt data.

### Logging

Common characteristics of log entries include the following:

* *Date/time*.
* *Source*.
* *Log level/Severity*.
* *Message*.

#### Understanding log levels

**TRACE**
    Use this level for *tracing* the code, such as being able to see when
    execution flow enters and exits specific methods.

**DEBUG**
    This level records diagnostic details that can be helpful during debugging.
    It can provid details such as executed queries and session information,
    which can be used in determining the cause of an issue.

**INFO**
    This level is for logging details about normal operations during the
    execution of logic. It is useful for information that you want to have
    but typically won't spend much time examining under normal circumstances.

**WARN**
    When you have a situation in which incorrect behavior takes place, but the
    application can continue, it can be logged at the warn level.

**ERROR**
    Use this level for exceptions and problems that caused an operation to fail.

**FATAL**
    This level is reserved for the most severe errors.

#### Routing log entires

Writing logs to text files on local disks has been a common practice,
but when your application is running on many different servers, it becomes
difficult to search through all of the files without the use of tools.

Cloud-native applications should simply treat their log as event streams
and should not be responsible for the routing and storage of those streams.
Instead of writing to a log file, it should write event streams
to *standard output* and *standard error*.

You can either leverage services that your cloud provider makes available
to aggergate and store log information, or you can provide your own
implementation.

#### Using Elastic Stack

The Elastic Stack is an integrated solution of open-source products that offer
a highly scalable ened-to-end solution for aggregating, searching, analyzing and
visualizing logging data.

##### Elasticsearch

Elasticsearch is an open-source, distributed search engine and document database
that can store, search, and analyze data.

It allows you to quickly search through data. It can be configured so that it
will send notifications based on certain conditions.

##### Logstash

Logstash is an open-source log-parsing engine that provides functionality to parse, transform, and transport data.
It aggregates, filters, and supplements data from a variety of sources.

Logstash can perfrom tasks such as transforming unstructured data into
structured data, filering out certain types of data, and adding to the data.

Once Logstash is done processing data, it can forward it to a destination.

##### Kibana

Kibana is a free tool that allows you to explore and visualize your
Elasticsearch data.

##### Beats

Beats ia a platform for small, lightweight data shippers.
These data shippers gather data from potentially large numbers of different
sources and send it to Logstash or Elasticsearch.

For logging, Filebeat can be used to aggregate log data.
It can collect logs from all of the containers running on that host.

## Cross-cutting concerns for microservices

### Leveraging a microservice chassis

Microservices are independently deployable, self-contained services.
As a result, implementing a cross-cutting concern has to be done repeatedly
for each microservice.

To overcome this challenge, a **microservice chassis** can be used.
A microservice chassis is a framework that can take care of many of the
cross-cutting concerns for microservices and do so in a way that allows all of
your microservices to utilize the functionality.

Some examples include Spring Cloud, Microdot, Gizmo, Go kit, and Dropwizard.

### Using the sidecar pattern

If your software is taking advantage of polyglot microservices, it can make it
difficult to mantain libraries for cross-cutting concerns.

One solution to this problem is to use the **sidecar pattern**.
The logic for cross-cutting concerns are places in their own process or
container (*sidecar container* or *sidekick container*) and then attached to
the *primary application*.

Primary and sidecar applications have access to the same resources.

It is a best practice to use a mechanism for *inter-process communication* (**IPC**) which is language and framework agnostic.