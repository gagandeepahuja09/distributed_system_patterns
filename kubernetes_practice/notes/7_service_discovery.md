* Kubernetes is a very dynamic system. 
* The system is involved in *placing Pods on nodes*, *making sure they are running*, and *rescheduling* them as needed.
* HPA: allows automatically changing the no. of pods based on load.
* The API driven nature of the system encourages to create higher and higher levels of automation.

* While the dynamic nature of Kubernetes makes it easy to run a lot of things, it creates problems when it comes to *finding* those things. 
* Most of the traditional network infrastructure wasn't built for the level of dynamism that k8 has.

**What is Service Discovery**
* It helps solve the problem of finding which *processes* are *listening* at which *addresses* for which *services*.
* A good service-discovery system will enable users to resolve this information *quickly and reliably*.
* A good service-discovery system can store a *richer definition* of what the service is. Eg. there could be multiple ports associated with the service.

* DNS is the traditional system of service discovery. It is designed for relatively stable name resolution with wide and efficient caching.
* It falls short in the dynamic world of kubernetes. Problems:
    1. *Client Caching* 
        * Many systems(eg. Java, by default) look up a name in DNS directly and never re-resolve.
        * This can lead to clients caching stale mappings and talking to the wrong IP.
        * Even with short TTLs and well-behaved clients, there is a natural delay between when a name resolution changes and when that client notices.
    2. *DNS Query Information Limitation*
        * Limitations to the amount and type of information that can be returned in a typical DNS query. 
        * Things start to break past 20-30 A records for a single name. SRV records solve some problem but are very hard to use.
    3. *Load Balancing*
        * Clients handle multiple IPs in a DNS record by taking the first IP and relying on the DNS server to randomize or round-robin the order of the records.
        * This is no substitute for purpose-built load balancing.

**The Service Object**
* Real service discovery in Kubernetes starts with a Service object.
* A Service object is a way to create a named label selector.
* kubectl create deployment => Easy way to create a Kubernetes deployment.
* kubectl expose deployment => To create a service. 
* --image=gcr.io/<namespace_name>/kuard-amd64:blue

`
    $ kubectl create deployment alpaca-prod \
    --image=gcr.io/default/kuard-amd64:blue \
    -- replicas=3 \
    --port=8080 \
    --labels="ver=1,app=alpaca,env=prod"
        output: pod/alpaca-prod created

    $ kubectl expose deployment alpaca-prod --port=8080

    $ kubectl create deployment bandicoot-prod \
    --image=gcr.io/default/kuard-amd64:green \
    -- replicas=2 \
    --port=8080 \
    --labels="ver=2,app=bandicoot,env=prod"

    $ kubectl expose deployment bandicoot-prod --port=8080

    $ kubectl get services -o wide
        Two of the services are the ones we just created. The kubernetes service is automatically created so that we can find and talk to the Kubernetes API from within the app.
`

* **Cluster IP**: 
    * Virtual IP assigned to a service.
    * This is a special IP address the system will load-balance across all of the pods that are identified by the selector.

* Port forwarding to the first Alpace pod:
    kubectl get pods -l app=alpaca-prod

`
    $ ALPACA_PROD=$(kubectl get pods -l app=alpaca \
        -o jsonpath='{.items[0].metadata.name}')
    $ kubectl port-forward $ALPACA_PROD 48858:8080
`

**Service DNS**
* Because the cluster IP is virtual, it is stable and hence appropriate to give it a DNS address.
* All of the issues arounds the client caching DNS no longer apply.
* Within a namespace, it is as easy as just using the service name to connect to one of the pods identified by a service.

* Kubernetes provides a DNS service exposed to pods running in the cluster.
    * This kubernetes service was installed as a system component when the cluster was first created.
    * This DNS service is managed by Kubernetes and a great example of kubernetes building on kubernetes.
    * It provides DNS names for cluster IPs.
...

**Readiness Checks**

**Looking Beyond The Cluster**
* Acheived by NodePorts to allow traffic outside of a cluster.
* $ kubectl edit service alpaca-prod
    * Change the spec.type field to NodePort.
    * We can also do this during service creation: kubectl expose --type=NodePort
* If we are sitting on the same network, we can access it directly. If the cluster is in cloud, we can use SSH tunneling:
    ssh <node> -L 8080:localhost:30005
    * 30005 is the NodePort.

**Advanced Details**
* Kubernetes is build to be an extensible system.
    * There are layers that allow for more advanced integrations.
* Understanding the details of how services is implemented will help us both troubleshoot and create more advanced integrations.