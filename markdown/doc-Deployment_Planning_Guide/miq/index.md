# Introduction to ManageIQ

ManageIQ delivers the insight, control, and automation that enterprises
need to address the challenges of managing virtual environments. This
technology enables enterprises with existing virtual infrastructures to
improve visibility and control, and those starting virtualization
deployments to build and operate a well-managed virtual infrastructure.

ManageIQ provides the following feature sets:

  - Insight: Discovery, Monitoring, Utilization, Performance, Reporting,
    Analytic, Chargeback, and Trending.

  - Control: Security, Compliance, Alerting, and Policy-Based Resource,
    and Configuration Enforcement.

  - Automate: IT Process, Task and Event, Provisioning, and Workload
    Management and Orchestration.

  - Integrate: Systems Management, Tools and Processes, Event Consoles,
    Configuration Management Database (CMDB), Role-based Administration
    (RBA), and Web Services.

## Architecture

The diagram below describes the capabilities of ManageIQ. Its features
are designed to work together to provide robust management and
maintenance of your virtual infrastructure. ![1845](images/1845.png)

The architecture comprises the following components:

  - The ManageIQ appliance (appliance) which is supplied as a secure,
    high-performance, preconfigured virtual machine. It provides support
    for HTTPS communications.

  - The ManageIQ Server (Server) resides on the appliance. It is the
    software layer that communicates between the SmartProxy and the
    Virtual Management Database. It includes support for HTTPS
    communications.

  - The Virtual Management Database (VMDB) resides either on the
    appliance or another computer accessible to the appliance. It is the
    definitive source of intelligence collected about your Virtual
    Infrastructure. It also holds status information regarding appliance
    tasks.

  - The ManageIQ Console (Console) is the Web interface used to view and
    control the Server and appliance. It is consumed through Web 2.0
    mash-ups and web services (WS Management) interfaces.

  - The SmartProxy can reside on the appliance or on an ESX Server. If
    not embedded in the Server, the SmartProxy can be deployed from the
    appliance. A SmartProxy agent must configured in each storage
    location, and must be visible to the appliance. The SmartProxy acts
    on behalf of the appliance communicating with it over HTTPS on
    standard port 443.

## Requirements

To use ManageIQ, certain virtual hardware, database, and browser
requirements must be met in your environment.

### Virtual Hardware Requirements

The ManageIQ appliance requires the following virtual hardware at
minimum:

  - 4 VCPUs

  - 12 GB RAM

  - 44 GB HDD + optional database disk

### Database Requirements

Red Hat recommends allocating the virtual machine disk fully at the time
of creation. Three main factors affect the size of your database over
time:

  - Virtual Machine Count: the most important factor in the calculation
    of virtual machine database (VMDB) size over time.

  - Host Count: the number of hosts associated with the provider.

  - Storage Count: the number of individual storage elements as seen
    from the perspective of the provider or host. It is not the total
    number of virtual disks for all virtual machines.

Use the following table as a guideline to calculate minimum requirements
for your database:

![5780](images/5780.png)

<div class="note">

When enabling capacity and utilization for metrics gathering over a
period of time, it is recommended that the VMDB size scale accordingly.
Evaluate the number of instances in your provider inventory and storage
duration requirements to plan for increased VMDB sizing requirements.

</div>

Use the following information to plan for your increased VMDB needs when
working with metrics gathering:

  - Realtime metrics data are stored for 4 hours.

  - Rollup metrics data are stored for 6 months.

**Example**:

|                                 |                        |                                                                                   |                                                                                                |
| ------------------------------- | ---------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
|                                 | **Minute**             | **Hour**                                                                          | **Day**                                                                                        |
| **OpenStack Provider Instance** | **3** Realtime Metrics | **181** (3 records \* 60 minutes = 180 Realtime Metrics + 1 hourly Rollup Metric) | **4,345** (3 records \* 60 minutes \* 24 hours =4320 Realtime Metrics + 1 daily Rollup Metric) |

  - Metrics data storage times can be configured by editing the Advanced
    Settings.

### Browser Requirements

To use ManageIQ, the following browser requirements must be met:

  - One of the following web browsers:
    
      - Mozilla Firefox for versions supported under Mozilla’s Extended
        Support Release (ESR)
    
      - Internet Explorer 10 or higher
    
      - Google Chrome for Business

  - A monitor with minimum resolution of 1280x1024.

<div class="important">

Due to browser limitations, Red Hat supports logging in to only one tab
for each multi-tabbed browser. Console settings are saved for the active
tab only. For the same reason, ManageIQ does not guarantee that the
browser’s **Back** button will produce the desired results. Red Hat
recommends using the breadcrumbs provided in the Console.

</div>

### Additional Requirements

