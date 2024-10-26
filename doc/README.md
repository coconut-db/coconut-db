# CoconutDB

## concepts

### Dictionary

List of all objects, basically a key-value storage of following items:

* Key
* ObjectType
* Create Timestamp
* Last Update Timestamp
* Last Read Timestamp
* Last Commit Timestamp
* Storage Type [Hot, Cold]
* Time To Leave [TTL]

### Object Type

Supported data structures:

* Linear Hash Table
* Sorted Table

### Shards

* [P) Primary](#)
* R) Replica

 Host 1           | Host 2           | Host 3           
------------------|------------------|------------------
 [Shard A (P)](#) | Shard A (R)      | Shard A (R)      
 Shard B (R)      | [Shard B (P)](#) | Shard B (R)      
 Shard C (R)      | Shard C (R)      | [Shard C (P)](#) 
 [Shard D (P)](#) | Shard D (R)      | Shard D (R)      
 Shard E (R)      | [Shard E (P)](#) | Shard E (R)      

### Hot and Cold Storage

### Commit and Flush

### Replication

### Leader Election

### Quorum (100% Consensus)

### Voting and Timeout

## CLI
