# Cosmos DB

## Section Objectives

* Select the appropriate API for your solution
* Implement partitioning schemes
* interact with data using appropriate SDK
* set appropriate consistency level for operations
* create Cosmos DB containers
* implement scaling (partitions, containers)
* implement server side programming including stored procs, triggers, change feed notifications



## Relational vs no-SQL

### Relational

* Table based structure
* Fixed Schema
* Vertical scaling and manual sharding for scalability
* ACID Guarantees (atomicity, consistency, isolation, durability)
* Data is normalized

### NO SQL

* Schema is fluid
* Multiple structures (key-value, graph, document, wide column)
* Horizontal scaling and data partitioning
* BASE (basically available, soft state, eventual consistency)
* data is non-normalized

## Capabilities

* extremely low latency
* SLA for throughput, latency, availability, consistency
* multi region replicaiton
* 5 nines reads and writes
* elastic scalability
* pricing based on throughput
* multiple consistency options

## Features
* integrated analytics
* region support
* schema agnostic
* automatic indexing
* multiple sdk's

## DB organization (SQL API)

* account is high level container
* select API at account level
* databases inside account
* DBs contain containers
* containers contain items

## DB APIs

* SQL - SQL-like syntax
* Cassandra
* Monfo
* Gremlin
* Azure Table

## Cassandra

* makes sense if already familiar or existing tooling
* can migrate Cassandra DBs
* might want to use wide column format

## Mongo

* if familiar with Mong already
* can leverage existing tooling
* can migrate existing Mongo DB
* store data as JSON documents

## Gremlin
* store graph relaitonships between data
* recommendation engines, social networks
* leverage Apache tinkerpop Gremlin language


## Azure table API

* existing knowledge of Az table API
* migrate from tabel storage
* Odata -linq

## DB entity names
* SQL,Mongo,Gremlin: "Database"
* Cassandra: Keyspace
* AZ Table: N/A

## Container entities

* SQL: container
* Cassandra: Table
* Mongo: Collection
* Gremlin: Graph
* AZ Table: Table


## SQL

* this is the core API
* SQL like queries
* JSON documents
* the default

## selecting an SDK
* SQL - use latest for platform
* Mongo/Cassandra/FGramlin: use SDK for those SDKs
* Az table - use table storage API - need to understand differences



## Resources:

Pluralsight

https://app.pluralsight.com/library/courses/microsoft-azure-developer-develop-solutions-cosmos-db-storage


MS Docs

main: https://docs.microsoft.com/en-us/azure/cosmos-db/
