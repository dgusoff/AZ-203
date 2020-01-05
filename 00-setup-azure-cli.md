# Azure CLI

## Logging in

login with browser popup

`az login`

[login with service principal](https://docs.microsoft.com/en-us/cli/azure/authenticate-azure-cli?view=azure-cli-latest#sign-in-with-a-service-principal)

`az login --service-principal -u http://servicePrincipalName -p <password-or-cert> --tenant <tenant>`

list accounts

`az account list`

set the desired account as default

`az account set --subscription <subscription guid or name>`

## Working with rource groups

list resource groups

`az group list`

using output to table

`az account list --output table`

[more on outputs](https://docs.microsoft.com/en-us/cli/azure/format-output-azure-cli?view=azure-cli-latest)

## service principals

[docs on service principals](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest)

### Create a service principal


### list service principals

`az ad sp list --query "[].{id:appId, name:appDisplayName, tenant:appOwnerTenantId}"`
