# Perfomrance

## Throughput and Scaling

### Request Unit (RU)

consolidates resources into a single unit
 
1 RU is equal to a 1kb item read operation

* processor
* memory
* IOPs

### types of throughput

* provisioned throughput
* serverless


### Provisioned throughput

* for prod workloads
* can be config'd at database or container level
* evenly dist to partitions
* min 10 RU per GB or storage
* rate limited after RUs consumed
* requires manaual scaling approach (trigger alert, increase RU)

## autoscaled provisioned

* specify maximum RU amount
* min is 10% of maximum

## serverless

* pay only for consumption and storage
* ideal for development workloads
* max 5k RU
* requires a new account type (only SQL at the moment)


## best practices

* use a partition strategy
* provision at container for predictable performance
* link between consistency types and RU's consumed

# Consistency Levels

-- tradeoff between read consistency, availability, latency and throughput

## Consistency level spectrum

* Eventual -- low latency - data not up to date
* Consistent Prefix
* Session
* Bounded Staleness
* Strong -- hiher latency, lower throughput, lower availability

* String Consistency - guaranteed to get latest
* Bounded Staleness - fairly recent (time or versions)
* Session - client session can read its own writes
* Consistent Prefix - updates guaranteed to be read in order
* Eventual - no guarantees

## setting in SQL

setting consistency levels
* account default
* request specific


# Partitioning

* logical partition
* physical partition
* partition key
* replica set


## Logical Partition
* set of items sharing same partition key

## physical partitions
* include logical partitions
* will contain multiple replicas (replica set)

### strategy considerations
* throughput distibuted evenly across partitions (hot partition)
* transactions require triggers/stored procs
* minimize cross partition queries for heavier workloads
* decide strategy before creating container







