# Specification

## HTTP Basics

### REST API Entry Point

The REST API is available via the `/api` URL prefix. It is accessed on
the ManageIQ server as follows:

    https://<host_fqdn>/api

`Response`

``` json
{
  "name" : "API",
  "description" : "REST API",
  "version" : "2.0.0",
  "versions" : [
    {
      "name" : "2.0.0",
      "href" : "https://hostname/api/v2.0.0"
    },
  ]
  "collections" : [
    {
      "name" : "automation_requests",
      "href" : "https://hostname/api/automation_requests",
      "description" : "Automation Requests"
    },
    {
      "name" : "availability_zones",
      "href" : "https://hostname/api/availability_zones",
      "description" : "Availability Zones"
    },
    ...
  ]
}
```

  - `version` is the current API version, accessible via either of the
    following:

  - /api/

  - /api/v2.0.0/

  - `versions` lists all the earlier API versions that are still exposed
    via their respective entry points:

  - /api/vVersion/

### Supported Content Types

Requests:

    Accept: application/json

Responses:

    Content-Type: application/json

### URL Paths

The recommended convention for URLs is to use alternative collection or
resource path segments, relative to the API entry point as described in
the following example:

| URL                                 | Description                                                |
| ----------------------------------- | ---------------------------------------------------------- |
| /api                                | The REST API Entrypoint                                    |
| /api/v**Version**                   | The REST Entrypoint for a specific version of the REST API |
| /api/:collection                    | A top-level collection                                     |
| /api/:collection/:id                | A specific resource of that collection                     |
| /api/:collection/:id/:subcollection | Sub-collection under the specific resource                 |

### Methods and related URLs

The basic HTTP Methods used for the API are GET, POST, PUT, PATCH and
DELETE.

| URL                         | Semantic                                          |
| --------------------------- | ------------------------------------------------- |
| GET /api/:collection        | Return all resources of the collection            |
| GET /api/:collection/:id    | Return the specific resource                      |
| POST /api/:collection       | Create a resource in the collection               |
| POST /api/:collection/:id   | Perform an Action on a resource in the collection |
| PUT /api/:collection/:id    | Update a specific resource                        |
| PATCH /api/:collection/:id  | Update a specific resource                        |
| DELETE /api/:collection/:id | Delete a specific resource                        |

`:collection` represents specific entities such as services, hosts, and
virtual machines.

### Updating Resources

Use the following methods to update attributes in a resource:

  - Update a resource via the `PUT` HTTP Method

  - Update a resource via a `POST` Method with an **edit** action.

  - Update a resource via the `PATCH` HTTP Method

While `PUT` is the common method, the `PATCH` mechanism gives better
control on which attribute to edit or add, and enables removal, which is
not available with the other two methods.

### Modifying Resource Attributes

`PUT /api/vms/42`

    {
      "name" : "A new VM name",
      "description" : "A Description for the new VM"
    }

`POST /api/vms/42`

    {
      "action" : "edit",
      "resource" : {
        "name" : "A new VM name",
        "description" : "A Description for the new VM"
      }
    }

`PATCH /api/vms/42`

    [
      { "action": "edit", "path": "name", "value": "A new VM name" },
      { "action": "add", "path": "description", "value": "A Description for the new VM" },
      { "action": "remove", "path": "policies/3/description" }
    ]

In the `PATCH` implementation, path either references local attributes
or attributes from a related resource in a subcollection.

### Return Codes

  - **200 OK** - The request has succeeded without errors, this code
    should be returned for example when retrieving a collection or a
    single resource.

  - **201 Created** - The request has been fulfilled and resulted in a
    **new resource being created**. The resource is available before
    this status code is returned. The response includes the HTTP body of
    the newly created resource.

  - **202 Accepted** - The request has been accepted for processing, but
    the processing has not been completed. Like, resource is not fully
    available yet. This status code is usually returned when the
    resource creation happens asynchronously. In this case the HTTP
    response includes a pointer to **monitor** or a **job** where the
    client can query to get the current status of the request and the
    estimate on when the request will be actually fulfilled.

  - **204 No Content** - The server has fulfilled the request but does
    not need to return an entity-body, and might want to return updated
    meta information. This HTTP response is commonly used for the
    `DELETE` requests, as the resource that was deleted does not exists
    anymore.

<!-- end list -->

  - **400 Bad Request** - The request could not be understood by the
    server due to malformed syntax. The client SHOULD NOT repeat the
    request without modifications. In REST API this status code should
    be returned to client when the client use the wrong combination of
    attributes, like expanding the non-existing collection, or using the
    pagination parameter incorrectly. Another use-case could be creating
    or performing actions on the resource, when the wrong JSON
    serialization of the resource or action is used.

  - **401 Unauthorized** - The request requires user authentication. The
    response MUST include a **Authenticate** header field containing a
    challenge applicable to the requested resource. If the request
    include **Authenticate** header, then this HTTP status code might
    indicate that the current user is **not authorized** to perform
    given action or to access given resource.

  - **403 Forbidden** - The server understood the request, but is
    refusing to fulfill it. Authorization will not help in this case.
    This HTTP status code might indicate that the action performed is
    not supported for this resource or collection.

  - **404 Not Found** - In this case, the server has not found anything
    that matches with the URL.

  - **415 Unsupported Media Type** - The server is refusing to service
    the request because the entity of the request is in a format not
    supported by the requested resource for the requested method. This
    error must be returned, when the client is explicitly asking for
    format other than JSON (application/json).

<!-- end list -->

  - **500 Internal Server Error** - The server encountered an unexpected
    condition which prevented it from fulfilling the request. This error
    code must be used when an exception is raised in the application and
    the exception has nothing to do with the client request.

### CRUD Examples

The following examples show the basic CRUD operations (Create, Read,
Update, Delete) using the REST API.

The commands below use basic authentication via the `--user
admin:smartvm` credentials argument. For multiple API calls, it is
recommended to access the ManageIQ REST API via token-based
authentication. See [Authentication](#_sect_authentication) for details.

**Show a Collection of Resources.**

Get a collection of services: **GET /api/services**

    curl --user admin:smartvm
        -i -X GET -H "Accept: application/json"
        https://hostname/api/services

**Return a Single Resource.**

Return a single service: **GET /api/services/:id**

    curl --user admin:smartvm
        -i -X GET -H "Accept: application/json"
        https://hostname/api/services/1

**Create a Resource.**

Create a new provider: **POST /api/providers**

    curl --user admin:smartvm
          -i -X POST -H "Accept: application/json"
          -d '{
                "type"      : "ManageIQ::Providers::Redhat::InfraManager",
                "name"      : "RHEVM Provider",
                "hostname"  : "rhevm.local.com",
                "ipaddress" : "192.168.5.1",
                "credentials" : {
                  "userid"   : "admin",
                  "password" : "12345"
                }
          }'
          https://hostname/api/providers

**Update a Resource.**

Update the name of a service: **PUT /api/services/:id**

    curl --user admin:smartvm
          -i -X PUT -H "Accept: application/json"
          -d '{ "name" : "updated service name" }'
          https://hostname/api/services/1

**Delete a Resource.**

Delete a service: **DELETE /api/services/:id**

    curl --user admin:smartvm
        -i -X DELETE -H "Accept: application/json"
        https://hostname/api/services/1

## Authentication

There are two methods of authentication for the ManageIQ REST API:

  - **Basic Authentication**: The user and password credentials are
    passed in with each HTTP request.

  - **Token based Authentication**: The client requests a token for the
    username/password credentials specified. Then the token is used in
    lieu of the username/password for each subsequent API call.

### Using Basic Authentication

The following example demonstrates how to use basic authentication:

    $ curl --user username:password
          -i -X GET -H "Accept: application/json"
          https://hostname/api/services/1013

Red Hat recommends token-based authentication for multiple REST API
calls.

### Using Authentication Tokens

  - Are associated with the user credential.

  - Provide the necessary identification for RBAC in subsequent REST
    calls.

  - Expire after a certain amount of time (10 minutes by default).

**Request.**

    $ curl --user username:password
            -i X GET -H "Accept: application/json"
            https://hostname/api/auth

**Response.**

    HTTP/1.1 200 OK
    Content-Type: application/json
    
    {
      "auth_token" : "af0245-238722-4d23db",
      "expires_on" : "2013-12-07T18:20:07Z"
    }

**Request using Token based authentication.**

    $ curl -i -X GET -H "Accept: application/json"
           -H "X-Auth-Token: af0245-238722-4d23db"
           https://hostname/api/services/1013

**Failed response due to invalid token.**

    HTTP/1.1 401 Unauthorized
    WWW-Authenticate: Basic realm="Application"
    ...

When a request fails due to an invalid token, the client must
re-authenticate with the user credentials to obtain a new Authentication
Token.

## JSON Specification

The API uses JSON throughout; the Content-Type for all requests and
responses is `application/json`.

As is general practice with REST, clients should not make assumptions
about the server’s URL space. Clients are expected to discover all URL’s
by navigating the API. To keep this document readable, we still mention
specific URL’s, generally in the form of an absolute path. Clients
should not use these, or assume that the actual URL structure follows
these examples, and instead use discovered URL’s. Any client should
start its discovery with the API entry point, here denoted with `/api`.

### Basic types

The following are basic data types and type combinators that are used
throughout:

