# 

ManageIQ can manage a variety of external environments, known as
providers and managers. A provider or manager is any system that
ManageIQ integrates with for the purpose of collecting data and
performing operations.

In ManageIQ, a *provider* is an external virtualization, cloud, or
containers environment that manages multiple virtual machines or
instances residing on multiple hosts. One example is Red Hat
Virtualization, a platform that manages multiple hosts and virtual
machines.

In ManageIQ, a *manager* is an external management environment that
manages more than one type of resource. One example of a manager is
OpenStack, which manages infrastucture, cloud, network, and storage
resources.

This guide covers working with providers and managers in ManageIQ, which
include:

  - Infrastructure providers

  - Configuration management providers

  - Automation management providers

  - Cloud providers

  - Networking management providers

  - Container providers

  - Storage managers

For information on working with the resources contained by a provider or
manager, see *Managing Infrastructure and Inventory*.

# Infrastructure Providers

In ManageIQ, an infrastructure provider is a virtual infrastructure
environment that you can add to a ManageIQ appliance to manage and
interact with the resources in that environment. This chapter describes
the different types of infrastructure providers that you can add to
ManageIQ, and how to manage them. Infrastructure providers can be either
discovered automatically by ManageIQ, or added individually.

The web interface uses virtual thumbnails to represent infrastructure
providers. Each thumbnail contains four quadrants by default, which
display basic information about each provider:

![2189](images/2189.png)

1.  Number of hosts

2.  Management system software

3.  Currently unused

4.  Authentication status

| Icon                     | Description                                                                    |
| ------------------------ | ------------------------------------------------------------------------------ |
| ![2190](images/2190.png) | Validated: Valid authentication credentials have been added.                   |
| ![2191](images/2191.png) | Invalid: Authentication credentials are invalid.                               |
| ![2192](images/2192.png) | Unknown: Authentication status is unknown or no credentials have been entered. |

Provider authentication status

## Discovering Infrastructure Providers

In addition to individually adding providers, you can also discover
infrastructure providers in a given subnet range.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Discover Infrastructure Providers](images/1942.png)
    (**Discover Infrastructure Providers**).

3.  Select the infrastructure provider to discover.

4.  Provide a **Subnet Range**. Enter the **From Address** and **To
    Address** of the address range.

5.  Click **Start**.

The appliance searches for all infrastructure providers in the specified
subnet range, and adds them to the user interface. However, before you
can manage providers added via discovery, you must edit each provider
and specify authentication details.

## Discovering Physical Infrastucture Providers

In addition to discovering virtual infrastructure providers, ManageIQ
has the ability to discover physical infrastructure providers in a given
subnet range.

1.  Navigate to <span class="menuchoice">Compute \> Physical
    Infrastructure \> Providers</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Discover Physical Infrastructure Providers](images/1942.png)
    (**Discover Physical Infrastructure Providers**).

3.  Select the provider in **Discovery Type**.

4.  Provide a **Subnet Range**. Enter the **From Address** and **To
    Address** of the address range.

5.  Enter a **Port**.

6.  Click **Start**.

The appliance searches for all physical infrastructure providers in the
specified subnet range, and adds them to the user interface. However,
before you can manage providers added via discovery feature, you must
edit each provider to enter authentication details.

## Red Hat Virtualization Providers

To use a Red Hat Virtualization provider, add it to the appliance and
authenticate its hosts. You can also configure capacity and utilization
data collection to help track usage and find common issues.

### Enabling Red Hat Virtualization Capacity and Utilization Data Collection

