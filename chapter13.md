# Chapter 13 - DevOps and Software Architecture

**Shift left** is a common term associated with DevOps. The idea is to
perform tasks earlier in the life cycle, or to shift them left in the timeline.

In addition to testing earlier in the process (with automated tests),
DevOps also considers what else can be moved to earlier in the process.
Involvment of the operations team should shift left and begin working with the development team much earlier.

## CALMS

CALMS is an acronym that represents the core values of DevOps: Culture,
Automation, Lean, Measurement, Sharing.

### Culture

DevOps requires changing the culture of an organization by breaking down
barriers between teams. DevOps necessitates cross-functional teams and
encourages teams with different skills and knowledge to work together.

Continous improvement is also a part of DevOps culture. Different teams in an
organization should learn from each other. If faults or other issues occur,
team members should learn from those experiences.

When mistakes are made individuals and teams should take ownership of them,
rather than blaming other teams.

### Automation

The first step in automating processes is to identify the current processes that
are executed and understand how they work.

Instituiting automated testing, build, and deployment processes is a key part of
DevOps.

### Lean

*Lean software development* took the best practices of lean manufacturing
ad applied them to software development.
It aim to optimize processes and minimize waste during the software
development process.

There are seven lean development principles:

**Eliminate waste**: Unnecessary functionality, code or effort is wasteful.
    Delaying the delivery of value to customers and ineffiecient processes are
    other examples of sotware development waste.

**Build quality in**: Quality should be a focus for everyone. Write tests and
    automate execution.

**Create knowledge**: Team members should share knowledge within the team and
    across teams.

**Defer commitment**: A decision should be made only after enough information
    has been collected.

**Deliver fast**: Value should be delivered to customers quickly.

**Respect people**: Communication and handling of confilicts should be done
    in a respectful way.

**Optimize the whole**: Processes should be optimized and bottlenecks should
    be eliminated when possible.

### Measumerment

Teams must be able to measure improvement. If they cannot measure it, they
cannot know whether process improvements, automation, and the introduction of
other DevOps practices have actually worked.

### Sharing

Information, tools, data, and the lessons that are learned need to be shared so
that the organization can improve as a whole.

## DevOps toolchain

A DevOps toolchain focues on the development and delivery of software systems.

DevOps tools are generally categorized as supporting one or more of the following
activities:

**Plan**: This category of tools help you you to define the requirements
    of the application and plan the work.

**Create**: Create tools are software that help in some way with design, coding,
    and building activities. (e.g. IDEs, version control repositories,
    build automation tools, and configuration management tools).

**Verify**: Verification tools consist of software that help to ensure the
    wuality of a software release. They can help with performance, acceptance,
    regression, and release testing. Static analysis tools can help to analyze
    the code, and scurity tools can help to identify vulnerabilities.

**Package**: Packaging tools are used for the tasks associated with preparing
    a release once it has been verified.

**Release**: The tools in the release category assist teams with the scheduling
    and coordination of deploying software systems into different environments.

**Configure**: Tools are available that assist with the configuration of
    software applications.

**Monitor**: It is critical to monitor software applications to identify issues
    and gain an understanding as to their impact.

## DevOps practices

In a DevOps release cycle, the following major activities generally take place:

1. Development
2. Integration
3. Build and unit testing
4. Delivery to staging
5. Acceptance testing
6. Deployment to production

### Continous integration (CI)

Continous integration is the practice of developers merging their changes
into a shared source control repository as often as possible.

The activities covered by continous integration include development,
integration (checking in the changes into a version control system),
and an automated build with automated unit testing.

### Software versioning

**Semantic versioning** is a popular convention that can be used for software
versioning. It uses a three-part version number that follows the
*major*.*minor*.*patch* format.

A new *major* version indicates that breaking changes are included with the
version. A new *minor* version means that addition and changes have been made, but
the software is backward compatible. A new *patch* version indicates that bug 
fixes are included.

### Automated testing

### Continous delivery (CD)

Continous delivery (CD) is the ability of an organization to release changes to
users quickly and in a sustainable, repeatable way. The software is released
in short cycles.

The aim of continous delivery is to have your application in a state where 
it can be deployed at any time.

In addition to continous integration activities, continous delivery also includes
automated delivery to staging, automated acceptance testing, and deployment
to production.

With continous delivery deployment to production is a manual process.
After deployment to production, post-deployment tests are typically executed.
They should at the very least consist of *smoke testing*.

A smoke test ensures tha all crucial functionality is working properly in the target environment.

### Continous deployment

Continous deployment is similar to continous delivery, but it automates the
deployment to production.

## Architecting for DevOps