| Name           | Explanation                                                                                                       | Example serialization                                                                                                   |
| -------------- | ----------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **Integer**    | Integer value                                                                                                     | { "id" : 10 }                                                                                                           |
| **String**     | JSON string                                                                                                       | { "state" : "running" }                                                                                                 |
| **URL**        | Absolute URL                                                                                                      | { "href" : "http://SERVER/vms/1/start" }                                                                                |
| **Timestamp**  | Timestamp in ISO8601 format                                                                                       | { "created" : "2013-12-05T08:15:30Z" }                                                                                  |
| **Array\[T\]** | Array where each entry has type T                                                                                 | { "vms" : \[ { "id" : 1 }, { "id" : 2 }\] }                                                                             |
| **Ref\[T\]**   | A reference to a T, used to model relations, the T is a valid Resource identifier                                 | { "vm" : { "href" : URL } }                                                                                             |
| **Collection** | Array\[T\] where T represents a Ref\[T\], this might allow actions to be executed on all members as a single unit | { "vms" : { "count" : 2, "resources" : \[ { "href" : URL}, { "href" : URL } \], "actions" : \[\] }                      |
| **Struct**     | A structure with sub-attributes                                                                                   | "power\_state": {"state" : "ON", "last\_boot\_time" : "2013-05-29T15:28Z", "state\_change\_time" : "2013-05-29T15:28Z"} |

### Common Attributes and Actions

The following describes attributes and actions that are shared by all
resources and collections defined in this API.

| Attribute | Type      | Description                                       |
| --------- | --------- | ------------------------------------------------- |
| id        | Integer   | An integer identifier for the referenced resource |
| href      | Ref(self) | A unique self reference                           |
| name      | String    | A human name of the resource                      |

Attributes

    {
      "href" : "https://hostname/api/resources/1",
      "id" : 1,
      "name" : "first_resource"
    }

| Action | HTTP method    | Description                           |
| ------ | -------------- | ------------------------------------- |
| create | POST           | Create new resource in the collection |
| edit   | PUT/PATCH/POST | Edit attributes in resource           |
| delete | DELETE         | Delete resource                       |

Actions

<div class="note">

The availability of these common actions depends on the role and
permissions that the current API user has for a particular resource.

</div>

### Collections

Resources can be grouped into collections. Each collection is unordered,
and is homogeneous so that it contains only one type of resource.
Resources can also exist outside any collection; these resources are
referred to as singleton resources. Collections are themselves resources
as well.

Collections can exist globally, at the top level of an API, and can also
be contained inside a single resource. The latter are referred to as
sub-collections. Sub-collections are usually used to express a
relationship where one resource is contained within another.

Collections are serialized in JSON in the following way:

    {
      "name" : "String",
      "count": String,
      "subcount": String,
      "resources": [ ... ],
      "actions": [ ... ]
    }

  - The `count` attribute in a collection always denotes the total
    number of items in the collection, not the number of items returned.

  - The `subcount` attribute in a collection depicts the number of items
    returned.

  - The `resources` attribute is an Array\[T\], where T might be a list
    of references to the T or, if expanded, a list of resources with all
    attributes.

  - The `actions` attribute contains an Array of actions that can be
    performed against the collection resources.

### Action Specification

The representation of each resource will only contain an action and its
URL if the current user is presently allowed to perform that action
against that resource. Actions will be contained in the `actions`
attribute of a resource; that attribute contains an array of action
definition, where each action definition has a rel, method and a href
attribute.

  - `name` attribute contains the action name

  - `method` attribute states the HTTP method that must be used in a
    client HTTP request in order to perform the given action (eg. GET,
    POST, PUT, DELETE)

  - `href` attribute contains the absolute URL that the HTTP request
    should be performed against

  - `form` is an optional attribute that references a JSON document
    which describes the resource attributes that can be provided in the
    message body when performing this action. This description indicates
    which of those attributes are mandatory and which are optional.

**Collection actions.**

The actions performed against a collection of resources, are in most
cases batch operations against multiple resources. The action request
must include an HTTP body with the action name and the list of resource
representations that the action will be performed against.

The resource representation might include the resource attributes as
they can change the way how the action is actually performed. In the
example below, the first resource is started with `enable_ipmi`
attribute, but the second resource omits this attribute which means the
default value will be used.

Sample JSON request body for collection action:

`POST /api/vms`

    {
      "action": "start",
      "resources" : [
        { "href" : "https://hostname/api/vms/1", "enable_ipmi" : "enabled", "initial_state" : "started" },
        { "href" : "https://hostname/api/vms/2" }
      ]
    }

Actions in collection:

    {
      "name" : "String",
      "count": String,
      "subcount": String,
      "resources": [ ... ],
      "actions": [
        {
        "name"   : "shutdown",
        "method" : "post",
        "href"   : "URL"
        },
        {
        "name"   : "restart",
        "method" : "post",
        "href"   : "URL"
        },
        {
        "name"   : "poweron",
        "method" : "post",
        "href"   : "URL"
        },
        {
        "name"   : "poweroff",
        "method" : "post",
        "href"   : "URL"
        },
        {
        "name"   : "suspend",
        "method" : "post",
        "href"   : "URL"
        },
        {
        "name"    : "edit",
        "method" : "post",
        "form"   : { "href" : "https://hostname/api/vms?form_for=add" },
        "href"   : "URL"
        },
        {
        "name"   : "destroy",
        "method" : "delete",
        "href"   : "URL"
        }
      ]
    }

**Resource actions.**

An action performed against a given resource is always described in the
body of the HTTP request. The HTTP body could contain a list of resource
attributes that dictate how the state of the receiving resource is to be
changed once the action is performed. At minimum the JSON document in
the message body must contain the name of the action to be performed.

In cases where no attributes are required to perform an action the HTTP
body will contain an empty JSON document, in which case default values
will be assigned to the corresponding attributes.

Sample JSON request body for resource action:

`POST /api/vms/123`

    {
      "action"   : "start",
      "resource" : { "enable_ipmi" : "enabled" }
    }

`POST /api/vms/321`

    {
      "action"   : "start",
      "resource" : {}
    }

Actions in a resource:

    {
      "href"  : "Ref(self)",
      "id"    : Integer,
      "name"  : "resource human name",
      "actions" : [
        {
        "name"   : "edit",
        "method" : "post",
        "form"   : { "href" : "https://hostname/api/vms?form_for=edit" },
        "href"   : "URL"
        }
      ]
    }

### Forms

**Getting a Form.**

The URL to fetch a form is part of the `action` serialization. In a case
when no form is referenced, the action does not require any attributes
to be performed.

Resource including an action with a Form:

    {
      "href" : "Ref(self)",
      "id" : Integer,
      "name" : "resource human name",
      "actions": [
        {
        "name    : "edit",
        "method" : "post",
        "form"   : { "href" : "https://hostname/vms?form_for=edit" },
        "href"   : "URL"
        }
      ]
    }

    GET /api/vms?form_for=edit HTTP/1.1

Example of a Form:

    {
      "required" : [ "name", "host" ],
      "optional" : [ "description" ]
      "internal" : [ "power_state", "created_on"]
    }

The following describes the semantics of the attribute identifiers:

  - **required** - These attributes must be specified for the action to
    be carried out.

  - **optional** - These are optional attributes, which may be specified
    and processed by the action. These may be shown in a UI but not
    enforced.

  - **internal** - It is not necessary to define these, but they are
    required for a UI form to show and extended a form with more
    attributes than the required and optional identifiers permit. This
    identifier shows what attributes are system managed and not
    modifiable by the REST client.

## Query Specification

This specification identifies the controls available when querying
collections.

### Control Attributes

The controls are specified in the GET URL as attribute value pairs as
follows:

    GET /api/resources?ctl1=val1&ctl2=val2

| Category | Attribute                           | Semantics                                                                                                                                        |
| -------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Paging   |                                     |                                                                                                                                                  |
|          | offset                              | 0-based offset of first item to return                                                                                                           |
|          | limit                               | number of items to return. If 0 is specified then the remaining items are returned                                                               |
| Scope    |                                     |                                                                                                                                                  |
|          | filter\[\]                          | One or more filters to search on. See [Filtering](#filtering) below.                                                                             |
|          | attributes=atr1,atr2,…​             | Which attributes in addition to id and href to return. If not specified or *all* (default is attributes=*all*), then all attributes are returned |
|          | expand=resources                    | To expand the resources returned in the collection and not just the href. See [Expanding Collection](#expanding_collections1) below              |
| Sorting  |                                     |                                                                                                                                                  |
|          | sort\_by=atr1,atr2,…​               | By which attribute(s) to sort the result by                                                                                                      |
|          | sort\_order=ascending or descending | Order of the sort                                                                                                                                |

  - The `count` attribute in a collection always denotes the total
    number of items in the collection, not the number of items returned.

  - The `subcount` attribute in a collection denotes the number of items
    from the collection that were returned, for example as the result of
    a paged request.

### Filtering

`GET` requests against collections support the following query
parameters to enable filtering:

  - `filter[]`: The SQL filter to use for querying the collection.

<!-- end list -->

    GET /api/resources?filter[]=name='myservice%25'

The query above requests resources that begin with the name `myservice`.
String values must be contained in single or double quotes. Special
characters within the quotes must be URL encoded. In the example above,
the database wildcard character, `%`, is encoded as `%25`.

### Expanding Collections

While in the JSON serialization example the description says that the
resource might be a list of references to the resource, using the
`expand` parameter returns a full JSON serialization of the resource
instead:

**GET** `/api/vms`

    {
      "name" : "vms"
      "count": 2,
      "subcount": 2,
      "resources": [
        { "href" : "https://hostname/api/vms/1" },
        { "href" : "https://hostname/api/vms/2" }
      ],
      "actions": []
    }

**GET** `/api/vms?expand=resources`

    {
      "name" : "vms"
      "count": 2,
      "subcount": 2,
      "resources": [
        {
          "href" : "https://hostname/api/vms/1",
          "id" : 1,
          "name" : "My First VM",
          ...
        },
        {
          "href" : "https://hostname/api/vms/2",
          "id" : 2,
          "name" : "My Second VM",
          ...
        }
      ],
      "actions": []
    }

# Reference Guide

## Authentication

| Type                         | Mechanism                                       |
| ---------------------------- | ----------------------------------------------- |
| Basic Authentication         | Basic HTTP Authorization with user and password |
| Token Based Authentication   |                                                 |
| \- Acquiring Token           | /api/auth with Basic Authentication             |
| \- Authenticating with Token | X-Auth-Token Header                             |

## HTTP Headers

| Header        | Value                                |
| ------------- | ------------------------------------ |
| Authorization | Basic base64\_encoded(user:password) |
| X-Auth-Token  | Token provided by /api/auth          |
| Accept        | application/json                     |
| Content-Type  | application/json                     |

## Listing and Querying Collections and Sub-Collections

| Feature                       | Path                                          |
| ----------------------------- | --------------------------------------------- |
| Listing Available Collections | /api                                          |
| Listing Collections           | /api/\<collection\>                           |
| Listing Sub-Collections       | /api/\<collection\>/\<id\>/\<sub-collection\> |

| Querying Capability  | Query Parameters                                                  |
| -------------------- | ----------------------------------------------------------------- |
| Paging               | offset, limit                                                     |
| Sorting              | sort\_by=attr, sort\_order=asc|desc                               |
| Filtering            | filter\[\]="…​"                                                   |
| Querying by Tag      | i.e. by\_tag=/department/finance                                  |
| Expanding Results    | expand=\<what\>, i.e. expand=resources,tags,service\_templates,…​ |
| Selecting Attributes | attributes=\<attr1\>,\<attr2\>,…​ i.e. attributes=id,name,type,…​ |
|                      | Attributes can be:                                                |
|                      | Database columns                                                  |
|                      | Virtual attributes                                                |
|                      | Relationships                                                     |

## Collection Queries

| Collection          | URL                       |
| ------------------- | ------------------------- |
| Automation Requests | /api/automation\_requests |
| Availability Zones  | /api/availability\_zones  |
| Cloud Networks      | /api/cloud\_networks      |
| Cloud Subnets       | /api/cloud\_subnets       |
| Clusters            | /api/clusters             |
| Conditions          | /api/conditions           |
| Container Images    | /api/container\_images/   |
| Datastores          | /api/data\_stores         |
| Events              | /api/events               |
| Flavors             | /api/flavors              |
| Groups              | /api/groups               |
| Hosts               | /api/hosts                |
| Network Routers     | /api/network\_routers     |
| Policies            | /api/policies             |
| Actions             | /api/policy\_actions      |
| Policy Profiles     | /api/policy\_profiles     |
| Providers           | /api/providers            |
| Provision Requests  | /api/provision\_requests  |
| Request Tasks       | /api/request\_tasks       |
| Requests            | /api/requests             |
| Resource Pools      | /api/resource\_pools      |
| Roles               | /api/roles                |
| Security Groups     | /api/security\_groups     |
| EVM Servers         | /api/servers              |
| Service Catalogs    | /api/service\_catalogs    |
| Service Requests    | /api/service\_requests    |
| Service Templates   | /api/service\_templates   |
| Services            | /api/services             |
| Tags                | /api/tags                 |
| Tasks               | /api/tasks                |
| Templates           | /api/templates            |
| Users               | /api/users                |
| Vms                 | /api/vms                  |
| Zones               | /api/zones                |

For example queries, see "Queries".

## Sub-Collection Queries

| Sub-Collection                                         | URL                                                   |
| ------------------------------------------------------ | ----------------------------------------------------- |
| Tagging                                                | /api/\<collection\>/:id/tags                          |
| Policies                                               | /api/\<collection\>/:id/policies                      |
| Policy Profiles                                        | /api/\<collection\>/:id/policy\_profiles              |
|                                                        |                                                       |
| Service Requests                                       | /api/service\_templates/:id/service\_requests         |
| Request Tasks                                          |                                                       |
|                                                        | /api/service\_requests/:id/request\_tasks             |
|                                                        | /api/automation\_requests/:id/request\_tasks          |
|                                                        | /api/provision\_requests/:id/request\_tasks           |
| Request Tasks can also be accessed via the tasks alias |                                                       |
|                                                        | /api/service\_requests/:id/tasks                      |
|                                                        | /api/automation\_requests/:id/tasks                   |
|                                                        | /api/provision\_requests/:id/tasks                    |
| Infrastructure Providers                               |                                                       |
|                                                        | /api/providers/:id/lans                               |
|                                                        | /api/hosts/:id/lans                                   |
|                                                        | /api/providers/:id/networks                           |
|                                                        | /api/providers/:id/folders (also returns Datacenters) |

## Available Actions

| Action                                      | Method | URL                                          |
| ------------------------------------------- | ------ | -------------------------------------------- |
| Add Service Catalog                         | POST   | /api/service\_catalogs                       |
| Add Service Catalogs                        | POST   | /api/service\_catalogs                       |
| Edit Service Catalog                        | POST   | /api/service\_catalogs/id                    |
| Edit Service Catalogs                       | POST   | /api/service\_catalogs                       |
| Automation Request                          | POST   | /api/automation\_requests                    |
| Automation Requests                         | POST   | /api/automation\_requests                    |
| Edit Service                                | POST   | /api/services/id                             |
| Edit Service via PUT                        | PUT    | /api/services/id                             |
| Edit Service via PATCH                      | PATCH  | /api/services/id                             |
| Edit Services                               | POST   | /api/services/                               |
| Assign Tags to a Service                    | POST   | /api/services/id/tags                        |
| Assign a Tag by Name to a Service           | POST   | /api/services/id/tags                        |
| Assign a Tag by Name to a Service           | POST   | /api/services/id/tags                        |
| Unassign Tags from Service                  | POST   | /api/services/id/tags                        |
| Assign Tags to Cloud Networks               | POST   | /api/cloud\_networks/id/tags                 |
| Assign Tags to Cloud Subnets                | POST   | /api/cloud\_subnets/id/tags                  |
| Assign Tags to Flavors                      | POST   | /api/flavors/id/tags                         |
| Assign Tags to Availability Zones           | POST   | /api/availability\_zones/id/tags             |
| Assign Tags to Network Routers              | POST   | /api/network\_routers/id/tags                |
| Assign Tags to Security Groups              | POST   | /api/security\_groups/id/tags                |
| Retire Service Now                          | POST   | /api/services/id                             |
| Retire Service in Future                    | POST   | /api/services/id                             |
| Retire Services                             | POST   | /api/services                                |
| Delete Service                              | DELETE | /api/services/id                             |
| Delete Services                             | POST   | /api/services                                |
| Edit Service Template                       | POST   | /api/service\_templates/id                   |
| Edit Service Templates                      | POST   | /api/service\_templates                      |
| Assign Tags to Service Template             | POST   | /api/service\_templates/id/tags              |
| Unassign Tags from Service Template         | POST   | /api/service\_templates/id/tags              |
| Delete Service Template                     | DELETE | /api/service\_templates/id                   |
| Delete Service Templates                    | POST   | /api/service\_templates                      |
| Assign Service Templates                    | POST   | /api/service\_catalogs/id/service\_templates |
| Unassign Service Templates                  | POST   | /api/service\_catalogs/id/service\_templates |
| Order Service                               | POST   | /api/service\_catalogs/id/service\_templates |
| Order Services                              | POST   | /api/service\_catalogs/id/service\_templates |
| Delete Service Catalog                      | DELETE | /api/service\_catalogs/id                    |
| Delete Service Catalogs                     | POST   | /api/service\_catalogs                       |
| Provision Request                           | POST   | /api/provision\_requests                     |
| Provision Requests                          | POST   | /api/provision\_requests                     |
| Create a Provider                           | POST   | /api/providers                               |
| Create a Provider with Compound Credentials | POST   | /api/providers                               |
| Edit a Provider                             | POST   | /api/providers                               |
| Update a Provider                           | POST   | /api/providers                               |
| Delete a Provider                           | POST   | /api/providers                               |
| Delete Multiple Providers                   | POST   | /api/providers                               |
| Refresh a Provider                          | POST   | /api/providers                               |
| Scan a VM                                   | POST   | /api/vms                                     |
| Set Owner of a VM                           | POST   | /api/vms                                     |
| Add a Lifecycle Event to a VM               | POST   | /api/vms                                     |
| Add an Event to a VM                        | POST   | /api/vms                                     |
| Start a VM                                  | POST   | /api/vms                                     |
| Stop a VM                                   | POST   | /api/vms                                     |
| Suspend a VM                                | POST   | /api/vms                                     |
| Delete VMs                                  | DELETE | /api/vms                                     |
| Scan a Container                            | POST   | /api/container\_images                       |

## Provisioning Request Attributes

  - [Request Attribute Groups](#provision-requests-attribute-groups)

  - [Requester Attributes](#requester-attributes)

  - [Custom Attributes](#custom-attributes)

  - [Environment Attributes](#environment-attributes)

  - [Service Catalog Attributes](#service-catalog-attributes)

  - [Schedule Attributes](#schedule-attributes)

  - [Network Attributes](#network-attributes)

  - [Hardware Attributes](#hardware-attributes)

### Provisioning Request Attribute Groups

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute Group</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>version</p></td>
<td><p>string</p></td>
<td><p>Interface version. Defaults to 1.1</p></td>
</tr>
<tr class="even">
<td><p>template_fields</p></td>
<td><p>hash</p></td>
<td><p>Fields used to find the template virtual machine. Provide any or all fields. Supply a guid or ems_guid to protect against matching same-named templates on different Providers within the appliance.</p>
<p>Supported fields are: name=[VM Template Name] Example: template_1 guid=[guid value from vms resource] ems_guid=[uid_ems value from vms resource]</p></td>
</tr>
<tr class="odd">
<td><p>vm_fields</p></td>
<td><p>hash</p></td>
<td><p>Allows for setting properties on the Service Catalog, Hardware, Network, Customize, and Schedule tabs in the Provisioning dialog.</p></td>
</tr>
<tr class="even">
<td><p>requester</p></td>
<td><p>hash</p></td>
<td><p>Allows for the setting of properties on the Requester tab in the Provisioning dialog.</p></td>
</tr>
<tr class="odd">
<td><p>tags</p></td>
<td><p>hash</p></td>
<td><p>Tags to apply to newly created virtual machine.</p>
<p>Example: network_location=Internal cc=001</p></td>
</tr>
<tr class="even">
<td><p>additional_values</p></td>
<td><p>hash</p></td>
<td><p>Additional values are name-value pairs stored with a provision request, but not used by the core provisioning code. These values are usually referenced from automate methods for custom processing.</p>
<p>Example: Store a request_id from an external system so the system can be notified during the provisioning process.</p></td>
</tr>
<tr class="odd">
<td><p>ems_custom_attributes</p></td>
<td><p>hash</p></td>
<td><p>Custom attributes applied to the virtual machine through the Provider as part of provisioning.</p></td>
</tr>
<tr class="even">
<td><p>miq_custom_attributes</p></td>
<td><p>hash</p></td>
<td><p>Custom attributes applied to the virtual machine and stored in the database as part of provisioning.</p></td>
</tr>
</tbody>
</table>

### Service Catalog Attributes

These attributes are used in the `vm_fields` attribute group:

| Attribute       | Type    | Description                                          | Default |
| --------------- | ------- | ---------------------------------------------------- | ------- |
| number\_of\_vms | integer | Number of virtual machines - maximum 50              | 1       |
| vm\_description | string  | Virtual machine description - maximum 100 characters |         |
| vm\_prefix      | string  | Virtual machine name prefix or suffix                |         |
| src\_vm\_id     | integer | Name                                                 |         |
| vm\_name        | string  | Virtual machine name                                 |         |
| pxe\_image\_id  | string  | Image                                                |         |
| pxe\_server\_id | integer | Server                                               |         |
| host\_name      | string  | Host name                                            |         |
| provision\_type | string  | Provision type                                       | vmware  |
| linked\_clone   | boolean | Linked clone                                         | false   |
| snapshot        | string  | Snapshot                                             |         |
| vm\_filter      | integer | Filter                                               |         |

### Hardware Attributes

These attributes are used in the `vm_fields` attribute group:

| Attribute           | Type    | Description       | Values                 | Default   |
| ------------------- | ------- | ----------------- | ---------------------- | --------- |
| disk\_format        | string  | Disk format       | thick, thin, unchanged | unchanged |
| cpu\_limit          | integer | CPU (MHz)         |                        |           |
| memory\_limit       | integer | Memory (MB)       |                        |           |
| number\_of\_sockets | integer | Number of sockets | 1, 2, 4, 8             | 1         |
| cores\_per\_socket  | integer | Cores per socket  | 1, 2, 4, 8             | 1         |
| cpu\_reserve        | integer | CPU (MHz)         |                        |           |
| vm\_memory          | string  | Memory (MB)       | 1024, 2048, 4096       | 1024      |
| memory\_reserve     | integer | Memory (MB)       |                        |           |
| network\_adapters   | integer | Network adapters  | 1, 2, 3, 4             | 1         |

### Network Attributes

These attributes are used in the `vm_fields` attribute group:

| Attribute    | Type   | Description |
| ------------ | ------ | ----------- |
| vlan         | string | vLAN        |
| mac\_address | string | MAC address |

### Custom Attributes

These attributes are used in the `vm_fields` attribute group:

| Attribute                              | Type    | Description                                                                         | Values             | Default   |
| -------------------------------------- | ------- | ----------------------------------------------------------------------------------- | ------------------ | --------- |
| dns\_servers                           | string  | DNS server list                                                                     |                    |           |
| sysprep\_organization                  | string  | Organization                                                                        |                    |           |
| sysprep\_password                      | string  | New administrator password                                                          |                    |           |
| sysprep\_custom\_spec                  | string  | Name (Note: This is not supported when being passed by VMware through an API call.) |                    |           |
| sysprep\_server\_license\_mode         | string  | Identification                                                                      | perServer, perSeat |           |
| ldap\_ous                              | string  | LDAP group                                                                          |                    |           |
| sysprep\_timezone                      | string  | Timezone                                                                            |                    |           |
| dns\_suffixes                          | string  | DNS suffix list                                                                     |                    |           |
| sysprep\_product\_id                   | string  | ProductID                                                                           |                    |           |
| sysprep\_identification                | string  | Identification                                                                      | domain, workgroup  |           |
| sysprep\_per\_server\_max\_connections | string  | Maximum connections                                                                 |                    | 5         |
| sysprep\_computer\_name                | string  | Computer name                                                                       |                    |           |
| sysprep\_workgroup\_name               | string  | Workgroup name                                                                      |                    | WORKGROUP |
| sysprep\_spec\_override                | boolean | Override specification                                                              |                    | false     |
| addr\_mode                             | string  | Address mode                                                                        | static, dhcp       | dhcp      |
| linux\_host\_name                      | string  | Computer name                                                                       |                    |           |
| sysprep\_domain\_admin                 | string  | Domain admin                                                                        |                    |           |
| sysprep\_change\_sid                   | boolean | Change SID                                                                          |                    | true      |
| sysprep\_domain\_name                  | string  | Domain name                                                                         |                    |           |
| sysprep\_upload\_file                  | string  | Upload                                                                              |                    |           |
| gateway                                | string  | Gateway                                                                             |                    |           |
| ip\_addr                               | string  | IP address                                                                          |                    |           |
| linux\_domain\_name                    | string  | Domain name                                                                         |                    |           |
| sysprep\_domain\_password              | string  | Domain password                                                                     |                    |           |
| sysprep\_auto\_logon                   | boolean | Auto Logon                                                                          |                    | true      |
| sysprep\_enabled                       | string  | Customize                                                                           |                    | disabled  |
| sysprep\_delete\_accounts              | boolean | Delete accounts                                                                     |                    | false     |
| sysprep\_upload\_text                  | string  | Sysprep text                                                                        |                    |           |
| wins\_servers                          | string  | WINS server list                                                                    |                    |           |
| subnet\_mask                           | string  | Subnet mask                                                                         |                    |           |
| sysprep\_full\_name                    | string  | Full name                                                                           |                    |           |
| sysprep\_auto\_logon\_count            | integer | Auto logon count                                                                    | 1, 2, 3            | 1         |
| customization\_template\_id            | integer | Script name                                                                         |                    |           |
| root\_password                         | string  | Root password                                                                       |                    |           |
| hostname                               | string  | Host name                                                                           |                    |           |
| customization\_template\_script        | string  | Script text                                                                         |                    |           |

### Schedule Attributes

These attributes are used in the `vm_fields` attribute group:

| Attribute        | Type    | Description                              | Values                                        | Default     |
| ---------------- | ------- | ---------------------------------------- | --------------------------------------------- | ----------- |
| schedule\_type   | string  | When to provision                        | schedule, immediately (*On Approval*)         | immediately |
| vm\_auto\_start  | boolean | Power on virtual machines after creation |                                               | true        |
| schedule\_time   | time    | Time to provision on                     |                                               |             |
| retirement       | integer | Time until retirement                    | 0 (*Indefinite*), 1.month, 3.months, 6.months | 0           |
| retirement\_warn | integer | Retirement warning                       | 1.week, 2.weeks, 30.days                      | 1.week      |

### Requester Attributes

These attributes are used in the **requester** attribute group:

| Attribute             | Type   | Description                 |
| --------------------- | ------ | --------------------------- |
| owner\_phone          | string | Phone                       |
| owner\_country        | string | Country/Region              |
| owner\_phone\_mobile  | string | Mobile phone                |
| owner\_title          | string | Title                       |
| owner\_first\_name    | string | First name                  |
| owner\_manager        | string | Manager name                |
| owner\_address        | string | Address                     |
| owner\_company        | string | Company                     |
| owner\_last\_name     | string | Last name                   |
| owner\_manager\_email | string | Manager e-mail address      |
| owner\_city           | string | City                        |
| owner\_department     | string | Department                  |
| owner\_load\_ldap     | button | Look up LDAP e-mail address |
| owner\_manager\_phone | string | Manager phone               |
| owner\_state          | string | State                       |
| owner\_office         | string | Office                      |
| owner\_zip            | string | Zip code                    |
| owner\_email          | string | E-Mail                      |
| request\_notes        | string | Notes                       |

### Environment Attributes

These attributes cannot be passed directly. To use these attributes,
provide **additional\_values** and allow customization methods to use
these attributes, then modify the request accordingly.

| Attribute                           | Type    | Description          | Values    | Default                                                                                                   |
| ----------------------------------- | ------- | -------------------- | --------- | --------------------------------------------------------------------------------------------------------- |
| new\_datastore\_grow\_increment     | integer | Grow increment (GB)  |           |                                                                                                           |
| new\_datastore\_create              | boolean | Create datastore     |           | false                                                                                                     |
| placement\_cluster\_name            | integer | Name                 |           |                                                                                                           |
| new\_datastore\_aggregate           | string  | Aggregate            |           |                                                                                                           |
| new\_datastore\_max\_size           | integer | Max size (GB)        |           |                                                                                                           |
| new\_datastore\_storage\_controller | string  | Controller           |           |                                                                                                           |
| cluster\_filter                     | integer | Filter               |           |                                                                                                           |
| host\_filter                        | integer | Filter               |           |                                                                                                           |
| ds\_filter                          | integer | Filter               |           |                                                                                                           |
| new\_datastore\_volume              | string  | Volume               |           |                                                                                                           |
| placement\_host\_name               | integer | Name                 |           |                                                                                                           |
| placement\_ds\_name                 | integer | Name                 |           |                                                                                                           |
| new\_datastore\_fs\_type            | string  | FS Type              | NFS, VMFS | NFS                                                                                                       |
| rp\_filter                          | integer | Filter               |           |                                                                                                           |
| new\_datastore\_thin\_provision     | string  | Thin provision       |           |                                                                                                           |
| placement\_auto                     | boolean | Choose automatically |           | false (**NOTE**: placement\_auto defaults to `true` for requests made from the API or ManageIQ Automate.) |
| new\_datastore\_size                | integer | Size (GB)            |           |                                                                                                           |
| new\_datastore\_autogrow            | string  | Autogrow             |           | false                                                                                                     |
| placement\_folder\_name             | integer | Name                 |           |                                                                                                           |
| new\_datastore\_name                | string  | Name                 |           |                                                                                                           |
| placement\_rp\_name                 | integer | Name                 |           |                                                                                                           |
| placement\_dc\_name                 | integer | Name                 |           |                                                                                                           |

# Examples

This section provides a collection of examples of using the REST API to
interact with resources in a ManageIQ environment.

## General Queries

This section introduces a number of general examples of how to use the
REST API to query resources, and return information about resources and
events.

### Queries

Query all virtual machines:

    GET /api/vms

Query a specific virtual machine:

    GET /api/vms/1386

Query all virtual machines, but return only the name and vendor:

    GET /api/vms?expand=resources&attributes=name,vendor

Query all virtual machines named sample\*, and return the name and
vendor:

    GET /api/vms?expand=resources&attributes=name,vendor&filter[]="name='sample%'"

Query all virtual machines, but only return the first 500 results:

    GET /api/vms?offset=0&limit=500

Query all virtual machines, but return the second 500 results:

    GET /api/vms?offset=500&limit=500

Query the first 1000 virtual machines named test\*, get the name,
vendor, and guid, and sort by name in ascending order:

    GET /api/vms?offset=0&limit=1000&filter[]="name='test%'"&expand=resources&attributes=name,vendor,guid&sort_by=name&sort_order=asc

Query services tagged for the finance department:

    GET /api/services?by_tag=/department/finance

Get the details of tags for the first service:

    GET /api/services/1/tags?expand=resources

Get the details of the first service catalog and related details on the
assigned service templates:

    GET /api/service_catalogs/1?expand=service_templates

    GET /api/service_templates/25/service_requests?expand=resources,request_tasks

Get a specific provision request with expanded details on the associated
provision request tasks:

    GET /api/provision_requests/120?expand=tasks

Query infrastructure provider information:

    GET /api/providers/120?expand=resources,lans,networks,folders

### Paging Queries

This series of requests shows paging queries and the expected responses
for each subsequent page.

#### Request:

    GET /api/vms?offset=0&limit=500
        &sort_order=asc&sort_by=name
        &expand=resources&attributes=name

#### Response:

``` json
{
  "name": "vms",
  "count": 1912,
  "subcount": 500,
  "resources": [
    {
      "href": "https://hostname/api/vms/176",
      "id": 176,
      "name": "53 Zone1"
    },
    ...
    {
      "href": "https://hostname/api/vms/1575",
      "id": 1575,
      "name": "VmEmpty-3de98f0f-c6f3-4f8b-a932-554713a61067"
    }
  ],
  "actions": [
  ]
}
```

#### Request:

    GET /api/vms?offset=500&limit=500
        &sort_order=asc&sort_by=name
        &expand=resources&attributes=name

#### Response:

``` json
{
  "name": "vms",
  "count": 1912,
  "subcount": 500,
  "resources": [
    {
      "href": "https://hostname/api/vms/1574",
      "id": 1574,
      "name": "VmEmpty-3e13ff43-6907-4a22-8f95-58aeb1bffa0b"
    },
    ...
    {
      "href": "https://hostname/api/vms/1076",
      "id": 1076,
      "name": "VmEmpty-9a885181-7771-4f91-9805-245c7606d833"
    }
  ],
  "actions": [
  ]
}
```

#### Request:

    GET /api/vms?offset=1000&limit=500
        &sort_order=asc&sort_by=name
        &expand=resources&attributes=name

#### Response:

``` json
{
  "name": "vms",
  "count": 1912,
  "subcount": 500,
  "resources": [
    {
      "href": "https://hostname/api/vms/1074",
      "id": 1074,
      "name": "VmEmpty-9ab9e101-92b0-4b6b-864e-e196538da8a8"
    },
    ...
    {
      "href": "https://hostname/api/vms/575",
      "id": 575,
      "name": "VmEmpty-f251f135-01c8-4d44-b8e1-37b30844a9dd"
    }
  ],
  "actions": [
  ]
}
```

#### Request:

    GET /api/vms?offset=1500&limit=500
        &sort_order=asc&sort_by=name
        &expand=resources&attributes=name

#### Response:

``` json
{
  "name": "vms",
  "count": 1912,
  "subcount": 412,
  "resources": [
    {
      "href": "https://hostname/api/vms/574",
      "id": 574,
      "name": "VmEmpty-f28912f3-b096-487f-9763-97b39b67364b"
    },
    ...
    {
      "href": "https://hostname/api/vms/1907",
      "id": 1907,
      "name": "yy_vm"
    }
  ],
  "actions": [
  ]
}
```

<div class="note">

In this last request, the **subcount** was less than the requested page
size, thus denoting the last page of data being returned.

</div>

### Querying a Delete Task

#### Request:

    GET /api/tasks/625

#### Response:

``` json
{
  "href": "https://hostname/api/tasks/625",
  "id": 625,
  "name": "Provider id:106 name:'rhevm102' deleting",
  "state": "Finished",
  "status": "Ok",
  "message": "Task completed successfully",
  "userid": "admin",
  "created_on": "2015-05-06T14:02:26Z",
  "updated_on": "2015-05-06T14:02:32Z"
}
```

## Service Catalogs

This section provides examples of how to interact with service catalogs.

### Adding a Sample Service Catalog

#### Request:

    POST /api/service_catalogs

``` json
{
   "action" : "create",
   "resource" : {
        "name" : "Sample Service Catalog",
        "description" : "Description of Sample Service Catalog",
        "service_templates" : [
          { "href" : "https://hostname/api/service_templates/3" },
          { "href" : "https://hostname/api/service_templates/4" }
        ]
   }
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 7,
      "name": "Sample Service Catalog",
      "description": "Description of Sample Service Catalog"
    }
  ]
}
```

### Adding Multiple Service Catalogs

#### Request:

    POST /api/service_catalogs

``` json
{
   "action" : "create",
   "resources" : [
      {
        "name" : "First Sample Service Catalog",
        "description" : "Description of First Sample Service Catalog",
        "service_templates" : [
          { "href" : "https://hostname/api/service_templates/1" },
          { "href" : "https://hostname/api/service_templates/2" }
        ]
      },
      {
        "name" : "Second Sample Service Catalog",
        "description" : "Description of Second Sample Service Catalog",
        "service_templates" : [
          { "href" : "https://hostname/api/service_templates/3" },
          { "href" : "https://hostname/api/service_templates/4" }
        ]
      },
      {
        "name" : "Third Sample Service Catalog",
        "description" : "Description of Third Sample Service Catalog",
        "service_templates" : [
          { "href" : "https://hostname/api/service_templates/5" },
          { "href" : "https://hostname/api/service_templates/6" }
        ]
      }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 8,
      "name": "First Sample Service Catalog",
      "description": "Description of First Sample Service Catalog"
    },
    {
      "id": 9,
      "name": "Second Sample Service Catalog",
      "description": "Description of Second Sample Service Catalog"
    },
    {
      "id": 10,
      "name": "Third Sample Service Catalog",
      "description": "Description of Third Sample Service Catalog"
    }
  ]
}
```

### Assigning Service Templates to Service Catalogs

#### Request:

    POST /api/service_catalogs/6/service_templates

``` json
{
  "action" : "assign",
  "resources" : [
    { "href" : "https://hostname/api/service_templates/5" },
    { "href" : "https://hostname/api/service_templates/1" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Service Template id:5 name:'template5'",
      "service_template_id": 5,
      "service_template_href": "https://hostname/api/service_templates/5",
      "href": "https://hostname/api/service_catalogs/6"
    },
    {
      "success": false,
      "message": "Service Template 1 is currently assigned to Service Catalog 3",
      "service_template_id": 1,
      "service_template_href": "https://hostname/api/service_templates/1",
      "href": "https://hostname/api/service_catalogs/6"
    }
  ]
}
```

### Editing a Service Catalog

#### Request:

    POST /api/service_catalog/7

``` json
{
   "action" : "edit",
   "resource" : {
      "description" : "Updated Description of the Seventh Service Catalog"
   }
}
```

#### Response:

``` json
{
  "href": "https://hostname/api/service_catalogs/7",
  "id": 7,
  "name": "Sample Service Catalog",
  "description": "Updated Description of the Seventh Service Catalog",
  "service_templates": {
    "count": 1,
    "resources": [
      {
        "href": "https://hostname/api/service_catalogs/7/service_templates/3"
      }
    ]
  }
}
```

### Editing Multiple Service Catalogs

#### Request:

    POST /api/service_catalogs

``` json
{
   "action" : "edit",
   "resources" : [
     {
       "href" : "https://hostname/api/service_catalogs/3",
       "description" : "Updated Description for Third Service Catalog"
     },
     {
       "href" : "https://hostname/api/service_catalogs/6",
       "description" : "Updated Description for Sixth Service Catalog"
     }
   ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 3,
      "name": "Service Catalog B Added from REST API",
      "description": "Updated Description for Third Service Catalog"
    },
    {
      "id": 6,
      "name": "Service Catalog E Added from REST API",
      "description": "Updated Description for Sixth Service Catalog"
    }
  ]
}
```

### Ordering a Single Service from a Service Catalog

#### Request:

    POST /api/service_catalogs/1/service_templates

``` json
{
  "action" : "order",
  "resource" : {
    "href" : "https://hostname/api/service_templates/3",
    "option_0_vm_target_name" : "test-vm-0001",
    "option_0_vm_target_hostname" : "test-vm-0001"
  }
}
```

#### Response:

``` json
{
  results: [
    {
      "approval_state": "pending_approval",
      "created_on": "2014-07-02T19:28:12Z",
      "description": "Provisioning Service [aws-ubuntu-api] from [aws-ubuntu-api]",
      "destination_id": null,
      "destination_type": null,
      "fulfilled_on": null,
      "id": 13,
      "message": "Service_Template_Provisioning - Request Created",
      "options": {
        "dialog": {
          "dialog_option_0_vm_target_name" : "test-vm-0001",
          "dialog_option_0_vm_target_hostname" : "test-vm-0001"
        }
    }
    "request_state": "pending",
    "request_type": "clone_to_service",
    "requester_id": 1,
    "requester_name": "Administrator",
    "source_id": 6,
    "source_type": "ServiceTemplate",
    "status": "Ok",
    "updated_on": "2014-07-02T19:28:12Z",
    "userid": "admin"
    }
  ]
}
```

### Ordering Multiple Services from a Service Catalog

#### Request:

    POST /api/service_catalogs/2/service_templates

``` json
{
  "action" : "order",
  "resources" : [
    {
      "href" : "https://hostname/api/service_templates/3",
      "option_1_vm_target_name" : "sample-vm-1201",
      "option_2_vm_target_hostname" : "sample-vm-1201"
    },
    {
      "href" : "https://hostname/api/service_templates/3",
      "option_1_vm_target_name" : "sample-vm-1202",
      "option_2_vm_target_hostname" : "sample-vm-1202"
    },
    {
      "href" : "https://hostname/api/service_templates/4",
      "option_1_vm_target_name" : "dev-vm1",
      "option_2_vm_target_hostname" : "dev-vm1",
      "option_3_vm_memory" : '16384'
    },
  ]
}
```

#### Response:

``` json
{
  results: [
    {
      "approval_state": "pending_approval",
      "created_on": "2014-07-02T19:28:12Z",
      "description": "Provisioning Service [sample-vm-1201] from [sample-vm-1201]",
      "destination_id": null,
      "destination_type": null,
      "fulfilled_on": null,
      "id": 13,
      "message": "Service_Template_Provisioning - Request Created",
      "options": {
        "dialog": {
          "dialog_option_0_vm_target_name" : "test-vm-0001",
          "dialog_option_0_vm_target_hostname" : "test-vm-0001"
        }
    }
    "request_state": "pending",
    "request_type": "clone_to_service",
    "requester_id": 1,
    "requester_name": "Administrator",
    "source_id": 6,
    "source_type": "ServiceTemplate",
    "status": "Ok",
    "updated_on": "2014-07-02T19:28:12Z",
    "userid": "admin"
    },
    {
      "approval_state": "pending_approval",
      "created_on": "2014-07-02T19:28:12Z",
      "description": "Provisioning Service [sample-vm-1202] from [sample-vm-1202]",
      "destination_id": null,
      "destination_type": null,
      "fulfilled_on": null,
      "id": 13,
      "message": "Service_Template_Provisioning - Request Created",
      "options": {
        "dialog": {
          "dialog_option_0_vm_target_name" : "test-vm-0001",
          "dialog_option_0_vm_target_hostname" : "test-vm-0001"
        }
    }
    "request_state": "pending",
    "request_type": "clone_to_service",
    "requester_id": 1,
    "requester_name": "Administrator",
    "source_id": 6,
    "source_type": "ServiceTemplate",
    "status": "Ok",
    "updated_on": "2014-07-02T19:28:12Z",
    "userid": "admin"
    },
    {
      "approval_state": "pending_approval",
      "created_on": "2014-07-02T19:28:12Z",
      "description": "Provisioning Service [sample-vm-1201] from [sample-vm-1201]",
      "destination_id": null,
      "destination_type": null,
      "fulfilled_on": null,
      "id": 13,
      "message": "Service_Template_Provisioning - Request Created",
      "options": {
        "dialog": {
          "dialog_option_0_vm_target_name" : "test-vm-0001",
          "dialog_option_0_vm_target_hostname" : "test-vm-0001"
        }
    }
    "request_state": "pending",
    "request_type": "clone_to_service",
    "requester_id": 1,
    "requester_name": "Administrator",
    "source_id": 6,
    "source_type": "ServiceTemplate",
    "status": "Ok",
    "updated_on": "2014-07-02T19:28:12Z",
    "userid": "admin"
    }
  ]
}
```

### Unassigning Service Templates from a Service Catalog

#### Request:

    POST /api/service_catalogs/6/service_templates

``` json
{
  "action" : "unassign",
  "resources" : [
    { "href" : "https://hostname/api/service_templates/1" },
    { "href" : "https://hostname/api/service_templates/5" },
    { "href" : "https://hostname/api/service_templates/8" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": false,
      "message": "Service Template 1 is not currently assigned to Service Catalog 3",
      "service_template_id": 1,
      "service_template_href": "https://hostname/api/service_templates/1",
      "href": "https://hostname/api/service_catalogs/6"
    },
    {
      "success": true,
      "message": "Unassigning Service Template id:5 name:'template5'",
      "service_template_id": 5,
      "service_template_href": "https://hostname/api/service_templates/5",
      "href": "https://hostname/api/service_catalogs/6"
    },
    {
      "success": false,
      "message": "Couldn't find ServiceTemplate with id=8",
      "href": "https://hostname/api/service_catalogs/6"
    }
  ]
}
```

### Deleting Multiple Service Catalogs

#### Request:

    POST /api/service_catalogs

``` json
{
  "action" : "delete",
  "resources" : [
    { "href" : "https://hostname/api/service_catalogs/8"  },
    { "href" : "https://hostname/api/service_catalogs/9"  },
    { "href" : "https://hostname/api/service_catalogs/10" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "service_catalogs id: 8 deleting",
      "href": "https://hostname/api/service_catalogs/8"
    },
    {
      "success": true,
      "message": "service_catalogs id: 9 deleting",
      "href": "https://hostname/api/service_catalogs/9"
    },
    {
      "success": true,
      "message": "service_catalogs id: 10 deleting",
      "href": "https://hostname/api/service_catalogs/10"
    }
  ]
}
```

## Tags

This section provides examples of how to interact with tags.

### Assigning Tags to a Service

#### Request:

    POST /api/services/101/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "category" : "location", "name" : "ny" },
    { "category" : "department", "name" : "finance" },
    { "category" : "environment", "name" : "dev" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'ny'",
      "href": "https://hostname/api/services/101",
      "tag_category": "location",
      "tag_name": "ny"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/services/101",
      "tag_category": "department",
      "tag_name": "finance"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'dev'",
      "href": "https://hostname/api/services/101",
      "tag_category": "environment",
      "tag_name": "dev"
    }
  ]
}
```

### Assigning Tags by Name to a Service

#### Request:

    POST /api/services/101/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "/department/finance" },
    { "name" : "/location/ny" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/services/101",
      "tag_category": "department",
      "tag_name": "finance"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'ny'",
      "href": "https://hostname/api/services/101",
      "tag_category": "location",
      "tag_name": "ny"
    }
  ]
}
```

### Assigning Tags by Reference to a Service

#### Request:

    POST /api/services/101/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "href" : "https://hostname/api/services/1/tags/49" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/services/101",
      "tag_category": "department",
      "tag_name": "finance",
      "tag_href": "https://hostname/api/tags/49"
    }
  ]
}
```

### Assigning Tags to a Service Template

#### Request:

    POST /api/service_templates/1/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "category" : "location", "name" : "ny" },
    { "category" : "department", "name" : "finance" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'ny'",
      "href": "https://hostname/api/service_templates/1",
      "tag_category": "location",
      "tag_name": "ny"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/service_templates/1",
      "tag_category": "department",
      "tag_name": "finance"
    }
  ]
}
```

### Assigning Tags to a Virtual Machine

#### Request:

    POST /api/vms/101/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "/department/finance" },
    { "name" : "/location/ny" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'ny'",
      "href": "https://hostname/api/vms/101",
      "tag_category": "location",
      "tag_name": "ny"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/vms/101",
      "tag_category": "department",
      "tag_name": "finance"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'dev'",
      "href": "https://hostname/api/vms/101",
      "tag_category": "environment",
      "tag_name": "dev"
    }
  ]
}
```

### Assigning Tags by Name to a Virtual Machine

#### Request:

    POST /api/vms/101/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "/department/finance" },
    { "name" : "/location/ny" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/vms/101",
      "tag_category": "department",
      "tag_name": "finance"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'ny'",
      "href": "https://hostname/api/vms/101",
      "tag_category": "location",
      "tag_name": "ny"
    }
  ]
}
```

### Assigning Tags by Reference to a Virtual Machine

#### Request:

    POST /api/vms/101/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "href" : "https://hostname/api/vms/1/tags/49" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/vms/101",
      "tag_category": "department",
      "tag_name": "finance",
      "tag_href": "https://hostname/api/tags/49"
    }
  ]
}
```

### Unassigning Tags from a Service

#### Request:

    POST /api/services/101/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "category" : "department", "name" : "finance" },
    { "category" : "environment", "name" : "dev" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/services/101",
      "tag_category": "department",
      "tag_name": "finance"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'environment' name:'dev'",
      "href": "https://hostname/api/services/101",
      "tag_category": "environment",
      "tag_name": "dev"
    }
  ]
}
```

