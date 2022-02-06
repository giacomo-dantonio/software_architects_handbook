# Chapter 10 - Performance considerations

Performance needs are requirements that must be met and their importance
should be reflected in the fact that the entireteam must take ownership
of performance.

## The importance of performance

### Performance affects user experience

The performance of your application affects the organization's business,
whether it is because custoemers are being gained/lost for a customer-facing site
or because productivity is being gained/lost for an enterprise application.

#### Bounce rate

A *bounce* occurs then a user has just a single-page session on a site and
leaves without visiting any of the other pages.

The **bounce rate** is the percentage of users who bounce 

    BR = #bounces / #entries to a page

As page load times incerase, so too does the bounce rate.

#### Conversion rate

The **conversion rate** is the percentage of site visitors who ultimately
take the desired conversion action (e.g. placing an order, registering
for membership, downloading a software product or subscribing to a newsletter).

    CR = #Goal achievements / #Visitors

### Performance is a requirement

Performance is a quality attribute of software systems and cannot be considered
as just an afterthought. It should play an integral part throughout the life cycle
of a software application.

Like other requirements, it mus be unambiguous, measurable and testable.

Treating performance as a requirement also means that we should have tests for it.

### Page speed affects search rankings

Page speed is a consideration in a site's mobile search ranking in Google
search results.

## Defining performance terminology

### Latency

*Latency* is the amount of time (or delay) it takes to send information from
a source to a destination.

In many instances, a significant portion of the total latency takes place between
your office or home and the internet service provider (ISP). This is known as
**last-mile latency**.

### Throughput

*Throughput* is a measure of a number of work items per a particular time unit.
In the context of a network, it is the amount of data that can be transfered
from one location to another in a given amount of time.

It is typically measured in *bits per second (bps)*, megabit per second (Mbps), or
gigabit per socnd (Gbps).

In the context of application logic, throughput is how much processing can be
done in a given amount of time.

### Bandwidth

*Bandwidth* is the maximum possible throughput for a particular logical or
physical communication path. It is measured in the same units as throughput.

### Processing time

*Processing time* is the length of time that it takes for a software system to
process a particular request, without including latency.

### Response time

*Response time* is the total amount of time between the user making a particular
request and the user receiving a response to that request (RT = PT + latency).

### Workload

*Workload* represents the amount of computation processing a machine has been
given to do at a particular time.

Some common type of workload that may be evaluated are CPU, memory, I/O, and
database workloads.

### Utilization

*Utilization* is the percentage of time that a resource is used when compared
with the total time that the resource is available for use.

As utilization approaches the maximum throughput, response time will rise.

## Taking a systematic approach to performance improvement

Teams will have greater success at optimizing performance when the entire team,
and not just certain individuals, take ownership of the performance of the
software application.

An iterative process that consists of the following steps can be used for performance improvement:

### Profiling the application

Profiling is an analysis of a software system that results in measurements of
the system's execution.

Development teams should not be guessing where performance issues exist, as they will not always be where you expect.

Two broad categories of how profiles collect infomration are through
*instrumentation* and by *sampling*.

#### Instrumentation

When instrumentation is used, code is added to the software system being profiled
in order to collect information (e.g. data on the time spent in a method,
a count of how many times the method is used, etc.).

Instrumentation can provide a greate level of detail. However,
the instrumentation code can affect the measurements.

#### Statitistical profilers

Statistical profilers work by *sampling* and le applications execute without any
runtime modifications.

An operating system (OS) interrupts the CPU at regular intervals, giving it
an opportunity for process switching. Sampling works by collecting information
during these interruptions.

Sampling is less intrusive, but the data collected is often an approximation and is not as numerically acurate as through instrumentation.

### Analyzing the results

*Bottlenecks* are parts of the software system that limit performance.
These parts in the software are unable to keep pace given their capacity and a
particular amount of work, which in turn slows down the overall performance of the application.

The focus of the performance imporvement effort should be on optimizing
the bottlenecks.

Some common bottlenecks include CPU, memory, network, database,
and disk utilization.

Some bottlenecks will lead you to conlcude that you need to either
scale horizontally or scale vertically.

Vertical scaling involves increasing the capacity of existing servers
by adding resources.

Horizontal scaling involves adding servers to your ppol of resources in order to
scale wider and handle more traffic.

### Implementing changes

Profiling and analyzing are necessary because we don't want to make changes unless
we know that it will be worth it.

You should implement one set of changes at a time, so as not to mix results
and make it more difficult to recongnize new performance issues that may have
been introduced.

The most important bottleneck and the one that is expected to provide the
biggest payoff should be prioritized.

### Monitoring results

