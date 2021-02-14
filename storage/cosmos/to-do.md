
# create a cosmos DB

to do:
create account and databases with each SDK using:
create stored procs
create UDF
create trigger
create change feed notification with az func

* portal
* AZ CLI
* Az Powershell
* ARM templates

understand differences between normal table storage API and Cosmos table storage API

## CLI examples

```
# create account
az cosmosdb create --name my-cosmos --resource-group my-resource-group

# create a sql DB
az cosmosdb database create --account-name my-cosmos --name my-db

# create a container
az cosmosdb sql container create --resource-group my-tg --account-name my-account --databasename mydb --name mycontainer --partition-key-path '/employeeid'
```