### Unassigning a Tag by Name from a Service

#### Request:

    POST /api/services/101/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "name" : "/managed/department/finance" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/services/101",
      "tag_category": "department",
      "tag_name": "finance"
    }
  ]
}
```

### Unassigning a Tag by Reference from a Service

#### Request:

    POST /api/services/101/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "href" : "tags/49" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/services/101",
      "tag_category": "department",
      "tag_name": "finance",
      "tag_href": "https://hostname/api/tags/49"
    }
  ]
}
```

### Unassigning Tags from a Service Template

#### Request:

    POST /api/service_templates/1/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "category" : "location", "name" : "ny" },
    { "category" : "department", "name" : "finance" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'location' name:'ny'",
      "href": "https://hostname/api/service_templates/1",
      "tag_category": "location",
      "tag_name": "ny"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'department' name:'finance'",
      "href": "https://hostname/api/service_templates/1",
      "tag_category": "department",
      "tag_name": "finance"
    }
  ]
}
```

### Assigning Tags to Cloud Networks

#### Request:

    POST /api/cloud_networks/223/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "category" : "location", "name" : "chicago" },
    { "category" : "department", "name" : "support" },
    { "category" : "environment", "name" : "test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'chicago'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "location",
      "tag_name": "chicago"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'support'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "department",
      "tag_name": "support"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

### Assigning Tags by Name to Cloud Networks

#### Request:

    POST /api/cloud_networks/223/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "location/chicago" },
    { "name" : "department/support" },
    { "name" : "environment/test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'chicago'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "location",
      "tag_name": "chicago"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'support'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "department",
      "tag_name": "support"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

### Unassigning Tags on Cloud Networks

#### Request:

    POST /api/cloud_networks/223/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "category" : "location", "name" : "chicago" },
    { "category" : "department", "name" : "support" },
    { "category" : "environment", "name" : "test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'location' name:'chicago'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "location",
      "tag_name": "chicago"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'department' name:'support'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "department",
      "tag_name": "support"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/cloud_networks/223",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

### Assigning Tags to Cloud Subnets

#### Request:

    POST /api/cloud_subnets/7/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "category" : "location", "name" : "london" },
    { "category" : "department", "name" : "marketing" },
    { "category" : "environment", "name" : "dev" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'ny'",
      "href": "https://hostname/api/cloud_subnets/7",
      "tag_category": "location",
      "tag_name": "ny"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'marketing'",
      "href": "https://hostname/api/cloud_subnets/7",
      "tag_category": "department",
      "tag_name": "marketing"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'dev'",
      "href": "https://hostname/api/cloud_subnets/7",
      "tag_category": "environment",
      "tag_name": "dev"
    }
  ]
}
```