Once changes have been implement, we must monitor the results to determine
whether the changes resolved the performance issues that were identified.

When changes are implemented to fix a bottleneck, either the performance issue
will remain unresolved, it will be fixed, or the bottleneck will be transferred
to another part of the system.

## Server-side caching

Server-side caches can be used to avoid making expensive data retrievals from the
original data store (e.g. a relational database. repeatedly).

The server-side cache should be plcaed as close to the application as possible to minimize latency and improve response times.

The type of storage used for a server-side cache is designed to be fast, such as
an in-memory database.

### Caching data in distributed applications

#### Using a private cache strategy

A *private cache* is held on the machine that is running the application that is
using it.

One of the ways that data is stored in a private cache is in-memory,
which makes it extremly fast.

Each application instance will have its own cache. This means that it is possible
for the same query to yield different results depending on the
application instance.

#### Using a shared cache strategy

A *shared cache* is located in a separate location, possibly accessible through
a cache service.

All application instances use the shared cache. This resolves the issue of
different instances potentially having different views of cached data.
It also improves scalability, because a cluster of servers can be used
for the cache.

### Priming the cache

*Priming the cache* means that an application pre-populates the cache at 
application startup with data that will either be needed at startup,
or is widely used enough that it makes sense to make the data available
in the cache right from the start.

### Invalidating cached data

Data in a cache may become stale if it is changed after it was placed
in the cache. *Cache invalidation* is the process of replacing or removing
cached items.

#### Expiring data

We can configure the data to expire from the cache after a specified
amount of time.

#### Evicting data

A cache may become full, in which case the caching system must know which
items it can discard. The following policies can be used:

*Least recently used* (**LRU**)
    Discards items that were least recently used first.
    Based on the assumption that cached items that have recently
    been used are the most likely to be used again soon.

*Most recently used* (**MRU**)
    Discards itmes that wer most recently used first.
    Based on the assmption that cached items that vae been recently used
    will not be needed again.

*First-in, first-out* (**FIFO**)
    Discards the item that was placed in the cache first (oldest data).

*Last-int, first-out* (**LIFO**)
    Discards the item that was placed n the cache most recently (newest data).

*Explicitly evicting data*

### Cache usage patterns

#### Cache-aside pattern

The application is reponsible for maintaing the data in the cache.
The cache is kept aside and doesn't interact with the database directly.

When data is written to the database, the application must handle potentially
invalidated cached data and ensure that the cache is consistent
with the system-of-record.

#### Read-through pattern

The cache is treated as the system-of-record and has a component
that is able to load data from the actual system-of-record (the database).

#### Write-through pattern

The caching system has a component that has the ability to write data to the
system-of-record.

#### Write-behind pattern

Like the write-through pattern treat the cache as the system-of-record
but the timing of the write to the system-of-record is different.

The write-behind pattern queues the writing of the data to the system-of-record.

## Improving web application performance

### Leveraging HTTP caching

Resources as CSS or JavaScript files might be shared across multiple pages of
your web application. In addition, users may return to your web application at
some point in the future. Taking advantge of *HTTP caching* will improve
performance and benefit the user.

To take advantage of HTTP caching, each response from your web server must
include the appropriate HTTP header directives.

#### Using a validation token

A common scenario with HTTP caching occures when a response has expired from the
cache but has not changed in any way.

A validation token in the `ETag` header of a response can be used
to check whether an expired resource has changed.

Clients send the validation token along with the request. The server will
return a *304 Not Modified* response.

#### Specifying cache-control directives

Cache-control directives in a response can control whether the response should be
cached, under what conditions and for how long it should be cached.

Possible directives are *no-store*, *private*, which allow caching in a user's
browser but not in any intermediate caches.

*no-cache* is used to specify that a response should not be used from the cache
until a check is performed with the server first to see whether the response
has changed. Only if the resource has not changed can the cache be used.

*max-age* is used to specify the maximum amount of time, in seconds, that a
response can be reused from the cache.

### Taking advantage of compression

Servers and browsers have compression implemented already.

#### File compression

Files such as images, video or audio should use a compressed format.

#### Content-encoding (end-to-end) compression

The server compresses the body of the HTTP message prior sending it to the client.
It will remain compressed until it reaches the client (end-to-end).

The client and the server must agree on the compression algorithm to use via
*content negotiation*.

**gzip** is the most common type of compression.
Brotli (content-encoding type of **br**) is an open source, lossles
data compression library. It is newer than gzip, but it is gaining support
and popularity.

### Minifying resources

### Bundling resoureces

*Bundling* is the process of combining multiple files of the same type into a
single file, which can be transferred in a single request.

Fewer HTTP requests lead to faster page load performance.

Bundling is an effective technique when we are using HTTP/1.1.

