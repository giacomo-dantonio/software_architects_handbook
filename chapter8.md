# Chapter 8 - Architecting Modern Applications

## Monolithic architecture

A *monolithic architecture* is one in which a software application is designed
to work as a single, self-contained unit.

### Benefits of a monolithic architecture

If an application is relatively small, there are benefits to using a monolithic
architecture.

* Better perfromance: the interaction between the machine running the application and other machines is minimized.
* Easier to deploy.
* Easier to test, because they are simpler, with fewer separate components.
* Usually easy to scale, because all it takes is to run multiple instances of
  the same application.

### Drawbacks of a monolithic architecture

As applications grow in size and complexity there are serious drawbacks.

Monolithic architectures greatly inhibit the agility of the organization:

* It becomes difficult to make changes to the software.
* Continous deployment is difficult to achieve.
  If a change is made to only one component of a monolithic application,
  the entire software system will need to be deployed.

Monolithic applications require a commitment to a particular programming language
and technology stack.

## Microservice architecture

The microservice architecture (**MSA**) pattern builds software applications
using small, autonomous, independently versioned, self-contained services.
These services use well-defined interfaces and communicate with each other over standard, lightweight protocols.

Each microservice focuses on doign one thing well and the can work together
with other microservices in order to accomplish tasks that are more complex.

Incoming requests are commonly handled by an API gateway, which servers as the
entry point to the system. It is an HTTP server that takes requests from clients
and routes them to the appropriate microservice.

### SOA done right

Microservice architeture emerged as the result of the shortcomings and drawbacks
of the traditional service-oriented architecture (SOA) and
monolithic architecture.

Rather than using an *enterprise service bus* (**ESB**), as is common with SOA,
microservice architecture favors implementing ESB-like functionality in the services themselves.

### Characteristics of microservice architecture

#### Small, focused services

Each microservice should do one thing and do it well.
Every service has a focused responsibility.

A microservice an be developed by a small team.

If a software system is also using domain-driven design (DDD), the concept
of **bounded contexts** works well with microservices as it helps with the
partitioning of services.

#### Well-defined service interfaces

Microservices are trated like black boxes, hiding their complexity and
implementation details from service consumers.
Services interact with each other through their interfaces.

#### Autonomous and independently deployable services

The services should be loosely coupled, interacting through their well-defined
interfaces and not dependent on the implemenation of the service.

Autonomous services are independetly deployable, making it easier to deploy
them to production. A microservice architecture enables continous deployment
because it is easier to release updates to the services.

#### Independent data storage

Each microservice can have its own data store. This helps services to be
independent and loosely coupled to other services.

If the data storage is a relational database management system (RDBMS),
then in addition to the option of having a separate database server,
data can be kept separate by designating certain tables to be owned
by a particular service.
Another option is to designate a schema that is to only be used by a single
microservice.

#### Better fault isolation

When one microservice goes down, other services can still operate normally,
allowing other parts of the system to remain operational.

#### Communicating with lightweight protocols

There is no rule dictating a praticular protocol, and microservices can
communicate synchronously or asynchronously.
A common implementation is to have them expose hTTP endpoints that are invoked
through REST API calls.

For synchronous communication **REST** is one of the preferred protocols.
It is common for REST to be used with JavasScript Object Notation (**JSON**).

A common messaging protocol used for asynchronous communicatio nwith microservices is *Advanced Message Queueing Protocol* (**AMQP**).
AMQP can support the followint types of message-delivery guarantees:

* **At least once**: a message is guaranteed to be selivered, butit may be delivered multiple times.
* **At most once**: a message is guaranteed the delivered once or never.
* **Exactly once**: a message is guaranteed to be delivered once and only once.

Another protocol that is popular with microservices is **gRPC**.
It was designed by Google as an alternative to REST.

gRPC is built on protocol buffers, also known as protobufs, which is a way
of serializing data that is language and platform neutral.

Given modern workloads gRPC is an attractivve choice because it is a
high-performance and lightweight protocol.

### Designing polyglot microservices

One of the many advantages of using a microservice architecture is that
it affords you the option of using multiple programming languages, runtimes,
frameworks and data storage technologies.

#### Polyglot programming

With polyglot programming a single application uses multiple programming
languages in its implementation.

Each microservice can be developed using the programming language that
best fits the problem at hand.

#### Polyglot persistence

With polyglot persistence multiple persistence options are used within a
single application.

Each microservice is in charge of its own data storage, so it can choose the best
data storage technology based on what it is trying to achieve.

### Considering service granularity

The granularity of a service refers to the *scope of its business functionality*.

With microservices the goal is to have fine-grained services so that each one
focuses on a single business capability.

#### Nanoservices

Services whose granularity is too fine-grained are referred to as **nanoservices**
and this is considered an anti-pattern.

As the number of services in a system increase, so does the amount of
communication that must take place. Services use up network resources
that are not infinite.

With nanoservices there is also an increase in the overall overhead
for the services.

If a single business task that fits well into a single, cohesive service is
decomposed further into multiple, smaller services, the logic becomes separated.

### Sharing dependencies between microservices