### Assigning Tags by Name to Cloud Subnets

#### Request:

    POST /api/cloud_subnets/7/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "location/internal" },
    { "name" : "department/marketing" },
    { "name" : "environment/dev" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'internal'",
      "href": "https://hostname/api/cloud_subnets/30",
      "tag_category": "location",
      "tag_name": "internal"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'marketing'",
      "href": "https://hostname/api/cloud_subnets/30",
      "tag_category": "department",
      "tag_name": "marketing"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'dev'",
      "href": "https://hostname/api/cloud_subnets/30",
      "tag_category": "environment",
      "tag_name": "dev"
    }
  ]
}
```

### Unassigning Tags on Cloud Subnets

#### Request:

    POST /api/cloud_subnets/7/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "category" : "location", "name" : "london" },
    { "category" : "department", "name" : "marketing" },
    { "category" : "environment", "name" : "dev" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'location' name:'london'",
      "href": "https://hostname/api/cloud_subnets/7",
      "tag_category": "location",
      "tag_name": "london"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'department' name:'marketing'",
      "href": "https://hostname/api/cloud_subnets/7",
      "tag_category": "department",
      "tag_name": "marketing"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'environment' name:'dev'",
      "href": "https://hostname/api/cloud_subnets/7",
      "tag_category": "environment",
      "tag_name": "dev"
    }
  ]
}
```