Configure the following to collect capacity and utilization data from a
Red Hat Virtualization provider:

  - In ManageIQ, enable the capacity and utilization server roles from
    the settings menu, in <span class="menuchoice">Configuration \>
    Server \> Server Control</span>. For more information on capacity
    and utilization collection, see [Assigning the Capacity and
    Utilization Server
    Roles](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/deployment_planning_guide/#assigning_the_capacity_and_utilization_server_roles)
    in the *Deployment Planning Guide*.

  - For information on selecting clusters and datastores used to collect
    data, see [Capacity and Utilization
    Collections](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/general_configuration/#capacity-and-utilization-collections)
    in the *General Configuration Guide*.

  - In your Red Hat Virtualization environment, install the Data
    Warehouse and Reports components, and create a ManageIQ user in the
    Data Warehouse database:
    
      - To install the Data Warehouse and Reports components in a Red
        Hat Virtualization environment, see the [Data Warehouse
        Guide](https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.1/html/data_warehouse_guide/).
    
      - To create a ManageIQ user in the Data Warehouse database, see
        [Data Collection for Red Hat Enterprise
        Virtualization](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/deployment_planning_guide/#data_collection_for_rhev_33_34)
        in the *Deployment Planning Guide*.

### Adding a Red Hat Virtualization Provider

After initial installation and creation of a ManageIQ environment, add a
Red Hat Virtualization provider to the appliance.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Add a New Infrastructure Provider](images/1862.png) (**Add a
    New Infrastructure Provider**).

3.  Enter a **Name** for the provider.

4.  Select **Red Hat Virtualization** from the **Type** list.

5.  Select the appropriate **Zone** for the provider. If you do not
    specify a zone, it is set to **default**.

6.  Under **Endpoints** in the **Default** tab, configure the following:
    
      - Enter the **Hostname** or IPv4 or IPv6 address of the Red Hat
        Virtualization Manager.
        
        <div class="important">
        
        The **Hostname** must be a unique fully qualified domain name.
        
        </div>
    
      - Enter the **API Port** if your provider uses a non-standard port
        for access.
    
      - Select **Yes** or **No** to **Verify TLS Certificates** to
        specify whether to authenticate securely to the provider using
        TLS.
        
          - If you select **Yes** for **Verify TLS Certificates**, you
            can either paste a custom certificate in the **Trusted CA
            Certificates** field in PEM format, or leave the **Trusted
            CA Certificates** field empty if your Red Hat Virtualization
            provider has a trusted Certificate Authority.
    
      - Provide the login credentials for the Red Hat Virtualization
        administrative user:
        
          - Enter the user name (formatted as `admin@internal`) in the
            **Username** field.
        
          - Enter the password in the **Password** field.
        
          - Confirm the password in the **Confirm Password** field.
        
          - Click **Validate** to confirm ManageIQ can connect to the
            Red Hat Virtualization Manager.

7.  Under **Endpoints** in the **C & U Database** tab, you can configure
    capacity and utilization metrics collection by providing login
    credentials for the ManageIQ user of the Red Hat Virtualization Data
    Warehouse database. You can also configure this later by editing the
    provider. Configure the following in the **C & U Database** tab:
    
    <div class="important">
    
    To collect capacity and utilization data from a Red Hat
    Virtualization provider, the capacity and utilization server roles
    must be enabled in ManageIQ. The Red Hat Virtualization environment
    must also contain the Data Warehouse and Reports components and a
    ManageIQ user. Specific clusters, hosts, and datastores can also be
    configured for collection. See [Enabling Red Hat Virtualization
    Capacity and Utilization Data Collection](#enabling_CU_RHV) for
    configuration details.
    
    </div>
    
      - Enter the database hostname or IPv4 or IPv6 address in
        **Hostname**.
    
      - Enter the **API Port** if your provider uses a non-standard port
        for access.
    
      - Enter the **Database Name**.
    
      - Enter the database user name in the **Username** field.
    
      - Enter the user password in the **Password** field.
    
      - Confirm the user password in the **Confirm Password** field.
    
      - Click **Validate** to confirm ManageIQ can connect to the
        database.

8.  Click **Add** to finish adding the Red Hat Virtualization provider.

### Authenticating Red Hat Virtualization Hosts

After adding a Red Hat Virtualization infrastructure provider, you must
authenticate its hosts to enable full functionality.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click on a provider to display its summary screen.

3.  On the summary screen, click **Hosts** in the **Relationships**
    information box to display the hosts on that provider.

4.  Select the hosts to authenticate. You can select all hosts using the
    **Check All** option.

5.  Click ![Configuration](images/1847.png) (**Configuration**).

6.  Click ![Edit this item](images/1851.png) (**Edit this item**).

7.  In the **Credentials** area, enter credentials for the following, as
    required:
    
    1.  **Default**: This field is mandatory. Users should have
        privileged access such as, root or administrator.
    
    2.  **Remote Login**: Credentials for this field are required if SSH
        login is disabled for the **Default** account.
    
    3.  **Web Services**: This tab is used for access to Web Services in
        Red Hat Virtualization.
    
    4.  **IPMI**: This tab is used for access to IPMI.

8.  Click **Validate**.

9.  If editing multiple hosts:
    
    1.  Select a host from the **Select Host to validate against** list.
    
    2.  If required, enter credentials for **Remote Login**, **Web
        Services**, and **IPMI** in their respective tabs; click
        **Validate**.
    
    3.  Select another host to validate each of these credentials
        against.

10. Click **Add**.

## OpenStack Infrastructure Providers

Enable an OpenStack Infrastructure provider by adding it to the
appliance.

### Adding an OpenStack Infrastructure Provider

After initial installation and creation of a ManageIQ environment, add
an OpenStack infrastructure provider to the appliance. ManageIQ supports
operating with the OpenStack `admin` tenant. When creating an OpenStack
infrastructure provider in ManageIQ, select the OpenStack infrastructure
provider’s `admin` user because it is the default administrator of the
OpenStack `admin` tenant. When using the `admin` credentials, a user in
ManageIQ provisions into the `admin` tenant, and sees images, networks,
and instances that are associated with the `admin` tenant.

<div class="note">

  - You can set whether ManageIQ should use the Telemetry service or
    Advanced Message Queueing Protocol (AMQP) for event monitoring. If
    you choose Telemetry, you should first configure the **ceilometer**
    service on the undercloud to store events. See [Configuring the
    Undercloud to Store Events](#openstack-events-uc) for instructions.
    For more information, see [OpenStack Telemetry
    (ceilometer)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/architecture_guide/#comp-telemetry)
    in the Red Hat OpenStack Platform *Architecture Guide*.

  - To authenticate the provider using a self-signed Certificate
    Authority (CA), configure the ManageIQ appliance to trust the
    certificate using the steps in [Using a Self-Signed CA
    Certificate](#app-self_signed_CA) before adding the provider.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Add a New Infrastructure Provider](images/1862.png) (**Add a
    New Infrastructure Provider**).

3.  Enter the **Name** of the provider to add. The **Name** is how the
    device is labeled in the console.

4.  Select **OpenStack Platform Director** from the **Type** list.

5.  Select the **API Version** of your OpenStack provider’s Keystone
    service from the list. The default is `Keystone v2`.
    
    <div class="note">
    
      - With Keystone API v3, domains are used to determine
        administrative boundaries of service entities in OpenStack.
        Domains allow you to group users together for various purposes,
        such as setting domain-specific configuration or security
        options. For more information, see [OpenStack Identity
        (keystone)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/architecture_guide/#comp-identity)
        in the Red Hat OpenStack Platform *Architecture Guide*.
    
      - The provider you are creating will be able to see projects for
        the given domain only. To see projects for other domains, add it
        as another cloud provider. For more information on domain
        management in OpenStack, see [Domain
        Management](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/users_and_identity_management_guide/#Domains)
        in the Red Hat OpenStack Platform *Users and Identity Management
        Guide*.
    
    </div>

6.  Select the appropriate **Zone** for the provider. By default, the
    zone is set to **default**.
    
    <div class="note">
    
    For more information, see the definition of host aggregates and
    availability zones in [OpenStack Compute
    (nova)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/architecture_guide/components#comp-compute)
    in the Red Hat OpenStack Platform *Architecture Guide*.
    
    </div>

7.  In the **Default** tab, under **Endpoints**, configure the host and
    authentication details of your OpenStack provider:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the provider:
        
          - **SSL without validation**: Authenticate the provider
            insecurely using SSL.
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option. This is the recommended authentication
            method.
        
          - **Non-SSL**: Connect to the provider insecurely using only
            HTTP protocol, without SSL.
    
    2.  Enter the **Host Name or IP address(IPv4 or IPv6)** of the
        provider. If your provider is an undercloud, use its hostname
        (see [Setting the Hostname for the
        System](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/director_installation_and_usage/#sect-Setting_the_Hostname_for_the_System)
        in Red Hat OpenStack Platform *Director Installation and Usage*
        for more details)
    
    3.  In **API Port**, set the public port used by the OpenStack
        Keystone service. By default, OpenStack uses port 5000 for
        non-SSL security protocol. For SSL, API port is 13000 by
        default.
    
    4.  In the **Username** field, enter the name of an OpenStack user
        with privileged access (for example, **admin**). Then, provide
        its corresponding password in the **Password** and **Confirm
        Password** fields.
    
    5.  Click **Validate** to confirm ManageIQ can connect to the
        OpenStack provider.

8.  Next, configure how ManageIQ should receive events from the
    OpenStack provider. Click the **Events** tab in the **Endpoints**
    section to start.
    
      - To use the Telemetry service of the OpenStack provider, select
        **Ceilometer**. Before you do so, the provider must first be
        configured accordingly. See [Configuring the Undercloud to Store
        Events](#openstack-events-uc) for details.
    
      - If you prefer to use the AMQP Messaging bus instead, select
        **AMQP**. When you do: In **Hostname (or IPv4 or IPv6 address)**
        (of the **Events** tab, under **Endpoints**), enter the public
        IP or fully qualified domain name of the AMQP host.
        
          - In the **API Port**, set the public port used by AMQP. By
            default, OpenStack uses port 5672 for this.
        
          - In the **Username** field, enter the name of an OpenStack
            user with privileged access (for example, **admin**). Then,
            provide its corresponding password in the **Password**
            field.
        
          - Click **Validate** to confirm the credentials.

9.  You can also configure SSH access to all hosts managed by the
    OpenStack infrastructure provider. To do so, click on the **RSA key
    pair** tab in the **Endpoints** section.
    
    1.  From there, enter the **Username** of an account with privileged
        access.
    
    2.  If you selected **SSL** in **Endpoints \> Default \> Security
        Protocol** earlier, use the **Browse** button to find and set a
        private key.

10. Click **Add** after configuring the infrastructure provider.

<div class="note">

ManageIQ requires that the `adminURL` endpoint for all OpenStack
services be on a non-private network. Accordingly, assign the adminURL
endpoint an IP address of something other than `192.168.x.x`. The
`adminURL` endpoint must be accessible to the ManageIQ appliance that is
responsible for collecting inventory and gathering metrics from the
OpenStack environment. Additionally, all the Keystone endpoints must be
accessible, otherwise refresh will fail.

</div>

#### Configuring the Undercloud to Store Events

To allow ManageIQ to receive events from a Red Hat OpenStack Platform
environment, you must configure the **notification\_driver** option for
the Compute service and Orchestration service in that environment. See
[Installing the
Undercloud](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/director_installation_and_usage/#chap-Installing_the_Undercloud)
and [Configuring the
Director](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/director_installation_and_usage/#sect-Configuring_the_Director)
in Red Hat OpenStack Platform *Director Installation and Usage* for
related details.

### Discovering OpenStack Infrastructure Providers

ManageIQ has the ability to discover OpenStack infrastructure providers.
In this process, ManageIQ scans a network segment and searches for the
Bare Metal (Ironic) service which runs on port `6385` by default. Note
that, currently, the discovery does not work if the Bare Metal service
has been moved to a different port.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Discover Infrastructure Providers](images/1942.png)
    (**Discover Infrastructure Providers**).

3.  Select **OpenStack Infrastructure** under **Discover**.

4.  Provide a **Subnet Range**. Enter the **From Address** and **To
    Address** of the address range.

5.  Click **Start**.

## VMware vCenter Providers

To use a VMware vCenter provider, add it to the appliance and
authenticate its hosts.

### Adding a VMware vCenter Provider

After initial installation and creation of a ManageIQ environment, add a
VMware vCenter provider to the appliance.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Add a New Infrastructure Provider](images/1862.png) (**Add a
    New Infrastructure Provider**).

3.  Enter the **Name** of the provider to add. The **Name** is how the
    device is labeled in the console.

4.  Select **VMware vCenter** from the **Type** list.

5.  Enter the **Host Name or IP address(IPv4 or IPv6)** of the provider.
    
    <div class="important">
    
    The **Host Name** must use a unique fully qualified domain name.
    
    </div>

6.  Select the appropriate **Zone** for the provider. By default, the
    zone is set to **default**.

7.  In the **Credentials** area, under **Default**, provide the login
    credentials required for the VMware vCenter administrative user:
    
      - Enter the user name in the **Username** field.
    
      - Enter the password in the **Password** field.
    
      - Confirm the password in the **Confirm Password** field.
    
      - Click **Validate** to confirm ManageIQ can connect to the VMware
        vCenter.

8.  Click **Add**.

#### Using a Non-Administrator Account for vCenter Hosts

After adding a VMware vCenter infrastructure provider, you must
authenticate its hosts to enable full functionality. You can use
administrator credentials, or create another user assigned to a role
created for ManageIQ. See the [VMware
documentation](https://www.vmware.com/support/pubs/vsphere-esxi-vcenter-server-pubs.html)
for instructions on how to create a role.

The following privileges should be enabled for the non-administrator
user:

From the Global group, check:

  - Cancel task

  - Diagnostics

  - Log Event

  - Set custom attribute

  - Settings

Check the entire set of privileges for the following groups:

  - Alarms

  - Datastores

  - dvPort Group

  - Host

  - Network

  - Resource

  - Scheduled Task

  - Tasks

  - Virtual Machine

  - vSphere Distributed Switch

Additionally, you must assign the new role to the following objects:

  - **Datacenter**: At the Datacenter the ManageIQ user/group must have
    at least the read-only role at the Datacenter level (Not Propagated)
    to be able to see the datacenter. Without this access, relationships
    cannot be made. Specifically, the datastores will not show up.

  - **Cluster**: Each Cluster that the ManageIQ needs access to must
    have the new role assigned and propagated.

  - **Folders**: Each Folder that ManageIQ needs access to must have the
    new role assigned and propagated.

  - **Datastores**: Each Datastore that ManageIQ needs access to must
    have the new role assigned and propagated.

  - **Networking**: Each vLAN or Port Group that ManageIQ needs access
    to must have the new role assigned and propagated.

### Authenticating VMware vCenter Hosts

The procedure below describes how to authenticate the VMware vCenter
hosts.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click on a provider to display its summary screen.

3.  On the summary screen, click **Hosts** in the **Relationships**
    information box to display the hosts on that provider.

4.  Select the hosts to authenticate. You can select all hosts using the
    **Check All** option.

5.  Click ![Configuration](images/1847.png) (**Configuration**)

6.  Click ![Edit Selected items](images/1851.png) (**Edit Selected
    items**).

7.  In the **Credentials** area, under **Default**, provide the VMware
    ESXi login credentials:
    
      - Enter the user name in the **Username** field.
    
      - Enter the password in the **Password** field.
    
      - Confirm the password in the **Confirm Password** field.
    
      - Click **Validate** to confirm ManageIQ can connect to the VMware
        vCenter host.

8.  If editing multiple hosts, select a host from the **Select Host to
    validate against** list; provide the VMware ESXi login credentials
    and click **Validate**.

9.  Click **Save**.

## Microsoft SCVMM Providers

To use a Microsoft System Center Virtual Machine Manager (SCVMM)
provider, add it to the appliance and set up the SCVMM server for
authentication.

<div class="note">

To use a SCVMM provider, you must have at least one network adapter
available for communication between the host and the SCVMM management
server. Make sure that **Used by Management** is checked for this
network adapter in the SCVMM host properties.

</div>

### Authenticating to Microsoft SCVMM

Before you can add a Microsoft SCVMM provider to your ManageIQ
environment, you must enable WinRM to listen for HTTP traffic on
Microsoft SCVMM servers. You must also set the appropriate execution
policy on the Microsoft SCVMM server to allow PowerShell scripts from
the appliance to run remotely.

1.  Log in to the Microsoft SCVMM server.

2.  Enable WinRM for configuration.
    
        winrm quickconfig

3.  Set the following options:
    
        winrm set winrm/config/client/auth @{Basic="true"}
        winrm set winrm/config/service/auth @{Basic="true"}
        winrm set winrm/config/service @{AllowUnencrypted="true"}

4.  For Windows 2012 R2 with PowerShell 4.0, use the following syntax to
    set these options:
    
        winrm set winrm/config/client/auth '@{Basic="true"}'
        winrm set winrm/config/service/auth '@{Basic="true"}'
        winrm set winrm/config/service '@{AllowUnencrypted="true"}'

5.  Enable remote script execution on the SCVMM server using the
    Set-ExecutionPolicy cmdlet.
    
        Set-ExecutionPolicy RemoteSigned
    
    For more information on SCVMM remote script execution policies, see
    [Using the Set-ExecutionPolicy
    Cmdlet](http://technet.microsoft.com/en-us/library/ee176961.aspx).

If PowerShell returns an error, search for `log_dos_error_results` in
the `evm.log` and `scvmm.log` files for information.

### Adding a Microsoft SCVMM Provider

After initial installation and creation of a ManageIQ environment, add a
Microsoft System Center Virtual Machine Manager (SCVMM) provider to the
appliance.

<div class="note">

To authenticate the provider using a self-signed Certificate Authority
(CA), configure the ManageIQ appliance to trust the certificate using
the steps in [Using a Self-Signed CA Certificate](#app-self_signed_CA)
before adding the provider.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1862](images/1862.png) (**Add a New Infrastructure Provider**).

3.  Enter the **Name** of the provider to add. The **Name** is how the
    device is labeled in the console.

4.  Select **Microsoft System Center VMM** from the **Type** list.

5.  Enter the **Host Name or IP address(IPv4 or IPv6)** of the provider.
    
    <div class="important">
    
    The **Host Name** must use a unique fully qualified domain name.
    
    </div>

6.  Select **Kerberos** or **Basic (SSL)** from the **Security
    Protocol** list.
    
    1.  For **Kerberos**:
        
        1.  Enter the user name and realm in the **Username** field.
        
        2.  Enter the password in the **Password** field.
        
        3.  Enter the password again in the **Confirm Password** field.
    
    2.  For **Basic (SSL)**:
        
        1.  Enter the user name in the **Username** field.
        
        2.  Enter the password in the **Password** field.
        
        3.  Enter the password again in the **Confirm Password** field.

7.  Click **Validate** to confirm that ManageIQ can connect to the
    Microsoft System Center Virtual Machine Manager.

8.  Click **Add**.

## Refreshing Providers

Refresh a provider to find other resources related to it. Use
**Refresh** after initial discovery to get the latest data about the
provider and the virtual machines it can access. Ensure the provider has
credentials to do this. If the providers were added using **Discovery**,
add credentials using ![Edit Selected Infrastructure
Provider](images/1851.png) (**Edit Selected Infrastructure Provider**).

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Select the providers to refresh.

3.  Click ![Configuration](images/1847.png) (Configuration), and then
    ![Refresh Relationships and Power States](images/2003.png)
    (**Refresh Relationships and Power States**).

4.  Click **OK**.

## Tagging Multiple Providers

Apply tags to all providers to categorize them together at the same
time.

1.  Navigate to <span class="menuchoice">Infrastructure \>
    Providers</span>.

2.  Check the providers to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/2158.png) (**Edit Tags**).

4.  In the **Tag Assignment** area, select a customer tag to assign from
    the first list, then select a value to assign from the second list.
    
    ![2194](images/2194.png)

5.  Select more tags as required; click (**Save**).

## Viewing a Provider

From a list of providers, you can review a specific provider by clicking
on it. This displays various options to access provider information.

There are two methods of viewing an infrastructure provider’s details:
the summary screen (default) and the dashboard screen. Use the summary
![Summary](images/Summary.png) and dashboard
![Dashboard](images/Dashboard.png) buttons to toggle between views.

Both the summary and dashboard screens contain a taskbar with
**Reload**, **Configuration**, **Policy**, **Monitoring**, and
**Authentication** buttons to manage the selected provider.

**Provider Summary Screen.**

![providers summary screen](images/providers-summary-screen.png)

The provider summary screen displays information about the provider in
table format.

  - Provider accordion: Displays details about the provider’s
    **Properties** and **Relationships** on the sidebar. Click to expand
    these lists.

  - Provider summary: Displays a provider’s **Properties**, **Status**,
    **Relationships**, and **Smart Management**. Click on an item in the
    **Relationships** table to see more information about that entity.

**Provider Dashboard Screen.**

![providers summary dashboard](images/providers-summary-dashboard.png)

From the dashboard, you can view:

  - Number of clusters, hosts, virtual machines, templates, datastores,
    resource pools, and other entities on the provider. Click on an
    entity to see more information about that item.

  - Aggregate utilization for CPU, memory, and storage

  - Network I/O statistics

  - Trends for hosts and virtual machines discovered

To view the dashboard:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click the infrastructure provider to view.

3.  To access the dashboard view, click
    ![Dashboard](images/Dashboard.png) (**Dashboard view**).

To return to the summary view, click ![Summary](images/Summary.png)
(**Summary view**).

## Removing a Provider

If a provider has been decommissioned or requires some troubleshooting,
it might require deletion from the VMDB.

Deleting a provider removes the account information from ManageIQ
console. You will no longer be able to view any associated history
including chargeback reports generated for the deleted provider.
Additionally, if ManageIQ is the database of record, deleting providers
would become a major problem for the other systems relying on it for
accurate and consistent billing information. Review all the dependencies
carefully before deleting a provider.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Select the check box for the provider to delete.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Remove Infrastructure Providers from the VMDB](images/2098.png)
    (**Remove Infrastructure Providers from the VMDB**).

4.  Click (**OK**).

## Viewing the Provider Timeline

View the timeline of events for the virtual machines registered to a
provider.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click a provider.

3.  Click ![Monitoring](images/1994.png) (**Monitoring**), and then
    ![Timelines](images/1995.png) (**Timelines**)from the taskbar, or
    from the provider accordion, click
    <span class="menuchoice">Properties \> Timeline</span>.

4.  From **Options**, customize the period of time to display and the
    types of events to see.
    
    ![provider timeline](images/provider-timeline.png)
    
      - Use **Show** to select regular Management Events or Policy
        Events.
    
      - Use the **Interval** dropdown to select hourly or daily data
        points.
    
      - Use **Date** to type the date for the timeline to display.
    
      - If you select to view a daily timeline, use **Show** to set how
        many days back to go. The maximum history is 31 days.
    
      - The three **Event Groups** lists allow you to select different
        groups of events to display. Each has its own color.
    
      - From the **Level** list, select a **Summary** event, or a
        **Detail** list of events. For example, the detail level of a
        **Power On** event might include the power on request, the
        starting event, and the actual **Power On** event. If you select
        **Summary**, only the Power On event displays in the timeline.

## Viewing Hosts and Clusters

Access a tree view of the hosts and clusters for a provider from the
**Provider Summary**.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click the provider to view the hosts and clusters.

3.  Click on the **Relationships** accordion, then click **Hosts &
    Clusters**.

![hostsandclusters](images/hostsandclusters.png)

## Viewing Virtual Machines and Templates

Access a tree view of the virtual machines and templates for a provider
from the **Provider Summary**.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click the provider to view the virtual machines and templates.

3.  From accordion menu, click **Relationships**, then click **VMs &
    Templates**.

# Configuration Management Providers

In ManageIQ, a configuration management provider is a systems management
product that you can add to a ManageIQ appliance to manage the lifecycle
of your resources. Configuration management providers are useful for
uniformly applying changes and updates across providers, and for
recording and reporting status and change activity. They can also help
eliminate the confusion and error brought about by the existence of
different providers.

This chapter describes the different types of configuration management
providers available to ManageIQ, and how to manage them. Configuration
management providers must be added individually to ManageIQ.

## Red Hat Satellite 6

Satellite 6 is a subscription and system management tool that provides a
way to provision hosts (both virtual and bare metal) and configure them
using a set of Puppet modules. ManageIQ provides functionality to
integrate with a Red Hat Satellite 6 server and take advantage of its
features. This includes:

  - Monitoring the inventory of your Red Hat Satellite 6 server,
    including independent hosts and hosts provisioned using hostgroups.

  - Reprovisioning existing bare metal system hosts to new host groups.

  - Applying ManageIQ policy tags to hosts.

<div class="important">

ManageIQ only reprovisions existing systems in a Red Hat Satellite 6
environment. Provisioning systems from Red Hat Satellite 6’s bare metal
discovery service is planned for a future release.

</div>

### Defining the Workflow

This section uses the following workflow:

1.  Add Red Hat Satellite 6 server details to ManageIQ.

2.  Refresh the state of your Red Hat Satellite 6 provider in ManageIQ.

3.  Select an existing bare metal host from Red Hat Satellite 6 for
    reprovisioning.

4.  Apply policy tags to Red Hat Satellite 6 hosts.

### Defining the Hostgroup Hierarchy

ManageIQ displays the Red Hat Satellite 6 infrastructure in a host group
and host relationship. A host group defines a set of default values that
hosts inherit when placed in that group. Hosts can belong to only one
host group, but host groups can be nested in hierarchies. You can create
a **"base"** or **"parent"** host group that represents all hosts in
your organization, and then create nested or **"child"** host groups
under that parent to provide specific settings.

### Adding a Satellite 6 Provider

To start provisioning bare metal machines, you need at least one Red Hat
Satelllite 6 provider added to ManageIQ.

1.  Navigate to <span class="menuchoice">Configuration \>
    Management</span>.

2.  Select <span class="menuchoice">Configuration \> Add a new
    Provider</span>.

3.  Enter a **Name** for the provider.

4.  Enter a **URL** for the provider. This is the root URL for the
    Satellite 6 server and can be either an IP address or a hostname.
    For example, *<http://satellite6.example.com>*.

5.  Select **Verify Peer Certificate** to use encrypted communication
    with the provider. This requires the **SSL certificates** from your
    Red Hat Satellite 6 provider.

6.  Enter a **Username** for a user on the provider. Ideally, this would
    be a user in Satellite 6 with administrative access.

7.  Enter a **Password**, and then enter it again in **Confirm
    Password**.

8.  Click **Validate** to test your connection with the Red Hat
    Satellite 6 server.

9.  Click **Add** to confirm your settings and save the provider.

ManageIQ saves the Satellite 6 provider in its database and triggers a
refresh of resources detected in the provider.

### Triggering a Refresh of a Satellite 6 Provider

Your Satellite 6 provider can still create new hosts independently of
ManageIQ. Your ManageIQ appliance detects these changes after an
automatic refresh period. However, you can trigger a manual refresh to
avoid waiting for the automatic refresh.

1.  Navigate to <span class="menuchoice">Configuration \>
    Management</span>.

2.  Select your Red Hat Satellite 6 provider using the checkbox, and
    click <span class="menuchoice">Configuration \> Refresh
    Relationships and Power States</span>. This triggers the refresh.

3.  When the refresh is complete, select the Red Hat Satellite 6
    provider to check the updated list of hosts groups in the provider.

### Displaying Red Hat Satellite 6 Contents

ManageIQ provides two methods for viewing the contents of a Red Hat
Satellite 6 provider:

  - **Providers** - This presents the Red Hat Satellite 6 contents as a
    hierarchy of host groups belonging to a provider, and then
    individual hosts belonging to each provider.

  - **Configured Systems** - This presents a list of all hosts on your
    Red Hat Satellite 6 server. This also provides a method to apply
    predefined filters to organized specific machines.

Change between these two views using the accordion menu on the left of
the user interface.

### Reprovisioning a Bare Metal Host

This procedure provides an example of reprovisioning an existing bare
metal system into a new hostgroup. For this example, your Red Hat
Satellite 6 environment requires the following:

  - An existing bare metal system stored as a host object in your Red
    Hat Satellite 6 server. This system can be one of the following:
    
      - A standalone system previously provisioned without a host group.
    
      - A system previously provisioned using a host group.

  - A target host group. This host group contains the system
    configuration to apply to the host when reprovisioning it. This
    includes:
    
      - A new operating system installation, including a new partition
        table.
    
      - A new networking configuration that the Red Hat Satellite 6
        server defines and manages.
    
      - Registration to any Red Hat subscriptions and repositories
        assigned to the host group.
    
      - Application of any Puppet modules assigned to the host group.

<!-- end list -->

1.  Navigate to <span class="menuchoice">Configuration \>
    Management</span>.

2.  Select **Configured Systems** from the accordion menu on the left.
    This displays the system list.

3.  Select one or more hosts to reprovision.

4.  Select <span class="menuchoice">Lifecycle \> Provision Configured
    Systems</span>.

5.  Under the **Request** tab, enter the following details:
    
    1.  **E-Mail address**
    
    2.  **First Name**
    
    3.  **Last Name**
    
    4.  This form also contains optional fields for users to enter a
        plain text **Note** to inform ManageIQ administrators of any
        special details, and a field to provide a manager’s name in case
        administrators require approval from a user’s manager.

6.  Select the **Purpose** tab and select any ManageIQ policy tags that
    apply to the system.

7.  Select the **Catalog** tab. This screen displays the list of chosen
    machines to reprovision and their current details. Select a **target
    host group** from the **Configuration Profile** list. ManageIQ
    communicates with Red Hat Satellite to apply the configuration from
    this host group to the selected host and reprovision the system.

8.  Select the **Customize** tab. This screen displays some customizable
    fields for the selected system. You can change the **Root Password**
    or change the **Hostname** and **IP Address**. Note that these
    fields are optional, because the host group in Red Hat Satellite 6
    contains this information. The fields here will override the
    settings from the host group.
    
    <div class="important">
    
    Provisioning bare metal systems still requires access to the network
    that Red Hat Satellite 6 manages. This is because Red Hat Satellite
    controls PXE booting, kickstarts, and Puppet configuration for bare
    metal systems. Ensure the IP address you enter in ManageIQ can
    access a DHCP service that Red Hat Satellite 6 provides either
    through the main server or through a Red Hat Satellite 6 Capsule
    server.
    
    </div>

9.  Select the **Customize** tab. This screen allows you to either
    launch the provisioning process immediately on approval or using a
    schedule. Click **Schedule** to show the date and time fields used
    to schedule the provisioning.

10. Click **Submit**.

Depending on the request settings on your ManageIQ appliance, this
provisioning request might require approval from an administrator. If
not, the provisioning request launches depending on your choice for the
schedule.

<div class="note">

Previously provisioned hosts might require manual selection of PXE boot
from the boot menu, otherwise they might boot to hard disk and not
reprovision.

</div>

### Tagging a Bare Metal Host

ManageIQ can also control policy settings of bare metal systems from Red
Hat Satellite 6 through tagging. Tagging attaches levels of metadata to
help define the policy rules required for a set of systems.

1.  Navigate to <span class="menuchoice">Configuration \>
    Management</span>.

2.  Select **Configured Systems** from the accordion menu on the left.
    This displays the system list.

3.  Select one or more hosts to tag.

4.  Select <span class="menuchoice">Policy \> Edit Tags</span>.

5.  Under **Tag Assignment**, select a tag from **Select a customer tag
    to assign** and then choose a value from **Select a value to
    assign**. For example, you can tag this system as located in Chicago
    by selecting `Location` as the tag and `Chicago` as the value. Once
    selected, the user interface automatically adds this tag and value
    to the table below.

6.  Click **Save**.

The bare metal system is now configured with a set of policy tags.

# Automation Management Providers

In ManageIQ, an automation management provider is a management tool that
integrates with ManageIQ to simplify automation operations for your
resources. This chapter describes the automation management providers
that you can use with ManageIQ, and how to work with them.

ManageIQ provides automation management features through the following:

**Automate** enables real-time, bi-directional process integration. This
provides you with a method to implement adaptive automation for
management events and administrative or operational activities.

**Ansible** integration delivers out-of-the-box support for backing
service, alert and policy actions using Ansible playbooks. Sync your
existing playbook repositories with CloudForms, add credentials to
access providers, and create service catalog items for actions ranging
from creating and retiring VMs, updating security software, or adding
additional disks when space runs low.

**Ansible Tower** is a management tool integrated with ManageIQ,
designed to help automate infrastructure operations utilizing existing
Ansible Tower providers in your inventory. ManageIQ allows you to
execute Ansible Tower jobs using service catalogs and Automate. Using
Ansible Tower, you can schedule Ansible playbook runs and monitor
current and historical results, allowing for troubleshooting or
identification of issues before they occur.

## Ansible

Ansible integrates with ManageIQ to provide automation solutions, using
playbooks, for Service, Policy and Alert actions. Ansible playbooks
consist of series of *plays* or tasks that define automation across a
set of hosts, known as the inventory.

Ranging from simple to complex tasks, Ansible playbooks can support
cloud management:

  - **Services** - allow a playbook to back a ManageIQ service catalog
    item.

  - **Control Actions** - ManageIQ policies can execute playbooks as
    actions based on events from providers.

  - **Control Alerts** - set a playbook to launch prompted by a ManageIQ
    alert.

Ansible is built into ManageIQ so there is nothing to install. The basic
workflow when using Ansible in ManageIQ is as follows:

1.  Enable the **Embedded Ansible** server role.

2.  Add a source control repository that contains your playbooks.

3.  Establish credentials with your inventory.

4.  Back your services, alerts and policies using available playbooks.

### Enabling the Embedded Ansible Server Role

In ManageIQ, the **Embedded Ansible** role is disabled by default.
Enable this server role to utilize Ansible Automation Inside.

<div class="note">

Configure your ManageIQ appliance network identity (hostname/IP address)
before enabling the Embedded Ansible server role. Restart the
`evmserverd` service on the appliance with the enabled Embedded Ansible
server role after making any changes to the hostname or IP address.

</div>

1.  Navigate to the settings menu, then **Configuration** →
    **Settings**.

2.  Select the desired server under **Zones**.

3.  Set the **Server Role** for **Embedded Ansible** to **On**.

### Verifying the Embedded Ansible Worker State

Verify that the Embedded Ansible worker has started to utilize its
features.

1.  Navigate to the settings menu, then **Configuration** →
    **Diagnostics** and click on the desired server.

2.  Click on the **Workers** tab.

A table of all workers and current status will appear from which you can
confirm the state of your embedded Ansible worker.

### Adding a Playbook Repository

Add a repository so that ManageIQ can discover and make available your
playbooks.

1.  Navigate to <span class="menuchoice">Automation \> Ansible \>
    Repositories</span>.

2.  Click **Add**.

3.  Provide a Repository Name in the **Name** field.

4.  Add a description for the repository in the **Description** field.

5.  Select an **SCM Type** from the drop-down menu.

6.  Add a **URL** or IP Address for the repository.

7.  Select the appropriate **SCM Credentials** from the drop-down menu.

8.  Provide a branch name in the **SCM Branch** field.

9.  Check the appropriate box for any **SCM Update Options**.

10. Click **Add**.

Once you have synced a repository, its playbooks will become available
to ManageIQ.

### Refreshing Repositories

ManageIQ allows you to refresh a targeted playbook repository or all
repositories in your inventory to ensure your playbooks are current.

Refresh a targeted repository:

1.  Navigate to <span class="menuchoice">Automation \> Ansible \>
    Repositories</span>.

2.  Click on a repository.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Refresh this Repository](images/2003.png) (**Refresh this
    Repository**).

Alternately, you can refresh some or all repositories from the list
view:

1.  Navigate to <span class="menuchoice">Automation \> Ansible \>
    Repositories</span>.

2.  Check those repositories to refresh. Click **Check All** to select
    all repositories.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Refresh Selected Ansible Repositories](images/2003.png) (**Refresh
    Selected Ansible Repositories**).

### Credentials

Credentials are utilized by ManageIQ for authentication when running
Ansible playbooks against machines, synchronizing with inventory
sources, and importing project content from a version control system.

#### Adding Credentials

ManageIQ can store credentials used by playbooks. Credentials saved in
ManageIQ are matched and executed with a playbook when run.

1.  Navigate to <span class="menuchoice">Automation \> Ansible \>
    Credentials</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Add a New Credential](images/1862.png) (**Add a New Credential**).

3.  Provide a **Name** for the credential.

4.  Select the **Credential Type**. Additional fields will appear
    depending on the type chosen.

5.  Click **Add**.

#### Credential Types

Each credential type used by ManageIQ is detailed in the following
sections.

##### Machine

Machine credentials enable ManageIQ to invoke Ansible on hosts under
your management. Just like using Ansible on the command line, you can
specify the SSH username, optionally provide a password, an SSH key, or
a key password. They define SSH and user-level privilege escalation
access for playbooks, and are used when running playbooks on a remote
host.

  - **Username**: The username to be used for SSH authentication.

  - **Password**: The actual password to be used for SSH authentication.

  - **SSH Private Key**: Copy or drag-and-drop the SSH private key for
    the machine credential.

  - **Private Key Passphrase**: If the SSH Private Key used is protected
    by a password, you can configure a Key Password for the private key.

  - **Privilege Escalation**: Specifies the type of escalation privilege
    to assign to specific users. Options include **sudo**, **su**,
    **pbrun**, **pfexec**.

  - **Privilege Escalation Username**: Enter the username to use with
    escalation privileges on the remote system.

  - **Privilege Escalation Password**: Enter the actual password to be
    used to authenticate the user via the selected privilege escalation
    type on the remote system.

  - **Vault Password**: Ansible Vault credentials have only the **Vault
    Password** attribute that may be configured.

<div class="note">

For more information on Ansible Vault, see [Using Vault in
playbooks](http://docs.ansible.com/ansible/latest/playbooks_vault.html).

</div>

##### Network

Network credentials are used by Ansible networking modules to connect to
and manage networking devices.

Network credentials have several attributes that may be configured:

  - **Username**: The username to use in conjunction with the network
    device.

  - **Password**: The password to use in conjunction with the network
    device.

  - **Authorize**: Select this from the Options field to add an
    Authorize password which signs the RSA key with a password.

  - **Authorize password**: If **Authorize** is checked, enter a
    password in the **Authorize Password** field.

  - **SSH Key**: Copy or drag-and-drop the actual SSH Private Key to be
    used to authenticate the user to the network via SSH.

  - **Private key passphrase**: The actual passphrase for the private
    key to be used to authenticate the user to the network via SSH.

##### SCM

SCM (source control) credentials are used with Projects to clone and
update local source code repositories from a remote revision control
system such as Git, Subversion, or Mercurial.

Source Control credentials have several attributes that may be
configured:

  - **Username**: The username to use in conjunction with the source
    control system.

  - **Password**: The password to use in conjunction with the source
    control system.

  - **Private key passphrase**: If the SSH private key used is protected
    by a passphrase, you may configure a key passphrase for the private
    key.

  - **Private Key**: Copy or drag-and-drop the actual SSH Private Key to
    be used to authenticate the user to the source control system via
    SSH.

##### Amazon

Selecting this credential type enables synchronization of cloud
inventory with Amazon Web Services.

  - **Access Key**: User credentials that allow for programmatic calls
    to Amazon Web Services.

  - **Secret Key**: The secret key that corresponds to the user access
    key.

  - **STS Token**: Token generated by Amazon Web Services Security Token
    Service.

##### Azure Classic (deprecated)

Selecting this credential type enables synchronization of cloud
inventory with Microsoft Windows Azure Classic.

Microsoft Azure credentials have several attributes to configure:

  - **Subscription ID**: The Subscription UUID for the Microsoft Azure
    Classic account.

  - **Management Certificate**: The PEM file that corresponds to the
    certificate you uploaded in the Microsoft Azure Classic console.

##### Azure

Selecting this credential type enables synchronization of cloud
inventory with Microsoft Azure.

Microsoft Azure credentials have several attributes to configure:

  - **Username**: The username to use to connect to the Microsoft Azure
    account.

  - **Password**: The password to use to connect to the Microsoft Azure
    account.

  - **Subscription ID**: The Subscription UUID for the Microsoft Azure
    account.

  - **Tenant ID**: The Tenant ID for the Microsoft Azure account.

  - **Client Secret**: The Client Secret for the Microsoft Azure
    account.

  - **Client ID**: The Client ID for the Microsoft Azure account.

##### OpenStack

Selecting this credential type enables synchronization of cloud
inventory with Red Hat OpenStack Platform.

OpenStack credentials have several attributes that may be configured:

  - **Username**: The username to use to connect to OpenStack.

  - **Password (API Key)**: The password or API key to use to connect to
    OpenStack.

  - **Host (Authentication URL)**: The host to be used for
    authentication.

  - **Project (Tenant Name)**: The Tenant name or Tenant ID used for
    OpenStack. This value is usually the same as the username.

  - **Domain name**: The FQDN to be used to connect to OpenStack.

##### Rackspace

Selecting this credential type enables synchronization of cloud
inventory with Rackspace.

Rackspace credentials have the following attributes that may be
configured:

  - **Username**: The username to use to connect to vCenter.

  - **API Key**: The public key related to the administrator ID.

##### Red Hat Virtualization

Selecting this credential type enables synchronization of cloud
inventory with Red Hat Virtualization.

Red Hat Virtualization credentials have several attributes that may be
configured:

  - **Username**: The username to use to connect to Red Hat
    Virtualization.

  - **Password**: The password to use to connect to Red Hat
    Virtualization.

  - **Host (Authentication URL)**: The host to be used for
    authentication.
    
    <div class="important">
    
      - Enter in **Host** the Red Hat Virtualization provider URL,
        followed by the path `/ovirt_engine/api`. Example:
        `https://your.rhv.com/ovirt_engine/api`
    
      - See [Ansible
        Roles](https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.1/html/administration_guide/chap-automating_rhv_configuration_using_ansible#Ansible_Roles)
        for more information on Ansible Roles available for Red Hat
        Virtualization.
    
    </div>

##### Satellite 6

Selecting this credential type enables synchronization of cloud
inventory with Red Hat Satellite 6.

Satellite credentials have several attributes that may be configured:

  - **Username**: The username to use to connect to Satellite 6.

  - **Password**: The password to use to connect to Satellite 6.

  - **Satellite 6 Host**: The Satellite 6 URL or IP address to connect
    to.

##### VMware

Selecting this credential type enables synchronization of inventory with
VMware vCenter.

<div class="important">

If both ManageIQ and a VMware provider are located in the same IPv6-only
network, use a DNS-resolvable hostname for the VMware provider in the
**vCenter Host** field when adding credentials.

</div>

VMware credentials have several attributes that may be configured:

  - **Username**: The username to use to connect to vCenter.

  - **Password**: The password to use to connect to vCenter.

  - **vCenter Host**: The vCenter hostname or IP address to connect to.

<div class="note">

If the VMware guest tools are not running on the instance, VMware
inventory sync may not return an IP address for that instance.

</div>

### Tagging Ansible Playbooks, Repositories, and Credentials

Apply tags to Ansible playbooks, repositories, and credentials to
categorize them. Tagging enables administrators to limit users to view
those Ansible elements that have been enabled for that set of user
permissions.

#### Adding Tags to Ansible Playbooks

1.  Navigate to <span class="menuchoice">Automate \> Ansible \>
    Playbooks</span>.

2.  Select the checkboxes for the Ansible playbooks to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/1851.png) (**Edit Tags**).

4.  Select a customer tag to assign from the first list.
    
    ![2219](images/2219.png)

5.  Select a value to assign from the second list.

6.  Click **Save**.

#### Adding Tags to Ansible Repositories

1.  Navigate to <span class="menuchoice">Automate \> Ansible \>
    Repositories</span>.

2.  Select the checkboxes for the Ansible repositories to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/1851.png) (**Edit Tags**).

4.  Select a customer tag to assign from the first list.
    
    ![2219](images/2219.png)

5.  Select a value to assign from the second list.

6.  Click **Save**.

#### Adding Tags to Ansible Credentials

1.  Navigate to <span class="menuchoice">Automate \> Ansible \>
    credentials</span>.

2.  Select the checkboxes for the Ansible credentials to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/1851.png) (**Edit Tags**).

4.  Select a customer tag to assign from the first list.
    
    ![2219](images/2219.png)

5.  Select a value to assign from the second list.

6.  Click **Save**.

### Optimizing Ansible Playbooks for ManageIQ

Ansible is a simple model-driven configuration management, multi-node
deployment, and remote-task execution system. When designing playbooks
for use with ManageIQ it is helpful to utilize solutions within the
playbook itself to ensure optimal implementation of playbook-backed
services or automated processes.

This section is intended to complement the existing documentation on
Ansible playbooks and guide administrators through optimizing playbooks
for use with ManageIQ.

#### Installing Roles on an Embedded Ansible Appliance

Roles are ways of automatically loading certain variable files, tasks,
and handlers based on a known file structure. Grouping content by roles
also allows easy sharing of roles with other users. Install roles on a
ManageIQ appliance with the Embedded Ansible server role activated to
optimize playbooks.

When using this role in a playbook on a ManageIQ appliance, add an empty
`roles` directory at the root of the playbook. In the `roles` directory,
include a `requirements.yml` file with the following contents:

    ---
    - src: <ansible-galaxy-role>

ManageIQ will automatically install the role once it sees the
`requirements.yml` file in the playbook.

#### Ansible Service Linking

ManageIQ provides a module allowing inventoried resources such as
virtual machines created using Ansible playbooks to link back to the
services used to generate them. During service ordering of a playbook
the `add_provider_vms` module will allow the playbook to connect back to
the worker appliance and identify the provider resources it was
responsible for generating. Once linked, the newly generated resources
are available to ManageIQ’s life cycle management features.

Linking VMs back to the service that created it requires implementing
the following tasks in the playbook used for provisioning:

1.  Create a resource and register it.

2.  Link the service using the `add_provider_vms` method to the newly
    created resource.

##### Example: Linking a virtual machine to a service

In the following playbook task examples, a virtual machine is deployed
to Amazon EC2 and linked back to the service. Examples are provided for
linking the resource to its service by both an *href slug* and as an
object.

<div class="note">

  - This example utilizes the \`syncrou.manageiq-vmdb\`role. This role
    allows ManageIQ users to modify and/or change VMDB objects using an
    Ansible playbook. For information on implementing and utilizing
    roles when writing Ansible playbooks for ManageIQ, see [Installing
    Roles on an Embedded Ansible Appliance](#installing-ansible-roles).

  - For more information on Ansible Galaxy and roles, see the [Ansible
    Galaxy
    documentation](http://docs.ansible.com/ansible/latest/galaxy.html).

  - Note the provider ID in order to successfully link to the service.

</div>

1.  Create and register the resource.
    
        - name: Create Ec2 Instance
          ec2:
            key_name: "{{ key }}"
            instance_tags: {Name: "{{ name }}"}
            group_id: "{{ security_group }}"
            instance_type: "{{ instance_type }}"
            region: "{{ region }}"
            image: "{{ image }}"
            wait: yes
            count: 1
            vpc_subnet_id: "{{ subnet }}"
            assign_public_ip: yes
          register: ec2

2.  Call the `add_provider_vms` method as an action to link to the
    service via an *href slug* or an object.
    
        - name: Service Linking via an href slug
          manageiq_vmdb:
            href: "href_slug::services/80"
            action: add_provider_vms
            data:
              uid_ems:
                - "{{ ec2.instances[0].id }}"
              provider:
                id: 24
        
        - name: Service Linking via an object
          manageiq_vmdb:
            vmdb: "{{ vmdb_object }}"
            action: add_provider_vms
            data:
              uid_ems:
                - "{{ ec2.instances[0].id }}"
              provider:
                id: 24

#### Modifying the Automate Workspace Using the `manageiq-automate` Role.

The `manageiq-automate` role allows users of ManageIQ Automate to modify
and add to the automate workspace via an Ansible playbook.

<div class="note">

When using this role in a playbook on a ManageIQ appliance with Embedded
Ansible activated, add an empty `roles` directory at the root of the
playbook. In the `roles` directory, include a `requirements.yml` file
with the following contents:

    ---
    - src: syncrou.manageiq-automate

ManageIQ will automatically install the role once it sees the
`requirements.yml` file in the playbook.

</div>

##### Role Variables

The `manageiq_automate` role employs the following variables when
implemented in a playbook run on a ManageIQ appliance. Variables are
defined in `defaults/main.yml` and `vars/main.yml`.

*auto\_commit*: By default is set to `True`. If set to False it will not
auto commit back to ManageIQ each call to a `set_` method in the
`manageiq_automate` module.

*manageiq\_validate\_certs*: By default is set to `True`. If passed in
via *extra\_vars* or assigned in the playbook variables then the lookup
will allow self-signed certificates to be used when using SSL REST API
connection URLs.

##### Example Playbook

The example below utilizes the `manageiq-automate` role. Using variable
substitution, playbook tasks retrieve method parameters which are then
used to modify object attributes. A final task uses the `set_retry`
module to update the retry interval.

    - name: Siphon Method Parameters into an object
      hosts: localhost
      connection: local
      vars:
      - auto_commit: True
      - object: root
      - interval: 600
    
      gather_facts: False
      roles:
      - syncrou.manageiq-automate
    
      tasks:
        - name: "Get the list of Method Parameters"
          manageiq_automate:
            workspace: "{{ workspace }}"
            get_method_parameters: yes
          register: method_params
    
        - name: "Set attributes"
          manageiq_automate:
            workspace: "{{ workspace }}"
            set_attributes:
              object: "{{ object }}"
              attributes: "{{ method_params.value }}"
    
        - name: Set Retry
          manageiq_automate:
            workspace: "{{ workspace }}"
            set_retry:
              interval: "{{ interval }}"

#### Callbacks in Multiple Appliance Environments

In a ManageIQ multiple appliance environment, enable the Embedded
Ansible server role on a dedicated ManageIQ appliance. Add
`store_session:sql` to Ansible playbooks to ensure successful callbacks
to ManageIQ appliances in a multiple appliance environment.

## Ansible Tower

Ansible Tower is a management tool integrated with ManageIQ, designed to
help automate infrastructure operations. ManageIQ allows you to execute
Ansible Tower jobs or workflows using service catalogs and Automate. No
custom configuration or Ruby scripting is needed in ManageIQ, as
configuration is done in Ansible Tower using playbooks.

You can use the large library of existing Ansible playbooks as ManageIQ
state machines to automate tasks such as deployments, backups, package
updates, and maintenance in your ManageIQ environment. This can be
particularly useful for quickly applying changes across large
environments with many virtual machines or instances.

Using Ansible Tower, you can schedule Ansible playbook runs and monitor
current and historical results, allowing for troubleshooting or
identification of issues before they occur.

ManageIQ supports Ansible Tower API v2 provider integration.

### Working with an Ansible Tower Provider

The basic workflow when using ManageIQ with an Ansible Tower provider is
as follows:

1.  Create an Ansible playbook which performs a specific task.

2.  A new Ansible Tower job template is created from the playbook (or
    workflow template created from disparate jobs), which is then
    retrieved by ManageIQ.

3.  From the Ansible Tower job or workflow template, create a new
    catalog item in ManageIQ, optionally with a service dialog that
    allows the user to enter parameters if needed.

4.  The user orders the service from the ManageIQ user interface, and
    fills out any additional arguments (for example, limiting the task
    to run on a specific set of virtual machines).

5.  The job or workflow executes.

<div class="note">

  - For more information on Ansible playbooks, see the [Ansible playbook
    documentation](https://docs.ansible.com/ansible/playbooks.html).

  - For more information on worklows, see
    [Workflows](https://docs.ansible.com/ansible-tower/latest/html/userguide/workflows.html)
    in the Ansible Tower *User Guide*.

</div>

### Adding an Ansible Tower Provider

To access your Ansible Tower inventory from ManageIQ, you must add
Ansible Tower as a provider.

<div class="note">

  - Ensure **ENABLE HTTP BASIC AUTH** is set to **On** in the Ansible
    Tower configuration settings before adding the provider. See [Tower
    Configuration](https://docs.ansible.com/ansible-tower/latest/html/administration/configure_tower_in_tower.html)
    in the Ansible Tower *Administration Guide*.

  - A trailing slash is **not** required at the end of the Ansible Tower
    provider URL. Adding the trailing slash to the provider URL may
    result in a validation error.

</div>

1.  Navigate to <span class="menuchoice">Automation \> Ansible Tower \>
    Explorer</span> and click on the **Providers** accordion tab.

2.  Under ![Configuration](images/1847.png) **Configuration**, click
    ![Add a new Provider](images/1862.png) **Add a new Provider**.

3.  In the **Add a new Provider** area:
    
    ![Add\_Ansible\_Provider](images/add-ansible-tower-provider.png)
    
    1.  Enter a **Name** for the new provider.
    
    2.  Add a **Zone** for the provider.
    
    3.  Enter the **URL** location or IP address to the Ansible Tower
        server. Add a trailing slash to the end of the Ansible Tower
        provider URL.

4.  Select the **Verify Peer Certificate** checkbox if desired.

5.  In the **Credentials** area, provide the **Username** and
    **Password**, and **Confirm Password**.

6.  Click **Validate** to verify credentials.

7.  Click **Add**.

After adding the Ansible Tower provider, refresh its relationships and
power states in order to view the current inventory.

### Refreshing an Ansible Tower Provider

Refresh relationships of all items related to an existing Ansible Tower
configuration management provider including inventory, hosts, virtual
machines, and clusters.

You can refresh inventory from ManageIQ, or by enabling the **Update on
Launch** option for inventory groups in Ansible Tower. The **Update on
Launch** option allows Ansible Tower to automatically update inventory
using a dynamic inventory script before launching an Ansible Tower job
from a playbook. See the [Ansible Tower
documentation](http://docs.ansible.com/ansible-tower/index.html) for
more information.

<div class="important">

It can take a long time to retrieve information from providers
containing many virtual machines or instances. The Ansible Tower dynamic
inventory script can be modified to limit updates to specific items and
reduce refresh time.

</div>

To refresh an Ansible Tower provider’s inventory in ManageIQ:

1.  Navigate to <span class="menuchoice">Automation \> Ansible Tower \>
    Explorer</span> and click the **Providers** accordion tab.

2.  Select the checkboxes for the Ansible Tower providers to refresh
    under **All Ansible Tower Providers**.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Refresh Relationships and Power States](images/2003.png)
    (**Refresh Relationships and Power States**).

4.  Click **OK**.

ManageIQ then queries the Ansible Tower API and obtains an inventory of
all available hosts, job and workflow templates.

### Viewing Ansible Tower Providers and Inventory

ManageIQ automatically updates its inventory from Ansible Tower. This
includes system groups (known as Inventories in Ansible Tower), basic
information about individual systems, and available Ansible Tower job or
workflow templates to be executed from the service catalog or Automate.

<div class="note">

To view and access Ansible Tower inventories and job or workflow
templates in ManageIQ, you must first create them in Ansible Tower.

</div>

To view a list of Ansible Tower providers and inventory:

1.  Navigate to <span class="menuchoice">Automation \> Ansible Tower \>
    Explorer</span>.

2.  select the **Providers** accordion menu to display a list of **All
    Ansible Tower Providers**.

3.  Select your Ansible Tower provider to expand and list the inventory
    groups on that Ansible Tower system. The inventory groups can be
    expanded to view the systems contained within each group, as well as
    configuration details for these systems.

Similarly, all discovered job and workflow templates are accessed under
the provider by expanding the <span class="menuchoice">Automation \>
Ansible Tower \> Explorer \> Templates</span> accordion menu.

### Viewing Ansible Tower Configured Systems

To view the systems in your Ansible Tower inventory:

1.  Navigate to <span class="menuchoice">Automation \> Ansible Tower \>
    Explorer \> Configured Systems</span>.

2.  Under **All Ansible Tower Configured Systems**, select **Ansible
    Tower Configured Systems** to display a list.

### Executing an Ansible Tower Job or Workflow Template from a Service Catalog

You can execute an Ansible Tower playbook from ManageIQ by creating a
service catalog item from an Ansible Tower job or workflow template.

<div class="important">

You must first create the job or workflow template in Ansible Tower. The
job or workflow templates are automatically discovered by ManageIQ when
refreshing your Ansible Tower provider’s inventory.

</div>

First, create a catalog:

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Add a New Catalog](images/1862.png) (**Add a New Catalog**)

3.  Enter a **Name** and **Description** for the catalog.

4.  Click **Add**.

Then, create an Ansible Tower service catalog item:

1.  Navigate to <span class="menuchoice">Automation \> Ansible Tower \>
    Explorer</span>, then click on the **Templates** according menu.

2.  Click **Ansible Tower Templates** and select an Ansible Tower job or
    workflow template.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Create Service Dialog from Template](images/1862.png) (**Create
    Service Dialog from this Template**).

4.  Enter a **Service Dialog Name** (for example,
    *ansible\_tower\_job*)and click **Save**.

5.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.
    Click **Catalog Items**.

6.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Add a New Catalog Item](images/1862.png) (**Add a New Catalog
    Item**) to create a new catalog item with the following details, at
    minimum:
    
      - For **Catalog Item type**, select **Ansible Tower**.
    
      - Enter a **Name** for the service catalog item.
    
      - Select **Display in Catalog**.
    
      - In **Catalog**, select the catalog you created previously.
    
      - In **Dialog**, select the service dialog you created previously
        (in this example, *ansible\_tower\_job*). To ask the user to
        enter extra information when running the task, **Service
        Dialog** must be selected. A dialog is required if **Display in
        Catalog** is chosen.
    
      - In **Provider**, select your Ansible Tower provider. This brings
        up the **Ansible Tower Template** option and configures the
        **Provisioning Entry Point State Machine** automatically.
    
      - Add configuration information for **Reconfigure Entry Point**
        and **Retirement Entry Point** as applicable.
    
      - Select your desired **Ansible Tower Template** from the list.
        Generally, this is the Ansible Tower job or workflow template
        previously used to create the service dialog.

7.  Click **Add**. The catalog item you created will appear in the **All
    Service Catalog Items** list.

To execute the Ansible Tower job:

1.  Navigate to <span class="menuchoice">Service Catalogs \> Ansible
    Tower catalog</span>.
    
    ![Order AT Catalog Item](images/Order_AT_Catalog_Item.png)

2.  Click **Order** for the catalog item.

3.  Enter any variables requested and click **Submit**.

ManageIQ takes you to the **Requests** queue page and show the status of
the job.

The service item’s details can be viewed in
<span class="menuchoice">Services \> My Services</span> in ManageIQ.

<div class="note">

Instead of running a single job at a time, multiple service catalog
items can also be grouped together as a catalog bundle to create one
deployment with multiple job templates. See [Catalogs and
Services](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.7/provisioning-virtual-machines-and-hosts/chapter-5-catalogs-and-services#catalogs-services)
in *Provisioning Virtual Machines and Hosts* for more information.

</div>

### Executing an Ansible Tower Job Using a Custom Automate Button

ManageIQ can execute Ansible Tower jobs on virtual machines or instances
using custom buttons in Automate.

Ansible Tower jobs can either be non-customizable, which do not require
any extra configuration from the user, or alternatively, they can allow
the user to specify a parameter (for example, a package name to
install). In Ansible Tower jobs containing a dialog, ManageIQ accepts
additional information from the user and adds it to the appropriate API
call in Automate, and then sends it into Ansible Tower.

**Prerequisites.**

Before creating an Automate button to execute an Ansible Tower job, the
following must be configured:

  - An Ansible playbook in Ansible Tower. See the [Ansible Tower
    documentation](https://docs.ansible.com/) for instructions.

  - Ansible Tower must be able to reach virtual machines or instances
    deployed by ManageIQ at the IP level.

  - The virtual machine template must have the Ansible Tower
    environment’s public SSH key injected. For cloud instances,
    `cloud-init` can be used and the public SSH key can be passed
    without rebuilding the image.

  - Any dynamic inventory scripts used must be configured to return the
    virtual machine names exactly as they are stored in ManageIQ,
    without the UUID appended.

**Executing an Ansible Tower Job using a Custom Automate Button.**

To configure a custom button to execute an Ansible Tower job on a
virtual machine or instance, first create the button:

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  Click the **Buttons** accordion menu.

3.  Click <span class="menuchoice">VM and Instance \> Unassigned
    Buttons</span>. This configures the button to run on virtual
    machines or instances.

4.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1862](images/1862.png) (**Add a new Button**).
    
      - In the **Adding a new Button** screen, configure the **Action**
        parameters as desired. **Dialog** can be left blank if the
        playbook does not require extra variables. To ask the user to
        enter extra information when running the task, **Service
        Dialog** must be selected.
    
      - Configure **Object Details** fields with the following request
        details:
        
          - For **System/Process**, select **Request**.
        
          - For **Message**, enter **create**.
        
          - For **Request**, enter **Ansible\_Tower\_Job**.
    
      - Configure **Attribute/Value Pairs** with the following
        parameters:
        
          - **job\_template\_name** is the Ansible Tower job template
            name to associate with the button. The
            **job\_template\_name** field is mandatory; other parameters
            are provided by the Tower job dialog.
    
      - Configure **Visibility** to all users, or limit visibility by
        role as desired.
        
        ![Add button](images/Add_button.png)
    
      - Click **Add**.

If you do not have an existing button group to assign the new button to,
create a new button group:

1.  From <span class="menuchoice">Automation \> Automate \>
    Customization</span>, navigate to <span class="menuchoice">Buttons
    \> VM and Instance \> Add a new Button Group</span>, and configure
    the following:
    
      - Configure **Basic Info** as desired. For example, name the
        button group `VM Actions`.
    
      - In **Assign Buttons**, select the button you just created from
        the **Unassigned** list and click ![1876](images/1876.png) to
        assign it to **Selected**.
        
        ![Create button group](images/Create_button_group.png)
    
      - Click **Add**.

To assign the button to an existing button group:

1.  Navigate to <span class="menuchoice">Buttons \> VM and Instance \>
    VM Actions \> Edit this Button Group</span>.

2.  In **Assign Buttons**, select the button you just created from the
    **Unassigned** list and click ![1876](images/1876.png) to assign it
    to **Selected**.

3.  Click **Add**.

To use the button to run an Ansible Tower job on a virtual machine:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the virtual machine to run the Ansible Tower job template on.

3.  Click the **VM Actions** button to show the button you created, and
    click the button from the list to run the Ansible Tower job
    template.
    
    ![Run Update Button](images/Run_Update_Button.png)

4.  Click **Submit** to execute the job.

ManageIQ then confirms the job has been executed.

If you selected a service dialog to run when creating the button,
ManageIQ will then prompt you to enter variables to complete the task.
After entering your desired parameters, ManageIQ takes you to the
**Requests** page.

The service item’s details can be viewed in
<span class="menuchoice">Services \> My Services</span> in ManageIQ.

# Cloud Providers

In ManageIQ, a cloud provider is a cloud computing environment that you
can add to a ManageIQ appliance to manage and interact with the
resources in that environment. This chapter describes the different
types of cloud providers that you can add to ManageIQ, and how to manage
them. Most cloud providers are added individually to ManageIQ.
Additionally, Amazon EC2 and Azure cloud providers can be discovered
automatically by ManageIQ.

The web interface uses virtual thumbnails to represent cloud providers.
Each thumbnail contains four quadrants by default, which display basic
information about each provider:

![Cloudthumbnail](images/Cloudthumbnail.png)

1.  Number of instances

2.  Management system software

3.  Number of images

4.  Authentication status

| Icon                     | Description                                                                    |
| ------------------------ | ------------------------------------------------------------------------------ |
| ![2190](images/2190.png) | Validated: Valid authentication credentials have been added.                   |
| ![2191](images/2191.png) | Invalid: Authentication credentials are invalid.                               |
| ![2192](images/2192.png) | Unknown: Authentication status is unknown or no credentials have been entered. |

Provider authentication status

## OpenStack Providers

### Adding OpenStack Providers

ManageIQ supports operating with the OpenStack `admin` tenant. When
creating an OpenStack provider in ManageIQ, select the OpenStack
provider’s `admin` user because it is the default administrator of the
OpenStack `admin` tenant. When using the `admin` credentials, a user in
ManageIQ provisions into the `admin` tenant, and sees images, networks,
and instances that are associated with the `admin` tenant.

<div class="note">

In OpenStack, you must add `admin` as a member of all tenants that users
want to access and use in ManageIQ.

See [Cloud
Tenants](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/5.0-beta/html-single/managing_infrastructure_and_inventory/index#tenants)
in *Managing Infrastructure and Inventory* for information on working
with OpenStack tenants (projects) in ManageIQ.

</div>

When adding an OpenStack cloud or infrastructure provider, enable
*tenant mapping* in ManageIQ to map any existing tenants from that
provider.

This means ManageIQ will create new cloud tenants to match each existing
OpenStack tenant; each new cloud tenant and its corresponding OpenStack
tenant will have identical resource assignments (including user and role
synchronization) with the exception of quotas. Tenant quotas are not
synchronized between ManageIQ and OpenStack, and are available for
reporting purposes only. You can manage quotas in ManageIQ but this will
not affect the quotas created in OpenStack.

During a provider refresh, ManageIQ will also check for any changes to
the tenant list in OpenStack. ManageIQ will create new cloud tenants to
match any new tenants, and delete any cloud tenants whose corresponding
OpenStack tenants no longer exist. ManageIQ will also replicate any
changes to OpenStack tenants to their corresponding cloud tenants.

If you leave tenant mapping disabled, ManageIQ will not create cloud
tenants or tenant object hierarchy from OpenStack.

<div class="note">

You can set whether ManageIQ should use the Telemetry service or
Advanced Message Queueing Protocol (AMQP) for event monitoring. If you
choose Telemetry, you should first configure the **ceilometer** service
on the overcloud to store events. See [Configuring the Overcloud to
Store Events](#openstack-events-oc) for instructions.

For more information, see [OpenStack Telemetry
(ceilometer)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/architecture_guide/components#comp-telemetry)
in the Red Hat OpenStack Platform *Architecture Guide*.

</div>

<div class="note">

To authenticate the provider using a self-signed Certificate Authority
(CA), configure the ManageIQ appliance to trust the certificate using
the steps in [Using a Self-Signed CA Certificate](#app-self_signed_CA)
before adding the provider.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Providers</span>.

2.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1862](images/1862.png) (**Add a New Cloud Provider**).

3.  Enter a **Name** for the provider.

4.  From the **Type** list, select **OpenStack**.

5.  Select the appropriate **API Version** from the list. The default is
    `Keystone v2`.
    
    If you select `Keystone v3`, enter the `Keystone V3 Domain ID` that
    ManageIQ should use. This is the domain of the user account you will
    be specifying later in the **Default** tab. If domains are not
    configured in the provider, enter **default**.
    
    <div class="note">
    
    Keystone API v3 is required to create cloud tenants on OpenStack
    cloud providers.
    
    </div>
    
    <div class="note">
    
      - With Keystone API v3, domains are used to determine
        administrative boundaries of service entities in OpenStack.
        Domains allow you to group users together for various purposes,
        such as setting domain-specific configuration or security
        options. For more information, see [OpenStack Identity
        (keystone)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/architecture_guide/#comp-identity)
        in the Red Hat OpenStack Platform *Architecture Guide*.
    
      - The provider you are creating will be able to see projects for
        the given domain only. To see projects for other domains, add it
        as another cloud provider. For more information on domain
        management in OpenStack, see [Domain
        Management](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/users_and_identity_management_guide/#Domains)
        in the Red Hat OpenStack Platform *Users and Identity Management
        Guide*.
    
    </div>

6.  Enter a region number in **Region**.

7.  Enter the appropriate **Zone** for the provider. If you do not
    specify a zone, it is set to `default`.

8.  (Optional) Enable tenant mapping by toggling the **Tenant Mapping
    Enabled** option to **Yes**. This synchronizes resources and users
    between the OpenStack cloud provider and ManageIQ. By default,
    tenant mapping is disabled.

9.  Select the appropriate **Zone** for the provider. By default, the
    zone is set to **default**.
    
    <div class="note">
    
    For more information, see the definition of host aggregates and
    availability zones in [OpenStack Compute
    (nova)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/architecture_guide/components#comp-compute)
    in the Red Hat OpenStack Platform *Architecture Guide*.
    
    </div>

10. In the **Default** tab, under **Endpoints**, configure the host and
    authentication details of your OpenStack provider:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the provider:
        
          - **SSL without validation**: Authenticate the provider
            insecurely using SSL.
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option. This is the recommended authentication
            method.
        
          - **Non-SSL**: Connect to the provider insecurely using only
            HTTP protocol, without SSL.
    
    2.  In **Hostname (or IPv4 or IPv6 address)**, enter the public IP
        or fully qualified domain name of the OpenStack Keystone
        service.
        
        <div class="note">
        
        The hostname required here is also the **OS\_AUTH\_URL** value
        in the **\~/overcloudrc** file generated by the director (see
        [Accessing the
        Overcloud](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/director_installation_and_usage/#sect-Accessing_the_Overcloud)
        in Red Hat OpenStack Platform *Director Installation and
        Usage*), or the **\~/keystonerc\_admin** file generated by
        Packstack (see [Evaluating OpenStack: Single-Node
        Deployment](https://access.redhat.com/articles/1127153)).
        
        </div>
    
    3.  In **API Port**, set the public port used by the OpenStack
        Keystone service. By default, OpenStack uses port 5000 for
        non-SSL security protocol. For SSL, API port is 13000 by
        default.
    
    4.  In the **Username** field, enter the name of a user in the
        OpenStack environment.
        
        <div class="important">
        
        In environments that use Keystone v3 authentication, the user
        must have the **admin** role for the relevant domain.
        
        </div>
    
    5.  In the **Password** field, enter the password for the user.
    
    6.  Click **Validate** to confirm ManageIQ can connect to the
        OpenStack provider.

11. Next, configure how ManageIQ should receive events from the
    OpenStack provider. Click the **Events** tab in the **Endpoints**
    section to start.
    
      - To use the Telemetry service of the OpenStack provider, select
        **Ceilometer**. Before you do so, the provider must first be
        configured accordingly. See [Configuring the Overcloud to Store
        Events](#openstack-events-oc) for details.
    
      - If you prefer to use the AMQP Messaging bus instead, or eventing
        is not enabled on Ceilometer, select **AMQP** and configure the
        following:
        
        1.  Select a **Security Protocol** method.
        
        2.  In **Hostname (or IPv4 or IPv6 address)** (of the **Events**
            tab, under **Endpoints**), enter the public IP or fully
            qualified domain name of the AMQP host.
        
        3.  In the **API Port**, set the public port used by AMQP. By
            default, OpenStack uses port 5672 for this.
        
        4.  In the **Username** field, enter the name of an OpenStack
            user with privileged access (for example, **admin**). Then,
            provide its corresponding password in the **Password**
            field.
        
        5.  Click **Validate** to confirm the credentials.

12. Click **Add** after configuring the cloud provider.

<div class="note">

  - To collect inventory and metrics from an OpenStack environment, the
    ManageIQ appliance requires that the adminURL endpoint for the
    OpenStack environment be on a non-private network. Hence, the
    OpenStack adminURL endpoint should be assigned an IP address other
    than `192.168.x.x`. Additionally, all the Keystone endpoints must be
    accessible, otherwise refresh will fail.

  - Collecting capacity and utilization data from an OpenStack cloud
    provider requires selecting the **Collect for All Clusters** option
    under **Configuration**, in the settings menu. For information, see
    [Capacity and Utilization
    Collections](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.5/html-single/general_configuration/#capacity-and-utilization-collections)
    in the *General Configuration Guide*.

</div>

#### Configuring the Overcloud to Store Events

By default, the Telemetry service does not store events emitted by other
services in a Red Hat OpenStack Platform environment. The following
procedure outlines how to enable the Telemetry service on your OpenStack
cloud provider to store such events. This ensures that events are
exposed to ManageIQ when a Red Hat OpenStack Platform environment is
added as a cloud provider.

1.  Log in to the undercloud host.

2.  Create an environment file called *ceilometer.yaml*, and add the
    following contents:
    
        parameter_defaults:
          CeilometerStoreEvents: true

3.  Please see the below **NOTE**.

If your OpenStack cloud provider was not deployed through the
undercloud, you can also set this manually. To do so:

1.  Log in to your Controller node.

2.  Edit */etc/ceilometer/ceilometer.conf*, and specify the following
    option:
    
        store_events = True

<div class="note">

Passing the newly created environment file to the overcloud deployment
is environment specific and requires executing commands in particular
order depending on use of variables. For further information please see
[*Director Installation and
Usage*](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/director_installation_and_usage/)
in the Red Hat OpenStack Platform documentation.

</div>

## Azure Providers

### Adding Azure Providers

ManageIQ supports Microsoft Azure providers. Before ManageIQ can be
authenticated to Microsoft Azure, you must complete a series of
prerequisite steps using the Azure portal; see [Create Active Directory
application and service principal account using the Azure
portal](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/).
Follow the steps to set up an Azure Active Directory (Azure AD) and
assign the required permissions to it, then create an Azure Active
Directory application, and obtain the **Application ID** (Client ID),
**Directory ID** (Tenant ID), **Subscription ID**, and **Key Value**
(Client Key) that are required to add and connect to the Azure instance
as a provider in ManageIQ. Currently, all of these steps can be
performed using either the Azure Resource Manager or Service Manager
(Classic) mode.

<div class="note">

In the steps described in [Create Active Directory application and
service principal account using the Azure
portal](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/):

  - The **Application ID** obtained during *Get Application ID and
    Authentication Key* is your **Client ID**. In the same section,
    after providing a description and a duration for the key, the
    **VALUE** displayed after clicking **Save** is your **Client Key**.
    If you choose an expiring key, make sure to note the expiration
    date, as you will need to generate a new key before that day in
    order to avoid an interruption.

  - The **Directory ID** obtained during *Get Tenant ID* is your
    **Tenant ID**. In Azure Active Directory (Azure AD), a tenant is a
    dedicated instance of the Azure AD service and is representative of
    an organization. It houses the users in a company and the
    information about them - their user profile data, permissions,
    groups, applications, and other information related to an
    organization and its security. To allow Azure AD users to sign in to
    your application, you must register your application in a tenant of
    your own which is assigned a Tenant ID (Directory ID).

  - During *Assign Application to Role*, select the **Contributor** role
    and not the **Reader** role.

  - To obtain your **Subscription ID**, log in to the Azure portal and
    click **Subscriptions** on the slide-out menu on the left. Find the
    appropriate subscription and see your Azure **Subscription ID**
    associated with it. Note that if the **Subscriptions** tab is not
    visible, then click on **More services \>** to find it. The Azure
    **Subscription ID** is like a billing unit for all of the services
    consumed in your Azure account, including virtual machines and
    storage. The **Subscription ID** is in the form of a Globally Unique
    Identifier (GUID).

</div>

So, after a service principal account (instance of an application in a
directory) has been created using the Azure portal, the following four
pieces of information will be available within the Azure AD module.

  - Directory ID (Tenant ID)

  - Subscription ID

  - Application ID (Client ID)

  - Client Key

You can now use these values in the procedure below to add an Azure
cloud instance as a provider to ManageIQ.

**To Add an Azure Cloud Provider**:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Providers</span>.

2.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1862](images/1862.png) (**Add a New Cloud Provider**).

3.  Enter a **Name** for the provider.

4.  From the **Type** list, select **Azure**.

5.  Select a region from the **Region** list. One provider will be
    created for the selected region.

6.  Enter **Tenant ID**.

7.  Enter **Subscription ID**.

8.  Enter **Zone**.

9.  In the **Credentials** section, enter the **Client ID** and **Client
    Key**; click **Validate**.

10. Click **Add**.

### Disabling Azure Cloud Regions

ManageIQ allows administrators to disable Azure cloud regions on the
appliance server. You can use this capability to disable certain
classified regions. Once disabled, the region will not be available when
adding a new Azure provider.

1.  Click ![config gear](images/config-gear.png) (**Configuration**).

2.  Click on the **Settings** accordion, then click **Zones**.

3.  Click the zone where the ManageIQ server is located, then click on
    the EVM server.

4.  Click on the **Advanced** tab.

5.  Search for `:ems_azure:`, and enter the regions you want to disable
    under `:disabled_regions:`.
    
        Example. To disable the `us-gov-arizona` and `us-gov-texas` regions:
        
        :ems_azure:
          :disabled_regions:
          - us-gov-arizona
          - us-gov-texas

6.  Click **Save**.

## Amazon EC2 Providers

### Permissions for Amazon EC2 Providers

Use Amazon EC2’s *Power User* Identity and Access Management (IAM)
policy when adding Amazon EC2 as a cloud provider in ManageIQ. This
policy allows those in the *Power User* group full access to AWS
services except for user administration, meaning a ManageIQ API user can
access all of the API functionality, but cannot access or change user
permissions.

<div class="note">

When adding an Amazon EC2 provider in ManageIQ with the intention to use
the SmartState analysis feature, assign *Admin* group privileges. For
situations in which assigning the *Admin* group is unacceptable,
manually create an Amazon EC2 policy role using specific permissions.
See [Manually Creating an Amazon EC2
Role](#amazon-ec2-manual-role-creation) for more information.

</div>

Further limiting API access limitations can limit Automate capabilities,
as Automate scripts directly access the AWS SDK to create brand new
application functionality.

The AWS services primarily accessed by the ManageIQ API include:

  - Elastic Compute Cloud (EC2)

  - CloudFormation

  - CloudWatch

  - Elastic Load Balancing

  - Simple Notification Service (SNS)

  - Simple Queue Service (SQS)

#### Manually Creating an Amazon EC2 Role

To eliminate the need to assign *Admin* group privileges to the Amazon
EC2 provider, create an IAM role following the procedure described in
[Creating a Role for an AWS Service
(Console)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html)
in the Amazon Web Services documentation.

Use the following parameters:

1.  Select **EC2** as the service the role will use.

2.  Attach the following permissions:
    
    1.  `AmazonEC2FullAccess`
    
    2.  `AmazonS3FullAccess`
    
    3.  `AmazonSQSFullAccess`

3.  Enter `smartstate` for the **Role name**.

Once the IAM role is created, assign the provider *Power User*
privileges as described in [Permissions for Amazon EC2
Providers](#amazon-provider-permissions).

### Adding Amazon EC2 Providers

Complete the following procedure to add an Amazon EC2 cloud provider in
ManageIQ.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Providers</span>.

2.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1862](images/1862.png) (**Add a New Cloud Provider**).

3.  Enter a **Name** for the provider.

4.  From the **Type** list, select **Amazon EC2**.

5.  Select a **Region**.

6.  Select the appropriate **Zone** if you have more than one available.

7.  Under **Endpoints**, click the **Default** tab.
    
    1.  Enter the **Endpoint URL**.
        
        <div class="note">
        
        AWS allows users to set a custom endpoint URL when connecting to
        certain services, which you can add in the ManageIQ user
        interface per Amazon EC2 provider. See [Interface VPC Endpoints
        (AWS
        PrivateLink)](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpce-interface.html)
        for more information.
        
        </div>
    
    2.  Generate an **Access Key** in the **Security Credentials** of
        your Amazon AWS account. The **Access Key ID** acts as your
        **User ID**, and your **Secret Access Key** acts as your
        **Password**.
    
    3.  Click **Validate** to validate the credentials.

8.  Click the **SmartState Docker** tab.
    
    1.  Enter the **SmartState Docker User Name** and **SmartState
        Docker Password**. Here use your docker registry credentials
        required to perform SmartState analysis on AWS. These
        credentials are required so that you can pull the image from the
        docker registry.

9.  Click **Add**.

### Enabling Public AMIs from Amazon EC2

By default, public AMIs from an Amazon EC2 provider are not viewable in
ManageIQ. To make these images viewable, you must edit the main
configuration file for the appliance.

<div class="note">

Syncing all public images may require additional memory resources. Also,
bear in mind that syncing happens in each configured Amazon EC2
provider, which will require a similar amount of total memory resources.

</div>

1.  Navigate to the settings menu, then
    <span class="menuchoice">Configuration \> Zone \> Advanced</span>.

2.  Select the configuration file to edit from the **File** list. If not
    already automatically selected, select **EVM Server Main
    Configuration**.

3.  Set the **get\_public\_images** parameter:
    
    1.  Set the parameter to **get\_public\_images: true** to make
        public images viewable.
    
    2.  Set the parameter to **get\_public\_images: false** to make
        public images not viewable.

4.  Optionally, configure an array of filters in
    **public\_images\_filters** to restrict which images are synced. See
    <http://docs.aws.amazon.com/sdkforruby/api/Aws/EC2/Client.html#describe_images-instance_method>
    for more details.

### Enabling AWS Config Notifications

Amazon’s AWS Config notifies subscribers of changes in a region through
its Simple Notification Service (SNS). ManageIQ subscribes to the SNS
service for AWS Config deltas and converts the deltas into ManageIQ
events.

1.  Enable the AWS Config service in the AWS Management Console. See the
    [AWS Config Developer
    Guide](http://aws.amazon.com/documentation/config/) for more
    information.

2.  Create a new Amazon SNS topic named `AWSConfig_topic`. ManageIQ
    automatically connects to this topic.

3.  (Optional) Configure the frequency of delta creation in the AWS
    Management Console.

You can assign ManageIQ policies to the AWS events listed below. The
appliance performs a provider refresh on all these events except for
`AWS_EC2_Instance_UPDATE`.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Event</th>
<th>Policies</th>
<th>Refresh</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AWS_EC2_Instance_CREATE</p></td>
<td><p>src_vm</p>
<p>vm_create</p></td>
<td><p>ems</p></td>
</tr>
<tr class="even">
<td><p>AWS_EC2_Instance_UPDATE</p></td>
<td><p>N/A</p></td>
<td><p>ems</p></td>
</tr>
<tr class="odd">
<td><p>AWS_EC2_Instance_running</p></td>
<td><p>src_vm</p>
<p>vm_start</p></td>
<td><p>ems</p></td>
</tr>
<tr class="even">
<td><p>AWS_EC2_Instance_stopped</p></td>
<td><p>src_vm</p>
<p>vm_power_off</p></td>
<td><p>ems</p></td>
</tr>
<tr class="odd">
<td><p>AWS_EC2_Instance_shutting-down</p></td>
<td><p>src_vm</p>
<p>vm_power_off</p></td>
<td><p>ems</p></td>
</tr>
</tbody>
</table>

### Enabling Amazon EC2 Events

After adding an Amazon EC2 provider and configuring an SNS topic in
[Enabling AWS Config
Notifications](#amazon-provider-aws-config-notifications), create a
CloudTrail, then configure CloudWatch rules on your EC2 provider to
automatically get events in ManageIQ for monitoring the provider.

<div class="note">

The following procedures are accurate at time of publishing. See the
[Amazon AWS
documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/)
for further details on these steps.

</div>

#### Creating a CloudTrail

In the CloudTrail area of the AWS Management Console, create a trail and
an S3 bucket:

1.  Create a **Trail** with a custom name.

2.  (Optional) If you want to apply the trail to all of your ManageIQ
    regions, select **Yes** for **Apply trail to all regions**.

3.  For **Management Events**, select **Read/Write events: All**.

4.  Create a new S3 bucket.

#### Creating CloudWatch Rules Based on Event Patterns

In the CloudWatch area of the AWS Management Console, create three
rules: one rule each for EC2, volumes, and snapshots.

<div class="important">

When an SNS topic is deleted and recreated (manually or by ManageIQ),
CloudWatch rules must be recreated as well, even though the SNS target
topic for CloudWatch rules appears to be assigned to these rules. The
CloudWatch rule does not send events to this recreated topic until it is
recreated too.

</div>

To create a CloudWatch rule for EC2:

1.  Navigate to <span class="menuchoice">Events \> Rules</span> and
    click **Create rule**.

2.  Select the **Event Pattern** radio button to specify the event
    source.

3.  Edit the **Event Pattern Preview** box, and paste and save the
    following code to create a rule based on a custom event pattern:
    
        {
          "source": [
            "aws.ec2"
          ],
          "detail-type": [
            "AWS API Call via CloudTrail"
          ],
          "detail": {
            "eventSource": [
              "ec2.amazonaws.com"
            ]
          }
        }

4.  Click **Add target** and specify the following attributes:
    
      - **Type**: `SNS Topic`
    
      - **Topic**: `AWSConfig_topic`
    
      - **Input**: `Matched event`

5.  Click **Configure Details** to save these details.

6.  Configure a name and description for the rule if desired. Ensure the
    **Enabled** checkbox is selected for **State**.

7.  Click **Create rule** to save the CloudWatch rule.

Repeat the same procedure to create a CloudWatch rule for volumes,
pasting the code snippet below to the **Event Pattern Preview** box:

1.  Navigate to <span class="menuchoice">Events \> Rules</span> and
    click **Create rule**.

2.  Select the **Event Pattern** radio button to specify the event
    source.

3.  Edit the **Event Pattern Preview** box, and paste and save the
    following code to create a rule based on a custom event pattern:
    
        {
          "source": [
            "aws.ec2"
          ],
          "detail-type": [
            "EBS Volume Notification"
          ]
        }

4.  Click **Add target** and specify the following attributes:
    
      - **Type**: `SNS Topic`
    
      - **Topic**: `AWSConfig_topic`
    
      - **Input**: `Matched event`

5.  Click **Configure Details** to save these details.

6.  Configure a name and description for the rule if desired. Ensure the
    **Enabled** checkbox is selected for **State**.

7.  Click **Create rule** to save the CloudWatch rule.

Repeat the same procedure to create a CloudWatch rule for snapshots,
pasting the code snippet below to the **Event Pattern Preview** box:

1.  Navigate to <span class="menuchoice">Events \> Rules</span> and
    click **Create rule**.

2.  Select the **Event Pattern** radio button to specify the event
    source.

3.  Edit the **Event Pattern Preview** box, and paste and save the
    following code to create a rule based on a custom event pattern:
    
        {
          "source": [
            "aws.ec2"
          ],
          "detail-type": [
            "EBS Snapshot Notification"
          ]
        }

4.  Click **Add target** and specify the following attributes:
    
      - **Type**: `SNS Topic`
    
      - **Topic**: `AWSConfig_topic`
    
      - **Input**: `Matched event`

5.  Click **Configure Details** to save these details.

6.  Configure a name and description for the rule if desired. Ensure the
    **Enabled** checkbox is selected for **State**.

7.  Click **Create rule** to save the CloudWatch rule.

EC2 can now automatically refresh events in ManageIQ.

### Disabling Amazon Cloud Regions

ManageIQ allows administrators to disable Amazon cloud regions on the
appliance server. Use this capability to disable certain classified
regions like AWS GovCloud. Once disabled, the region will not be
available when adding an Amazon EC2 provider.

1.  Click ![config gear](images/config-gear.png) (**Configuration**).

2.  Click on the **Settings** accordion, then click **Zones**.

3.  Click the zone where the ManageIQ server is located, then click on
    the EVM server.

4.  Click on the **Advanced** tab.

5.  Search for `:ems_amazon:`, and enter the regions you want to disable
    under `:disabled_regions:`.
    
        Example. To disable the `ap-northeast-1` region:
        
        :ems_amazon:
          :disabled_regions:
          - us-gov-west-1
          - ap-northeast-1

6.  Click **Save**.

<div class="note">

In AWS, Government regions are disabled by default. To enable a disabled
region, be sure to do so in the `production.yml` configuration file
manually.

</div>

## Refreshing Cloud Providers

Refresh a cloud provider to find other resources related to it. Ensure
the chosen cloud providers have the correct credentials before
refreshing.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Providers</span>.

2.  Select the checkboxes for the cloud providers to refresh.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Refresh Relationships and Power States](images/2003.png)
    (**Refresh Relationships and Power States**).

4.  Click **OK**.

## Tagging Cloud Providers

Apply tags to all cloud providers to categorize them together at the
same time.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Providers</span>.

2.  Select the checkboxes for the Cloud Providers to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/1851.png) (**Edit Tags**).

4.  Select a customer tag to assign from the first list.
    
    ![2219](images/2219.png)

5.  Select a value to assign from the second list.

6.  Click **Save**.

## Removing Cloud Providers

A cloud provider might require removal from the VMDB if it is no longer
in use.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Providers</span>.

2.  Check the cloud providers to remove.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Remove Cloud Providers from the VMDB](images/2098.png)
    (**Remove Cloud Providers from the VMDB**).

4.  Click **OK**.

## Editing a Cloud Provider

Edit information about a provider such as the name, IP address, and
login credentials.

<div class="note">

The **Type** value is unchangeable.

</div>

To use a different cloud provider, create a new one.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Providers</span>.

2.  Click the cloud provider to edit.

3.  Click ![Configuration](images/1847.png) **(Configuration)**, and
    then ![Edit Selected Cloud Provider](images/1851.png) **(Edit
    Selected Cloud Provider)**.

4.  Edit the **Basic Information**. This varies depending on the
    **Type** of provider.

5.  Fill out the **Credentials** by typing in a **Username**,
    **Password**, and a verification of this password (**Confirm
    Password**).
    
      - If selecting **Amazon EC2**, generate an **Access Key** in the
        **Security Credentials** of your Amazon AWS account. The
        **Access Key ID** acts as your **User ID**, and your **Secret
        Access Key** acts as your **Password**.
    
      - If selecting **OpenStack**, use the `Keystone User ID` and
        `Password` for your login credentials.

6.  If editing an OpenStack provider, use the **AMQP** subtab to provide
    credentials required for the Advanced Message Queuing Protocol
    service on your OpenStack Nova component.

7.  Click **Validate** and wait for notification of successful
    validation.

8.  Click **Save**.

## Viewing a Cloud Provider’s Timeline

View the timeline of events for instances registered to a cloud
provider.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Providers</span>.

2.  Click the desired cloud provider for viewing the timeline.

3.  Click ![Monitoring](images/1994.png) (**Monitoring**), and then
    ![Timelines](images/1995.png) (**Timelines**).

4.  From **Options**, customize the period of time to display and the
    types of events to see.
    
      - Use **Show** to select regular Management Events or Policy
        Events.
    
      - Use the **Type** list to select hourly or daily data points.
    
      - Use **Date** to type the date for the timeline to display.
    
      - If you select to view a daily timeline, use **Show** to set how
        many days back to go. The maximum history is 31 days.
    
      - The three **Event Groups** list allow you to select different
        groups of events to display. Each has its own color.
    
      - From the **Level** list, select a **Summary** event, or a
        **Detail** list of events.

# Network Managers

In ManageIQ, a network manager is an inventory of networking entities on
existing cloud and infrastructure providers managed by your ManageIQ
appliance.

This provider type exposes software-defined networking (SDN) providers
including *OpenStack Network (Neutron)*, *Azure Network*, and *Amazon
EC2 Network*, which enables software-defined networking inventory
collection. The OpenStack Network provider collects inventory of
floating IPs from OpenStack so that IPs can be allocated without
querying OpenStack database every time. Also, it refreshes all Neutron
data from both OpenStack and OpenStack Infrastructure, and extracts the
Neutron logic to a shared place. Note that management via the network
providers configuration is currently disabled.

This chapter describes the different types of network managers available
to ManageIQ, and how to manage them. Network managers are discovered
automatically by ManageIQ from other connected providers.

## Adding or Viewing Network Providers

<div class="note">

All supported network providers — OpenStack Network, Azure Network, and
Amazon EC2 Network, are added or removed automatically upon adding or
removing the respective cloud provider.

</div>

Viewing network providers:

1.  Navigate to <span class="menuchoice">Networks \> Providers</span> to
    see a list of all network providers, along with information such as
    *Name*, *Type*, *EVM Zone*, *Number of Instances*, *Subnets*, and
    *Region*.

2.  Click on a provider from the list to view its summary screen.

Network providers summary:

The summary screen includes tables containing information on
*Properties*, *Status*, *Relationships*, *Overview*, and *Smart
Management*. Click on rows in the *Relationship* and *Overview* tables
to see detailed information for individual entities.

Accordion tabs in the sidebar provide access to **Properties** and
**Relationships** details.

Click on **Reload**, **Configuration**, **Policy**, and **Monitoring**
actions in the taskbar to manage the selected provider.

<div class="note">

Alternatively, click on a cloud provider to see the cloud provider
details and its relationships such as Network Manager, Tenants,
Instances among others. In Relationships, click Network Manager to see
information about the network provider, and its relationship with the
cloud provider, on the summary page.

</div>

## Refreshing Network Providers

Refresh a network provider to find other resources related to it. Ensure
the selected network providers have the correct credentials before
refreshing.

1.  Navigate to <span class="menuchoice">Networks \> Providers</span>.

2.  Select the network providers to refresh.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Refresh Relationships and Power States](images/2003.png)
    (**Refresh Relationships and Power States**).

4.  Click **OK**.

## Tagging Network Providers

Apply tags to network providers to categorize them together at the same
time.

1.  Navigate to <span class="menuchoice">Networks \> Providers</span>.

2.  Select the network providers to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/2158.png) (**Edit Tags**).

4.  **Select a customer tag to assign** from the first list.

5.  Select a value to assign from the second list.

6.  Click **Save**.

## Removing Network Providers

Although network providers are added or removed automatically upon
adding or removing the respective cloud provider, you can manually
remove a network provider if it is no longer in use. This will remove
the network provider from the VMDB and any relationship with the cloud
provider.

1.  Navigate to <span class="menuchoice">Networks \> Providers</span>.

2.  Click the network provider to remove.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Remove this Network Provider from the VMDB](images/2098.png)
    (**Remove this Network Provider from the VMDB**).

4.  Click **OK**.

## Viewing a Network Provider’s Timeline

View the timeline of events for instances registered to a network
provider.

1.  Navigate to <span class="menuchoice">Networks \> Providers</span>.

2.  Click the network provider you want to monitor the timeline for.

3.  Click ![Monitoring](images/1994.png) (**Monitoring**), and then
    ![Timelines](images/1995.png) (**Timelines**).

4.  From **Options**, select the event type and interval, and customize
    the period of time to display and the types of events to see.
    
      - Select *Management Events* or *Policy Events* from the **Show**
        list.
    
      - Select an **Interval** between *Hourly* and *Daily*.
    
      - Select **Date**.
    
      - If you selected *Daily* for **Interval**, set the number of days
        in the past to see the event timeline for. The maximum is *31
        days back*.
    
      - Select **Summary** or **Detail** for **Level**.
    
      - Select the required **Event Groups** from the lists you want to
        monitor the timeline for.

You can also assign policy profiles to network providers, or remove
them. The method for doing so is similar to that of any normal policy
profile.

## Using the Topology Widget for Network Providers

The **Topology** widget is an interactive topology graph, showing the
status and relationships between the different entities of the network
providers that ManageIQ has access to.

The topology graph includes cloud subnets, virtual machines, security
groups, floating IP addresses, cloud networks, network routers, cloud
tenants, and tags within the overall network provider environment.

Each entity in the graph displays a color indication of its status:
green indicates an active entity, while red indicates inactivity or an
issue.

![Network Topology](images/Network_Topology.png)

1.  Navigate to <span class="menuchoice">Networks \> Topology</span>.

2.  Click the desired network provider for viewing the provider summary.

Alternatively, you can open the topology widget from the provider
summary page by clicking **Topology** under **Overview**.

  - Hovering over any individual graph element will display a summary of
    details for the individual element.

  - Double-click an entity in the graph to navigate to its summary page.

  - Drag elements to reposition the graph.

  - Click the symbols in the legend at the top of the graph to show or
    hide entities.

  - Click the **Display Names** checkbox to show or hide entity names.

  - Click **Refresh** to refresh the display of the network provider
    entities.

  - Enter a search term in the **Search** box to locate an entity by
    full or partial name.

# Containers Providers

A containers provider is a service that manages container resources,
that can be added to the ManageIQ appliance.

ManageIQ can connect to OpenShift Container Platform containers
providers and manage them similarly to infrastructure and cloud
providers. This allows you to gain control over different aspects of
your containers environment and answer questions such as:

  - How many containers exist in my environment?

  - Does a specific node have enough resources?

  - How many distinct images are used?

  - Which image registries are used?

When ManageIQ connects to a container’s environment, it collects
information on different areas of the environment:

  - Entities such as pods, nodes, or services.

  - Basic relationships between the entities, for example: Which
    services are serving which pods?

  - Advanced insight into relationships, for example: Which two
    different containers are using the same image?

  - Additional information, such as events, projects, routes, and
    metrics.

You can manage policies for containers entities by adding tags. All
containers entities except volumes can be tagged.

<div class="note">

This chapter provides details on managing containers providers. For
details on working with the resources within a container environment,
see [Container
Entities](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_infrastructure_and_inventory/#container_entities)
in *Managing Infrastructure and Inventory*.

</div>

The ManageIQ user interface uses virtual thumbnails to represent
containers providers. Each thumbnail contains four quadrants by default,
which display basic information about each provider:

![cp quad icon](images/cp-quad-icon.png)

1.  Number of nodes

2.  Container provider software

3.  Power state

4.  Authentication status

| Icon                     | Description                                                                    |
| ------------------------ | ------------------------------------------------------------------------------ |
| ![2190](images/2190.png) | Validated: Valid authentication credentials have been added.                   |
| ![2191](images/2191.png) | Invalid: Authentication credentials are invalid.                               |
| ![2192](images/2192.png) | Unknown: Authentication status is unknown or no credentials have been entered. |

Containers provider authentication status

## Obtaining an OpenShift Container Platform Management Token

When deploying OpenShift using `openshift-ansible-3.0.20` (or later
versions), the OpenShift Container Platform [service
account](https://docs.openshift.com/container-platform/latest/admin_guide/service_accounts.html)
and
[roles](https://docs.openshift.com/container-platform/latest/admin_guide/manage_authorization_policy.html)
required by ManageIQ are installed by default.

<div class="note">

See the [OpenShift Container Platform
documentation](https://docs.openshift.com/container-platform/latest/architecture/additional_concepts/authorization.html#roles)
for a list of the default roles.

</div>

Run the following to obtain the token needed to add an OpenShift
Container Platform provider:

    # oc sa get-token -n management-infra management-admin
    eyJhbGciOiJSUzI1NiI...

## Enabling OpenShift Cluster Metrics

Use the OpenShift Cluster Metrics plug-in to collect node, pod, and
container metrics into one location. This helps track usage and find
common issues.

  - Configure ManageIQ to allow for all three [**Capacity &
    Utilization** server
    roles](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.1/deployment-planning-guide/#assigning_the_capacity_and_utilization_server_roles).

  - Enable cluster metrics using the [OpenShift Container Platform
    documentation](https://access.redhat.com/documentation/en-us/openshift_container_platform/3.5/html-single/installation_and_configuration/#install-config-cluster-metrics).

## Adding an OpenShift Container Platform Provider

After initial installation and creation of a ManageIQ environment, add
an OpenShift Container Platform provider using the token obtained in
[Obtaining an OpenShift Container Platform Management
Token](#Obtaining_OpenShift_Container_Platform_Management_Token) and
following the procedure below.

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Add a New Containers Provider](images/1862.png) (**Add a New
    Containers Provider**).

3.  Enter a **Name** for the provider.

4.  From the **Type** list, select **OpenShift Container Platform**.

5.  Enter the appropriate **Zone** for the provider. If you do not
    specify a zone, it is set to `default`.

6.  From the **Alerts** list, select **Prometheus** to enable external
    alerts. Selecting **Prometheus** adds an **Alerts** tab to the lower
    pane to configure the Prometheus service. Alerts are disabled by
    default.

7.  From the **Metrics** list, select **Hawkular** or **Prometheus** to
    collect capacity and utilization data, or leave as **Disabled**.
    Selecting **Prometheus** or **Hawkular** adds a **Metrics** tab to
    the lower pane for further configuration. Metrics are disabled by
    default.

8.  In the **Default** tab, configure the following for the OpenShift
    provider:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the provider:
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option.
        
          - **SSL trusting custom CA**: Authenticate the provider with a
            self-signed certificate. For this option, copy your
            provider’s CA certificate to the **Trusted CA
            Certificates** box in PEM format.
            
            <div class="note">
            
            You can obtain your OpenShift Container Platform provider’s
            CA certificate for all endpoints (default, metrics, alerts)
            from `/etc/origin/master/ca.crt`. Paste the output (a block
            of text starting with `-----BEGIN CERTIFICATE-----`) into
            the **Trusted CA Certificates** field.
            
            </div>
        
          - **SSL without validation**: Authenticate the provider
            insecurely (not recommended).
    
    2.  Enter the **Hostname** (or IPv4 or IPv6 address) of the
        provider.
        
        <div class="important">
        
        The **Hostname** must use a unique fully qualified domain name.
        
        </div>
    
    3.  Enter the **API Port** of the provider. The default port is
        `8443`.
    
    4.  Enter a token for your provider in the **Token** box.
        
        <div class="note">
        
        To obtain a token for your provider, run the `oc get secret`
        command on your provider; see [Obtaining an OpenShift Container
        Platform Management
        Token](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#Obtaining_OpenShift_Container_Platform_Management_Token).
        
        For example:
        
        \# oc get secret --namespace management-infra
        management-admin-token-8ixxs --template='{{index .data
        "ca.crt"}}' | base64 --decode
        
        </div>
    
    5.  Click **Validate** to confirm that ManageIQ can connect to the
        OpenShift Container Platform provider.

9.  For the **Prometheus** alerts service, add the Prometheus alerts
    endpoint in the **Alerts** tab:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the service:
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option.
        
          - **SSL trusting custom CA**: Authenticate the provider with a
            self-signed certificate. For this option, copy your
            provider’s CA certificate to the **Trusted CA
            Certificates** box in PEM format.
        
          - **SSL without validation**: Authenticate the provider
            insecurely using SSL. (Not recommended)
    
    2.  Enter the **Hostname** (or IPv4 or IPv6 address) or alert
        **Route**.
    
    3.  Enter the **API Port** if your Prometheus provider uses a
        non-standard port for access. The default port is `443`.
    
    4.  Click **Validate** to confirm that ManageIQ can connect to the
        alerts service.

10. If you selected a metrics service, configure the service details in
    the **Metrics** tab:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the service:
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option.
        
          - **SSL trusting custom CA**: Authenticate the provider with a
            self-signed certificate. For this option, copy your
            provider’s CA certificate to the **Trusted CA
            Certificates** box in PEM format.
            
            <div class="note">
            
            In OpenShift, the default deployment of the router generates
            certificates during installation, which can be used with the
            **SSL trusting custom CA** option. Connecting a Hawkular
            endpoint with this option requires the CA certificate that
            the cluster uses for service certificates, which is stored
            in `/etc/origin/master/service-signer.crt` on the first
            master in a cluster.
            
            </div>
        
          - **SSL without validation**: Authenticate the provider
            insecurely using SSL. (Not recommended)
    
    2.  Enter the **Hostname** (or IPv4 or IPv6 address) of the
        provider, or use the **Detect** button to find the hostname.
    
    3.  Enter the **API Port** if your Hawkular or Prometheus provider
        uses a non-standard port for access. The default port is `443`.
    
    4.  Click **Validate** to confirm that ManageIQ can connect to the
        metrics endpoint.

11. Click the **Advanced** tab to add image inspector settings for
    scanning container images on your provider using OpenSCAP.
    
    <div class="note">
    
      - These settings control downloading the image inspector container
        image from the registry and obtaining the Common Vulnerabilities
        and Exposures (CVE) information (for effective scanning) via a
        proxy.
    
      - CVE URL that ManageIQ requires to be open for OpenSCAP scanning:
        <https://www.redhat.com/security/data/metrics/ds/>. This
        information is based on the source code of OpenSCAP.
    
    </div>
    
    1.  Enter the proxy information for the provider in either **HTTP**,
        **HTTPS**, or **NO Proxy** depending on your environment.
    
    2.  Enter the **Image-Inspector Repository** information. For
        example, `openshift3/image-inspector`.
    
    3.  Enter the **Image-Inspector Registry** information. For example,
        `registry.access.redhat.com`.
    
    4.  Enter the **Image-Inspector Tag** value. A tag is a mark used to
        differentiate images in a repository, typically by the
        application version stored in the image.
    
    5.  Enter `https://www.redhat.com/security/data/metrics/ds/` in
        **CVE location**.

12. Click **Add**.

<div class="note">

You can also set global default image-inspector settings for all
OpenShift providers in the advanced settings menu by editing the values
under `ems_kubernetes`, instead of setting this for each provider.

For example:

    :image_inspector_registry: registry.access.redhat.com
    :image_inspector_repository: openshift3/image-inspector

</div>

## Tagging Containers Providers

Apply tags to all containers providers to categorize them together at
the same time.

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span>.

2.  Select the checkboxes for the containers providers to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/1851.png)(**Edit Tags**).

4.  Select a tag to assign from the drop-down menu.
    
    ![2219](images/2219.png)

5.  Select a value to assign.

6.  Click **Save**.

## Removing Containers Providers

You may want to remove a containers provider from the VMDB if the
provider is no longer in use.

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span>.

2.  Select the checkboxes for the containers providers to remove.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Remove Containers Providers from the VMDB](images/2098.png)
    (**Remove Containers Providers from Inventory**).

4.  Click **OK**.

## Pausing / Resuming Containers Providers

In ManageIQ, you can pause and resume containers providers. This allows
users to add a number of potentially resource-intensive providers, then
pause and resume those that are not required at a given time.
Additionally, when performing maintenance on a provider, you can pause
the provider to prevent ManageIQ from connecting to it, to avoid
generating log errors or collecting partial data.

<div class="note">

  - While the provider is paused no data will be collected from it. This
    may cause gaps in inventory, metrics and events.

  - Also, the provider itself is not turned off when paused, but only
    temporarily disables the link between ManageIQ and the provider.
    Resuming the provider re-enables the link between ManageIQ and the
    provider.

</div>

To pause a containers provider:

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span>.

2.  Click the containers provider that you want to pause.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Pause this Containers
    Provider](images/pause-containers-provider.png) (**Pause this
    Containers Provider**).

4.  Click **OK**.

To resume a paused containers provider:

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span>.

2.  Click the paused containers provider that you want to resume.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Resume this Containers
    Provider](images/resume-containers-provider.png) (**Resume this
    Containers Provider**).

4.  Click **OK**.

## Editing a Containers Provider

Edit information about a provider such as the name, hostname, IP address
or port, and credentials as required. If you have just upgraded your
ManageIQ environment from an older version, edit the provider to specify
the authentication method the provider uses to connect to ManageIQ.

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span>.

2.  Click the containers provider to edit.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Edit Selected Containers Provider](images/1851.png) (**Edit
    Selected Containers Provider**).

4.  Edit the **Name** if required.
    
    <div class="note">
    
    The **Type** value is unchangeable.
    
    </div>

5.  Under **Endpoints** in the **Default** tab, edit the following as
    required:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the provider:
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option.
        
          - **SSL trusting custom CA**: Authenticate the provider with a
            self-signed certificate. For this option, copy your
            provider’s CA certificate to the **Trusted CA
            Certificates** box in PEM format.
            
            <div class="note">
            
            You can obtain your OpenShift Container Platform provider’s
            CA certificate for all endpoints (default, metrics, alerts)
            from `/etc/origin/master/ca.crt`. Paste the output (a block
            of text starting with `-----BEGIN CERTIFICATE-----`) into
            the **Trusted CA Certificates** field.
            
            </div>
        
          - **SSL without validation**: Authenticate the provider
            insecurely (not recommended).
    
    2.  Enter the **Hostname** (or IPv4 or IPv6 address) of the
        provider.
        
        <div class="important">
        
        The **Hostname** must use a unique fully qualified domain name.
        
        </div>
    
    3.  Enter the **API Port** of the provider. The default port is
        `8443`.
    
    4.  Enter a token for your provider in the **Token** box.
        
        <div class="note">
        
        To obtain a token for your provider, run the `oc get secret`
        command on your provider; see [Obtaining an OpenShift Container
        Platform Management
        Token](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#Obtaining_OpenShift_Container_Platform_Management_Token).
        
        For example:
        
        \# oc get secret --namespace management-infra
        management-admin-token-8ixxs --template='{{index .data
        "ca.crt"}}' | base64 --decode
        
        </div>
    
    5.  Click **Validate** to confirm that ManageIQ can connect to the
        OpenShift Container Platform provider.

