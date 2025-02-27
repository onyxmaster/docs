---
sourcePath: en/ydb/ydb-docs-core/en/core/concepts/_includes/serverless_and_dedicated/10_arch_diff.md
---
## {{ ydb-short-name }} architecture in different operating modes

### Separate compute and storage layers {#separate-layers}

Please note that YDB has two separate explicit layers: storage and compute. The storage layer is responsible for securely storing data on storage devices and replicating data between nodes to ensure fault tolerance.

In YDB, user data is stored in tables that are partitioned. A shard is an entity that is responsible for storing a table partition (typically one). An entity called a tablet is responsible for changing data in a shard. It's a component that implements consistent changes in the shard data and solves the issue of distributed consensus. A tablet instance can be viewed as an object that is generated in the process address space and consumes CPU resources and RAM. Tablets store all their statuses in the storage layer. This means, among other things, that a tablet instance can be raised in an arbitrary process that the storage layer is available from. The YDB compute layer essentially consists of tablets and the YQL query execution layer.

It should be noted that the concept of a database comprises user tables and, accordingly, tablet instances serving these tables as well as certain system entities. For example, there is a tablet called SchemeShard. It serves the data schema of all tables. There is a coordination system for distributed transactions whose items are also tablets.

### YDB Dedicated mode {#dedicated}

Dedicated mode assumes that resources for tablet instances and for executing YQL queries are selected from the compute resources explicitly allocated to the database. Compute resources are VMs that have a certain amount of vCPUs and memory. The task of selecting the optimal amount of resources for the DB is currently the user's responsibility. If there aren't enough resources to serve the load, the latency of requests increases, which may eventually lead to the denial of service for requests, such as that with the ```OVERLOADED``` return code. The user can add compute resources (VMs) to the database in the UI or CLI to ensure it has the necessary amount of computing resources. Adding compute resources to the DB is relatively fast and comparable to the time it takes to start a VM. After that, YDB automatically balances tablet instances across the cluster based on the resources added.

### YDB Serverless mode {#serverless}

In Serverless mode, the YDB infrastructure determines the amount of computing resources to be allocated to serve the user database. The amount of allocated resources can be either very large (an arbitrary number of cores) or very small (significantly less than one core). If a user created a DB that contains a single table with a single entry and makes DB queries very rarely, YDB actually uses a small amount of RAM on tablet instances that are part of the user DB. This is possible due to the fact that the user database components are objects rather than processes. If the load increases, the DB components start using more CPU time and memory. If the load grows to the point where there are not enough VM resources, the YDB infrastructure can balance the system granularly, generating tablet instances on other VMs.

This technology lets you package virtual entities (tablet instances) very tightly together into physical resources based on actual consumption. This makes it possible to invoice the user for the operations performed rather than the allocated resources.