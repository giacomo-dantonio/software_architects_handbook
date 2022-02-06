# Chapter 11 - Security Considerations

## Securing software systems

Security involves protecting one of the most important assets that
an organizazion can posses, which is information.
Information assets include not just data but also things such as *logs* and
*source code*.

Security is a quality attribute. We must think about and document the requirements
for quality attributes. Requirements for security must be specified and they must
be precise, measurable, and testable.

Security is architectural and must be considered during requirements, design,
development, and testing.

### The three states of information

The information that we strive to proect can be in one of three states:
it can either be **at rest**, **in use** or **in transit**.

### The CIA triad

The CIA triad summarizes the attributes that we want our software system to
exhibit.

#### Confidentiality

Software applications should *protect confidentiality*.

Confidentiality involves preventing unauthorized individuals from accessing
information.

The application must protect its data.

#### Integrity

Software applications should *ensure integrity*.

The goal is to prevent unauthorized individuals from modifying or destroying
information.

#### Availability

Software applications should *maintain availability*.

If the security mechanisms employed are overly extensive given the requirements,
then the usability and availability of the system will be lessened.
Securing data serves no purpose if authorized users cannot get to it.

## Threat modeling

Threat modeling is a structured apparoach to analyzing security
for an application.

Threat modeling is a process that identifies and proritizes potential security
threats so that a development team can understand where their application is
most vulnerable.

Modern approaches to software security use trheat modeling to focus on security
from the attacker's viewpoint, instead of the defender's.

A **threat agent** is an individual or group that may attack a software system.

### Decomposing an application

Decomposing an application includes knowing the assets that an attacker
may be interested in, the potential attackers of the system, the interactions
with external entities, and the entry points into the system.

*Assets* are the things of value to attackers. They can be physical, such as
login credential or a software system's data, or abstract, such as an
organization's reputation.

Attackers may be external or internal to an organization.
Attackers will be motivated by the assets you have identified, so taking assets
into consideration will help you to identify potential attackers.

You need to understand how the software system interacts with different external
entities (users and external systems). These interaction will allow you to
identify entry points into your system.

### Identifying and categorizing potential threats - STRIDE threath model

A *threat classification model* provides a set of threat categories with
definitions so that each identified threat can be categorized in a systematic
and repetable way. **STRIDE** is one type of threat classification model.

STRIDE is a security threat model that was originally created by Microsoft.

#### Spoofing identity

Spoofing identity is the act of representing yourself as someone else.

E.g. gaining access to someone' authentication information, forging an
email address or modifying header information in a request.

#### Tampering with data

Tampering involves an attacker who modifies data.

#### Repudiation

Repudiation threats can occur if a software system does not properly track and log
actions that take place. This allows user, legitimate or otherwise,
to be able to deny that they performed a particular action.

Such an attack could involve sending inaccurate information to log files, making the entries in the log files misleading and unusable.

Strong authentication, accurate and thorough logging, and the use of digital
certificates can be used to counter repudiation threats.

#### Information disclosure

Information disclosure involves a software system failing to protect information
from individual who are not supposed to have access to it.
For example, allowing an attacker to read data form a database or while in
transit over a network.

#### Denial-of-service

A denial of service attack takes place whenever an attacker is able to deny
service to valid users.

#### Elevation of privilege

Elevation of privilege takes places when an attacker is able to gain
authorization for operations beyond what was originally granted.

### Prioritizing potential threats - DREAD risk assessment model

DREAD is a risk assessment model that can be used to prioritize security threats.

Each risk factor for a given threath can be given a score (for example, 1 to 10).
The average score represents the overall level of risk for the threat.

#### Damage potential

Damage potential represents the level of damage that could be done to users
and the organization if an attack were to succeed.

For example damage to an individual user's data would be rated lower than an attack tha could bring down the entire system.

#### Reproducibility

Reproducibility is a measure of how easy it is to reproduce a particular attack.

#### Exploitability

The exploitability of a threat describes how difficult it is to exploit
a vulnerability.

While some exploits are easily understood and could be done by anyone,
somer require advanced techniques, tools, or scripts.

#### Affected users

The affected users risk factor represents percentage of users that will
be affected by a particular threat.

#### Discoverability

Discoverability signifies how easy it is to learn about the vulnerability.

Security by obscurity is a weak security control and it is not wise to consider
a security risk less of a threat simply because it is difficult to discover.

### Responses to threats

As a response to a security risk, we can avoid the risk, transfer ther risk to
another party, accept the risk or mitigate the risk.

#### Avoiding the risk

Not all security risks can be avoided, and avoiding a security risk can lead
to other risks.

#### Transferring the risk

Some common ways in which risks can be shifted to another party is through an
insurance policy and through contracts.

An insurance company will assume the financial risks that might result from a
security threat. It may not be possible for an insurance to make up for the damage
that a security attack can inflict on an organization's reputation.

We can also transfer a security risk to another party by contracting out the work.
We can opt to have another organization handle it for us through a contract.
An example of this approach is hosting your application with a cloud provider.

