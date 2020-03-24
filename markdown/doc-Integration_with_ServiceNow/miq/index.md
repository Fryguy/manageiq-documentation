# Overview

ManageIQ integration with ServiceNow enables authentication with an
existing ServiceNow database and **add/amend** items in the ServiceNow
database during state machine processing, such as the virtual machine
provisioning state machine. Note that information in this guide assumes
you have credentials and access to a ServiceNow database instance.

The following new namespace and class delivers support for the
management of **ServiceNow Configuration Management Database** (CMDB)
records using **ServiceNow’s RESTful** web service.

    /RedHat/Integration/ServiceNow/CMDB

You can manage records in the **CMDB\_CI\_SERVER** table, including
`create`, `update`, and/or `delete`. The following methods are included:

| Method        | Action                                                                    |
| ------------- | ------------------------------------------------------------------------- |
| create        | Create record in specified ServiceNow table.                              |
| delete        | Delete record in specified ServiceNow table.                              |
| get           | Get record from specified ServiceNow table and list its attributes.       |
| get\_all      | Get all records in ServiceNow and list attributes.                        |
| update        | Get specified record, update required attributes and post updated record. |
| update\_patch | Post required attributes to specified record.                             |

<div class="note">

Configuration item (CI) and record are used interchangeably and refer to
items in a ServiceNow database table.

</div>

# Configuring ServiceNow Connection

Configure the connection to the ServiceNow database by specifying the
credentials in the **CMDB schema** or instances within.

The following methods are included:

|                |                                                         |
| -------------- | ------------------------------------------------------- |
| snow\_server   | ServiceNow database IP address or resolvable hostname.  |
| snow\_user     | ServiceNow user account with the necessary permissions. |
| snow\_password | Associated user account password.                       |

The table name cannot be changed unless there is a specific requirement
to manage records elsewhere. Entries in this table appear in the
<span class="menuchoice">Configuration \> Base Items \> Servers</span>
menu in the ServiceNow web user interface.

|             |                                             |
| ----------- | ------------------------------------------- |
| table\_name | ServiceNow cmdb\_ci\_server database table. |

# Managing Record Attributes

You can specify any attribute via the **URI** or **CMDB** class
instance. If neither exists, the value is determined from the ManageIQ
**VM** or **miq\_provision** objects.

The attributes can be reduced or extended as required by amending the
Ruby methods.

<div class="note">

Some attributes are not free-text (variable) fields, that is, they must
be specific values. For example, the `vendor` value must already exist
in the ServiceNow Vendor table beforehand.

</div>

## Create and Update (\_patch) Record

You can use the following attributes when creating and/or updating a
record.

### Attribute

|                    |                                                   |
| ------------------ | ------------------------------------------------- |
| Attribute          | Value                                             |
| virtual            | Boolean true or false, set to true.               |
| name VMs           | Virtual infrastructure name.                      |
| short\_description | ManageIQ virtual machine GUID.                    |
| host\_name         | The virtual machine’s operating system hostname.  |
| cpu\_count         | The virtual machine’s CPU count.                  |
| ram                | The virtual machine’s memory.                     |
| vendor             | The virtual machine’s hardware vendor (provider). |
| sys\_id \[1\]      | ServiceNow record unique system ID.               |

## Get and Delete Record

You can use the following attribute for getting or deleting a record.

|           |                                     |
| --------- | ----------------------------------- |
| Attribute | Value                               |
| sys\_id   | ServiceNow record unique system ID. |

## Get All Records

There are no attributes required to get all records. This method gets
all records in the specified **ServiceNow table** and writes their
attributes to `automation.log`.

# Use Cases

The following examples show how ServiceNow can be integrated with
automation workflows.

## Provisioning a Virtual Machine from a Template

The Cloud and Infrastructure **Provision VM from Template** State
Machines contain **RegisterCMDB** and **ActivateCMDB** states.

To create a new ServiceNow record during virtual machine provisioning,
amend the **ActiveCMDB** state to call the `create` method, for example:

    /Integration/ServiceNow/CMDB/create

![StateActiveCMDBActiveCMDBstate](images/6667.png)

## Virtual Machine Retirement

The Cloud and Infrastructure default **Retirement** State Machines
contain the **DeactivateCMDB** state.

To update a virtual machine’s ServiceNow record during virtual machine
retirement, amend the **DeactivateCMDB** state to call the
`update_patch` method, for example:

    Integration/ServiceNow/CMDB/update_patch?description=VM%20${/#vm.guid}%20retired%20from%20{productname_short}

![StateActiveCMDBDeactiveCMDBstate](images/6668.png)

## Virtual Machine Reconfiguration (VMware Only)

Create a new **System Event** instance to update the ServiceNow record
after a virtual machine reconfiguration request has been approved and
completed.

Create a new **/System/Event/ReconfigVM\_Task\_Complete** instance with
a relationship value:

    /Integration/ServiceNow/CMDB/update_patch

![ReconfigVMTaskComplete](images/6670.png)

1.  sys\_id attribute is not required during `create`. Its value is
    returned from the `create` request and the ManageIQ object custom
    attribute **servicenow\_sys\_id** is created and updated.