### Assigning Tags to Availability Zones

#### Request:

    POST /api/availability_zones/14/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "category" : "location", "name" : "london" },
    { "category" : "department", "name" : "engineering" },
    { "category" : "environment", "name" : "test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'london'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "location",
      "tag_name": "ny"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'engineering'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "department",
      "tag_name": "engineering"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

### Assigning Tags by Name to Availability Zones

#### Request:

    POST /api/availability_zones/14/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "location/london" },
    { "name" : "department/engineering" },
    { "name" : "environment/test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'location' name:'london'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "location",
      "tag_name": "london"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'department' name:'engineering'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "department",
      "tag_name": "engineering"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

### Unassigning Tags on Availability Zones

#### Request:

    POST /api/availability_zones/14/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "category" : "location", "name" : "london" },
    { "category" : "department", "name" : "engineering" },
    { "category" : "environment", "name" : "test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'location' name:'london'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "location",
      "tag_name": "london"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'department' name:'engineering'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "department",
      "tag_name": "engineering"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/availability_zones/14",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

### Assigning Tags to Flavors

#### Request:

    POST /api/flavors/223/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "category" : "owner", "name" : "production linux team" },
    { "category" : "service level", "name" : "gold" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'owner' name:'production linux team'",
      "href": "https://hostname/api/flavors/223",
      "tag_category": "owner",
      "tag_name": "production linux team"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'service level' name:'gold'",
      "href": "https://hostname/api/flavors/223",
      "tag_category": "service level",
      "tag_name": "gold"
    }
  ]
}
```

### Assigning Tags by Name to Flavors

#### Request:

    POST /api/flavors/223/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "owner/production linux team" },
    { "name" : "service level/gold" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'owner' name:'production linux team'",
      "href": "https://hostname/api/flavors/223",
      "tag_category": "owner",
      "tag_name": "production linux team"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'service level' name:'gold'",
      "href": "https://hostname/api/flavors/223",
      "tag_category": "service level",
      "tag_name": "gold"
    }
  ]
}
```

### Unassigning Tags on Flavors

#### Request:

    POST /api/flavors/223/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "category" : "owner", "name" : "production linux team" },
    { "category" : "service level", "name" : "gold" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'owner' name:'production linux team'",
      "href": "https://hostname/api/flavors/223",
      "tag_category": "owner",
      "tag_name": "production linux team"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'owner' name:'gold'",
      "href": "https://hostname/api/flavors/223",
      "tag_category": "service level",
      "tag_name": "gold"
    }
  ]
}
```

### Assigning Tags to Network Routers

#### Request:

    POST /api/network_routers/400/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "category" : "network location", "name" : "cloud" },
    { "category" : "environment", "name" : "production" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'network location' name:'cloud'",
      "href": "https://hostname/api/network_routers/400",
      "tag_category": "network location",
      "tag_name": "cloud"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'production'",
      "href": "https://hostname/api/network_routers/400",
      "tag_category": "environment",
      "tag_name": "production"
    }
  ]
}
```

### Assigning Tags by Name to Network Routers

#### Request:

    POST /api/cloud_networks/400/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "network location/cloud" },
    { "name" : "environment/production" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'network location' name:'cloud'",
      "href": "https://hostname/api/cloud_networks/400",
      "tag_category": "network location",
      "tag_name": "cloud"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'production'",
      "href": "https://hostname/api/cloud_networks/400",
      "tag_category": "environment",
      "tag_name": "production"
    }
  ]
}
```

### Unassigning Tags on Network Routers

#### Request:

    POST /api/network_routers/400/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "category" : "network location", "name" : "cloud" },
    { "category" : "environment", "name" : "production" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'network location' name:'cloud'",
      "href": "https://hostname/api/network_routers/400",
      "tag_category": "network location",
      "tag_name": "cloud"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'environment' name:'production'",
      "href": "https://hostname/api/network_routers/400",
      "tag_category": "environment",
      "tag_name": "production"
    }
  ]
}
```

### Assigning Tags to Security Groups

