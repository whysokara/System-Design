### Vertical Scaling
* add more CPR, RAM, Disk to database
* requires downtime during reboot --
* has a physical hardware limitation --

### Horizontal Scaling : read replicas
* for vvv large data
* when read:write = 90:10
* all read requests are moved to read replica (nothing but a copy of your db)
* write goes to master db
* how to send read/write request to different db's? create multiple connections while at api server instead of single connection  
fire read query to replica db (put connection in business logic)

#### Replication

##### There are two types of replication:
1. Synchronous
user => API => Master => Replica  
api does npt respond to user untiland unless the input data from user reaches replica, (either from api or master regardless)
> Master and Replica will always be in sync
> It is slow, higher latency but zero replication lag

2. Asynchronous
user => API => Master => Replica
replication lag as Master don't write data into replica then and there
> Faster writes
in asynchronous replication, instead of master pushing data to replica, replica pulls data periodically
> no strong consistency (replica lag)

### Horizontal Scaling : Sharding
instead of one data node containing all the data, we will have 3 different nodes (shards)containing subsets of data (mutually exclusive) 
* shards are idependent, no replicatioin between them
* each shard cn have its own replica if needed

## Sharding and Partitioning
1. Sharding : method of distributing data across multiple machines/servers
2. Partitioning : splitting a subset of data within the same instance

> partitioning is about data, sharding is about databases