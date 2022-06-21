* The availability and reliability requirements have drastically increased over the past few decades.
* The potential of rapid, viral growth has led to application being required to be built to scale nearly instantly.
* Hence, every application that is built, needs to be a distributed system.
* Containers and container orchestrators are the building blocks for building reliable distributed systems.

**A Brief History of Systems Development**
* Started with purpose built machines: eg. for running precise, mathematical calculations.
* These machines evolved into general-purpose programmable machines.
* These machines evolved from a running one program to running multiple programs on a single machine via time-sharing operating systems.

* These machines were still disjoint from each other.
* Later, machines started to be networked with each other and client-server architecture was born. 
* Power of client-server achitecture: A relatively low-powered machine on someone's desk could be used to harness the power of a mainframe in another room or building.

* Distributed system: Many replicas(relatively low-cost) running across different machines, all communicating together to build a system like web-search or a retail sales platform.
* Pros:
    * Because of their distributed nature, when structured properly, distributed systems are more reliable.
    * When architected correctly, they can lead to much more scalable organizational models.
* Cons:
    * They can be much more complex to build, design and debug correctly.

* Fortunately, using containers and container orchestrators we can establish a collection of patterns and reusable components.

**A Brief History of Patterns in Software Development**