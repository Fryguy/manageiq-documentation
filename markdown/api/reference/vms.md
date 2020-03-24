# Vm Management

Management of Virtual Machines adds support of the following actions:

| Action                | Description                              |
| --------------------- | ---------------------------------------- |
| start                 | Starts a VM                              |
| stop                  | Stops a VM                               |
| suspend               | Suspends a VM                            |
| refresh               | Refreshes a VM                           |
| reset                 | Resets a VM                              |
| reboot\_guest         | Reboots guest in VM                      |
| shutdown\_guest       | Shuts down guest in VM                   |
| scan                  | Scans a VM (Perform SmartState Analysis) |
| set\_miq\_server      | Sets the server of a VM                  |
| set\_owner            | Sets the owner of a VM                   |
| add\_event            | Adding an Event to a VM                  |
| add\_lifecycle\_event | Add a Lifecycle Event to a VM            |
| edit                  | Edits a VM                               |
| delete                | Deletes a VM in the Appliance            |

  - [Targeting VMs](#targeting-vms)

  - [Querying VMs](#querying-vms)

  - [Starting a VM](#start-vm)

  - [Stopping a VM](#stop-vm)

  - [Suspending a VM](#suspend-vm)

  - [Refreshing a VM](#refresh-vm)

  - [Resets a VM](#reset-vm)

  - [Reboots guest in VM](#reboot-guest-vm)

  - [Shuts down guest in VM](#shutdown-guest-vm)

  - [Scanning a VM](#scan-vm)

  - [Setting Server of a VM](#set-miq-server-vm)

  - [Setting Owner of a VM](#set-owner-vm)

  - [Adding an Event to a VM](#add-event-vm)

  - [Adding a Lifecycle Event to a VM](#add-lifecycle-event-vm)

  - [Editing a VM](#edit-vm)

  - [Deleting a VM](#delete-vm)

## Targeting VMs

These actions can be triggered on individual vm resources:

``` data
/api/vms/:id
```

As simply as POSTing the following action to a VM.

``` json
{
  "action" : "start"
}
```

Requests can also be made on multiple vms by targetting the primary
collection:

``` data
/api/vms
```

``` json
{
  "action" : "start",
  "resources" : [
    { "href" : "http://localhost:3000/api/vms/11" },
    { "href" : "http://localhost:3000/api/vms/12" },
    ...
  ]
}
```

## Querying VMs

Virtual Machines are queried via the primary collection URL:

``` data
/api/vms
```

Filtering, sorting and paging as mentioned on the
[Querying](../overview/query.html) page.

When querying vms, expanding the resources themselves as well as the
following subcollections:

|          |
| -------- |
| accounts |
| software |

For example:

    GET /api/vms?expand=resources,accounts,software

Or querying and individual vm

    GET /api/vms/:id?expand=accounts,software

## Starting a VM

``` json
{
  "action" : "start"
}
```

## Stopping a VM

``` json
{
  "action" : "stop"
}
```

## Suspending a VM

``` json
{
  "action" : "suspend"
}
```

## Refreshing a VM

``` json
{
  "action" : "refresh"
}
```

## Resetting a VM

``` json
{
  "action" : "reset"
}
```

## Rebooting guest in VM

``` json
{
  "action" : "reboot_guest"
}
```

## Shuts down guest in VM

``` json
{
  "action" : "shutdown_guest"
}
```

## Scanning a VM

``` json
{
  "action" : "scan"
}
```

## Setting Server of a VM

``` json
{
  "action" : "set_miq_server",
  "resource" : {
    "miq_server" : { "href" : "http://localhost:3000/api/servers/5" }
  }
}
```

``` json
{
  "action" : "set_miq_server",
  "resource" : {
    "miq_server" : { "id" : "6" }
  }
}
```

To remove the Server from the VM, pass in an empty reference as follows:

``` json
{
  "action" : "set_miq_server",
  "resource" : {
    "miq_server" : {}
  }
}
```

## Setting Owner of a VM

``` json
{
  "action" : "set_owner",
  "resource" : {
    "owner" : "admin"
  }
}
```

## Adding an Event to a VM

``` json
{
  "action" : "add_event",
  "resource" : {
    "event_type" : "...",
    "event_message" : "...",
    "event_time" : "UTC Time"
  }
}
```

<div class="note">

event\_time above is optional. If skipped, current time will be used.

</div>

## Adding a Lifecycle Event to a VM

``` json
{
  "action" : "add_lifecycle_event",
  "resource" : {
    "event" : "...",
    "status" : "...",
    "message" : "...",
    "created_by" : "..."
  }
}
```

## Editing a VM

Basic information of VMs can be edited. This includes the following:

| VM Info           | Attribute                                            |
| ----------------- | ---------------------------------------------------- |
| description       | description                                          |
| custom attributes | custom\_1 …​ custom\_9                               |
| parent resource   | parent\_resource - resource href reference           |
| child resources   | child\_resources - array of resource href references |

VM resources can be edited as follows:

``` data
POST /api/vms/:id
```

``` json
{
  "action" : "edit",
  "resource" : {
    "description" : "Updated VM Description",
    "custom_1" : "custom_attribute_1",
    "parent_resource" : { "href" : "http://localhost:3000/api/vms/11" },
    "child_resources" : [
      { "href" : "http://localhost:3000/api/vms/101" },
      { "href" : "http://localhost:3000/api/vms/102" },
      { "href" : "http://localhost:3000/api/vms/103" },
      { "href" : "http://localhost:3000/api/vms/104" }
    ]
  }
}
```

VMs can also be edited in Bulk as follows:

``` data
POST /api/vms
```

``` json
{
  "action" : "edit",
  "resources" : [
    {
      "href" : "http://localhost:3000/api/vms/11",
      "custom_9" : "vm_class_a"
    },
    {
      "href" : "http://localhost:3000/api/vms/12",
      "custom_9" : "vm_class_a"
    },
    {
      "href" : "http://localhost:3000/api/vms/13",
      "custom_9" : "vm_class_a"
    }
  ]
}
```

## Deleting a VM

``` json
{
  "action" : "delete"
}
```

Or simply doing the following:

    DELETE /api/vms/:id

Additional VM Management examples can be found on the main REST API
Examples section.
