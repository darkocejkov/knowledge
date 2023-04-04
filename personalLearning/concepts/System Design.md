System Design is a very high-level decision process. It's a discipline that is very important because it provides an excellent way to design and plan system interfaces before we start a project.
It's important to know because these design *decisions* influence what, how, and why we use the tools and technology we use when it comes to planning a product.
The idea of a "product" or "project" or "feature" is dependent on the system that it uses.

### Personal Experience
Working on a project from the very beginning has shown me that it really was the case that almost no design or planning was in-place before the project actually started. Trying to build a robust product/service was super difficult on these terms, because we started with the very basics, and started adding new tools along the way, without researching "the best" for our use-case. 
Adding new tech, libraries, tools through our decisions without researching and comparing the competition lead us to have an insane amount of re-factoring to do.
A more concrete example of this is the fact that the project started without any real-time messaging "engine" to help us synchronize users - it had to be done entirely through RESTful API queries, and involved an incredibly complex system to ping client and server status. Then, we learnt of webhooks, and re-implemented features to use webhooks instead. Then, we learnt of WebSockets, then re-re-implemented the same features. It just lead to an insane amount of variations in components and features, and a lot more complexity than it needed to be - all because we did not sit down and design how these discrete component systems would work together.
___

# Why?
System design is the *optimization* of systems to enable a higher limit of what is possible for a given product. It's a very important step and it's even more important to *do it right*. Modern systems need to handle unfathomable amounts of users in the millions and billions in small time frames. Without optimizing and designing systems, you'll never get there by just trial-and-error.

# What?
> The process of defining architecture, interfaces, and data model for system that must satisfy specific requirements
> It entails knowing and understanding every part of the system, especially understanding the PROs and the CONs of each decision and pattern that's being used.

# [Fundamentals](https://www.educative.io/blog/complete-guide-to-system-design#whatissystemdesign)

## Scalability
The ability to handle and withstand increased workload without sacrificing latency. It's desirable to have as many users as possible, without having to worry about if the servers can handle it. 

**Horizontal** scaling, also called "scaling *out*", is when we can add more *hardware* to the existing pool of hardware. This means that we can  add more servers as a way to handle more traffic. Think of distributed computing, or CDNs - they work so well because they horizontally scale to handle requests from different areas, in the most efficient way. 

**Vertical** scaling, also called "scaling *up*" is when we can add more power to the server, upgrading its hardware to have more storage, more power (CPU/GPU), or more bandwidth. 

## Microservices
A microservice architecture is one in which the various functional components of a service can be seperated and exist on different hosts. Imagine your server has a single API service that handles all requests - it has the possibility to bottleneck when different services might be trying to work heavily at the same time. 
> Think of various silos, or teams which handle each service as a task. Instead of having one giant team handle all tasks, we can split up into smaller teams and focus on each task. If one team needs another team's work, they can request the other team to do so, and vice versa.

Each service can be individually developed, deployed and maintained, which makes microservices scale really well because they can have their own database, codebase, and hardware dedicated to them. If one service goes down, not all of them necessarily stop functioning.
When microservices also need to expand and scale themselves, they are able to do so by creating a mini-microservice architecture as their own service.

[Containers](https://cloud.google.com/learn/what-is-microservices-architecture#:~:text=Microservices%20architecture%20(often%20shortened%20to,its%20own%20realm%20of%20responsibility.) are often used in conjunction with microservices as a way to maintain and host these services in their singular silos. With `Docker Compose`, we can compose or orchestrate multiple Docker containers instead of having to manage each microservice's container individually.

## Proxy Servers
A *proxy* server is a "middle-man" server, that seperates the client and server from direct communication. 
There are many applications and uses of proxy servers:
- if you're requesting a website, you might be contacting a proxy server that represents the actual server, for which the proxy may cache or request the data from the real server
- there may be a proxy server that stands in-between your client and all network requests, such as a school's network. it intercepts all requests you make and can check your requests to make sure you're not trying to access blocked resources

## CAP Theorem
A **distributed** system can only provide TWO of the THREE:
1. Consistency
2. Availability
3. Partition Tolerance

> [!Distributed Systems]
> A network of computers that is used to handle different requests (almost like [[#Microservices]]), and acts as single computer in the perspective of the user.

It means that there must always be a trade-off:
- Consistency
	- all nodes see the same data simultaneously
- Availability
	- the entirety of the system is operational
- Partition Tolerance
	- the ability to perform its function regardless of whether or not necessary nodes are able to communicate
		- Requires redundancy of information across nodes and networks

## Redundancy + Replication
Redundancy is the duplication of critical system components to increase reliability/performance.
- backups, fail-safes, secondary servers
- or, in the context of SQL databases, repeated data already in database

Replication is a process of maintaining consistent state between redundancies.