Development teams should avoid sharing dependencies, such as frameworks
and third-party libraries, between microservices.

Each microservice should remain independent of other microservices.
If we want to update the dependencies, we don't want to affect any other services.

Microservices should function independetly of the host they are deployed to.

### Stateless versus stateful microservices

Each microservice can be either *stateless* or *stateful*.
A system that uses microservices typically has a stateless web and/or
mobile application that uses stateless and/or stateful services.

Stateless microservices do not mantain any state within the services across call.
A stateful microservice persists state in some form in order for it to function.

A microservice should store state information externally, in some type of data
store. Persisting the state externally provides availability, reliability,
scalability, and consistency for the state information.

### Service discovery

Service discovery is more complex with a cloud-based aplication using microservices.
The number and locaton of service instances changes dynamically.

A **service registry** plays a key role in service discovery.
It is a database containing instances and their locations.
Service instances must be registered and deregistered with the service registry,
either through self-registration or third-party registration.

#### Self-registration pattern

[See picture on page 277]

When a service instance starts up, it must ergister itself from the service
registry. When it shuts down it must unregister itself from the service registry.

It is a common requirement to have registered service instances periodically
renew their registration or send a heartbeat request to indicate they are still 
alive and responsive.

The self-registration pattern is sufficient for small application.

#### Third-party registration pattern

A dedicated component, sometimes called the *service registrar*, handles
registering, deregistering, and checking the health of service instances.

Like the service registry itself, the service registrar must be highly available.

[See picture on page 278]

By either polling the available service instances or subscribing to relevant
events, the service registrar can register new service instances and deregister
service instances that no longer exist.

The service instances are decoupled from the registry.

### Types of service discovery

#### Client-side discovery pattern

[See picture on page 279]

The service client queries a service registry for the locations of
available service instances.

The service client then uses a load balancing algorithm to select one of them.
At that point, the service client can interact with a specific service instance.

This pattern couples the service client with the service registry.

#### Server-side discovery pattern

The service client makes a request to a router. The router is typically a load
balancer.

[See picture on page 280]

It is the load balancer that queries the service registry for the locations
of available services instances. The load balancer is then responsible
for forwarding the request to one of the available service instances.

Clients are decoupled from the service registry.

### Disadvantages of microservices

A microservice architecture introduces complexity simply not found in
monolithic applications. When multiple services are working together and
something goes wrong, there is added complexity in figuring out what and
where something failed.

## Serverless architecture

The term *serverless* refers to the fact that compute services are provided
without requiring you to manage or administer servers.
Your code is executed on demand, as it is needed.

A number of cloud vendors, including Amazon, Microsoft, Google and IBM, provide
compute services.

### Function as a Service (FaaS)

In a serverless architecture, a small piece of code, like a function, can be
executed using an ephemeral compute service to produce a result.
This is known as *Function as a Service*.

By ephemeral we mean that it will only last for a limited amount of time.
The code executes in a container that is spun up on invocation an then brought
back down when it is complete.

Each function should follow the *single responsibility principle* and serve a
single, well-defined purpose.

Function should be designed to be idempotent, so that multiple executions
of the same request yield the same result, and if the same request is processed
more than once, there should not be any adverse effects.

An important part of a serverless architecture is its API gateway.
An API gateway is the entry point to a system.
It is an HTTP server that takes requests from clients and uses its
routing configuration to route them to the relevant function container.

### Backend as a Service (BaaS)

Backend as a Service has its roots in *Mobile Backend as a Service*.
It allows developers to take advantage of service applications provided by
third parties.

In contrast with FaaS, where development teams write their own code for the
various functions, BaaS offers the use of existing services.

Examples include a database, push notifications, file storage,
and authentication services.

### Advantages of serverless architectures

#### Cost savings

Your code is only executed when needed. You get utility billing.

#### Scalable and flexible

You avoid being in a situation where you do not have enough servers
during periods of peak capacity or have to omany servers sitting idly during
off-peaks periods.

#### Focus on building your code products

Allows organizations to focus on creating solutions and shipping more features.

#### Polyglot development

Development teams are provided with the ability to select best-of-breed languages
and runtimes based on the required functionality.

### Disadvantages of serverless architectures

#### Difficulties with debugging and monitoring

There is complexity in debugging distributed systems using serverless architecture.

#### Multitenancy issues

Any time software for different customers are executed on the same machine, there
is the possibility of one customer affecting a different customer.

Example of this includes security issues or performance issues.

#### Vendor lock-in

Moving from one serverless environment to another one can be quite involved.