#### Request:

    POST /api/security_groups/30/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "category" : "network location", "name" : "internal" },
    { "category" : "owner", "name" : "windows 2008 test team" },
    { "category" : "environment", "name" : "test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'network location' name:'internal'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "network location",
      "tag_name": "internal"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'owner' name:'windows 2008 test team'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "owner",
      "tag_name": "windows 2008 test team"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

### Assigning Tags by Name to Security Groups

#### Request:

    POST /api/security_groups/30/tags

``` json
{
  "action" : "assign",
  "resources" : [
    { "name" : "network location/internal" },
    { "name" : "owner/windows 2008 test team" },
    { "name" : "environment/test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Assigning Tag: category:'network location' name:'internal'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "network location",
      "tag_name": "internal"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'owner' name:'windows 2008 test team'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "owner",
      "tag_name": "windows 2008 test team"
    },
    {
      "success": true,
      "message": "Assigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

### Unassigning Tags on Security Groups

#### Request:

    POST /api/security_groups/30/tags

``` json
{
  "action" : "unassign",
  "resources" : [
    { "category" : "network location", "name" : "internal" },
    { "category" : "owner", "name" : "windows 2008 test team" },
    { "category" : "environment", "name" : "test" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Unassigning Tag: category:'network location' name:'internal'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "network location",
      "tag_name": "internal"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'owner' name:'windows 2008 test team'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "owner",
      "tag_name": "windows 2008 test team"
    },
    {
      "success": true,
      "message": "Unassigning Tag: category:'environment' name:'test'",
      "href": "https://hostname/api/security_groups/30",
      "tag_category": "environment",
      "tag_name": "test"
    }
  ]
}
```

## Automation Requests

This section provides examples of how to interact with automation
requests.

### Triggering a Single Automation Request

    With automation requests:

  - **version** defaults to `1.1` if not specified.

  - **user\_name** defaults to the `REST API` authenticated user if not
    specified.

#### Request:

    POST /api/automation_requests

``` json
{
  "version" : "1.1",
  "uri_parts" : {
    "namespace" : "System",
    "class" : "Request",
    "instance" : "InspectME",
    "message" : "create"
  },
  "parameters" : {
    "var1" : "xxxxx",
    "var2" : "yyyyy",
    "var3" : 1024,
    "var4" : true,
    "var5" : "last value"
  },
  "requester" : {
    "user_name" : "admin",
    "auto_approve" : true
  }
}
```

Optionally, the action-based request format is also supported:

#### Request:

    POST /api/automation_requests

``` json
{
  "action" : "create",
  "resource" : {
    "version" : "1.1",
    "uri_parts" : {
      "namespace" : "System",
      "class" : "Request",
      "instance" : "InspectME",
      "message" : "create"
    },
    "parameters" : {
      "var1" : "xxxxx",
      "var2" : "yyyyy",
      "var3" : 1024,
      "var4" : true,
      "var5" : "last value"
    },
    "requester" : {
      "user_name" : "admin",
      "auto_approve" : true
    }
  }
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 12,
      "description": "Automation Task",
      "approval_state": "approved",
      "type": "AutomationRequest",
      "created_on": "2015-04-16T21:49:55Z",
      "updated_on": "2015-04-16T21:49:55Z",
      "requester_id": 1,
      "requester_name": "Administrator",
      "request_type": "automation",
      "request_state": "pending",
      "status": "Ok",
      "options": {
        "message": "create",
        "namespace": "System",
        "class_name": "Request",
        "instance_name": "InspectME",
        "user_id": 1,
        "attrs": {
          "var1": "xxxxx",
          "var2": "yyyyy",
          "var3": 1024,
          "var4": true,
          "var5": "last value",
          "userid": "admin"
        }
      },
      "userid": "admin"
    }
  ]
}
```

### Triggering Multiple Automation Requests

With automation requests:

  - **version** defaults to `1.1` if not specified.

  - **user\_name** defaults to the `REST API` authenticated user if not
    specified.

#### Request:

    POST /api/automation_requests

``` json
{
  "action" : "create",
  "resources" : [
    {
      "version" : "1.1",
      "uri_parts" :  {
        "namespace" : "System",
        "class" : "Request",
        "instance" : "InspectME",
        "message" : "create"
      },
      "parameters" : {
        "vm_name" : "test_1",
        "var2" : "yyyyy",
        "var3" : 1024,
        "var4" : true,
        "var5" : "last value"
      },
      "requester" :  {
        "user_name" : "jdoe",
        "auto_approve" : true
      }
    },
    {
      "uri_parts" :  {
        "namespace" : "System",
        "class" : "Request",
        "instance" : "InspectME",
        "message" : "create"
      },
      "parameters" : {
        "vm_name" : "test_2",
        "vm_memory" : 1024,
        "memory_limit" : 16384
      },
      "requester" :  {
        "auto_approve" : true
      }
    },
    {
      "uri_parts" :  {
        "namespace" : "System",
        "class" : "Request",
        "instance" : "InspectME",
        "message" : "create"
      },
      "parameters" : {
        "vm_name" : "test_3",
        "vm_memory" : 2048,
        "memory_limit" : 16384
      },
      "requester" :  {
        "auto_approve" : true
      }
    },
    {
      "uri_parts" :  {
        "namespace" : "System",
        "class" : "Request",
        "instance" : "InspectME",
        "message" : "create"
      },
      "parameters" : {
        "vm_name" : "test_4",
        "vm_memory" : 4096,
        "memory_limit" : 16384
      },
      "requester" :  {
        "auto_approve" : true
      }
    }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 14,
      "description": "Automation Task",
      "approval_state": "approved",
      "type": "AutomationRequest",
      "created_on": "2015-04-16T21:59:42Z",
      "updated_on": "2015-04-16T21:59:42Z",
      "requester_id": 13,
      "requester_name": "aab",
      "request_type": "automation",
      "request_state": "pending",
      "status": "Ok",
      "options": {
        "message": "create",
        "namespace": "System",
        "class_name": "Request",
        "instance_name": "InspectME",
        "user_id": 13,
        "attrs": {
          "vm_name": "test_1",
          "var2": "yyyyy",
          "var3": 1024,
          "var4": true,
          "var5": "last value",
          "userid": "aab"
        }
      },
      "userid": "aab"
    },
    {
      "id": 15,
      "description": "Automation Task",
      "approval_state": "approved",
      "type": "AutomationRequest",
      "created_on": "2015-04-16T21:59:42Z",
      "updated_on": "2015-04-16T21:59:42Z",
      "requester_id": 1,
      "requester_name": "Administrator",
      "request_type": "automation",
      "request_state": "pending",
      "status": "Ok",
      "options": {
        "message": "create",
        "namespace": "System",
        "class_name": "Request",
        "instance_name": "InspectME",
        "user_id": 1,
        "attrs": {
          "vm_name": "test_2",
          "vm_memory": 1024,
          "memory_limit": 16384,
          "userid": "admin"
        }
      },
      "userid": "admin"
    },
    {
      "id": 16,
      "description": "Automation Task",
      "approval_state": "approved",
      "type": "AutomationRequest",
      "created_on": "2015-04-16T21:59:42Z",
      "updated_on": "2015-04-16T21:59:42Z",
      "requester_id": 1,
      "requester_name": "Administrator",
      "request_type": "automation",
      "request_state": "pending",
      "status": "Ok",
      "options": {
        "message": "create",
        "namespace": "System",
        "class_name": "Request",
        "instance_name": "InspectME",
        "user_id": 1,
        "attrs": {
          "vm_name": "test_3",
          "vm_memory": 2048,
          "memory_limit": 16384,
          "userid": "admin"
        }
      },
      "userid": "admin"
    },
    {
      "id": 17,
      "description": "Automation Task",
      "approval_state": "approved",
      "type": "AutomationRequest",
      "created_on": "2015-04-16T21:59:42Z",
      "updated_on": "2015-04-16T21:59:42Z",
      "requester_id": 1,
      "requester_name": "Administrator",
      "request_type": "automation",
      "request_state": "pending",
      "status": "Ok",
      "options": {
        "message": "create",
        "namespace": "System",
        "class_name": "Request",
        "instance_name": "InspectME",
        "user_id": 1,
        "attrs": {
          "vm_name": "test_4",
          "vm_memory": 4096,
          "memory_limit": 16384,
          "userid": "admin"
        }
      },
      "userid": "admin"
    }
  ]
}
```

## Provisioning Requests

This section provides examples of how to interact with provisioning
requests.

### Triggering a Single Provision Request

With provisioning requests:

  - **version** defaults to `1.1` if not specified.

  - **user\_name** defaults to the `REST API` authenticated user if not
    specified.

#### Request:

Provisioning requests are made available via the following entrypoint,
either by specifying a `create` action or by posting the request
directly to `/api/provision_requests`:

    POST /api/provision_requests

``` json
{
  "version" : "1.1",
  "template_fields" : {
    "guid" : "afe6e8a0-89fd-11e3-b6ac-b8e85646e742"
  },
  "vm_fields" : {
    "number_of_cpus" : 1,
    "vm_name" : "aab_rest_vm1",
    "vm_memory" : "1024",
    "vlan" : "rhevm"
  },
  "requester" : {
    "user_name" : "jdoe",
    "owner_first_name" : "John",
    "owner_last_name" : "Doe",
    "owner_email" : "jdoe@sample.com",
    "auto_approve" : true
  },
  "tags" : {
    "network_location" : "Internal",
    "cc" : "001"
  },
  "additional_values" : {
    "request_id" : "1001"
  },
  "ems_custom_attributes" : { },
  "miq_custom_attributes" : { }
}
```

Optionally, the action-based request format is also supported:

#### Request:

    POST /api/provision_requests

``` json
{
  "action" : "create",
  "resource" : {
    "version" : "1.1",
      "template_fields" : {
        "guid" : "afe6e8a0-89fd-11e3-b6ac-b8e85646e742"
      },
      "vm_fields" : {
        "number_of_cpus" : 1,
        "vm_name" : "aab_rest_vm1",
        "vm_memory" : "1024",
        "vlan" : "rhevm"
      },
      "requester" : {
        "user_name" : "jdoe",
        "owner_first_name" : "John",
        "owner_last_name" : "Doe",
        "owner_email" : "jdoe@sample.com",
        "auto_approve" : true
      },
      "tags" : {
        "network_location" : "Internal",
        "cc" : "001"
      },
      "additional_values" : {
        "request_id" : "1001"
      },
      "ems_custom_attributes" : { },
      "miq_custom_attributes" : { }
  }
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 18,
      "description": "Provision from [bd-clone-template] to [aab_rest_vm1]",
      "approval_state": "pending_approval",
      "type": "MiqProvisionRequest",
      "created_on": "2015-05-08T17:42:55Z",
      "updated_on": "2015-05-08T17:42:55Z",
      "requester_id": 1,
      "requester_name": "Administrator",
      "request_type": "template",
      "request_state": "pending",
      "message": "VM Provisioning - Request Created",
      "status": "Ok",
      "options": {
        "use_pre_dialog": false,
        "request_type": "template",
        "miq_request_dialog_name": "miq_provision_redhat_dialogs_template",
        "owner_first_name": "John",
        "owner_last_name": "Doe",
        "owner_email": "jdoe@sample.com",
        "vm_tags": [
          62,
          58
        ],
        "addr_mode": [
          "static",
          "Static"
        ],
        "placement_cluster_name": [
          null,
          null
        ],
        "cluster_filter": [
          null,
          null
        ],
        "placement_auto": [
          true,
          1
        ],
        "placement_dc_name": [
          null,
          null
        ],
        "number_of_vms": [
          1,
          "1"
        ],
        "src_vm_id": [
          1947,
          "bd-clone-template"
        ],
        "provision_type": [
          "native_clone",
          "Native Clone"
        ],
        "linked_clone": [
          null,
          null
        ],
        "vm_name": "aab_rest_vm1",
        "pxe_server_id": [
          null,
          null
        ],
        "schedule_type": [
          "immediately",
          "Immediately on Approval"
        ],
        "vm_auto_start": [
          true,
          1
        ],
        "schedule_time": "2015-05-09T13:42:54-04:00",
        "retirement": [
          0,
          "Indefinite"
        ],
        "retirement_warn": [
          604800,
          "1 Week"
        ],
        "stateless": [
          false,
          0
        ],
        "vlan": [
          "rhevm",
          "rhevm"
        ],
        "disk_format": [
          "default",
          "Default"
        ],
        "number_of_sockets": [
          1,
          "1"
        ],
        "cores_per_socket": [
          1,
          "1"
        ],
        "vm_memory": [
          "1024",
          "1024"
        ],
        "network_adapters": [
          1,
          "1"
        ],
        "placement_host_name": [
          null,
          null
        ],
        "placement_ds_name": [
          null,
          null
        ],
        "src_vm_nics": [

        ],
        "src_vm_lans": [

        ],
        "customize_enabled": [
          "enabled"
        ],
        "src_ems_id": [
          105,
          "rhevm230"
        ],
        "auto_approve": false,
        "ws_values": {
          "request_id": "1001"
        },
        "ws_ems_custom_attributes": {
        },
        "ws_miq_custom_attributes": {
        }
      },
      "userid": "jdoe",
      "source_id": 1947,
      "source_type": "VmOrTemplate"
    }
  ]
}
```

### Triggering Multiple Provision Requests

With provisioning requests:

  - **version** defaults to `1.1` if not specified.

  - **user\_name** defaults to the `REST API` authenticated user if not
    specified.

#### Request:

    POST /api/provision_requests

``` json
{
  "action" : "create",
  "resources" : [
    {
      "version" : "1.1",
      "template_fields" : { "guid" : "afe6e8a0-89fd-11e3-b6ac-b8e85646e742" },
      "vm_fields" : {
        "vm_name" : "jdoe_rest_vm1",
        "number_of_cpus" : 1,
        "vm_memory" : "1024",
        "vlan" : "nic1"
      },
      "requester" : {
        "user_name" : "jdoe",
        "owner_first_name" : "John",
        "owner_last_name" : "Doe",
        "owner_email" : "jdoe@sample.com",
        "auto_approve" : true
      },
      "tags" : {
        "network_location" : "Internal",
        "cc" : "001"
      },
      "additional_values" : { "request_id" : "1001" },
      "ems_custom_attributes" : { },
      "miq_custom_attributes" : { }
    },
    {
      "template_fields" : { "guid" : "afe6e8a0-89fd-11e3-b6ac-b8e85646e742" },
      "vm_fields" : {
        "vm_name" : "jdoe_rest_vm2",
        "number_of_cpus" : 1,
        "vm_memory" : "2048",
        "vlan" : "nic1"
      },
      "requester" : {
        "owner_first_name" : "John",
        "owner_last_name" : "Doe",
        "owner_email" : "jdoe@sample.com",
        "auto_approve" : true
      },
      "tags" : {
        "network_location" : "Internal",
        "cc" : "001"
      },
      "additional_values" : { "request_id" : "1002" }
    },
    {
      "template_fields" : { "guid" : "afe6e8a0-89fd-11e3-b6ac-b8e85646e742" },
      "vm_fields" : {
        "vm_name" : "jdoe_rest_vm3",
        "number_of_cpus" : 1,
        "vm_memory" : "4096",
        "vlan" : "nic1"
      },
      "requester" : {
        "owner_first_name" : "John",
        "owner_last_name" : "Doe",
        "owner_email" : "jdoe@sample.com",
        "auto_approve" : true
      },
      "tags" : {
        "network_location" : "Internal",
        "cc" : "001"
      },
      "additional_values" : { "request_id" : "1003" }
    }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 19,
      "description": "Provision from [bd-clone-template] to [aab_rest_vm1]",
      "approval_state": "pending_approval",
      "type": "MiqProvisionRequest",
      "created_on": "2015-05-08T18:25:25Z",
      "updated_on": "2015-05-08T18:25:26Z",
      "requester_id": 1,
      "requester_name": "jdoe",
      "request_type": "template",
      "request_state": "pending",
      "message": "VM Provisioning - Request Created",
      "status": "Ok",
      "options": {
        "use_pre_dialog": false,
        "request_type": "template",
        "miq_request_dialog_name": "miq_provision_redhat_dialogs_template",
        "owner_first_name": "John",
        "owner_last_name": "Doe",
        "owner_email": "jdoe@sample.com",
        "vm_tags": [
          62,
          58
        ],
        "addr_mode": [
          "static",
          "Static"
        ],
        "placement_cluster_name": [
          null,
          null
        ],
        "cluster_filter": [
          null,
          null
        ],
        "placement_auto": [
          true,
          1
        ],
        "placement_dc_name": [
          null,
          null
        ],
        "number_of_vms": [
          1,
          "1"
        ],
        "src_vm_id": [
          1947,
          "bd-clone-template"
        ],
        "provision_type": [
          "native_clone",
          "Native Clone"
        ],
        "linked_clone": [
          null,
          null
        ],
        "vm_name": "aab_rest_vm1",
        "pxe_server_id": [
          null,
          null
        ],
        "schedule_type": [
          "immediately",
          "Immediately on Approval"
        ],
        "vm_auto_start": [
          true,
          1
        ],
        "schedule_time": "2015-05-09T14:25:25-04:00",
        "retirement": [
          0,
          "Indefinite"
        ],
        "retirement_warn": [
          604800,
          "1 Week"
        ],
        "stateless": [
          false,
          0
        ],
        "vlan": [
          "rhevm",
          "rhevm"
        ],
        "disk_format": [
          "default",
          "Default"
        ],
        "number_of_sockets": [
          1,
          "1"
        ],
        "cores_per_socket": [
          1,
          "1"
        ],
        "vm_memory": [
          "1024",
          "1024"
        ],
        "network_adapters": [
          1,
          "1"
        ],
        "placement_host_name": [
          null,
          null
        ],
        "placement_ds_name": [
          null,
          null
        ],
        "src_vm_nics": [

        ],
        "src_vm_lans": [

        ],
        "customize_enabled": [
          "enabled"
        ],
        "src_ems_id": [
          105,
          "rhevm230"
        ],
        "auto_approve": false,
        "ws_values": {
          "request_id": "1001"
        },
        "ws_ems_custom_attributes": {
        },
        "ws_miq_custom_attributes": {
        }
      },
      "userid": "jdoe",
      "source_id": 1947,
      "source_type": "VmOrTemplate"
    },
    {
      "id": 20,
      "description": "Provision from [bd-clone-template] to [aab_rest_vm2]",
      "approval_state": "pending_approval",
      "type": "MiqProvisionRequest",
      "created_on": "2015-05-08T18:25:28Z",
      "updated_on": "2015-05-08T18:25:29Z",
      "requester_id": 1,
      "requester_name": "jdoe",
      "request_type": "template",
      "request_state": "pending",
      "message": "VM Provisioning - Request Created",
      "status": "Ok",
      "options": {
        "use_pre_dialog": false,
        "request_type": "template",
        "miq_request_dialog_name": "miq_provision_redhat_dialogs_template",
        "owner_first_name": "John",
        "owner_last_name": "Doe",
        "owner_email": "jdoe@sample.com",
        "vm_tags": [
          62,
          58
        ],
        "addr_mode": [
          "static",
          "Static"
        ],
        "placement_cluster_name": [
          null,
          null
        ],
        "cluster_filter": [
          null,
          null
        ],
        "placement_auto": [
          true,
          1
        ],
        "placement_dc_name": [
          null,
          null
        ],
        "number_of_vms": [
          1,
          "1"
        ],
        "src_vm_id": [
          1947,
          "bd-clone-template"
        ],
        "provision_type": [
          "native_clone",
          "Native Clone"
        ],
        "linked_clone": [
          null,
          null
        ],
        "vm_name": "aab_rest_vm2",
        "pxe_server_id": [
          null,
          null
        ],
        "schedule_type": [
          "immediately",
          "Immediately on Approval"
        ],
        "vm_auto_start": [
          true,
          1
        ],
        "schedule_time": "2015-05-09T14:25:28-04:00",
        "retirement": [
          0,
          "Indefinite"
        ],
        "retirement_warn": [
          604800,
          "1 Week"
        ],
        "stateless": [
          false,
          0
        ],
        "vlan": [
          "rhevm",
          "rhevm"
        ],
        "disk_format": [
          "default",
          "Default"
        ],
        "number_of_sockets": [
          1,
          "1"
        ],
        "cores_per_socket": [
          1,
          "1"
        ],
        "vm_memory": [
          "1024",
          "1024"
        ],
        "network_adapters": [
          1,
          "1"
        ],
        "placement_host_name": [
          null,
          null
        ],
        "placement_ds_name": [
          null,
          null
        ],
        "src_vm_nics": [

        ],
        "src_vm_lans": [

        ],
        "customize_enabled": [
          "enabled"
        ],
        "src_ems_id": [
          105,
          "rhevm230"
        ],
        "auto_approve": false,
        "ws_values": {
          "request_id": "1001"
        },
        "ws_ems_custom_attributes": {
        },
        "ws_miq_custom_attributes": {
        }
      },
      "userid": "jdoe",
      "source_id": 1947,
      "source_type": "VmOrTemplate"
    },
    {
      "id": 21,
      "description": "Provision from [bd-clone-template] to [aab_rest_vm3]",
      "approval_state": "pending_approval",
      "type": "MiqProvisionRequest",
      "created_on": "2015-05-08T18:25:32Z",
      "updated_on": "2015-05-08T18:25:32Z",
      "requester_id": 1,
      "requester_name": "jdoe",
      "request_type": "template",
      "request_state": "pending",
      "message": "VM Provisioning - Request Created",
      "status": "Ok",
      "options": {
        "use_pre_dialog": false,
        "request_type": "template",
        "miq_request_dialog_name": "miq_provision_redhat_dialogs_template",
        "owner_first_name": "John",
        "owner_last_name": "Doe",
        "owner_email": "jdoe@sample.com",
        "vm_tags": [
          62,
          58
        ],
        "addr_mode": [
          "static",
          "Static"
        ],
        "placement_cluster_name": [
          null,
          null
        ],
        "cluster_filter": [
          null,
          null
        ],
        "placement_auto": [
          true,
          1
        ],
        "placement_dc_name": [
          null,
          null
        ],
        "number_of_vms": [
          1,
          "1"
        ],
        "src_vm_id": [
          1947,
          "bd-clone-template"
        ],
        "provision_type": [
          "native_clone",
          "Native Clone"
        ],
        "linked_clone": [
          null,
          null
        ],
        "vm_name": "aab_rest_vm3",
        "pxe_server_id": [
          null,
          null
        ],
        "schedule_type": [
          "immediately",
          "Immediately on Approval"
        ],
        "vm_auto_start": [
          true,
          1
        ],
        "schedule_time": "2015-05-09T14:25:31-04:00",
        "retirement": [
          0,
          "Indefinite"
        ],
        "retirement_warn": [
          604800,
          "1 Week"
        ],
        "stateless": [
          false,
          0
        ],
        "vlan": [
          "rhevm",
          "rhevm"
        ],
        "disk_format": [
          "default",
          "Default"
        ],
        "number_of_sockets": [
          1,
          "1"
        ],
        "cores_per_socket": [
          1,
          "1"
        ],
        "vm_memory": [
          "1024",
          "1024"
        ],
        "network_adapters": [
          1,
          "1"
        ],
        "placement_host_name": [
          null,
          null
        ],
        "placement_ds_name": [
          null,
          null
        ],
        "src_vm_nics": [

        ],
        "src_vm_lans": [

        ],
        "customize_enabled": [
          "enabled"
        ],
        "src_ems_id": [
          105,
          "rhevm230"
        ],
        "auto_approve": false,
        "ws_values": {
          "request_id": "1001"
        },
        "ws_ems_custom_attributes": {
        },
        "ws_miq_custom_attributes": {
        }
      },
      "userid": "jdoe",
      "source_id": 1947,
      "source_type": "VmOrTemplate"
    }
  ]
}
```

### Monitoring Request

Once a provisioning request is created, the response result will include
the queryable provision request itself, for example:
`/api/provision_requests/:id`

#### Response:

``` json
{
  "results": [
    {
      "id": 3068,
      "description": "Provision from [template1] to [###]",
      "approval_state": "pending_approval",
      "type": "MiqProvisionRequest",
      "created_on": "2015-04-14T17:36:30Z",
      "updated_on": "2015-04-14T17:36:30Z",
      "requester_id": 88913,
      "requester_name": "API User",
      "request_type": "template",
      "request_state": "pending",
      "message": "VM Provisioning - Request Created",
      "status": "Ok"
      "options": {
        "use_pre_dialog": false,
        "request_type": "template",
        "miq_request_dialog_name": "miq_provision_dialogs",
        "src_vm_id": [
          109996,
          "template1"
        ],
        "src_vm_nics": [],
        "src_vm_lans": [],
        "src_ems_id": [
          59136,
          "ems_0000000000002"
        ],
        "placement_auto": [
          true,
          1
        ],
        "vm_tags": [],
        "ws_values": {
        },
        "ws_ems_custom_attributes": {
        },
        "ws_miq_custom_attributes": {
        },
        "tags": {
        }
      },
      "userid": "admin",
      "source_id": 109996,
      "source_type": "VmOrTemplate"
    }
  ]
}
```

In the above example, the request can be queried periodically until the
`request_state` reaches the `finished` state with:

    GET /api/provision_requests/3068

<div class="note">

The `requests` tasks of a provisioning request can also be queried by
expanding the `request_tasks` subcollection as follows:

</div>

    GET /api/provision_requests/:id?expand=request_tasks

An alias **tasks** is also defined for the above subcollection:

    GET /api/provision_requests/:id?expand=tasks

For a list of available attributes, see the [Provisioning Request
Attributes](#provision-request-supported-attributes) section.

### Placement of Environmental Variables in Provisioning Requests

Pass environment values directly through the `vm_fields` attribute group
of a provisioning request by first adding `"placement_auto":"false"` to
the hash.

<div class="note">

Once `"placement_auto:"false"` has been added, you must pass values for
all the required fields on the Environment tab.

