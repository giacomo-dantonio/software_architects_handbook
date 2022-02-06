# Chapter 3 - Understanding the domain

Understanding the domain requires general business knowledge and
a keen understanding of your organization's business.

## Developing business acumen

A technically advanced software is of no use if it does not meet its goals.

You must consider the goals of the *business*, the *users* and the *software system*.
Each of these areas has its own goals, which can significantly overlap or impact the others.
You need to find an acceptable balance between them when designing your software architecture.

### Familiaritiy with general business topics

Understanding the language of business will ensure that you have a common understanding
wih the stakeholders.

*Return on investement* (ROI), calculations, cost-effectiveness analysis, etc.

### Understanding your organization's business

Gain an understanding of your organization's product and services, and the value
they provide to their customers.

Learn about the market that your organization operates in and its trends.

- What do competitors do differntly?
- What do they do that is similar?
- What are the strengths and weaknesses of your competitors?

Spend the time to understand your organization's customers.

## Domain-driven design

Eric Evans' book:

    Domain-Driven Design: Tackling Complexity in the Heart of Software

DDD is an approach to developing software, that aims to make the software
better by focusing on the domain.

DDD encourages and improves communication. In particular, DDD stresses
the importance of interacting with domain experts.

A *domain expert*, or *subject matter expert* (*SME*), is someone
who posseses expertise about, and is an authority in, a particular area.

### Ubiquitous languages

The development teams uses its own language when discussing the functionality
and discuss the domain in terms of their technical design.

The stakeholders, including the domain experts, will use their own jargon
when discussing their domain, and may not have a good understanding
of the technical terms.

None of these dialects can be a common language, because none serves all needs.

Some team members may become familiar with the domain terminology and act as
*translators* for the rest of the team, but they can become bottlenecks.

An *ubiquitous language* is a common language among all team members and stakeholders
based on the domain model.

Developing a ubiquitous language can take time, and can evolve and grow as the 
team's understanding of the domain changes.

The ubiquitous language should be used during *discussions* and in all project
artifacts such as *documentation*, *diagrams*, *code*, and *tests*.

### Entities

- Are defined by their identity and not their attributes.
- The values of their attributes can change without changing their identity (*mutable*).
- Example: A *person* can change last name. Also two persons with the same attributes
  (first and last name) are still different persons.

### Value objects

- Are described by their attributes and have no concept of identity.
- They are immutable.
- Example: points in a 2D space.

### Aggregates and root entities

- Gropings of entities and value objects that are treated as a single unit.

### Separating the domain into subdomains

One or more subdomains may be designated as a *core domain*, which is
the part of the domain that is fundamental to the organization.
Core domains are the reason that the software is worth writing.
(e.g. in a PLM system this would be BOM and CAD Data).

### Bounded contexts

A *domain model* is a conceptual model based on the domain.
It contains behaviour and data. It represents a part of the overall solution
that fulfills the goals of the business.

*Boundend contexts* are a pattern in DDD that represent partitions in the
domain model. Similar to *subdomains* which are partion in the domain.

Example:
- An online shop has two contextes: Marketing context and Order processing context.
- The entities "Mailing list" and "Newsletter" are unique to the marketing context.
- The entities "Order", "Shipping address", "Order Line Item" and "Payment Info"
  are unique to the Order processing context.
- Both contextes have the entity "Customer".

Since the Customer entity has different attributes in each context, they should be
separate entitites. This is comforming to the *single responsibility principle* (SRP).

DDD and the concept of bounded contexts work well with microservices.

## Requirements engineering

*Requirements engineering* involves establishing the functionality that is required
by the stakeholders, along with the constraints under which the software must be developed
and operate.

Types of software requirements:
- Business requirements
- Functional requirements
- Non-functional requirements
- Constraints

*Business requirements* represent the high-level business goals of the organization
building the software.
E.g.
- must include the key functionalities of the competitors' software.
- must differentiate itself from the competitors.

*Functional requirements* describes the functionality of the software.
The functionality and capabilities described by the functional requirements
enable stakeholders to perform their tasks.

Functional requirements include the interaction of the software with its environment.
They consist of the inputs, outputs, services and external interfaces that should
be included with the software.

They can be:
- *Organizational requirements*
- *Legislative requirements*
- *Ethical requirements*
- *Delivery/Deployment requirements*
- *Standards requirements*
- *External requirements* (originating from external systems)

*Non functional requirements* are conditions that must be met in order for the
solution to be effective.

Quality attributes are a subset of the non functional requirements (maintainability,
usability, testability, and interoperability).

*Constraints* are some type of restriction on the solution and may be technical
or non-technical in nature.
They are decisions that have already been made and must be honored.
Examples:
- An existing agremeent wiht a particular vendor, an already purchased
  technology that must be used.
- A law or regulation the software must follow.
- A deadline for a milestone or for the final delivery.

### Importance of Requirements Engineering

Steve McConnell - Code Complete (second edition)

    the principle is to find an error as close as possible to the time at which
    it was introduced. The longer the defect stays in the software food chain,
    the more damage it causes further down the chain.

### Software requirements must be measurable and testable

Each software requirement should be unambigous, measurable and testable.
Testing should be considered when requirements are written.
Requerements need to be specific enough, that they can be verified.

## Requirements elicitation

*known knowns*, *known unknowns* and *unknown unknows*.
We seek to eliminate *unknown unknowns* and consider as many of the requirements
as possible when designing the software.

This is called *requirements gathering* or *requirements elicitation*.
Often it is necessary to *elicit* the requirements from the stakeholders
because not all of them are at the forefront of the thoughts of stakeholders.

### Techniques to elicit requirements

**Interviews**

  One or more people ask questions.
  Ask open-ended questions to spur discussion and get information,
  but ask closed-ended questions that can be used to confirm facts.

  Not a good way to reach consensus because not all of the
  stakeholders may be present, but they could be effective to obtain information.

**Requirements workshops**

  A group of relevant stakeholders is invited to attend a session in which
  they will provide their feedback.
  Higher level of clarity on how the software should work, and what it is
  required to do.

**Brainstorming**

  Get thoughts from a group spontaneously and document them. Fun and productive.
  Make sure you have a variety of stakeholders.

  The session should have clear goals and not be too broad.
  A facilitator should encourage participation, especially at the beginning
  of the session, since some participants may hold back their thoughts.

  Criticism of ideas shouldn't be tolerated, to not discourage anyone
  from participating further. But if the discussion gets off-topic,
  the facilitator should limit the discussion and steer it in another
  direction.

**Observation**

  Someone studies a stakeholder in their work environment.
  Useful to understand a current process.

**Focus groups**

  More formal than brainstorming. Commonly used for public applications
  that will have external users. In that case the invited participants
  are external users or outside experts.

**Surveys**

  Surveys should have a clear purpose. Do not create a large survey
  that covers many topics.

  Questions should be well thought out, clear, and concise.
  Tipically the questions are closed-ended.

**Document analysis**

  Utilizes existing documentation to obtain information and requirements.
  There may be existing software that provides part or all of the functionality
  you are seeking to implement. By analyzing that documentation you can get
  the requirements for your software system.

**Prototyping**

  Involves building a prototype that stakeholders can use to some degree,
  or at least see.

  The scope of a prototype can be as broad or narrow as you want it to be.

**Reverse engineering**

  Existing code is analyzed to determine the requirements.