A downside of caching is that it can cause the cache to be invalidated more frequently. Without bundling we can control the caching of each individual file.

Even with the use of buindling, the number of assets that a web page needs may be
higher than the maximum number of connections.
Additional requests for assets from the same host are queued by the browser
and will have to wait until a connection becomes available.
To work around this limitatin, the techinque of **domain sharding**
was introduced.

Domain sharding is a technique in which resources are split among multiple
domains, allowing more to be downloaded in parallel.

## Using HTTP/2

HTTP/2 is the latest version of the application layer protocol for data
communication. The HTTP status codes, verbs, methods, and most of the headers
will continue to be the same.

HTTP/2 is binary, whereas HTTP/1.1 is textual.

### Multiplexing

Multiplexing is the ability to send multiple HTTP requests and receive
multiple HTTP responses asynchronously through a single TCP connection.

With HTTP/2 we should no longer be concatenating files into a small
number of large bundles. This avoids the expensive cache invalidation
of a bundle.

Domain sharding is no longer necessary.

### Server push

HTTP/2 provides a feature in which the server can *push* responses that
it thinks a client will need.

When a resource is requested from a client, it may contain references
to other resources that are needed. Rather than wait for the client to send
additional requests for these resources, the server can proactively send them.

With server push there is no longer a need to inline resources.

If server push is not used properly, resources that a client already has could
be transfered unnecessarily.

Some web servers have the functionality to mitigate the problem of pushing
assets that the client does not need, and some browers may introduce
a *cache digest* to let the server know what assets it already has in its
local cache.

### Header compression

HTTP/2 performs header compression to improve performance.

## Using content delivery networks (CDNs)

Content delivery networks are a geographically distributed group of servers
that can deliver content to users quickly.

In addition CDNs improve load times through efficient load balancing,
caching, minification, and file compression.

## Optimizing web fonts

A CSS feature called *web fonts* provides you with the ability to download font
files so that any browser that supports web fonts can make the fonts that you
want to use for your page available.

Optimization of web fonts can reduce the overall size of a page and decrease
rendering times.

You should minimize the number of fonts that you use on your pages to minimize
the number of resources needed.

There is no standard on font formats. Different browsers support different
formats. This means that you will need to support four different
formats for each font:

* *Web Open Font Format version 2* (**WOFF 2.0**)
* *Web Open Font Format version 1* (**WOFF**)
* *TrueType font* (**TTF**)
* *Embedded Open Type* (**EOT**)

WOFF 2.0 and WOFF have built-in compression, but the TTF and EOT formats
are not compressed by efault, so servers should use compression when
delivering these formats.

The `unicode-range` property in `@font-face` is used to split up a font
into multiple substes, so that only the characters that are actually
needed will be downloaded.

Font resourcers are not updated frequently. You should ensure that this
type of resource is cached with a caching policy tha will allow them to live
in the cache for a long period of time.

## Optimizing the critical rendering path

The *critical rendering path* (**CRP**) is the set of steps in between
a browser receiving bytes from the server (e.g. HTML, CSS, and JavaScript files)
and the processing involved to render pixels on the device's screen.

Before a page can be rendered by a browser, it must construct both the
*Document Object Model* (**DOM**) and the *CSS Object Model* (*CSSOM**).
DOM and CSSOM are then combined to form a render tree, which has both the content
as well as the style information.

Once the render tree has been constructed, the browser moves to the layout stage
where it calculates the size and position of the various visible elements.
Finally the paint stage is reached, where the browser uses the results of the
layout to paint pixels on the screen.

We are mostly concerned with the portion of the page that is *above the fold*,
which referes to the part of the page that is visible without scrolling.

We want to prevent render blocking by reducing, as much as possible, the
resources that will prevent the content above the fold from rendering.

The inital step is to determine what resources are truly necessary for the
initial rendering. Using compression and caching, can help to load critical resources faster.

Resources that are not required for the above-the-fold content or are otherwise
not critical for the initial rendering can either be eliminated, their
download can be deferred, or they can be loaded asynchronously.

# Database performance

## Designing an efficient database schema

### Normalizing a database

Normalization is the process of designing tables and columns so that
they not only meet data requirements, but minimize data redundancy and increase
data integrity.

Attribues with a close logical relationship should be placed together in
the same relation. Redundancy of attributes should be kept to a minumum.

### Denormalizing a database

For performance and scalability reasons, there may be cases where it makes
sense to denormalize part of the database. A database should be normalized
firstt and then if there are cases where it makes sense to denormalize,
it should be done after careful consideration.

While denormalization might improve read performance, it will negatively
affect write performance. Using database constraints can help to enforce rules
that will keep the data consistent even when it is denormalized.