</div>

The example request displays how the `vm_fields` attribute group should
appear when passing environment values.

#### Request:

Provisioning requests are made available via the following entrypoint,
either by specifying a create action or by posting the request directly
to /api/provision\_requests:

    POST /api/provision_requests

    "vm_fields" : {
      "vm_name" : "aab_rest_vm1",
      "placement_auto": "false",
      "placement_availability_zone": "2",
      "cloud_network": "2",
      "cloud_subnet": "3",
      "security_groups": "64",
      "instance_type": "2",
    },

## Providers

This section provides examples of how to interact with providers.

### Creating a Provider

#### Request:

    POST /api/providers

``` json
{
  "type"      : "ManageIQ::Providers::Redhat::InfraManager",
  "name"      : "rhevm101",
  "hostname"  : "rhevm101",
  "ipaddress" : "100.200.300.101",
  "credentials" : {
    "userid"    : "admin_account",
    "password"  : "admin_password"
  }
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 105,
      "name": "rhevm101",
      "hostname": "rhevm101",
      "ipaddress": "100.200.300.101",
      "created_on": "2015-05-05T15:47:41Z",
      "updated_on": "2015-05-05T15:47:41Z",
      "guid": "10360312-f33e-11e4-86c7-b8e85646e742",
      "zone_id": 1,
      "type": "ManageIQ::Providers::Redhat::InfraManager"
    }
  ]
}
```

### Creating a Provider with Compound Credentials

#### Request:

    POST /api/providers

``` json
{
  "type"      : "ManageIQ::Providers::Redhat::InfraManager",
  "name"      : "rhevm102",
  "hostname"  : "rhevm102",
  "ipaddress" : "100.200.300.102",
  "credentials" : [
    {
      "userid"    : "default_userid",
      "password"  : "default_password"
    },
    {
      "userid"    : "metrics_userid",
      "password"  : "metrics_password",
      "auth_type" : "metrics"
    }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 106,
      "name": "rhevm102",
      "hostname": "rhevm102",
      "ipaddress": "100.200.300.102",
      "created_on": "2015-05-05T15:57:44Z",
      "updated_on": "2015-05-05T15:57:44Z",
      "guid": "acbd610e-f3f6-11e4-aaba-b8e85646e742",
      "zone_id": 1,
      "type": "ManageIQ::Providers::Redhat::InfraManager"
    }
  ]
}
```

### Refreshing a Provider

#### Request:

    POST /api/providers/105

``` json
{
  "action" : "refresh"
}
```

#### Response:

``` json
{
  "success": true,
  "message": "Provider id:105 name:'rhevm105' refreshing",
  "href": "https://hostname/api/providers/105"
}
```

### Updating a Provider

#### Request:

    POST /api/providers/106

``` json
{
  "action"    : "edit",
  "ipaddress" : "100.200.300.112",
  "credentials" : [
    {
      "userid"    : "updated_metrics_userid",
      "password"  : "updated_metrics_password",
      "auth_type" : "metrics"
    }
  ]
}
```

#### Response:

``` json
{
  "href": "https://hostname/api/providers/106",
  "id": 106,
  "name": "rhevm102",
  "hostname": "rhevm102",
  "ipaddress": "100.200.300.112",
  "created_on": "2015-05-06T13:49:11Z",
  "updated_on": "2015-05-06T13:53:06Z",
  "guid": "acbd610e-f3f6-11e4-aaba-b8e85646e742",
  "zone_id": 1,
  "type": "ManageIQ::Providers::Redhat::InfraManager"
}
```

### Deleting a Provider

#### Deleting a Single Provider

### Request:

    DELETE /api/provider/105

Or via the delete action as follows:

    POST /api/provider/105

``` json
{
  "action" : "delete"
}
```

### Response:

``` json
{
  "success": true,
  "message": "Provider id:106 name:'rhevm102' deleting",
  "task_id": 625,
  "task_href": "https://hostname/api/tasks/625",
  "href": "https://hostname/api/providers/106"
}
```

<div class="note">

Delete actions are done asynchronously as it can take a while to
complete. The delete task can be queried as follows:

</div>

### Request:

    GET /api/tasks/625

### Response:

``` json
{
  "href": "https://hostname/api/tasks/625",
  "id": 625,
  "name": "Provider id:106 name:'rhevm102' deleting",
  "state": "Finished",
  "status": "Ok",
  "message": "Task completed successfully",
  "userid": "admin",
  "created_on": "2015-05-06T14:02:26Z",
  "updated_on": "2015-05-06T14:02:32Z"
}
```

#### Deleting Multiple Providers

### Request:

    POST /api/providers

``` json
{
  "action" : "delete",
  "resources" : [
    { "href" : "https://hostname/api/providers/107" },
    { "href" : "https://hostname/api/providers/108" }
  ]
}
```

### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "Provider id:107 name:'rhevm102' deleting",
      "task_id": 626,
      "task_href": "https://hostname/api/tasks/626",
      "href": "https://hostname/api/providers/107"
    },
    {
      "success": true,
      "message": "Provider id:108 name:'rhevm103' deleting",
      "task_id": 627,
      "task_href": "https://hostname/api/tasks/627",
      "href": "https://hostname/api/providers/108"
    }
  ]
}
```

## Services

This section provides examples of how to interact with services.

### Editing a Service

#### Request:

    POST /api/services/101

``` json
{
  "action" : "edit",
  "resource" : {
    "name" : "service_101",
    "description" : "This is an updated description for service 101"
  }
}
```

#### Response:

``` json
{
  "href": "https://hostname/api/services/101",
  "id": 101,
  "name": "service_101",
  "description": "This is an updated description for the service 101",
  "guid": "4a8f96de-a1a6-11e4-9f8d-b8e85646e742",
  "options": {
  },
  "created_at": "2015-01-21T19:47:11Z",
  "updated_at": "2015-04-16T22:17:15Z"
}
```

### Editing Multiple Services

#### Request:

    POST /api/services

``` json
{
  "action" : "edit",
  "resources" : [
    {
      "href" : "https://hostname/api/services/81",
      "description" : "This is an updated description for service 81"
    },
    {
      "href" : "https://hostname/api/services/82",
      "description" : "This is an updated description for service 82"
    }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 81,
      "name": "api_gen_A_81",
      "description": "This is an updated description for service 81",
      "guid": "eb6daaf8-7c9b-11e4-8a3a-b8e85646e742",
      "options": {
      },
      "created_at": "2014-12-05T16:29:43Z",
      "updated_at": "2015-04-16T22:43:37Z"
    },
    {
      "id": 82,
      "name": "api_gen_A_82",
      "description": "This is an updated description for service 82",
      "guid": "eb6de400-7c9b-11e4-8a3a-b8e85646e742",
      "options": {
      },
      "created_at": "2014-12-05T16:29:43Z",
      "updated_at": "2015-04-16T22:43:37Z"
    }
  ]
}
```

### Editing a Resource with the PATCH Method

Supported attribute actions for PATCH include add, edit and remove.

#### Request:

    PATCH /api/services/90

``` json
[
  { "action" : "edit", "path" : "name", "value" : "updated_service_90" },
  { "action" : "remove", "path" : "description"}
]
```

#### Response:

``` json
{
  "href": "https://hostname/api/services/90",
  "id": 90,
  "name": "updated_service_90",
  "guid": "eb6fc61c-7c9b-11e4-8a3a-b8e85646e742",
  "options": {
  },
  "created_at": "2014-12-05T16:29:43Z",
  "updated_at": "2015-04-16T22:38:57Z"
}
```

<div class="note">

Note that the description attribute is no longer defined for this
service.

</div>

### Editing a Service with the PUT Method

#### Request:

    PUT /api/services/90

``` json
{
  "name" : "new_service_90",
  "description" : "This is a new description for service 90"
}
```

#### Response:

``` json
{
  "href": "https://hostname/api/services/90",
  "id": 90,
  "name": "new_service_90",
  "description": "This is a new description for service 90",
  "guid": "eb6fc61c-7c9b-11e4-8a3a-b8e85646e742",
  "options": {
  },
  "created_at": "2014-12-05T16:29:43Z",
  "updated_at": "2015-04-16T22:41:37Z"
}
```

### Retiring a Service Immediately

#### Request:

    POST /api/services

``` json
{
  "action" : "request_retire",
  "resource" : { "href" : "https://hostname/api/services/35" }
}
```

#### Response:

``` json
{
  "results" : [
    {
      "href": "https://hostname/api/services/95",
      "id": 95,
      "name": "sample_service_95",
      "description": "Description for sample_service_95",
      "guid": "eb713538-7c9b-11e4-8a3a-b8e85646e742",
      "options": {
      },
      "created_at": "2014-12-05T16:29:43Z",
      "updated_at": "2015-05-08T19:32:00Z"
    }
  ]
}
```

Alternatively, this can be done by targeting the service directly:

    POST /api/services/95

``` json
{
  "action" : "request_retire"
}
```

#### Response:

``` json
{
  "href": "https://hostname/api/services/95",
  "id": 95,
  "name": "sample_service_95",
  "description": "Description for sample_service_95",
  "guid": "eb713538-7c9b-11e4-8a3a-b8e85646e742",
  "options": {
  },
  "created_at": "2014-12-05T16:29:43Z",
  "updated_at": "2015-05-08T19:32:00Z"
}
```

### Retiring a Service at a Future Time

#### Request:

    POST /api/services/93

``` json
{
  "action" : "request_retire",
  "resource" : { "date" : "10/31/2015", "warn" : "7"  }
}
```

#### Response:

``` json
{
  "href": "https://hostname/api/services/93",
  "id": 93,
  "name": "sample_service_93",
  "description": "Description for sample_service_93",
  "guid": "eb709e02-7c9b-11e4-8a3a-b8e85646e742",
  "options": {
  },
  "created_at": "2014-12-05T16:29:43Z",
  "updated_at": "2015-05-08T19:40:19Z",
  "retired": false,
  "retires_on": "2015-10-30",
  "retirement_warn": 7
}
```

### Retiring Multiple Services

#### Request:

    POST /api/services

``` json
{
  "action" : "request_retire",
  "resources" : [
      { "href" : "https://hostname/api/services/100" },
      { "href" : "https://hostname/api/services/101", "date" : "11/01/2015", "warn" : "4" },
      { "href" : "https://hostname/api/services/102", "date" : "11/02/2015", "warn" : "4" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 100,
      "name": "cloud_service_100",
      "description": "Description for cloud_service_100",
      "guid": "eb725f94-7c9b-11e4-8a3a-b8e85646e742",
      "options": {
      },
      "created_at": "2014-12-05T16:29:43Z",
      "updated_at": "2015-05-08T19:46:11Z"
    },
    {
      "id": 101,
      "name": "cloud_service_101",
      "description": "Description for cloud_service_101",
      "guid": "4a8f96de-a1a6-11e4-9f8d-b8e85646e742",
      "options": {
      },
      "created_at": "2015-01-21T19:47:11Z",
      "updated_at": "2015-05-08T19:46:19Z",
      "retired": false,
      "retires_on": "2015-11-01",
      "retirement_warn": 4
    },
    {
      "id": 102,
      "name": "cloud_service_102",
      "description": "Description for cloud_service_102",
      "guid": "e2da0cb0-e47e-11e4-a47f-b8e85646e742",
      "options": {
      },
      "created_at": "2015-04-16T21:23:55Z",
      "updated_at": "2015-05-08T19:46:19Z",
      "retired": false,
      "retires_on": "2015-11-02",
      "retirement_warn": 3
    }
  ]
}
```

### Deleting Services

#### Request:

    POST /api/services

``` json
{
  "action" : "delete",
  "resources" : [
    { "href" : "https://hostname/api/services/97" },
    { "href" : "https://hostname/api/services/98" },
    { "href" : "https://hostname/api/services/99" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "services id: 97 deleting",
      "href": "https://hostname/api/services/97"
    },
    {
      "success": true,
      "message": "services id: 98 deleting",
      "href": "https://hostname/api/services/98"
    },
    {
      "success": true,
      "message": "services id: 99 deleting",
      "href": "https://hostname/api/services/99"
    }
  ]
}
```

## Virtual Machines

This section provides examples of how to interact with virtual machines.

### Provisioning a Virtual Machine Using Cloud-init

#### Request:

    POST api/provision_requests/

``` json
{"version"=>"1.1",
 "template_fields"=>
  {"guid"=>"1dbfed74-1c8b-4535-9f1e-c654a5456805",
   "name"=>"template_name",
   "request_type"=>"template"},
 "vm_fields"=>
  {"customization_template_id"=>10000000000000,
   "addr_mode"=>"static",
   "sysprep_enabled"=>"fields",
   "placement_auto"=>true,
   "number_of_vms"=>1,
   "provision_type"=>"native_clone",
   "vm_name"=>"name_of_vm_to_provision",
   "vm_auto_start"=>true,
   "retirement"=>0,
   "retirement_warn"=>604800,
   "vlan"=>"9af50e0c-b277-422a-a5c3-11e158d21fa8",
   "disk_format"=>"default",
   "number_of_sockets"=>1,
   "cores_per_socket"=>1,
   "vm_memory"=>"2048",
   "memory_reserve"=>341,
   "memory_limit"=>8192,
   "network_adapters"=>1},
 "requester"=>{"owner_email"=>"test@testing.com"},
 "tags"=>{},
 "additional_values"=>nil,
 "ems_custom_attributes"=>nil,
 "miq_custom_attributes"=>nil}
