**Pattern: The Shared Database**
* Major issue: *information hiding*. We deny ourselves the opportunity to decide *what is shared and what is hidden*.
    * It can be difficult to understand what parts of a schema can be changed safely.
    * Knowing that an external service can access your database is one thing but knowing what part of the schema they use is another.
    * Views can help mitigate this, but that's not a total solution.

* *Unclear on who owns the data.*

* *Tight coupling*: 
    * Eg. Three services can directly change information in one of the tables.
    * What happens if the behavior is inconsistent across the services.
    * What happens if the behavior needs to change? Do I need to apply to all services?

**Pattern: Database Views**

**Pattern: Database Wrapping Service**

**Pattern: Database-as-a-Service Interface**
* We are moving away from batch based method of data replication to real-time. Eg. CDC ==> change data capture.

**Transfering Ownership**
* The above solutions are mostly like applying bandages.
* If our new microservice needs to interact with an aggregate that is still owned by the monolith, we need to expose it via a well-defined interface.

**Pattern: Aggregate exposing monolith**

**Pattern: Change Data Ownership**
* Consider the impact of breaking foreign-key constraints, breaking transactional boundaries.

**Data Synchronization**
* When adpoting a pattern like the strangler fig pattern, we'll need to ensure that we keep both the DBs in sync.
* Try to avoid big-bang switchover, migrating both the database and the code.

**Pattern: Synchronize Data in Application**

**Step 1: Bulk Synchronize Data**
* Create a bulk export and bulk import it to the other DB.
* A change data capture process was implemented so that the changes since the import could be applied.

**Step 2: **