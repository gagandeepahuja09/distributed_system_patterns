* The adapter container is used to modify the interface of the application container so that it conforms to some predefined interface that is expected of all applications.
    * Eg. Ensuring that the log files are always written to stdout.

* Very useful when we might be having variety of conventions being followed for monitoring, logging, or other common services.

* When each application provides metrics using a different format and interface, it is very difficult to collect all these metrics in a single place for visualization. Adapter pattern becomes very useful here.

**Monitoring**
* Rolling out new versions of the application doesn't require a rollout of the monitoring adapter.
* The monitoring container can be reused with multiple different application containers.
* The monitoring container may even have been supplied by the monitoring system maintainers independent of the application developers.
* Deploying the monitoring adapter as a separate container ensures that each container gets its own dedicated resources in terms of both CPU and memory. This ensures that a misbehaving monitoring adapter cannot cause problems with a user-facing service.

**Hands On: Using Prometheus for Monitoring**
* Prometheus is a monitoring aggregator which collects metrics and aggregates them into a single time-series database.
* On top of this, prometheus provides visualization and query language for introspecting the collected metrics.
* To collect metrics, prometheus expects every container to expose a specific metrics API.

* Redis doesn't expose the metrics API in a format compatible with prometheus.
* We can find a prometheus container on docker hub: https://hub.docker.com/r/oliver006/redis_exporter

* The example not only shows adapter pattern, but container reuse in general.
* The absence of adapter pattern, this would have required significantly more effort.

**Logging**
* Much like monitoring, there is a wide variety of hetrogenity in how systems log data to an output stream.
    * Logging at different levels(info, debug, warning, err) with each log going to separate file.
    * Logging to stdout and stderr. This can be problematic as container get access to only stdout logs using docker logs and kubectl logs.
    * Structured information like date/time, but the format could vary across differen libraries.

* How adapter pattern will solve the problem?
    * The application container logs to a file, the adapter container redirects it to stdout.
    * Different application containers can log in different formats, but the adapter container can transform that data into a single structured format that can be consumed by the log aggregator.

* *The adapter is taking a heterogeneous worlds of applications and creating a homogeneous world of common interfaces*. 

* Why not modify the application container itself?
    * Container can be a third-party one. In that case, deriving a slightly modified image that we have to maintain (patch, rebase, etc) is significantly more expensive than developing an adapter container that run alongside party's image.
    * Other usecase: reuse and alternative solution if enforcing a practice throughout is difficult(which generally is). 