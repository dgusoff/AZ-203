# Event Grid

https://app.pluralsight.com/library/courses/microsoft-azure-developer-develop-event-based-solutions

## 3 event types
1. discrete changes - actionable state changes - event grid
2. series - condition, time ordered, analyzable (ie, Telemtry) - event hub
3. user notification (notification hub)


## Event Grid
event based achitectures (pub/sub)
publishers emit, subscribers consume

many subscribers to one publisher
subscribers can set filter rules
scalable all the way up and down
serverless

need to enable the resource provider at subscription level

`az provider register --namespace Microsoft.EventGrid`

`az provideer show --namespace Microsoft.EventGrid --query "registrationState"`

enable via CLI and via portal

### pub/sub concetps
event signifies something that changed

publisher has no expectation of subscriber actions

subscriber determines what to do

terminology
* Event what happened
* publisher - emit the event
* topics - endpoint - colleciton of related events
* subscription - routes and filters to handlers
* handlers - endpoints that receive events

publishers. ex,
app config
app servce
blob storage
communicaiton svc
container registry
event hubs
ML
maps
resource groups
signalR

custom topics
user defined

event handlers
az function bindings
webhooks
service bus
storage queues


workflow
create a topic(endoint)
send publisher events
add subscriber
events all have same schema. `data` property will have custom properties