6.  Under **Endpoints** in the **Metrics** tab, configure the following
    for gathering capacity and utilization metrics for Hawkular or
    Prometheus based on the selection:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the provider:
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option.
        
          - **SSL trusting custom CA**: Authenticate the provider with a
            self-signed certificate. For this option, copy your
            provider’s CA certificate to the **Trusted CA
            Certificates** box in PEM format.
        
          - **SSL without validation**: Authenticate the provider
            insecurely using SSL. (Not recommended)
    
    2.  Enter the **Hostname** (or IPv4 or IPv6 address) of the
        provider.
    
    3.  Enter the **API Port** if your provider uses a non-standard port
        for access. The default port is `443`.
    
    4.  Click **Validate** to confirm that ManageIQ can connect to the
        endpoint.

7.  Under **Endpoints** in the **Alerts** tab, configure the following
    for Prometheus alerting from the cluster.
    
      - **SSL**: Authenticate the provider securely using a trusted
        Certificate Authority. Select this option if the provider has a
        valid SSL certificate and it is signed by a trusted Certificate
        Authority. No further configuration is required for this option.
    
      - **SSL trusting custom CA**: Authenticate the provider with a
        self-signed certificate. For this option, copy your provider’s
        CA certificate to the **Trusted CA Certificates** box in PEM
        format.
    
      - **SSL without validation**: Authenticate the provider insecurely
        using SSL. (Not recommended)
        
        1.  Enter the **Hostname** (or IPv4 or IPv6 address) of the
            provider.
        
        2.  Enter the **API Port** if your provider uses a non-standard
            port for access. The default port is `443`.
        
        3.  Click **Validate** to confirm that ManageIQ can connect to
            the endpoint.