#### Accepting the risk

If the priorization of a security threat is low, it is sometimes decided
to accept the risk.

#### Mitigating the risk

Risk mitigation involves implementing some type of security control.

Security controls are countermeasures or safeguards that are used to handle
security risks.

#### Types of security controls

We can categorize security controls by the manner in which they work
(physical, administrative, and technical), or by their overall goal and purpose
(prevention, detection, or response to a threat).

##### Physical security controls

Physicial security controls prevent unauthorized access to facilities,
equipment (e.g. servers), personnel, and other resources.

Some security threats are only made possible when an attacker gains
physical access to one or more resources.

##### Administrative controls

Administrative controls include organizational policies and procedures
that are put in place for security.

##### Technical security controls

Technical security controls utilize technology to provide security for a software
system.

##### Prevention

Preventing a security threat requires analysis and planning.
Some physical, administrative, and technical security controls are used
for prevention (e.g. locks and key cards, security awareness training,
encription, etc.).

##### Detection

Regardless of the preventive measures that are put into place, you should expect
that they will fail and assume that a security attack will ahppen.

Security cameras, motion detectors, system monitoring, logging, auditing, and
the use of anti-virus and malware detection software are examples of
detection security controls.

##### Response

Plans for the responses to various attacks should be made in advance.

Examples include the sounding of an alarm and the locking of the doors (physical),
an escalation plan that dictates the actions to be taken in the event of an attack
(administrative), taking servers offline, rolling back to abackup version of the application, revoking user permissions (technical).

## Secure by design

### Minimizing the attack surface

The design of a software system should attempt to minimize the total attack
surface area as much as possible.

### Defense in depth

Defense in depth is the oncept of using multiple techinques in conjunction
and the belief that doing so a software system will be made more secure.

### Principle of least privilege (PoLP)

The principle of least privilege (also principle of least authority)
informs us that the least amount of privileges that are necessary should be
granted to a user or process in order to reduce security risks.

Additionally, each component of a system should only be granted the privileges
that are necessary. If necessary, complex components may need to be split up
into simpler components.

### Avoiding security by obscurity

Security by obscurity is the belief that a software system is secure as long
as internal details are kept hidden and vulnerabilities are not known or
are difficult to detect.

It is a weak security control and should be avoided.

### Keep software design simple

A system that software architects and developers have a difficult time
understanding is one that may not be secure.

Software systems that are more complicated thend to have a larger attack surface.

### Secure by default

Secure by default is the concept of delivering the software in a state that
maximizes security out of the box, without requiring any changes.

For example, if a software allows two-factor authenatication, it should be
turned on by default.

### Default deny

Access should be denied by default unless it has specifically been granted.

### Validating input

A number of software vulnerabilities can be avoided by being diligent about
validating input from any untrusted sources.

### Secure the weakest link

Security of a software system is only as secure as its weakest component.
Attackers will focus on the weakest component, so be sure that the weakest
poiint in the system is secure enough.

### Security must be usable

Legitimate users should only be impacted to the point that is required
to make the system secure. If the security controls are too annoying,
users will seek to circumvent them.

### Fail securely

Software architects should desing solutions that consider what should happen
when something fails and ensure that the software system and its data remain
in a secure state after the failure.

## Cryptography

### Encryption

Encryption is the process of transforming ordinary data, which is referred to as
plaintext, into a format that is unreadable, which is referred to as cyphertext.

Data is encrypted using an encryption algorithm in conjunction with an encryption
key. Larger key sizes result in greater encryption strength but make the process of encryption/decryption slower.

*Symmetric encryption* is generally faster than asymmetric. The main drawback
is that both parties must have access to the secret key.

### Cryptographic hash functions

A hash function is a function that retunrs a fixed output for a given input.
Hash functions ar enot reversible.

The following are the main propertis of a cryptographic hash function

* **Quick**
* **Deterministic**
* **One-way function**
* **Collision resistant**
* **Small changes result in vastly different hashes**

## Identity and access management (IAM)

### Authentication

*Multi-factor authentication* adds an extra level of security. In MFA a person
has to present two or more authentication factors.

The following are different types of authentication factor:

* **Knowledge factor**: Something the person knows, such as a password or PIN.
* **Possession factor**: Something the person has, suh as a cell phone, or a
    company identification card.
* **Inherence factor**: Something the person is, using a fingerprint scanner, palm
    reader, retina scanner, or some other type of biometric authentication.

### Authorization

Authorization is the process of determining what a subject is permitted to do and
what resources that subject is allowed to access.
In involves granting rights to allow users or progrmas to have access to a
system or parts of a system.

If privileges are too coarse-grained, they may be too large and encompass too many rights.

### Storing plaintext passwords

Don't do.

### Storing encrypted passwords

If an attacker can either intercept a decrypted password or obtain the details
necessary to decrypt a password, security will be compromized.

### Storing hashed passwords

