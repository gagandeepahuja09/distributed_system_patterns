* Kubernetes is a very dynamic system. 
* The system is involved in placing Pods on nodes, making sure they are running, and *rescheduling* them as needed.
* HPA: allows automatically changing the no. of pods based on load.
* The API driven nature of the system encourages to create higher and higher levels of automation.

* While the dynamic nature of Kubernetes makes it easy to run a lot of things, it creates problems when it comes to *finding* those things. 
* Most of the traditional network infrastructure wasn't built for the level of dynamism that k8 has.

**What is Service Discovery**
* It helps solve the problem of finding which *processes* are *listening* at which *addresses* for which *services*.
* A good service-discovery system will enable users to resolve this information *quickly and reliably*.
* A good service-discovery system can store a richer definition of what the service is. Eg. there could be multiple ports associated with the service.