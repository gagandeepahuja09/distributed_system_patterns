* Kubernetes: Open source orchestrator for deploying containerized applications.
* It provides the software necessary to build reliable and scalable distributed systems.

* Why to use Kubernetes?
    * Velocity
    * Scaling(of both software and teams)
    * Abstracting your infrastructure
    * Efficiency

**Velocity**
* Changing landscape of everything being on the internet has led to speed of developing, deploying features being a critical factor.
* Speed shouldn't come at the cost of reliability.
* Core concepts that enable speed:
    * Immutability
    * Declarative Configuration
    * Online self-healing systems
* **Immutability**
    * apt-get update ==> Update to a mutable system.
    * In a mutable system, it is highly likely that the incremental updates are done by many different people and in many cases, won't be recorded properly.
    * In an immutable system, rather than a series of updates, an entirely new, complete image is built.
    * Building a new image means that the old image is still around and can be used for a rollback if required.
    * In contrast if we copy a new binary over an existing binary, such a rollback is nearly impossible.

**Declarative Configuration System**
