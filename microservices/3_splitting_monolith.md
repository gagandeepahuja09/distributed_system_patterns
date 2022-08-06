**What to move first? Code or Data**

**Code First**
* Even if we decide to move the code first, we should prepare a plan on:
    * Whether it is possible to move all the required data out.
    * The dependencies on the other teams or tables/entities to move the code out.

**Data First**
* It is less common but has the advantage if we are unsure whether the data can be cleaned up separately.
* If forces us to *deal up front with issues like loss of enforced data integrity or trasnsaction operations* across both or multiple sets of data. We might require implementing *distributed transactions*.

**Strangler Fig Pattern**
* Interception layer decides whether code should be handled by the monolith or the microservice.
* The interception layer can be build in a separate service or gateway level or in the monolith.

**Parallel Run**
* Running both monolith and microservice side-by-side and comparing the results.
* Canary deployments don't allow comparing exactly the same request.

**Data Decomposition Concerns**

**Performance**
* Database joins won't be possible.