Another reason to introduce denormalization is to keep historical data.

### Identifying primary and foreing keys

Database constraints based on the primery and foreing keys shoudl be created
to enforce data intergrity.

### Selecting the most appropriate data types

We want to choose a data type that will sufficiently hold all possible
values but also be the smallest data type that is necessary.

## Using database indexes

When designing a table, one appreach is to keep the rows unordered and
create as many secondary indexes as necessary. Such an unordered structure
is called an *heap*.

Another approach is to create a *primary index*, also known as *clustered
index*, to order the rows by the primary key.

### Primary/clustered indexes

It is common to have a clustered index on a table which is known as a
*clustered table*.

A clustered index sorts the rows in a table based on their key values
and physically stores them on disk based on that order. Each table can only have
one clustered index.

### Secondary/ non-clustered indexes

Non-clustered indexes are defined by one or more columns that are ordered
logically and serve as pointers to find the rest of the data for a given record.
The order of a non-clustered index does not match the order of how the records
are stored on disk.

The key could be a foreing key or any column that will be frequently used in
joins, where clauses, ordering, or grouping.

### Having too many indexes

Every time that a record is added or updated in a table, an index record
also has to be added or updated, incurring some additional overhead to those
transactions.

Indexes take up additional disk space, increasing the overall size
of the database.

The more indexes you have on a table, the mor the query optimizer of the
DBMS will have to take into consideration for a particular query.
As a result, an increased number of indexes on a table could adversely affect
performance.

## Scaling up and out

Prior scaling up (vertically) or scaling out (horizontally), software
architects and DBAs should ensure that the database schema has been designed
properly and that indexes have been applied properly.

In addition, the application using the database should be optimized
to improve performance and remove bottlenecks.

Scaling up should be done first because there are additional complications
with scaling a database server out. You may need to horizontally partition
some of the table and consider data replication.

## Database concurrency

Having a database that performs well is only useful if it can handle
multiple processes accesing and changing data at the same time.

Concurrency control ensures that database transactions that are performed
concurrently maintain data integrity.

### Database transactions

A database transaction is a sequence of operations that are performed as a
single unit of work.

### Optimistic versus pessimistic concurrency control

*Optimistic concurrency control* (or *optimistic locking*) works
under the assumption that resource conflicts between multiple users,
while possible, are not common.

It allows transactions to execute without locking resources.
If there is a conflict, only one transaction is successful while the others
fail.

In constract, *pessimistic concurrency* (or *pessimistic locking*)
assumes that more than one user will want to update the same record at the same time.

It locks the appropriate reources as they are required for the duration
of the transaction.

### CAP theorem

The *Consistency, Availability, and Partition tolerance* (**CAP**) theorem
(a.k.a Brewer's theorem)  states that a distributed system can only achieve
two of the following three guarantees, but not all three:

* **Consistency** Every read either returns the latest data or an error.
    Every transaction either completes successfully or is rolled back.
* **Availability** A system always provides a response to every request.
* **Partition tolerance** In a distributed system, if one of the nodes
    fails, the system should still be able to function.

A traditional relational database will focus on consistency and availability.
Some NoSQL databases will value availability and partition tolerance over
consistency. For such databases, eventual consistency, rather than strong
consistency, is acceptable.

### ACID model

Databases that want to ensure consistency and availability will follow
the *ACID consistency model*. Strong consistency will place limits on
performance and scalability.

#### Atomicity

A transaction must be and atomic unit of work, meaning that either all of
its data modifications are perfomed, or none at all.

#### Consistency

After a transaction takes place, all of the data must be in a consistent state.
If a transaction leaves data in an invalid state, the transaction is aborted
and an error is reported.

#### Isolation

Changes made by concurrent transactions must be isolated from changes made by
any other concurrent transactions.

For example a DMBS may place a lock on a record being updated so that another
transaction cannot update the same record at the same time.

#### Durability

Once a transaction completes and is committed, its changes are persisted in the
database.

### BASE Model

Some databases focus on availability and partition tolerance.
They provide eventual consistency, rather than strong consistency.

This approach enables a higher degree of scalability and can yield faster
performance. These databases use the **BASE consistency model**.

#### Basic availability

The database is available most of the time and a response will be sent for
every request. However, confilcts can occur and the response may indicate
that a failure occurred when trying to access or change data.

#### Soft state

The concept here is that the state of the system coudl change over time. Even
if no additional transactions are being created, changes could take place
due to eventual consistency.

#### Eventual consistency

A data change will eventually propagate to everywhere that it needs to go.
If there are no further changes to a piece of data, the data will be in a
consistent state.
The system will not check the consistency of every transaction.