```

Following are some possible cases where the VLAN field is not set
correctly, which can lead to a validation failure:

    Provision failed for the following reasons:\n'Network/Virtual NIC Profile ID or Profile Name (Network Name)' is required.

1.  When providing VNIC profile ID:
    
    1.  vnic\_profile\_id does not belong to the expected cluster
        (*should match the VNIC profile ID of the network taken from RHV
        based on template’s cluster assigned network*)
    
    2.  Non-existent VNIC profile ID (*should be available under RHV,
        i.e.: https:/\<RHV FQDN\>/ovirt-engine/api/vnicprofiles*)

2.  When providing: “profile name (network name)”:
    
    1.  Non-existent network name
    
    2.  Wrong format (*missing space before the first bracket*:
        “profile\_name(network\_name)”)
    
    3.  Use Network name that was used in V3 instead of: “profile\_name
        (network\_name)”

| VLAN value                                     | Result                                   |
| ---------------------------------------------- | ---------------------------------------- |
| “vlan": "1dbfed74-1c8b-4535-9f1e-c654a5456805" | Failed, no such ID                       |
| "vlan": "aaa (aaa)"                            | Failed, no such VNIC profile/network     |
| "vlan": "ovirtmgmt(ovirtmgmt)"                 | Failed, invalid format                   |
| "vlan": "0000000a-000a-000a-000a-000000000398" | Failed, VNIC profile ID of other cluster |
| "vlan": "ovirtmgmt"                            | Failed, not supported by v4              |

Examples of incorrect VLAN value:

| VLAN value                                     | Result                        |
| ---------------------------------------------- | ----------------------------- |
| "vlan": "654281a3-db89-4718-ae43-9466b81eb001" | Passed, valid VNIC profile ID |
| "vlan": "ovirtmgmt (ovirtmgmt)"                | Passed, supported format      |

Examples of correct VLAN value:

### Scanning a Virtual Machine

#### Request:

    POST /api/vms/1922

``` json
{
  "action": "scan"
}
```

#### Response:

``` json
{
  "success": true,
  "message": "VM id:1922 name:'aab_test_vm' scanning",
  "task_id": 618,
  "task_href": "https://hostname/api/tasks/618",
  "href": "https://hostname/api/vms/1922"
}
```

Optionally, to query the status of the scan:

#### Request:

    GET /api/tasks/618

#### Response:

``` json
{
  "href": "https://hostname/api/tasks/618",
  "id": 618,
  "name": "VM id:1922 name:'aab_test_vm' scanning",
  "state": "Finished",
  "status": "Ok",
  "message": "Task completed successfully",
  "userid": "admin",
  "created_on": "2015-05-05T19:37:32Z",
  "updated_on": "2015-05-05T19:37:38Z"
}
```

### Setting the Virtual Machine Owner

#### Request:

    POST /api/vms/1921

``` json
{
  "action": "set_owner",
  "resource" : {
    "owner" : "admin"
  }
}
```

#### Response:

``` json
{
  "success": true,
  "message": "VM id:1921 name:'aab_demo_vm' setting owner to 'admin'",
  "href": "https://hostname/api/vms/1921"
}
```

### Adding an Event to a Virtual Machine

#### Request:

    POST /api/vms/1921

``` json
{
  "action": "add_event",
  "resource" : {
    "event_type" : "BadUserNameSessionEvent",
    "event_message" : "Cannot login user@test.domain"
  }
}
```

#### Response:

``` json
{
  "success": true,
  "message": "Adding Event type=BadUserNameSessionEvent message=Cannot login user@test.domain",
  "href": "https://hostname/api/vms/1921"
}
```

### Adding a Lifecycle Event to a Virtual Machine

#### Request:

    POST /api/vms/1921

``` json
{
  "action" : "add_lifecycle_event",
  "resource" : {
    "event" : "event_name",
    "status" : "event_status",
    "message" : "Message about the event",
    "created_by" : "user_name"
  }
}
```

#### Response:

``` json
{
  "success": true,
  "message": "VM id:1921 name:'aab_demo_vm' adding lifecycle event=event_name message=Message about the event",
  "href": "https://hostname/api/vms/1921"
}
```

### Starting a Virtual Machine

#### Request:

    POST /api/vms/1921

``` json
{
  "action": "start"
}
```

#### Response:

``` json
{
  "success": true,
  "message": "VM id:1921 name:'aab_demo_vm' starting",
  "task_id": 610,
  "task_href": "https://hostname/api/tasks/610",
  "href": "https://hostname/api/vms/1921"
}
```

### Querying Task Progress

#### Request:

    GET /api/tasks/620

#### Response:

``` json
{
  "href": "https://hostname/api/tasks/610",
  "id": 610,
  "name": "VM id:1921 name:'aab_demo_vm' starting",
  "state": "Queued",
  "status": "Ok",
  "message": "Queued the action: [VM id:1921 name:'aab_demo_vm' starting] being run for user: [admin]",
  "userid": "admin",
  "created_on": "2015-05-05T15:58:08Z",
  "updated_on": "2015-05-05T15:58:08Z"
}
```

### Stopping a Virtual Machine

#### Request:

    POST /api/vms/1921

``` json
{
  "action": "stop"
}
```

#### Response:

``` json
{
  "success": true,
  "message": "VM id:1921 name:'aab_demo_vm' stopping",
  "task_id": 619,
  "task_href": "https://hostname/api/tasks/619",
  "href": "https://hostname/api/vms/1921"
}
```

### Suspending a Virtual Machine

#### Request:

    POST /api/vms/1921

``` json
{
  "action": "suspend"
}
```

#### Response:

``` json
{
  "success": true,
  "message": "VM id:1921 name:'aab_demo_vm' suspending",
  "task_id": 620,
  "task_href": "https://hostname/api/tasks/620",
  "href": "https://hostname/api/vms/1921"
}
```

### Deleting Virtual Machines

#### Deleting a Single Virtual Machine

### Request:

    DELETE /api/vms/334

On success, the virtual machine targeted for deletion asynchronously and
no response content with an HTTP status code of 204 are returned.

#### Deleting Multiple Virtual Machines

### Request:

    DELETE /api/vms

``` json
{
  "action" : "delete",
  "resources" : [
    { "href" : "https://hostname/api/vms/348" },
    { "href" : "https://hostname/api/vms/349" },
    { "href" : "https://hostname/api/vms/3" }
  ]
}
```

### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "VM id:348 name:'aab-temp1' deleting",
      "task_id": 616,
      "task_href": "https://hostname/api/tasks/616",
      "href": "https://hostname/api/vms/348"
    },
    {
      "success": true,
      "message": "VM id:349 name:'aab-temp2' deleting",
      "task_id": 617,
      "task_href": "https://hostname/api/tasks/617",
      "href": "https://hostname/api/vms/349"
    }
  ]
}
```

Optionally, monitor the asynchronous virtual machine deletion by
accessing the related task as follows:

### Request:

    GET /api/tasks/616

### Response:

``` json
{
  "href": "https://hostname/api/tasks/616",
  "id": 616,
  "name": "VM id:348 name:'aab-temp1' deleting",
  "state": "Finished",
  "status": "Ok",
  "message": "Task completed successfully",
  "userid": "admin",
  "created_on": "2015-05-05T19:33:35Z",
  "updated_on": "2015-05-05T19:33:40Z"
}
```

## Service Templates

This section provides examples of how to interact with service
templates.

### Editing a Service Template

#### Request:

    POST /api/service_templates/2

``` json
{
  "action" : "edit",
  "resource" : {
    "name" : "updated_svc_template_02",
    "description" : "This is an updated description for service template 02"
  }
}
```

#### Response:

``` json
{
  "href": "https://hostname/api/service_templates/2",
  "id": 2,
  "name": "updated_svc_template_02",
  "description": "This is an updated description for service template 02",
  "guid": "6f7918b4-d6e7-11e4-9837-b8e85646e742",
  "options": {
  },
  "created_at": "2015-03-30T14:17:02Z",
  "updated_at": "2015-04-16T22:30:02Z",
  "service_type": "unknown",
  "service_template_catalog_id": 6
}
```

### Editing Multiple Service Templates

#### Request:

    POST /api/service_templates

``` json
{
  "action" : "edit",
  "resources" : [
    {
      "href" : "https://hostname/api/service_templates/1",
      "description" : "This is an updated description for the first sample service template"
    },
    {
      "href" : "https://hostname/api/service_templates/2",
      "description" : "This is an updated description for the second sample service template"
    }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "id": 1,
      "name": "template1",
      "description": "This is an updated description for the first sample service template",
      "guid": "6a6fdf7e-d6e7-11e4-9837-b8e85646e742",
      "options": {
      },
      "created_at": "2015-03-30T14:16:53Z",
      "updated_at": "2015-04-16T22:33:09Z",
      "service_type": "unknown",
      "service_template_catalog_id": 3
    },
    {
      "id": 2,
      "name": "updated_svc_template_02",
      "description": "This is an updated description for the second sample service template",
      "guid": "6f7918b4-d6e7-11e4-9837-b8e85646e742",
      "options": {
      },
      "created_at": "2015-03-30T14:17:02Z",
      "updated_at": "2015-04-16T22:33:09Z",
      "service_type": "unknown",
      "service_template_catalog_id": 6
    }
  ]
}
```

### Deleting Multiple Service Templates

#### Request:

    POST /api/service_templates

``` json
{
  "action" : "delete",
  "resources" : [
    { "href" : "https://hostname/api/service_templates/4" },
    { "href" : "https://hostname/api/service_templates/5" }
  ]
}
```

#### Response:

``` json
{
  "results": [
    {
      "success": true,
      "message": "service_templates id: 4 deleting",
      "href": "https://hostname/api/service_templates/4"
    },
    {
      "success": true,
      "message": "service_templates id: 5 deleting",
      "href": "https://hostname/api/service_templates/5"
    }
  ]
}
```

## Containers

This section provides examples of how to interact with containers.

### Scanning Containers

Scan containers using SmartState Analysis.

<div class="note">

  - Scanning containers requires enabling the SmartProxy server role.
    See
    [Servers](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.6/html-single/general_configuration/#servers)
    in the *General Configuration Guide* for information on server
    roles.

  - Attached OpenSCAP policies do not affect responses.

</div>

#### Request:

    POST /api/container_images/440

``` json
{
  "action": "scan"
}
```

#### Response:

``` json
{
"success": true,
"message": "ContainerImage id:440 name:'cbud_test_cont' scanning",
"task_id": "2133",
"task_href": "https://<hostname>/api/tasks/2133",
"href": "https://<hostname>/api/container_images/440"
}
```

## Datastores

This section provides examples of how to interact with datastores.

### Deleting Datastores

#### Request:

    POST /api/data_stores

``` json
{
  "action" : "delete",
  "resources" : [
    { "href" : "https://hostname/api/data_stores/7" },
  ]
}
```

#### Response:

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

#### Request:

``` json
GET /api/tasks/1
```

#### Response:

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
