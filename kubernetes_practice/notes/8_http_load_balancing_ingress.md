* The Service object operates at layer 4. This means that it only forwards TCP and UDP connections and doesn't look inside of these connections.
* Because of this, hosting many applications on a cluster requires having many different exposed services.
* In case where the services are type: NodePort, we'll need to have clients connect to unique port per service.
* For type: LoadBalancer, we'll be allocating cloud resources for each service with is often expensive or scarce.

* For HTTP-based services, we can do better.
* **Virtual Hosting**
    * Hosting many HTTP sites on a single IP address.
    * The user uses a load balancer or reverse proxy to accept incoming connections on HTTP(80) and HTTPS(443) ports.
    * The program then parses the HTTP connection and based on the Host header and the URL path that is requested, proxies the HTTP call to some other program.
    * **Ingress** is a kubernetes-native way of implementing the virtual-hosting pattern.
    * One of the more complex aspects of this pattern is that the user has to maintain the load balancer configuration file. In a dynamic environment and as the set of virtual hosts expands, this can be very complex.
    * Kubernetes ingress system works to simplify this by:
        1. Standardizing that configuration.
        2. Moving it to a standard kubernetes object.
        3. Merging multiple Ingress objects into a single config for the load balancer. 
