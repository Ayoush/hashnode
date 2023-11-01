---
title: "Unveiling Software Architecture Styles - Part 2"
datePublished: Wed Nov 01 2023 03:10:40 GMT+0000 (Coordinated Universal Time)
cuid: clof6kbe0000109md7z57fyle
slug: unveiling-software-architecture-styles-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/q10VITrVYUM/upload/76934df9868596f52ac4b2fa3eef368c.jpeg
tags: software-development, technology, learning, system-architecture, system-design

---

In the first part of our exploration, we delved into the world of software architecture, uncovering the significance of architectural styles and their impact on the development process. We also ventured into real-world examples to understand how the likes of Airbnb, Netflix, and Amazon leveraged architectural decisions for success.

Now, in Part 2, we’re going to dig deeper into the two primary categories of architectural structures: monolithic and distributed architectures. As we traverse this architectural landscape, we’ll uncover the strengths, weaknesses, and real-world applications of each, helping you make informed decisions for your next software project.

### **Monolithic Architecture: Simplicity at Its Core**

In the world of software development, monolithic architecture styles are the cornerstone of simplicity. This architectural approach embodies the concept of a single deployment unit, making it relatively easy to design and implement. Such applications are often considered cost-effective, especially in terms of initial development costs.

However, while simplicity and cost-efficiency are the strong points of monolithic architecture, it has its limitations. A critical error, such as running out of memory, can lead to a system-wide failure, bringing all functionalities to a halt. Additionally, mean time to recovery (MTTR) and mean time to start (MTTS) are often measured in minutes, making rapid recovery and resilience to faults challenging.

