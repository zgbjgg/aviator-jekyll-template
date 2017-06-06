---
title: How it works?
position: 2
---

#### **_Cluster (Nodes)_**

**Hurakan** is designed for distributed computing, what it means is that the system runs over `"nodes"`.  

**Hurakann** is written in Erlang taking advantage of concurrency, native lightweight processes and availability.

Each node in **Hurakann** is a set of tools of a package, ready for building a cluster.

**Hurakann** is designed so that each node in the cluster balances the incoming requests among nodes avoiding that one member processes all. Each node in the cluster is an identical copy of other members so that all incoming requests are able to be processed by all members.

**Hurakann** uses primitive remote procedure calls (RPC) to balance the load of requests among nodes, so that a node receiving the request lookup for a `"free node of load"` or for a `"node with less load"` in the cluster and passes the request for processing.

One node could be of type:

* `Neighbor:`  the node is a worker in a cluster, and only processes required requests.  It is like an extension in the cluster.

* `Root:`  the node works as `"main"`, controlling neighbor nodes and balancing requests among them. This node type has a special feature: if it is disconnected from a cloud node then it will keep changes on the database for synced when it detects a connection. This node type is intended to work as an `"offline"` node, and the synced could be set as: enabled or disabled at any time. When a connection is detected the root node could handoff all data in the cloud to sync up the database, using vclocks.

* `Cloud:` the node is in the cloud and could have root nodes connected. The node is responsible for keeping all set of data of all root nodes connected or simply work as a "root" node but in the cloud. Root nodes could be added, as you need them at any time.


#### **_Vnodes_**

`Vnode` (Virtual Node) is a term used for describing virtual unique processes into a node, each virtual node is responsible for treating data, logging transactions and ensure atomicity and consistency of data. The `vnode` is a temporal process that lives while the processing of data is taking place.

A `vnode` starts when incoming a request (from client) and it keeps alive while the request is processed, stops when the process of data has finished (commonly when client receive response). A `vnode` uses `last write wins` so for example if two or more request collide in the system at the same time, the last of them writting, updating or deleting data will win and this will be the final data preserved into the backend database.

`Vnodes` are built with 3 processes linked, each process is responsible for a specific task into the `vnode`, they are:

* Worker
* Tracer
* Transactor

A `worker` process executes the `dirty work` in the `vnode`, so the `worker` process and validate the data flow ensuring the consistency in the data when writting, deleting or updating in the backend database, so in more simple words the `worker` execute transaction by transaction (write, update, delete, fetch) in the backend database.

A `tracer` process looks each transaction executed by the `worker`, so the `tracer` knows which one data is being modified at time, in others words the `tracer` is logging each transaction (write, update, delete, fetch) in the database backend.

A `transactor` process saves the log of data that the `tracer` is looking and is `'supervising'` to the `worker` so if the `worker` finish the `transactor` can determinate if it terminates with a `success` or `failure`. If the `worker` (for any reason) terminates in a `success` state the `transactor` can commit all data to the database backend, otherwise if the `worker` (for failure reasons) terminates (or abort) in a `failure` state the `transactor` can rollback all data to the database backend to a previous state and keeps the entire database in a state before executes the client request.


#### **_Plugins or addons_**

Plugins or addons is a special feature to allow adding modules, workers or applications into **Hurakann** node, and becomes an extension arm of the system.

Plugins allow **Hurakann** to process specific tasks on the node, replicating all behaviour in the cluster. For example if you need to process incoming messages on a specific port and format, a nicely protocol implementation for a specific message, generating random data can be created with plugins.

Plugins must be written in erlang and they are managed by **Hurakann**.

 
#### **_Security Concerns_**

`Ckey` (Client Key Token) is an id to access the API, so it's is used as an auth method against the black-box side, is an unique and unrepeatable value for each segment in the database. This token joined to another certificates in the core system ensures that all data are encrypted and stored in a specific segment of the database isolated from others, so only `vnodes` that are certificates to use the `ckey` can access data in the database. Ckey must be send in the Headers of each request in order to retrieve or push data. The certificates (including ckey) are created at the first time using the `CLI` and provided to the client.
