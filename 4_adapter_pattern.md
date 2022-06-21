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