8.  Click **Save**.

## Hiding Environment Variables for Containers Providers

You can restrict users from viewing container provider environment
variables by configuring user roles.

This is useful as the environment variables panel can expose sensitive
information, such as passwords, that you may not want certain users to
view.

<div class="note">

The default user roles in ManageIQ are read-only. To customize a role’s
settings, create a new role or a copy of an existing role.

</div>

You can view role information and the product features the role can
access (marked by a checkmark) by clicking on any role in **Access
Control**. Expand the categories under **Product Features** to see
further detail.

To configure user access to container environment variables:

1.  Click ![config gear](images/config-gear.png) (**Configuration**).

2.  Click the **Access Control** accordion, then click **Roles**.

3.  Select a existing custom role from the **Access Control Roles**
    list, and click ![1847](images/1847.png) (**Configuration**), then
    ![1851](images/1851.png) (**Edit the selected Role**).
    
    Alternatively, to create a new custom role, select a role from the
    **Access Control Roles** list, and click ![1847](images/1847.png)
    (**Configuration**), then ![1851](images/1851.png) (**Copy this Role
    to a new Role**).

4.  Edit the name for the role if desired.

5.  For **Access Restriction for Services, VMs, and Templates**, select
    if you want to limit users with this role to only see resources
    owned by the user or their group, owned by the user, or all
    resources (**None**).