Hashing alone is not sufficient for storing passwords. A *dictionary attack*
can be executed to guess a password by comparing it with a pre-compiled list.
A table of pre-calculated hashes (rainbow table) can be used for comparison
to determine the password.

Software applications should hash a combination of the password with some
piece of random data, known as *salt*.

### Using domain authentication

On Windows servers, the *domain controller* (**DC**), along with a directory
service such as *Active Directory* (**AD**), can manage resources and users
for the entire domain.

### Implementing a centralized identity provider (IdP)

The ability to grant access to resources across applications without
sharing login credentials is a common requirement and can be
accomplished by implementing a *centralized identity provider* (**IdP**).

The task of authentication becomes the responsability of the IdP.

### OAuth 2/OpenID Connect (OIDC)

*OAuth 2* is an open standard for authorization. It allows **an application** to
be granted access to resources **from another application** and share its own
resources with other applications.

*OpenID Connect* (**OIDC**) is an identity layer that sits on top of
OAuth 2. It can be used to verify the identity of an end-user.

#### OAuth 2 roles

* **Resource owner**: the person or application who owns the resource.
* **Resource server**: the server that hosts the resources.
* **Client**: the application that is requesting the resource.
* **Authorization server**: the server that authorizers the client application
    to have access to a resource.

#### Authentication

Authentication is performed by an authorization server along with OpenID Connect.
The client application is referred to as *relying party* because it relies on
the identity provider. It requires a user's identity.

There are various flows. In one example, the client application redirects to
the authorization server, which servers as the identity provider.
It sends an authentication request to the *authorization endpoint*.

If the user is authenticated, the identiy provider redirects back to
the client application using a *redirection endpoint* and returning
and authorization code and an identity token (JSON Web token).

#### JSON Web token (JWT)

A JWT is an open standard for representing claims between two parties.
It has three parts, separated by a dot:

* Header (JSON, base64 encoded)
* Payload (JSON, base64 encoded)
* Signature

Once a user is authenticated and the *identity token* is returned,
the client application can send a token request to the token endpoint to
receive an **access token**.

Access tokens can be revokes, scoped, and time-limited, providing flexibility
for authorization.

## Most commoon web application security risks

### Injection

This security risk occurs when untrusted data is sent to an interpreter
and unintendend commands are executed.

Anyone who can send untreustred data, including external and internal users,
is a possible threat agent.

A *web application firewall* (**WAF**), which sits between users and the
web application, can protect software systems from some of the more common
SQL injection attacks. However it is impossible to identify all possible
attacks.

Validating untrusted data, using SQL parameters, and unsing the priciple of least privilege can help to prevent or lessen the effect of SQL injection attacks.

### Broken authentication

Attackers can find a flaw in authentication or session management manually and
then use automated tools to exploit it.

Hashing passwords with a salt, using multi-factor authentication,
and being secure by default can help secure your system from these kind of
attacks.

### Sensitive data exposure

This security risk involves not properly protecting sensitive data such
as social security numbers, credit card numbers, credentials, and other
important data.

Only store sensitive data if it is necessary and discard it as soon as possible.
Data that isn't retained in any way cannot be stolen.

When sensitive data is at rest, it should be encrypted. You should consider
disabling the caching of responses that contain sensitive data.

### XML external entity attack

An XML external entity attack (**XXE**) can take place against an application that
parses XML input.

One of the most effective ways of preventing this type of attack is to use
a different data format, such as JSON.
If not possible, disabling *document type definitions* (**DTDs**) completely,
or disabling entity expansion, is also effective.

### Broken access control

Lack of access control can be detected manually or, in some cases, by using
automated tools. This can allow attackers to act with elevated privileges,
which may allow them to retrieve, add, update, or delete data.

### Security misconfiguration

Software applications that are more complex have a greater chance of being
misconfigured. The application must be configured to be secure prior
to deployment.

Everything that is unnecessary in a production environment should be disabled,
removed, or simply not installed.

### Cross-site scripting

Cross site scripting (**XSS**) vulnerabilities allow attackers to execute
scripts in the browser.

With **reflected XSS** an application or API takes untrusted data and sends it
to the browser without proper validation or escaping.

**Stored XSS** is possible when an application or API stores user input data
that has not been properly validated or escaped, which is viewed at a later time.

**DOM XSS** is possible when data tha is controlled by an attacker is included
dynamically by a JavasScript framework, API, or other code.

### Insecure deserialization

Deserialization exploits are possible when an attacker modfies an object
that an application or API subsequently deserializes.

### Using components with known vulnerable components

Development teams must be aware of existing vulnerabilities in the components
they are using, keep up with the latest announcements of new vulnerabilities,
and apply patches and/or new versions that will fix vulnerabilities.

### Insufficient logging and monitoring

In order for attacers to be successful, they need to go undetected for as long
as possible.

A software system needs the ability to answer some fundamental who/what/when
questions.

### Unvalidated redirects and forwards

Attackers can use redirects to send users to malicious sites or use
forwards to access unauthorized pages.
