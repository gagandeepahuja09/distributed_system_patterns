* The traditional method of running multiple programs on a single machine require that all programs share the same versions of the shared libraries.
* If the different programs are developed by different teams or organizations, these shared dependencies add needless complexity and coupling between the teams.
* A program can only execute successfully if it can be reliably deployed onto the machine where it should run.
* This makes the task of rolling out a new version of a distributed system a labour-intensive task.

* The container images provides the immutability that is required to solve this problem. It solves all the problems of *dependency management* and *encapsulation*.

* Docker makes it easy to package an executable and push it to a remote registry where it can later be pulled by others.
* Container registeries and the services to build images are available in all of the major clouds.
* Registries make it easy for users to manage and deploy private images, while image builder provides easy integration with continuous delivery systems.

* Container images bundle a program and its dependencies into a single artifact under a root filesystem.

************************************************************************************

**Container Images**

**The Docker Image Format**
* The docker image format is made up of a series of filesystem layers.
* Each layer adds, removes or modifies files from the preceding layer in the filesystem. This is an example of an *overlay* filesystem.
* The overlay system is used both when packaging up the image and when the image is actually being used.

* 2 categories of containers:
    * System Containers
    * Application Containers

* System containers seek to mimic virtual machines and often run a full boot process. They are now seen as a poor practice and application containers have gained favor.
* Application containers differ from system containers in the fact that they commonly run a single program. Running a single program per container provides the level of granularity required for composing scalable applications and is a design philosophy that is leveraged heavily by Pods.