Additionally, the following must be configured to use ManageIQ:

  - The ManageIQ appliance must already be installed and activated in
    your enterprise environment.

  - The SmartProxy must have visibility into the virtual machines and
    cloud instances that you want to control.

  - For more information, see
    [SmartProxies](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.2/html-single/general_configuration/#smartproxies)
    in the ManageIQ *General Configuration* guide.

## Terminology

The following terms are used throughout the documentation. Review them
before proceeding.

  - Account Role  
    The level of access a user has to different parts and functions of
    the ManageIQ console. There are a variety of Account Roles, which
    can be assigned to users to restrict or allow access to parts of the
    console and virtual infrastructure.

  - Action  
    An execution that is performed after a condition is evaluated.

  - Alert  
    ManageIQ alerts notify administrators and monitoring systems of
    critical configuration changes and threshold limits in the virtual
    environment. The notification can take the form of either an email
    or an SNMP trap.

  - Analysis Profile  
    A customized scan of hosts, virtual machines, or instances. You can
    collect information from categories, files, event logs, and registry
    entries.

  - Cloud  
    A pool of on-demand and highly available computing resources. The
    usage of these resources are scaled depending on the user
    requirements and metered for cost.

  - ManageIQ Appliance  
    A virtual machine where the virtual management database (VMDB) and
    ManageIQ reside.

  - ManageIQ Console  
    A web-based interface into the ManageIQ appliance.

  - ManageIQ Role  
    A designation assigned to a ManageIQ server that defines what a
    ManageIQ server can do.

  - ManageIQ Server  
    The application that runs on the ManageIQ appliance and communicates
    with the SmartProxy and the VMDB.

  - Cluster  
    Hosts that are grouped together to provide high availability and
    load balancing.

  - Condition  
    A control policy test triggered by an event, which determines a
    subsequent action.

  - Discovery  
    Process run by the ManageIQ server which finds virtual machine and
    cloud providers.

  - Drift  
    The comparison of a virtual machine, instance, host, cluster to
    itself at different points in time.

  - Event  
    A trigger to check a condition.

  - Event Monitor  
    Software on the ManageIQ appliance which monitors external providers
    for events and sends them to the ManageIQ server.

  - Host  
    A computer running a hypervisor, capable of hosting and monitoring
    virtual machines. Supported hypervisors include RHV-H, VMware ESX
    hosts, Windows Hyper-V hosts.

  - Instance/Cloud Instance  
    A on-demand virtual machine based upon a predefined image and uses a
    scalable set of hardware resources such as CPU, memory, networking
    interfaces.

  - Managed/Registered VM  
    A virtual machine that is connected to a host and exists in the
    VMDB. Also, a template that is connected to a provider and exists in
    the VMDB. Note that templates cannot be connected to a host.

  - Managed/Unregistered VM  
    A virtual machine or template that resides on a repository or is no
    longer connected to a provider or host and exists in the VMDB. A
    virtual machine that was previously considered registered may become
    unregistered if the virtual machine was removed from provider
    inventory.

  - Provider  
    An external management system that ManageIQ integrates in order to
    collect data and perform operations.

  - Policy  
    A combination of an event, a condition, and an action used to manage
    a virtual machine.

  - Policy Profile  
    A set of policies.

  - Refresh  
    A process run by the ManageIQ server which checks for relationships
    of the provider or host to other resources, such as storage
    locations, repositories, virtual machines, or instances. It also
    checks the power states of those resources.

  - Regions  
    A region is the collection of zones that share the same database for
    reporting and charting. A master region may be added to synchronize
    multiple VMDBs into one VMDB for higher-level reporting, providing a
    "single pane of glass" view.

  - Resource  
    A host, provider, instance, virtual machine, repository, or
    datastore.

  - Resource Pool  
    A group of virtual machines across which CPU and memory resources
    are allocated.

  - Repository  
    A place on a datastore resource which contains virtual machines.

  - SmartProxy  
    The SmartProxy is a software agent that acts on behalf of the
    ManageIQ appliance to perform actions on hosts, providers, storage
    and virtual machines.

:: The SmartProxy can be configured to reside on the ManageIQ appliance
or on an ESX server version. The SmartProxy can be deployed from the
ManageIQ appliance, and provides visibility to the VMFS storage. Each
storage location must have a SmartProxy with visibility to it. The
SmartProxy acts on behalf of the ManageIQ appliance. If the SmartProxy
is not embedded in the ManageIQ server, it communicates with the
ManageIQ appliance over HTTPS on standard port 443.

  - SmartState Analysis  
    Process run by the SmartProxy which collects the details of a
    virtual machine or instance. Such details include accounts, drivers,
    network information, hardware, and security patches. This process is
    also run by the ManageIQ server on hosts and clusters. The data is
    stored in the VMDB.

  - SmartTags  
    Descriptors that allow you to create a customized, searchable index
    for the resources in your clouds and infrastructure.

  - Storage Location  
    A device, such as a VMware datastore, where digital information
    resides that is connected to a resource.

  - Tags  
    Descriptive terms defined by a ManageIQ user or the system used to
    categorize a resource.

  - Template  
    A template is a copy of a preconfigured virtual machine, designed to
    capture installed software and software configurations, as well as
    the hardware configuration, of the original virtual machine.

  - Unmanaged Virtual Machine  
    Files discovered on a datastore that do not have a virtual machine
    associated with them in the VMDB. These files may be registered to a
    provider that the ManageIQ server does not have configuration
    information on. Possible causes may be that the provider has not
    been discovered or that the provider has been discovered, but no
    security credentials have been provided.

  - Virtual Machine  
    A software implementation of a system that functions similar to a
    physical machine. Virtual machines utilize the hardware
    infrastructure of a physical host, or a set of physical hosts, to
    provide a scalable and on-demand method of system provisioning.

  - Virtual Management Database (VMDB)  
    Database used by the ManageIQ appliance to store information about
    your resources, users, and anything else required to manage your
    virtual enterprise.

  - Virtual Thumbnail  
    An image in the web interface representing a resource, such as a
    provider or a virtual machine, showing the resource’s properties at
    a glance. Each virtual thumbnail is divided into quadrants, which
    provide information about the resource, such as its software and
    power state.

  - Worker Appliance  
    A ManageIQ appliance dedicated to a role other than user interface
    or database.

  - Zones  
    ManageIQ Infrastructure can be organized into zones to configure
    failover and to isolate traffic. Zones can be created based on your
    environment. Zones can be based on geographic location, network
    location, or function. When first started, new servers are put into
    the default zone.

# Planning

This guide provides some general guidelines to planning a deployment on
ManageIQ. This includes creating multiple regions containing ManageIQ
appliances, CPU sizing recommendations, database sizing recommendations,
and database configuration.

## Regions

Regions are used for centralizing data which is collected from public
and private virtualization environments. A region is ultimately
represented as a single database for the VMDB. Regions are particularly
useful when multiple geographical locations need to be managed, as they
enable all the data collection to happen at each particular location and
avoid data collection traffic across slow links between networks.

When multiple regions are being used, each with their own unique ID, a
master region can be created to centralize the data of all the children
regions into a single master database. To do this, configure each child
region to replicate its data to the master region database (Red Hat
recommends use of region 99, though any number up to three digits will
work). This parent and child region is a one-to-many relationship.

Regions can contain multiple zones, which in turn contain appliances.
Zones are used for further segregating network traffic along with
enabling failover configurations. Each appliance has the capability to
be configured for a number of specialized server roles. These roles are
limited to the zone containing the appliance they run on.

Only one failover type of each server role can run in a zone. If
multiple appliances have the same failover role, the extras are used as
backups that activate only if the primary appliance fails. Non-failover
server roles can run on multiple appliances simultaneously in a zone, so
resources can be adjusted according to the workload those roles are
responsible for.

The following diagram demonstrates an example of the multiple regions
working together in a ManageIQ environment.

![7151](images/7151.png)

The master appliance is located in Chicago and contains a master region
and a subregion that manages the worker appliances. The Mahwah
technology center contains a single subregion that manages two zones.
Likewise, the San Diego technology center contains a single subregion
managing a single zone.

<div class="note">

  - Replicating a parent region to a higher-level parent is not
    supported.

  - Parent regions can be configured after the child regions are online.

</div>

The following diagram provides a closer look at a region:

![7150](images/7150.png)

In this region, we have several ManageIQ appliances acting as UI nodes
and worker nodes. These worker nodes execute tasks on the providers in
your environment. The region also uses a region database that reports to
a master database on the main ManageIQ appliance. All appliances can
connect to the authentication services (Active Directory, LDAP, Identity
Management), outgoing mail (SMTP), and network services (SNMP).

<div class="note">

ManageIQ can be configured in a highly available setup. In this case,
all PostgreSQL instances must be running on a server that is deployed
from the ManageIQ appliance. High availability is achieved by database
replication between two or more database servers.

</div>

## Roles

Server roles define what a server can do. Assigning different server
roles to appliances can allow them to focus on specific functions. When
planning a deployment, consider which roles to assign to each appliance.
Some server roles are enabled by default in ManageIQ. Many server roles
start worker processes.

Some roles are also dependent on other roles. For example, because the
ManageIQ user interface relies on the API for access, the Web Services
role must be enabled with the User Interface role for users to log in to
the appliance. See [Server
Roles](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html/general_configuration/configuration#server-roles)
in *General Configuration* for details on each server role and its
function.

### Appliance Types

Depending on the needs of your environment, you may choose to separate
worker and database tasks between appliances. One example of this is to
implement a highly available configuration so that certain appliances
are running the PostgreSQL database and providing failover. For more
details about configuring high availability, see the [*High Availability
Guide*](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/high_availability_guide/).

The following provides a summary of types of appliances:

| Appliance Type                | Database | Workers | Description                                                                                                                                                                                                                                                      |
| ----------------------------- | -------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| VMDB appliance                | Yes      | Yes     | Worker processes are running, and it also hosts its own database that other appliances can connect to.                                                                                                                                                           |
| Non-database appliance        | No       | Yes     | Worker processes are running on the appliance, but it does not host a database. The appliance is connected to an external database.                                                                                                                              |
| Dedicated-database appliance  | Yes      | No      | This appliance contains no worker processes, only a database for other appliances to connect to.                                                                                                                                                                 |
| Non-ManageIQ VM with database | Yes      | No      | This appliance contains no worker processes, only a database. As this is not a ManageIQ appliance, you cannot run any ManageIQ `rake` tasks on it. This appliance must be migrated using a non-database appliance that is pointed at it, using it as a database. |

Appliance types

## Centralized Administration

ManageIQ includes centralized administration capabilities, where certain
operations can be initiated from the global region and processed and
executed on remote regions. From the global region, you can also access
the user interfaces of virtual machines residing in remote regions.

The following life cycle management operations can be initiated from the
global region using centralized administration:

  - Virtual machine provisioning

  - Virtual machine power operations

  - Virtual machine retirement

  - Virtual machine reconfiguration

  - Service provisioning

  - Service retirement

  - Opening a virtual machine in the remote region

<div class="note">

ManageIQ life cycle operations other than those listed above are not
supported. Centralized administration capabilities are not supported
from the Self Service user interface.

</div>

With centralized administration, the remote\_queue\_put leverages a new
system-to-system REST API request to forward the original request to the
remote region. This request is put in the local queue in the remote
region, which is then delivered by a worker in the remote region as if
it was queued there all along. As a result, a ManageIQ operator in the
global region can be seen as provisioning on behalf of a remote region.

![Centralized Administration Diagram](images/centralized_admin.png)

<div class="note">

The operations initiated from the global region are subject to the
role-based access control (RBAC) rules on the remote region. The user in
the remote region which matches the logged-in user’s **user ID** will be
used to enforce RBAC in the target region. The operation will fail on
the remote system if the user does not have the required permissions.

</div>

In this version of ManageIQ, configuring database replication
automatically enables centralized configuration, eliminating the need
for further configuration.

## Tenancy

ManageIQ supports multitenancy. Tenants can be totally separate or they
can be in a parent-child or peer relationship. Tenants in a relationship
can share or inherit a certain configuration. You can subdivide and
create child tenants and they, in turn, can have child tenants, and so
on. The ability to have multi-level (nested) tenants in a hierarchy
enables those at the bottom to inherit permissions from those above.
This configuration allows for granular user permissions to be set on
specific tenants.

A tenant can also contain a self-contained child tenant known as a
*project*. A project cannot have a child tenant, but is useful for
allocating resources to a small group or team within a larger
organization.

<div class="note">

If you do not add any additional tenants, all resources and user
accounts are contained in a single base tenant which is your ManageIQ
appliance itself. In ManageIQ, is sometimes referred as *tenant zero*.

</div>

**Tenancy Account Roles.**

In ManageIQ, the following two account roles are associated with
tenancy:

  - Tenant administrator

  - Tenant quota administrator

<div class="important">

Tenant administrator and tenant quota administrator roles are like
administrator and super administrator. These roles are not limited to
the tenant upon which they are acting and act across all tenants, and
therefore should be considered privileged users. These are not roles
inside a tenant.

</div>

**Tenancy Models.**

The following two approaches exist for tenancy planning:

  - **Tenantless** - You can create a single large tenant, sometimes
    referred as *tenant zero*, and perform all your operations in there
    without any subdivision of resources or user accounts.

  - **Enterprise model** - A common scenario is to create a single
    tenant, and then subdivide it based on the structures or departments
    within your organization. Those departments are then able to further
    subdivide their resources into distinct projects. With this model,
    you have a single URL for user access, while still having the
    ability to divide resources into nested hierarchical tenants.

**Tenancy Configuration.**

You can create and configure tenancy using the ManageIQ user interface
in the same place you set up users, groups and roles by selecting
**Configuration** from the settings menu, and then clicking on the
**Access Control** accordion.

**Tenancy in Automation.**

One of the features of tenancy is that each tenant can have its own
automate domain. Tenant-based domains can help in several use cases,
such as if you have:

  - groups that need their own naming routines

  - varying types of approval needs

  - departments that use different end ticketing systems

  - a customer who is a holding company or centralized IT organization
    for managing different business units

Just like standard domains are nested, you can also add automate domains
that are nested at the tenant level.

**Tenancy Quota and Reporting.**

You can allocate and enforce quotas for the following attributes:

  - Virtual CPUs

  - Memory in GB

  - Storage in GB

  - Number of virtual machines

  - Number of templates

You can generate or schedule a report for **Tenant Quotas** similar to
other reports.

<div class="note">

Currently, in tenant quota reports you will see all of the tenants but
there is no nesting information available by parent and child tenants.

</div>

**Example:.**

In the following example of a tenant quota report, *DevOps Teams* is a
parent tenant and *Team Alpha* and *Team Bravo* are child tenants.

![tenant quotas report](images/tenant-quotas-report.png)

  - Total Quota: Total quota enforced per attribute for a tenant

  - In Use: Amount of quota currently in use by tenants

  - Allocated: Amount of quota given to all child tenants

  - Available: *Total Quota* minus (-) *In Use* minus (-) *Allocated*

**Tenancy Chargeback.**

You have the ability to do tenancy in chargeback where you are able to
assign rates and have a different rate for each tenant. You can make use
of the default rate or create your own set of rates depending on the
tenant. As well, there is an ability to create chargeback reports by
tenant.

**Tenancy Service Catalogs.**

Similar to automate domains, you can have service catalogs at each level
of tenancy. Once you add a service catalog at a particular level of
tenancy, it is visible to that tenant and its children (unless you use
tagging to exclude).

**Tenancy Providers.**

Providers can be added at any level of tenancy. Once added, a provider
is visible to any child or lower tenants, making it possible to easily
separate resources that are owned or accessed by one group, and should
not be available to other tenants.

**Tenancy Relationships and Properties.**

The tenant summary page found in <span class="menuchoice">Configuration
\> Access Control \> Tenants \> *Tenant*</span> provides detailed
information about the tenant and its relationships including:

  - Catalog items and bundles

  - Automate domains

  - Provider relationships

## Using a Load Balancer

Deploying multiple user interface worker appliances and placing them
behind a third-party load balancer allows for redundancy and improved
performance. This requires extra configuration in both the load balancer
and in the ManageIQ user interface worker appliances.

### Configuring the Load Balancer

  - Configure the load balancer to use sticky sessions. This ensures
    that when a session is started, all requests for that session are
    sent to the same worker appliance.

  - Configure the load balancer to test for connectivity using the
    ManageIQ ping response page: `https://appliance_name/ping`. The
    expected reply from the appliance is the text string *pong*. Using
    this URL is preferable to the appliance login URL as it does not
    establish a connection to the database.

### Configuring Worker Appliances for Load Balancing

When using a load balancer, configure appliances that have the **User
Interface** role enabled to store session data in the database. As a
result, the user does not need to re-login if the load balancer
redirects them to an alternative server in the case the original user
interface worker is unresponsive.

On each appliance, configure the session data storage location using the
`session_store` parameter within the advanced settings page in the
ManageIQ user interface:

1.  Click ![config gear](images/config-gear.png) (**Configuration**).

2.  Click the **Advanced** tab.

3.  Change the `session_store` parameter to `sql` in the following line
    (the default parameter is `cache`):
    
        :server:
        ...
         :session_store: sql

4.  Click **Save**.

<div class="important">

Configure the `session_store` parameter to point to `sql` on each user
interface appliance behind the load balancer.

</div>

## Database Configuration

This section describes the ManageIQ PostgreSQL database configuration.
The below table provides information on each file: its location, primary
function, and notes regarding behavior or recommendations.

| File                    | Location                          | Description                                              | Note                                                                  |
| ----------------------- | --------------------------------- | -------------------------------------------------------- | --------------------------------------------------------------------- |
| `postgresql.conf`       | Data Directory                    | Default server configuration                             | Adds directive to include `/etc/manageiq/postgresql.conf.d` directory |
| `postgresql.auto.conf`  | Data Directory                    | Contains configuration set by the `ALTER SYSTEM` command | **Do not edit manually**                                              |
| `01_miq_overrides.conf` | `/etc/manageiq/postgresql.conf.d` | Contains ManageIQ default overrides                      | Overwritten on upgrades                                               |
| \<other files\>         | `/etc/manageiq/postgresql.conf.d` | Contains user overrides                                  | Takes precedence if alphabetically after `01_miq_overrides.conf`      |

Database files

### User Overrides

Store custom configurations, or user overrides, in
`/etc/manageiq/postgresql.conf.d`. Name the user override file so that
it follows `01_miq_overrides.conf` alphabetically. This ensures custom
configurations are not overwritten on ManageIQ upgrades.

The following file name example follows `01_miq_overrides.conf`
alphabetically in the `/etc/manageiq/postgresql.conf.d` directory:

**Example.**

    test_miq_overrides.conf

### Reading Configuration Settings

Query the ManageIQ PostgreSQL database directly to read configuration
settings. See the [PostgreSQL
Documentation](https://www.postgresql.org/docs/9.5/index.html) for more
information.

The following example queries the ManageIQ for current value set for
`max_wal_senders`:

**Example.**

    `psql -d vmdb_production -c 'show max_wal_senders'

# Capacity Planning

## Capacity and Utilization Collection

ManageIQ server can collect and analyze capacity and utilization data
from your virtual infrastructure. Use this data to understand the
limitations of your current environment and plan for growth.

For some capacity and utilization data, ManageIQ calculates and shows
trend lines in the charts. Trend lines are created using linear
regression, which is calculated using the capacity and utilization data
collected by ManageIQ during the interval you specify for the chart. The
more data you have the better the predictive value of the trend line.

There are three server roles associated with the collection and metric
creation of capacity and utilization.

  - The Capacity & Utilization Coordinator role checks to see if it is
    time to collect data, somewhat like a scheduler. If it is time, a
    job is queued for the Capacity & Utilization Data Collector. The
    Coordinator role is required to complete capacity and utilization
    data collection. If more than one server in a specific zone has this
    role, only one will be active at a time.

  - The Capacity & Utilization Data Collector performs the actual
    collection of capacity and utilization data. This role has a
    dedicated worker, and there can be more than one server with this
    role in a zone.

  - The Capacity & Utilization Data Processor processes all of the data
    collected, allowing ManageIQ to create charts. This role has a
    dedicated worker, and there can be more than one server with this
    role in a zone.

## Assigning the Capacity and Utilization Server Roles

1.  Click **Configuration**, then select the server to configure from
    <span class="menuchoice">Settings \> Zone</span> in the accordion
    menu on the left.

2.  Navigate to the **Server Roles** list in the
    <span class="menuchoice">Server \> Server Control</span> section.
    From there, set the required capacity and utilization roles to
    **ON**, namely:
    
    1.  **Capacity & Utilization Coordinator**
    
    2.  **Capacity & Utilization Data Collector**
    
    3.  **Capacity & Utilization Data Processor**

3.  Click **Save**.

Data collection is enabled immediately. However, the first collection
begins 5 minutes after the server is started, and every 10 minutes after
that. Therefore, the longest the collection takes after enabling the
Capacity & Utilization Collector role is 10 minutes. The first
collection from a particular provider may take a few minutes since
ManageIQ is gathering data points going one month back in time.

<div class="note">

In addition to setting the server role, you must also select which
clusters and datastores to collect data for. For more information, see
the *General Configuration* guide. You must have super administrator
rights to edit these settings.

</div>

## Adding Database Credentials for Data Collection

After creating the new user, add the user’s credentials to the settings
for the provider.

1.  From <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>, select an infrastructure provider to update its
    settings.

2.  Click ![1847](images/1847.png)**Configuration**, and then
    ![1851](images/1851.png)**Edit Selected Infrastructure Provider**.

3.  In the **Credentials** area, click **C & U Database**.

4.  Type in the credentials for the new database user you created.

5.  Click **Save**.

6.  Restart the Capacity and Utilization Data Collector.

## Data Collection for Red Hat Virtualization

To collect capacity and utilization data for Red Hat Virtualization
(RHV), you must add a user to the RHV-M history database for ManageIQ to
use.

Perform this procedure on the PostgreSQL server where the history
database (ovirt\_engine\_history) is located. Usually, this is the RHV-M
server.

1.  Using SSH, access the RHV-M database server as the root user:
    
        $ ssh root@example.postgres.server

2.  Switch to the postgres user:
    
        # su - postgres
    
    <div class="important">
    
    For RHV 4.2, the PostgreSQL database is delivered as a software
    collection in version 9.5 and must be enabled first. Therefore, to
    run the following psql commands, you will need to enable the
    *rh-postgresql95* collection and load into the current shell prompt
    using the source command:
    
    $ source /opt/rh/rh-postgresql95/enable
    
    </div>

3.  Create the user for ManageIQ to be granted read-only access to the
    history database:
    
        $ psql -U postgres -c "CREATE ROLE cfme WITH LOGIN ENCRYPTED PASSWORD '[password]';" -d ovirt_engine_history

4.  Grant the newly created user permission to connect to the history
    database:
    
        $ psql -U postgres -c "GRANT CONNECT ON DATABASE ovirt_engine_history TO cfme;"

5.  Grant the newly created user usage of the public schema:
    
        $ psql -U postgres -c "GRANT USAGE ON SCHEMA public TO cfme;" ovirt_engine_history

6.  Generate the rest of the permissions that will be granted to the
    newly created user and save them to a file:
    
        $ psql -U postgres -c "SELECT 'GRANT SELECT ON ' || relname || ' TO cfme;' FROM pg_class JOIN pg_namespace ON pg_namespace.oid = pg_class.relnamespace WHERE nspname = 'public' AND relkind IN ('r', 'v', 'S');" --pset=tuples_only=on  ovirt_engine_history > grant.sql

7.  Use the file you created in the previous step to grant permissions
    to the newly created user:
    
        $ psql -U postgres -f grant.sql ovirt_engine_history

8.  Remove the file you used to grant permissions to the newly created
    user:
    
        $ rm grant.sql

9.  Exit to the RHV-M database server prompt:
    
        $ exit

10. Update the server’s firewall to accept TCP communication on port
    5432:
    
        # firewall-cmd --add-port=5432/tcp --permanent

11. Enable external md5 authentication.
    
    1.  For RHV 4.0 and RHV 4.1, update the following line in
        `/var/lib/pgsql/data/pg_hba.conf` as shown below:
        
            host    all      all    0.0.0.0/0     md5
    
    2.  For RHV 4.2, update the following line in
        `/var/opt/rh/rh-postgresql95/lib/pgsql/data/pg_hba.conf` as
        shown below:
        
            host    all      all    0.0.0.0/0     md5

12. Enable PostgreSQL to listen for remote connections.
    
    1.  For RHV 4.0 and RHV 4.1, ensure the `listen_addresses` line in
        `/var/lib/pgsql/data/postgresql.conf` is as shown below:
        
            listen_addresses  =  '*'
    
    2.  For RHV 4.2, ensure the `listen_addresses` line in
        `/var/opt/rh/rh-postgresql95/lib/pgsql/data/postgresql.conf` is
        as shown below:
        
            listen_addresses  =  '*'

13. Reload the PostgreSQL configuration.
    
    1.  For RHV 4.0 and RHV 4.1:
        
            # systemctl reload postgresql
    
    2.  For RHV 4.2:
        
            # systemctl reload rh-postgresql95-postgresql

## Data Collection for Red Hat Enterprise Linux OpenStack Platform

Before you can collect data from a Red Hat Enterprise Linux OpenStack
Platform (RHEL-OSP) provider, you must install Ceilometer and configure
it to accept queries from external systems.

These instructions require a Red Hat Enterprise Linux 6.4 @base
installation of RHEL-OSP and registration to a satellite that has access
to both the `RHEL-OSP` and `RHEL Server Optional` channels. Perform all
steps on your RHEL-OSP system.

1.  Add the required channels and update your system:
    
        # rhn-channel --add -c rhel-x86_64-server-6-ost-3 -c rhel-x86_64-server-optional-6
        # yum update -y
        # reboot

2.  Install `Ceilometer`:
    
        # yum install *ceilometer*

3.  Install and start the MongoDB store:
    
        # yum install mongodb-server
        # sed -i '/--smallfiles/!s/OPTIONS=\"/OPTIONS=\"--smallfiles /' /etc/sysconfig/mongod
        # service mongod start

4.  Create the following users and roles:
    
        # SERVICE_TENANT=$(keystone tenant-list | grep services | awk '{print $2}')
        # ADMIN_ROLE=$(keystone role-list | grep ' admin ' | awk '{print $2}')
        # SERVICE_PASSWORD=servicepass
        # CEILOMETER_USER=$(keystone user-create --name=ceilometer \
        --pass="$SERVICE_PASSWORD" \
        --tenant_id $SERVICE_TENANT \
        --email=ceilometer@example.com | awk '/ id / {print $4}')
        # RESELLER_ROLE=$(keystone role-create --name=ResellerAdmin | awk '/ id / {print $4}')
        # ADMIN_ROLE=$(keystone role-list | awk '/ admin / {print $2}')
        # for role in $RESELLER_ROLE $ADMIN_ROLE ; do
        keystone user-role-add --tenant_id $SERVICE_TENANT \
        --user_id $CEILOMETER_USER --role_id $role
        done

5.  Configure the authtoken in `ceilometer.conf`:
    
        # openstack-config --set /etc/ceilometer/ceilometer.conf keystone_authtoken auth_host 127.0.0.1
        # openstack-config --set /etc/ceilometer/ceilometer.conf keystone_authtoken auth_port 35357
        # openstack-config --set /etc/ceilometer/ceilometer.conf keystone_authtoken auth_protocol http
        # openstack-config --set /etc/ceilometer/ceilometer.conf keystone_authtoken admin_tenant_name services
        # openstack-config --set /etc/ceilometer/ceilometer.conf keystone_authtoken admin_user ceilometer
        # openstack-config --set /etc/ceilometer/ceilometer.conf keystone_authtoken admin_password $SERVICE_PASSWORD

6.  Configure the user credentials in `ceilometer.conf`:
    
        # openstack-config --set /etc/ceilometer/ceilometer.conf DEFAULT os_auth_url http://127.0.0.1:35357/v2.0
        # openstack-config --set /etc/ceilometer/ceilometer.conf DEFAULT os_tenant_name services
        # openstack-config --set /etc/ceilometer/ceilometer.conf DEFAULT os_password $SERVICE_PASSWORD
        # openstack-config --set /etc/ceilometer/ceilometer.conf DEFAULT os_username ceilometer

7.  Start the Ceilometer services:
    
        # for svc in compute central collector api ; do
          service openstack-ceilometer-$svc start
          done

8.  Register an endpoint with the service catalog. Replace
    `$EXTERNALIFACE` with the IP address of your external interface:
    
        # keystone service-create --name=ceilometer \
        --type=metering --description="Ceilometer Service"
        # CEILOMETER_SERVICE=$(keystone service-list | awk '/ceilometer/ {print $2}')
        # keystone endpoint-create \
        --region RegionOne \
        --service_id $CEILOMETER_SERVICE \
        --publicurl "http://$EXTERNALIFACE:8777/" \
        --adminurl "http://$EXTERNALIFACE:8777/" \
        --internalurl "http://localhost:8777/"

9.  Enable access to Ceilometer from external systems:
    
        # iptables -I INPUT -p tcp -m multiport --dports 8777 -m comment --comment "001 ceilometer incoming" -j ACCEPT
        # iptables save

10. Confirm the status of OpenStack and the Ceilometer services:
    
        # openstack-status
        # for svc in compute central collector api ; do
          service openstack-ceilometer-$svc status
          done

11. Verify Ceilometer is working correctly by authenticating as a user
    with instances running, for example `admin`. Pipe the sample for the
    CPU meter to count lines, and confirm that the value changes
    according to the interval specified in
    `/etc/ceilometer/pipeline.yaml`. The default interval is 600
    seconds.
    
        # . ~/keystonerc_admin
        # ceilometer sample-list -m cpu |wc -l

12. Add the configured OpenStack provider to ManageIQ. See Managing
    Providers After adding the provider, capacity and utilization data
    for your instances populate in a few minutes.

## Capacity and Utilization Data Collected

ManageIQ generates charts from the collected data which can be used to
plan your hardware and virtual machine needs. Depending on the type of
data, these charts may include lines for averages, maximums, minimums,
and trends.

<div class="note">

For reporting of daily capacity and utilization data, incomplete days
(days with less than 24 hourly data points from midnight to midnight)
that are at the beginning or end of the requested interval are excluded.
Days with less than 24 hourly data points would be inaccurate and
including them would skew trend lines. Therefore, at least one full day
of hourly data from midnight to midnight is necessary for displaying the
capacity and utilization charts under the
<span class="menuchoice">Compute \> Infrastructure</span> tab.

</div>

### Capacity and Utilization Charts for Hosts, Clusters, and Virtual Machines

| Resource Type   | CPU Usage | CPU States | Disk I/O | Memory Usage | Network I/O | Running VMS | Running Hosts |
| --------------- | --------- | ---------- | -------- | ------------ | ----------- | ----------- | ------------- |
| Host            | Y         | Y          | Y        | Y            | Y           | Y           | NA            |
| Cluster         | Y         | Y          | Y        | Y            | Y           | Y           | Y             |
| Virtual Machine | Y         | Y          | Y        | Y            | Y           | NA          | NA            |

Capacity and Utilization Charts for Hosts, Clusters, and Virtual
Machines

### Capacity and Utilization Charts for Datastores

Charts created include:

| Space by VM Type     | Virtual Machines and Hosts |
| -------------------- | -------------------------- |
| Used Space           | Number of VMs by Type      |
| Disk files Space     | Hosts                      |
| Snapshot Files Space | Virtual Machines           |
| Memory Files Space   |                            |
| Non-VM Files         |                            |
| Used Disk Space      |                            |

Capacity and Utilization Charts for Datastores

## Capacity and Utilization Chart Features

Capacity and utilization charts for host, clusters, virtual machines,
and datastore provides its own set of special features including zooming
in on a chart and shortcut menus.

### Zooming into a Chart

1.  Navigate to the chart you want to zoom. If you hover anywhere on the
    chart, two dashed lines will appear to target a coordinate of the
    chart.

2.  Click ![2251](images/2251.png)(**Click to zoom in**) in the lower
    left corner of the chart to zoom into it.

3.  To go back to the regular view click
    ![2252](images/2252.png)(**Click to zoom out**) on the enlarged
    chart.

### Drilling into Chart Data

1.  Navigate to the chart you want to get more detail from.

2.  Hover over a data point to see the coordinates.

3.  Click on a data point to open a shortcut menu for the chart. In this
    example, we can use the shortcut menu to go to the hourly chart or
    display the virtual machines that were running at the time the data
    was captured.
    
      - If you are viewing the **CPU**, **Disk**, **Memory**, or
        **Network** charts, selecting from the **Chart** option will
        change all of the charts on the page to the new interval
        selected.
    
      - If you are viewing the **CPU**, **Disk**, **Memory**, or
        **Network** charts, selecting from the **Display** option will
        allow you to drill into the virtual machines or **Hosts** that
        were running at the time.
    
      - If you are viewing the **VM** or **Hosts** chart, the
        **Display** menu will allow you to view running or stopped
        virtual machines. The time of the data point will be displayed
        in addition to the virtual machines that apply. From here, click
        on a virtual machine to view its details.