One way to mitigate this disadvantage is to use a framework that packages
your application in a way that allows for development to any cloud provider
(e.g. https://www.serverless.com/).

#### Complexity of designing many functions

Software systems that have a serverless architecture tend to consist of
numerous functions and there is inherent complexity in designing many functions.
It will take time to make decisions on the granularity of functions.

#### Not as many runtime optimizations

In a traditional environment, optimizations might be made rearding memory,
processors, disks, and the network.

#### Still immature

Standards and best practices for serverless architetctures have not been
as throughly estabilished as other types of software architectures.

### Taking a hybrid approach to serverless

You may choose to design a part of your system with a serverless architecture
and use a different architecture pattern for the other parts of your system.

### Function deployment

When functions are deployed in a serverless system, they go through a deployment
pipeline.

Developers must first upload the function definition, which contains
specifications about the function as well as the code.

The specifications and metadata include things such as a unique identifier,
name, description, version identifier, runtime language, resource requirements,
execution timeout, created date/time, and last modified date/time.

[See picture on page 287]

The starting of an instance function can be the result of **cold start** or
**warm start**.

With a warm start, one or more functins instances have already been deployed
and are ready to be executed when needed.

### Function invocation

#### Synchronous request

Examples include an HTTP request or a gRPC call.

[See picture on page 288]

The API gateway will either use client-side service discovery or pass it on to a
router (load balancer) for the server-side service discovery.

#### Asynchronous request (message queue)

When you want to process requests asynchronously, the publish-subscribe
pattern can be used.

Incoming requests are published to an *exchange*.
Exchanges distribute messages to one or more queues, using rules called 
**bindings**.

[See picture on page 289]

#### Message stream

When there is a need for real-time processing of messages, a message stream can
be used.

Message streams can ingest, buferm and process large amount of streaming data.
A stream is typically partitioned into *shards*, with each shard going
to a single worker for processing.

[See picture on page 289]

#### Batch job

Batch jobs are placed in a job queue, either on-demand or based on a schedule.
The master/worker (or master/slave) pattern speeds up jobs by splitting them up
into smaller tasks, so that the tasks can be processed in parallel.

Workers continue to pull from the working set untile there are no more tasks to
complete.

[See picture on page 290]

## Cloud-native applications

In modern application development, the development team needs to have more
knowledge about, and a vested interest in, how their application
runs in production.
Similarly the operations team must be able to work with the develpment team to
improve upon, over time, how the application is deployed and executes in a
production environment.

### Reasons to move to the cloud

* Reducing costs
* Greater flexibility and scalability
* Automatic updates
* Disaster recovery

### What are cloud-native applications?

The *Cloud Natvie Computing Foundation* (**CNCF**) defines cloud-native
as using an open surce software stack to make applications that are
containerized, dynamically orchestrated, and microservice-oriented.

#### Containerized

Packaging your software with its dependencies in a container based on open
standards allows us to know that it can be run anywhere that supports conatiners.

It provides us with predicatbility in that we know the software will work as
expected because the container is the same, no matter where it is executed.

In a cloud-native application, each part of the system is packaged
in its own container.

#### Dynamically orchestrated

A cloud-native application will need the ability to run multiple
containers across multiple machines.

Once you have multiple containers running on different machines,
you will need to dynamically orchestrate them.
The system must start the correct container at the right time,
be able to scale containers by adding and removing them based on demand,
and launch containers on different machines in the event of a failure.

Currently the most popular orchestration tool is Kubernetes.

#### Microservice-oriented

A cloud-native application should be partitioned into microservices.

#### No downtime

Applications today are expected to be available at all times.

Cloud-native applications are *designed for failure* and keep fault tolerance
in mind so that they can recover rapidly and minimize downtime.

If a physical server fails unexpectedly or is taken down as part of planned
maintenance, a failover system will redirect traffic to a different server.
Sotware components should be designed so that they are loosely coupled,
such that if one fails, a reduntant component can take over.

#### Continous delivery

Cloud-native applications should release software updates rapidly.

#### Support for a variety of devices

In order to provide this type of support, cloud-native applications ensure that
backend services are able to provide the functionality that a variety of frontend
devices need.

### Twelve-factor apps

The **twelfe-factor app methodology** is a set of principles that can be followed
when developing applications to be deployed to the cloud.

An application that follows this methodology adheres to certain constraints
and conforms to a *contract*.

#### Codebase

One codebase tracked in revision control, many deployments.

#### Dependencies

Explicitly declare and isolate dependencies.

#### Configuration

Store configuration in the environment and not in the application code.

An application's configuration consists of values that can vary across
deployments, such as database connection information,
URLs for web services, etc.

#### Backing services

Treat backing services as attached resources.

A backing service is any service that the application uses over the network
that is separate from the application itself (data store, distributed
caching system, messaging/queueing system, etc.)

#### Build, release, run

Strictly separate the build and run stages.

#### Processes

Execute the app as one or more stateless processes.

A cloud-native application should consist of one or more stateless processes,
with any persisted data being stored using a backing service.

#### Port binding

Cloud-native applications are completely self-contained. Services should
make themselves available to other services by specified ports.

#### Concurrency

Scale out via the process model.

#### Disposability

Maximize robustness with fast startup and graceful shutdown.

The processes of a cloud-native application should be disposable,
so that they can be started or stopped at any time.

#### Development/production parity

Keep development, staging, and production as similar as possible.

One way to eliminate these differences is through the use of containers.

#### Logs

Treat logs as event streams.

Cloud-native applications should not be responsible for the routing and
storage of its output stream.

#### Administrative processes

Run admin/management tasks as one-off processes.
