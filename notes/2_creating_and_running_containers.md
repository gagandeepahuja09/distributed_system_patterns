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

**Building Application Images With Docker**

**Dockerfiles**
* Can be used to automate the creation of a docker container image. It is the recipe for how to build the container image.
* Check the node example
* npm install --save express
* docker build -t simple-node .
* docker run --rm -p 3011:3011 simple-node.

**Optimizing Image Sizes**
1. Files that are removed by subsequent layers in the system are actually still present in the images; they are just inaccessible.
2. Image caching and building: Every time you change a layer, it changes every layer that comes after it.
Hence the layers should be ordered from least likely to change to most likely to change. Hence better to install dependencies first in the layer before adding the source code file. A dev is going to update code much more often than updating the dependencies. 

**Image Security**
* Don't build containers with password baked in. Secrets and images should never be mixed.
* Deleting a file in one layer doesn't delete that file from preceding layers. It can be accessed by anyone with the right tools.

**Multistage Image Builds**
* One of the most common ways to accidentally build large images is to do the actual program compilation as part of the construction of the application container image.
* It leaves all of the unnecessary development tools lying around inside of your image and slows down the development.

* To resolve this problem, docker introduced multistage builds. Through this, a dockerfile can produce multiple images where each image is considered as a stage.

* Hands on example:
    * The single stage Dockerfile produces a container image containing the static executable but it also includes all the Go, React development tools and the source code of the application. None of this is needed in the final application. 
    * In multistage build, the build image contains all of of the above files but the deployment image only contains the executable file. This reduces the final container image size by 100s of MBs and dramatically speeds up deployment times.
* docker build -t project-name .
* docker run --rm -p 8080:8080 project-name

**Storing Images in A Remote Registry**
* What good is a container image if it's only available on a single machine.

* Kubernetes relies on the fact that images described in a pod manifest are available across every machine in the cluster.

* Remote registry can be private(aws/azure/gcr[google container registry]) or public(dockerhub)

* docker tag project-name gcr.io/project-name-demo/project-name-amd64:v1