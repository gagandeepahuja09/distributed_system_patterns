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
* Everything in Kubernetes is a declarative configuration object that represents the *desired state of the system*.
* It is the job of Kubernetes to ensure that the actual state of the system matches the desired state.
* Much like mutable vs immutable infrastructure, declarative configuration is an alternative to imperative configuration. 
* In imperative configuration the state of the world is defined by the execution of a series of instructions rather than a declaration of the desired state of the world.
* While imperative configurations define actions, declarative configuration define state.
* Imperative => "run A, run B, run C", Declarative => "replicas = 3".
* Since the effects of declarative configuration can be understood far before they are executed, they are far less error-prone.
* Storing declarative configuration in source code => Infrastructure as code.
* Declarative configuration makes rollback of a change trivially easy. This is usually impossible with imperative systems, because although they describe how to go from point A to point B, they rarely include the reverse instructions.

**Self Healing Systems**
* When Kubernetes receives the desired state, it does not take action once to ensure that the current state matches the desired state a single time.
* It continuously takes action to ensure that the current state matches the desired state.
* This means that not only will k8s initialize your system, it will guard it against any failures that may destabilize the system.
* Imperative repair or human intervention is more expensive(requires on-call operator).
* Kubernetes both reduces the burden on operators and improves the overall reliability.

* More advanced form of self healing: *Operator* paradigm of kubernetes.
    * More advanced logic need to maintain, scale and heal a specific piece of software is encoded into an operator application that runs as a container in the cluster.