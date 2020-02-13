# SNS Messaging

## Message Format

### Message Attributes

These attributes are included with every SNS message.

``` yaml
divID: division_id:Integer
environment: RightsLine_environment:String,
userID: user_id:Integer
```

### Entity Messsages

#### Entity Created

``` json 
{
    "action": "created",
    "messageGroupId": 1,
    "template": {
        "templateId": 1,
        "templateName": "Series"
    },
    "status":{
        "statusId": 1,
        "statusName": "Created"
    },
    "entityUrl":"https://api.rightsline.com/v3/catalog-item/400",
    "entityId": 400,
    "createdBy": 100,
    "createdDate": "2016-01-22T16:10:31.617Z"
}
```

#### Entity Updated

``` json 
{
    "action": "updated",
    "messageGroupId": 1,
    "template": {
        "templateId": 1,
        "templateName": "Series"
    },
    "status":{
        "statusId": 2,
        "statusName": "Active"
    },
    "entityUrl":"https://api.rightsline.com/v3/catalog-item/400",
    "entityId": 400,
    "lastUpdatedBy": 100,
    "lastUpdatedDate": "2016-01-22T16:10:31.617Z"
}
```

#### Entity Deleted

``` json 
{
    "action": "deleted",
    "messageGroupId": 1,
    "template": {
        "templateId": 1,
        "templateName": "Series"
    },
    "status":{
        "statusId": 3,
        "statusName": "Deleted"
    },
    "entityUrl":"https://api.rightsline.com/v3/catalog-item/400",
    "entityId": 400,
    "deletedBy": 100,
    "deletedDate": "2016-01-22T16:10:31.617Z"
}
```
