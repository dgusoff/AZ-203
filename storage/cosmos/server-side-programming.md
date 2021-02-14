# server side programming

* stored procs
* triggers
* UDF
* change feed

## internal
* sprocs, triggers, UDF executed within the DB engine (SQL only)
* created in Javascript

## stored procedures

* created in Javascript
* executes on single partition and only has access to that partition
* must provide partition key with request
* supports a transaction model

## triggers

* defined in JavaScript
* pre- and post- event triggers
* scoped to single partition
* not guaranteed to execute

## user defined functions

* javascript
* can be used inside a query
* encapsulate common logic


## change feed processing

* outside cosmos engine
* notfy for insert/update
* no deletes unless you use soft delete
* set TTL to low value to support deletes
* will consume throughput
* updates across partitions will not be returned in order
* supported for all APIs except Azure Table

## approaches

* Azure Functions (trigger)
* change feed processor