![](https://cdn-images-1.medium.com/max/1600/0*J_oVJknqQSrzSeoF.png align="left")

### Real-World Examples of Monolithic Architecture

1. **Layered Architecture**: The layered architecture style divides the application into distinct layers, such as presentation, business logic, and data access. It’s widely used in traditional web applications.
    
2. **Modular Monolith**: In this approach, the application is built as a monolith but is divided into modules, which can be independently developed, tested, and deployed.
    
3. **Pipeline Architecture**: Often seen in data processing applications, the pipeline architecture processes data sequentially through a series of stages.
    
4. **Microkernel Architecture**: Microkernel architectures use a small, essential kernel and add features through dynamically loadable modules. The Windows operating system is an example of this approach.
    

### Distributed Architecture: Embracing Complexity

Distributed architectures, in contrast, are a realm of complexity. They consist of multiple deployment units, typically services, collaborating to achieve a unified business function. The operational characteristics of distributed architectures, such as scalability, elasticity, fault tolerance, and performance, often shine at the service level.

One of the significant advantages of distributed architectures is the high degree of fault tolerance they offer. Even if a service fails, the system as a whole can remain operational. Agility is another superpower of distributed architectures, allowing for quick response to change. With separate deployment units, it becomes easier to locate and apply changes, reduce testing scope, and minimize deployment risks.

![](https://cdn-images-1.medium.com/max/1600/0*MkYKNlxNqVkZCnkw.png align="left")

### Challenges and Fallacies in Distributed Architectures

However, distributed architectures come with their own set of challenges. The fallacies of distributed computing, including beliefs such as “the network is reliable,” “bandwidth is infinite,” and “latency is zero,” make maintaining determinism and reliability a considerable challenge.

Distributed architectures involve complexities like distributed transactions, eventual consistency, workflow management, error handling, data synchronization, and contract management. These complexities usually result in higher initial implementation and ongoing maintenance costs compared to monolithic architectures.

### Real-World Examples of Distributed Architecture

1. **Event-Driven Architecture**: Event-driven architecture relies on asynchronous communication through events, offering responsiveness and scalability. Examples include real-time systems and IoT applications.
    
2. **Microservices Architecture**: Microservices divide an application into small, independent services that can be developed and deployed separately. Netflix and Uber are prominent users of this architecture.
    
3. **Service-Based Architecture**: Service-based architecture involves collaborating services that work together to deliver a business function. It’s prevalent in modern enterprise applications.
    
4. **Service-Oriented Architecture (SOA)**: SOA focuses on services as the fundamental building blocks for creating software systems, promoting reusability and flexibility.
    
5. **Space-Based Architecture**: Space-based architecture, or distributed data grid, is suitable for applications requiring high performance and low latency, like financial systems and online gaming.
    

### Architectural Partitioning: Technical and Domain Strategies

Besides being classified as either monolithic or distributed, architectures can also be categorized based on how the overall structure of the system is partitioned. Architectures, whether they are monolithic or distributed, can be either technically partitioned or domain partitioned.

### Technical Partitioning

Technically partitioned architectures have the components of the system organized by technical usage. The classic example of a technically partitioned architecture is the layered (n-tiered) architecture style. In this architecture style, components are organized by technical layers; for example, presentation components that have to do with the user interface, business layer components that have to do with business rules and core processing, persistence layer components that interact with the database, and the database layer containing the data for the system.

![](https://cdn-images-1.medium.com/max/1600/0*VhS3aJIYe4YiXXao.png align="left")

For example, the customer domain functionality resides in the presentation layer as customer screens, the business layer as customer logic, the presentation layer as customer queries, and the database layer as customer tables. Manifested as namespaces, these components would be organized as follows: `app.presentation.customer`, [`app.business`](http://app.business)`.customer`, `app.persistence.customer`, and so on. Notice how the second node in the namespace specifies the technical layering, and that the customer node is spread across those layers.

Technical partitioned architectures are useful if a majority of your changes are isolated to a specific technical area in the application. If changes primarily affect one part of the architecture, like the user interface or the business rules, technical partitioning can be a suitable choice.

However, imagine implementing a new requirement to add an expiration date to items for customer wish lists in a technically partitioned architecture. This type of change is considered a domain-based change and impacts all layers of the architecture. To implement this change, you would need to coordinate across multiple teams and layers, which could be complex and time-consuming.

### Domain Partitioning

Domain-partitioned architectures organize components by domain areas, not technical usage. All functionality, including presentation, business logic, and persistence logic, is grouped by domain and subdomain areas in separate parts of the application. Components can be manifested through a namespace structure such as `app.customer`, `app.shipping`, `app.payment`, and so on. Even though domains may be organized by technical usage within these areas, the primary structure is still partitioned by domain.

![](https://cdn-images-1.medium.com/max/1600/0*WOnlsqMhH7_dB_aT.png align="left")

Domain-driven design, a software modeling and analysis technique coined by Eric Evans, places an emphasis on the design of a domain rather than on complex workflows and technical components. This approach allows teams to collaborate closely with domain experts and focus on one key part of the system, thus developing software that closely resembles that domain functionality.

The clear advantage of domain partitioning within an architecture is that changes to a particular domain or subdomain are self-contained within a specific area of the system, allowing teams to pinpoint exactly the area of the system that requires the change.

For example, when implementing changes like adding expiration data for a customer’s wish list items, with domain partitioning, the changes in code are isolated to one small part of the system. Presentation logic, business logic, and persistence logic are all within the same area, making changes more effective, maintenance easier, testing simpler, and deployment less risky.

### Choosing the Right Partitioning Approach

As you embark on your software development journey, one of the crucial decisions you’ll face is choosing between a monolithic or distributed architecture. The question you should ask is whether your system requires consistent architectural characteristics throughout or if different parts have distinct needs.

When deciding between technical and domain partitioning, consider your overall team structure and the nature of expected changes:

### Technical Partitioning:

Technically partitioned architectures (monolithic or distributed) are suitable when your team structure aligns with technical usage areas. It’s also ideal when most anticipated changes align with technical layers.

### Domain Partitioning:

Domain partitioned architectures excel when your teams are cross-functional, and you emphasize domain specialization. Be cautious when selecting domain partitioning if you anticipate frequent changes to technical usage layers.

In the next instalment of our series, we’ll unveil real-world case studies that showcase the effectiveness of architectural partitioning. Stay tuned for more insights into the world of software architecture.

---

In this article, we’ve explored the contrasting worlds of monolithic and distributed architecture, as well as the crucial concept of architectural partitioning. We’ve emphasized the importance of choosing the right partitioning approach based on your team structure and anticipated changes. Stay tuned for Part 3, where we’ll dive into individual architectural styles