6.  Expand the **Product Features (Editing)** tree options to show
    <span class="menuchoice">Everything \> Compute \> Containers \>
    Containers Explorer \> All Containers \> View Containers</span>.

7.  Clear the **Environment Variables** checkbox to restrict the user
    role from viewing container environment variables.
    
    ![restrict env vars](images/restrict_env_vars.png)

8.  Click **Save**.

For more information about user roles, see
[Roles](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/general_configuration/#roles)
in *General Configuration*.

## Viewing a Containers Provider’s Timeline

View the timeline of events for instances registered to a containers
provider.

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span>.

2.  Click the desired containers provider for viewing the timeline.

3.  Click ![Monitoring](images/1994.png) (**Monitoring**), and then
    ![Timelines](images/1995.png) (**Timelines**).

4.  From **Options**, customize the period of time to display and the
    types of events to see.
    
      - Use **Show** to select regular Management Events or Policy
        Events.
    
      - Use the **Interval** dropdown to select hourly or daily data
        points.
    
      - Use **Date** to type the date for the timeline to display.
    
      - If you select to view a daily timeline, use **Show** to set how
        many days back to go. The maximum history is 31 days.
    
      - From the **Level** dropdown, select a **Summary** event, or a
        **Detail** list of events.
    
      - The three **Event Groups** dropdowns allow you to select
        different groups of events to display. Each has its own color.

Click on an item for more detailed information.

# Storage Managers

In ManageIQ, a storage manager is a service providing storage resources
that you can manage from a ManageIQ appliance. This chapter describes
the different types of storage managers used by ManageIQ, and how they
are added to ManageIQ.

There are three types of storage managers currently available to
ManageIQ:

  - Amazon Elastic Block Store

  - OpenStack Block Storage (`openstack-cinder`)

  - OpenStack Object Storage (`openstack-swift`)

## Amazon Elastic Block Store Managers

The Amazon Elastic Block Store service provides and manages persistent
block storage resources that Amazon EC2 instances can consume.

To use the Amazon Elastic Block Store service as a storage manager, you
must first add an Amazon EC2 cloud provider to your ManageIQ appliance.
The Amazon Elastic Block Store service is automatically discovered by
ManageIQ, and added to the **Storage Managers** list. See [Adding Amazon
EC2 Providers](#adding-amazon-ec2-providers) for instructions on adding
an Amazon EC2 cloud provider.

## OpenStack Block Storage Managers

The OpenStack Block Storage service (`openstack-cinder`) provides and
manages persistent block storage resources that OpenStack infrastructure
instances can consume.

To use OpenStack Block Storage as a storage manager, you must first add
an OpenStack cloud provider to your ManageIQ appliance and enable
events. The Block Storage service will be automatically discovered by
ManageIQ and added to the **Storage Managers** list in ManageIQ. See
[Adding OpenStack Providers](#adding_openstack_cloud_providers) for
instructions on adding a cloud provider and enabling events.

## OpenStack Object Storage Managers

The OpenStack Object Storage (`openstack-swift`) service provides cloud
object storage.

To use the OpenStack Object Storage service as a storage manager, you
must first add an OpenStack cloud provider to your ManageIQ appliance
and enable events. The Object Storage service will be automatically
discovered by ManageIQ and added to the **Storage Managers** list in
ManageIQ. See [Adding OpenStack
Providers](#adding_openstack_cloud_providers) for instructions on adding
a cloud provider and enabling events.

### Viewing Object Stores

The object store summary page shows details including the object store’s
size, parent cloud, storage manager, cloud tenant, and the number of
cloud objects on the object store.

In ManageIQ, view object stores on a object storage manager by following
these steps:

1.  Navigate to <span class="menuchoice">Storage \> Object Stores</span>
    to display a list of object store containers.

2.  Click a container to open a summary page for that object store
    container.

3.  Click **Cloud Objects** to view a list of object stores in the
    object store container.

4.  Click an object store from the list to view the object store’s
    summary page.

# Appendix

## Using a Self-Signed CA Certificate

Adding a self-signed Certificate Authority (CA) certificate for SSL
authentication requires additional configuration on OpenStack Platform
and Microsoft System Center Virtual Machine Manager (SCVMM) providers.

<div class="note">

This procedure is not required for OpenShift Container Platform, Red Hat
Virtualization, or middleware manager providers, which have the option
to select **SSL trusting custom CA** as a **Security Protocol** in the
user interface. These steps are needed only for providers without this
option in the user interface.

</div>

Before adding the provider, configure the following:

1.  Copy your provider’s CA certificate in PEM format to
    `/etc/pki/ca-trust/source/anchors/` on your ManageIQ appliance.

2.  Update the trust settings on the appliance:
    
        # update-ca-trust

3.  Restart the EVM processes on the server:
    
        # rake evm:restart

The CA certificate is added to the appliance, and you can add the
provider to ManageIQ.
