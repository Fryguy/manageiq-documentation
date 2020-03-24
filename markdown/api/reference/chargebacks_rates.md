# Chargebacks & Rates

Queries of Chargebacks and Management of Rates is provided via the
following collections:

``` data
/api/chargebacks
```

``` data
/api/rates
```

  - [Querying Chargebacks](#querying-chargebacks)

  - [Creating Chargeback Rates](#creating-rates)

  - [Updating Chargeback Rates](#updating-rates)

  - [Deleting Chargeback Rates](#deleting-rates)

## Querying Chargebacks

Querying all chargebacks in the system is simply:

    GET /api/chargebacks

or Query a specific chargeback, for example:

    GET /api/chargebacks/1

``` json
{
  "href": "http://localhost:3000/api/chargebacks/1",
  "id": "1",
  "guid": "b47a0ef0-4335-11df-aba8-001d09066d98",
  "description": "Default",
  "rate_type": "Compute",
  "created_on": "2014-11-20T19:10:03Z",
  "updated_on": "2014-11-20T19:10:03Z",
  "default": true
}
```

Optionally, one can query the rates details for a chargeback as follows:

    GET /api/chargebacks/:id/rates

Example getting additional rates details

### Request:

    GET /api/chargebacks/1/rates?expand=resources&attributes=description,metric,group,source,friendly_rate

### Response:

``` json
{
  "name": "rates",
  "count": 10,
  "subcount": 8,
  "resources": [
    {
      "href": "http://localhost:3000/api/chargebacks/1/rates/8",
      "id": "8",
      "description": "Fixed Compute Cost 2",
      "group": "fixed",
      "source": "compute_2",
      "friendly_rate": "0.0 Hourly"
    },
    {
      "href": "http://localhost:3000/api/chargebacks/1/rates/7",
      "id": "7",
      "description": "Fixed Compute Cost 1",
      "group": "fixed",
      "source": "compute_1",
      "friendly_rate": "1.0 Hourly"
    },
    {
      "href": "http://localhost:3000/api/chargebacks/1/rates/6",
      "id": "6",
      "description": "Used Disk I/O in KBps",
      "group": "disk_io",
      "metric": "disk_usage_rate_average",
      "source": "used",
      "friendly_rate": "Hourly @ 0.0 + 1.0 per Kbps from 0.0 to Infinity"
    },
    {
      "href": "http://localhost:3000/api/chargebacks/1/rates/5",
      "id": "5",
      "description": "Used Network I/O in KBps",
      "group": "net_io",
      "metric": "net_usage_rate_average",
      "source": "used",
      "friendly_rate": "Hourly @ 0.0 + 0.0 per Kbps from 0.0 to Infinity"
    },
    {
      "href": "http://localhost:3000/api/chargebacks/1/rates/4",
      "id": "4",
      "description": "Allocated Memory in MB",
      "group": "memory",
      "metric": "derived_memory_available",
      "source": "allocated",
      "friendly_rate": "Hourly @ 0.0 + 1.0 per Megabytes from 0.0 to Infinity"
    },
    {
      "href": "http://localhost:3000/api/chargebacks/1/rates/3",
      "id": "3",
      "description": "Used Memory in MB",
      "group": "memory",
      "metric": "derived_memory_used",
      "source": "used",
      "friendly_rate": "Hourly @ 0.0 + 0.0 per Megabytes from 0.0 to Infinity"
    },
    {
      "href": "http://localhost:3000/api/chargebacks/1/rates/2",
      "id": "2",
      "description": "Allocated CPU Count",
      "group": "cpu",
      "metric": "derived_vm_numvcpus",
      "source": "allocated",
      "friendly_rate": "Hourly @ 0.0 + 1.0 per Cpu from 0.0 to Infinity"
    },
    {
      "href": "http://localhost:3000/api/chargebacks/1/rates/1",
      "id": "1",
      "description": "Used CPU in MHz",
      "group": "cpu",
      "metric": "cpu_usagemhz_rate_average",
      "source": "used",
      "friendly_rate": "Hourly @ 0.0 + 0.0 per Megahertz from 0.0 to Infinity"
    }
  ]
}
```

## Creating Chargeback Rates

Creating a Chargeback Rate is done by posting a new resource or *create*
action to the rates collection.

Example follows:

### Request:

    POST /api/rates

``` json
{
  "per_time" : "daily",
  "chargeback_rate_id" : "1",
  "description": "My CPU allocation rate",
  "group" : "cpu",
  "per_unit" : "megahertz",
  "source" : "allocated"
}
```

### Response:

``` json
{
  "results": [
    {
      "id": "16",
      "enabled": true,
      "description": "My CPU allocation rate",
      "group": "cpu",
      "source": "allocated",
      "per_time": "daily",
      "per_unit": "megahertz",
      "friendly_rate": "",
      "chargeback_rate_id": "1",
      "created_on": "2016-08-16T08:27:22Z",
      "updated_on": "2016-08-16T08:27:22Z"
    }
  ]
}
```

<div class="note">

Please refer to the [Resource
Attributes](../appendices/resource_attributes.html#chargeback-rates)
page for a list of available attributes when creating Chargeback Rates.

</div>

## Updating Chargeback Rates

Updating rates can be done by posting **edit** actions on the rates
resource.

### Request:

    POST /api/rates/16

``` json
{
  "action" : "edit",
  "resource" : { "rate" : "0.02" }
}
```

### Response:

``` json
{
  "href": "http://localhost:3000/api/rates/16",
  "id": "16",
  "enabled": true,
  "description": "Allocated NICs",
  "group": "net_io",
  "rate": "0.02",
  "per_time": "hourly",
  "created_on": "2015-11-10T19:19:59Z",
  "updated_on": "2015-11-10T19:23:57Z"
}
```

## Deleting Chargeback Rates

Deleting Chargeback Rates can be done via either the **delete** post
action or the DELETE HTTP method.

### Request:

    POST /api/rates/16

``` json
{
  "action" : "delete"
}
```

### Response:

``` json
{
  "success": true,
  "message": "rates id: 16 deleting",
  "href": "http://localhost:3000/api/rates/16"
}
```

or simply:

    DELETE /api/rates/16
