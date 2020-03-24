# Deleting Datastores

## Request:

    POST /api/data_stores

``` json
{
  "action" : "delete",
  "resources" : [
    { "href" : "https://hostname/api/data_stores/7" },
  ]
}
```

## Response:

``` json
{
    "results": [
        {
            "success": true,
            "message": "Deleting Data Store id:7 name:'NFS_Datastore_1'",
            "task_id": "1",
            "task_href": "https://hostname/api/tasks/1",
            "href": "https://hostname/api/data_stores/7"
        }
    ]
}
```

Confirm the task deleted successfully using the `task_id` in the
response.

## Request:

``` json
GET /api/tasks/1
```

## Response:

``` json
{
    "href": "https://hostname/api/tasks/1",
    "id": "1",
    "name": "Deleting Data Store id:7 name:'NFS_Datastore_1'",
    "state": "Finished",
    "status": "Ok",
    "message": "Task completed successfully",
    "userid": "admin",
    "created_on": "2018-08-22T08:35:26Z",
    "updated_on": "2018-08-22T08:35:34Z",
    "pct_complete": null,
    "context_data": null,
    "results": null,
    "miq_server_id": "1",
    "identifier": null,
    "started_on": "2018-08-22T08:35:34Z",
    "zone": null,
    "actions": [
        {
            "name": "delete",
            "method": "post",
            "href": "https://hostname/api/tasks/1"
        },
        {
            "name": "delete",
            "method": "delete",
            "href": "https://hostname/api/tasks/1"
        }
    ]
}
------
```
