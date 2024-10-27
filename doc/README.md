# CoconutDB

## Proposal Concepts

### Block-Shards

* [P) Primary](#)
* R) Replica

 Host 1     | Host 2     | Host 3     
------------|------------|------------
 [A (P)](#) | A (R)      | A (R)      
 B (R)      | [B (P)](#) | B (R)      
 C (R)      | C (R)      | [C (P)](#) 
 [D (P)](#) | D (R)      | D (R)      
 E (R)      | [E (P)](#) | E (R)      

### Block-Shards Meta Space

Each **Block-Shard** has its own dictionary to use as look-up for Metadata. It is a Look-up key-value storage to store Metadata related to records.  
List of all objects, basically a key-value storage of following items:

* [Key]
* ObjectType
* Create Timestamp
* Last Update Timestamp
* Last Read Timestamp
* Last Commit Timestamp
* Storage Type [Hot, Cold]
* Time To Leave [TTL]

### Object Type

Supported data structures:

* Hash Table
* Sorted Table

### OS Level Memory Blocking

technics to use for block-Shards:

#### Memory Advice `madvise` 
The madvise system call allows you to provide the OS with hints about memory usage, which can optimize how memory is handled. For instance, `MADV_SEQUENTIAL` can inform the OS that memory will be accessed sequentially, potentially improving read performance.

```go
// Size of memory to allocate
const size = 1024 * 1024

// Allocate and mmap memory
addr, err := unix.Mmap(-1, 0, size, unix.PROT_READ|unix.PROT_WRITE, unix.MAP_PRIVATE|unix.MAP_ANON)
if err != nil {
log.Fatalf("mmap failed: %v", err)
}

// Use madvise to give memory usage hints
if err := unix.Madvise(addr, unix.MADV_SEQUENTIAL); err != nil {
log.Fatalf("madvise failed: %v", err)
}

// Use the memory...

// Unmap memory when done
if err := unix.Munmap(addr); err != nil {
log.Fatalf("munmap failed: %v", err)
}
```

#### Locking Pages in Memory `mlock` and `munlock`
The `mlock` function locks specific pages in memory, preventing them from being swapped to disk. This can be important for applications requiring low-latency access to data.

```go
// Size of memory to allocate
const size = 1024 * 1024

// Allocate a slice of bytes
mem := make([]byte, size)

// Lock the memory to prevent it from being swapped out
if err := unix.Mlock(mem); err != nil {
log.Fatalf("mlock failed: %v", err)
}

// Use the memory...

// Unlock the memory after use
if err := unix.Munlock(mem); err != nil {
log.Fatalf("munlock failed: %v", err)
}
```


### Hot and Cold Storage

### Commit and Flush

### Replication

### Leader Election

### Quorum (100% Consensus)

### Voting and Timeout

## CLI
