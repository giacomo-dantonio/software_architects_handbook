# Chapter 2 - Software architecture in an Organization

## Types of software architects

- Enterprise Architect (Frank)
    * Responsible for the technical solutions and *strategic direction* of an organization.
    * They must look into the future.
    * Work on high-level architecture design documents.
    * Provide guidance, mentorship, advice, and technical leadership for other architects and developers.

- Solution architect
    * Converts requirements into a *reusable* architecture for a solution.
    * Bridges a gap between entreprise and application architects.

- Application architect (Arne)
    * Ensures that the requirements for their application are satisfied
      by the design of that application.
    * May recommend solutions or technologies for an application and
      evaluate alternative approaches to problems.
    * Ensures that developers are following best practices and standards.

- Data/information architect (Michael)
    * Focus on data management systems.
    * Creates designs and models and decides how data will be stored,
      consumed and integrated into the organization's various software systems.
    * Ensures the security of the organization's data.
    * May support developers by assisting with their database design.

- Infrastracture architect
    * Basically a DevOP-Architect.

- Information security architect (Michael/Kai)

- Cloud architect (Jan)

## Software development methodologies

### Waterfall model

* Sequential: each stage of the lifecycle must be completed in its entirety
    before moving on to the next stage.
* Simple and easy to understand.
* Transparency in terms of timeline, functionality and cost.
* Each steps has detailed documentation.
* No testing feedback until later in the life cycle.
* Users can have difficulty visualizing the final product from
  just requirements documentation and may miss important requirements.
* Making changes late in the development process can be a large effort.

Phases:

* Requirements
* Design
* Implementation
* Verification
* Maintenance

### Agile

* There are a variety of different types of Agile processes.
  - Scrum
  - Kanban
  - Extreme Programming (XP)
  - Crystal
* They all focus on being adaptable to change.

12 Principle of Agile software (Agile Manifesto). Of which 4 are the core ones:

1. Individuals and interactions are valued more than processes and tools.
2. Working software is more important than documentation.
3. Customer interaction and continous engagement are valued over contract negotiation.
4. Responding to change is more important than following a plan.

* Agile methodologies are *iterative*.
* Phases
  - Evaluation/Priorization
  - Requirements
  - Design & Analysis
  - Implementation
  - QA/Acceptance Testing
  - And so on..
* There is continous feedback. If something needs to be changed, it becomes apparent soon.
* Adaptive rather than predictive

## Project Management

* Put effort into estimates, rather than off-the-cuff estimates that amount to little more
  than guesswork.
* Create Proof Of Concepts for unknown tasks.
* Be a realist (or even a pessimist).

### Getting a project back on schedule

* Working overtime
  - lowering morale and productivity
  - pay extra for overtime work
* Reducing scope
* Adding resources
  - may cause the project to take even longer
  - make sure the team is prepared to support the new members
* Relocating resources
* Identifying problem areas
  - try to understand why a project is late
  - get thoughts from the team as to what improvements could be done
* Act as early as possible
  - do not cut test time short

## Office Politics

* Understand your organization's goals
* Address the concerns of others
* Assist people with their goals
* Know when to compromise
* Be aware of cultural differences

## Software risk management

* Organizations, and the people working for them, have different levels
  of *risk tolerance*.
* An organization should have a plan for *risk management*.

- Functional risks (requirements)
- Technical risks (complexity, technologies)
- Personell risks
- Financial risks
- Legal risks
- Management risks

* A risk should be evaluated for its *potential impact* and
  the *probability that it will occurr*.

### Risk avoidance

Change the project in some way, that eliminates the risk altogether.

Not all risks can be avoided and avoiding a risk could lead to other risks.
Taking risks is sometimes necessary in order to take advantage of an opportunity.

### Transfer the risk to another party

E.g. hire a subcontractor to implement parts of the project.

Additional risk that the subcontractor may not complete their deliverables
on time or that their derivables may not meet certain quality standards.

### Risk mitigation

Reduce the likelihood that a risk will occurr.

### Risk acceptance

Simply accept the risk and any possible consequences.

Actions taken to resolve a risk by mitigating or transferring it may have
their own set of risks.

## Configuration management

Identifying configuration items (software, documents, models, plans),
implementing a change control process, and managing the process
and tools used for builds.

## Change management

Formal change control process to handle changes to a software product.
Includes all aspects of a software system, such as requirements, source code,
and documentation.

*Change control board (CCB)*: a group of project stakeholders
who are designated to analyze proposed changes and decide whether
they should be implemented.

# Software product lines

*Product line engineering* (*PLE*).
Product lines are multiple products from a single company that address
a particular need or market.

Without any type of reuse, the same functionality may be written multiple times.
You should seek to reuse architecture by building software systems from core assets.

*Core assets* (reusable components):
- Requirement analysis
- Domain models and analysis
- Software architecture design
- Test plans and test cases
- Work plans, schedules, budgets
- Processes, methods, tools
- The knowlede, skills, and experience of the employees
- User guides and technical documentation

The core assets need to be built while keeping in mind, that they will be used
across multiple products in a product line.
Core assets should be built with *variation points*.