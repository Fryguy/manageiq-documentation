Unresolved directive in master.adoc -
include::topics/common/introduction.adoc\[\]

# Key Red Hat CloudForms Features for OpenStack Cloud Providers

Red Hat CloudForms provides several interface features specific to
OpenStack cloud providers:

  - The CloudForms **Topology** widget ([Using the Topology
    Widget](#using-the-topology-widget)) provides an interactive
    visualization of the OpenStack cloud.

  - CloudForms provides a user interface for managing OpenStack storage
    resources ([Managing Storage](#storage_managers)).

  - *Custom buttons*, which allows you to provide automation for
    specific actions to OpenStack tenants
    ([appendix\_title](#custom-button-tenants)).

When adding an OpenStack cloud provider, you can also:

  - Enable *tenant mapping*. This creates a one-to-one association
    between tenants in CloudForms and OpenStack.

  - Connect to OpenStack through the Keystone V3 API. This API enables
    multiple OpenStack identity domains. Domains are high-level
    containers for projects, users, and groups. Users of different
    domains can be represented in different authentication back ends.

For information about tenant mapping and the Keystone V3 API, see
[Adding an OpenStack Cloud Provider](#add-openstack-oc).

# Installing and Configuring Red Hat CloudForms

Unresolved directive in master.adoc -
include::topics/installing.adoc\[\]

## Configuring Red Hat CloudForms

Unresolved directive in master.adoc -
include::topics/configuration-quick.adoc\[\]

# Adding an OpenStack Infrastructure Provider

After initial installation and creation of a Red Hat CloudForms
environment, add an OpenStack infrastructure provider to the appliance.
Red Hat CloudForms supports operating with the OpenStack `admin` tenant.
When creating an OpenStack infrastructure provider in Red Hat
CloudForms, select the OpenStack infrastructure provider’s `admin` user
because it is the default administrator of the OpenStack `admin` tenant.
When using the `admin` credentials, a user in Red Hat CloudForms
provisions into the `admin` tenant, and sees images, networks, and
instances that are associated with the `admin` tenant.

<div class="note">

  - You can set whether Red Hat CloudForms should use the Telemetry
    service or Advanced Message Queueing Protocol (AMQP) for event
    monitoring. If you choose Telemetry, you should first configure the
    **ceilometer** service on the undercloud to store events. See
    [Configuring the Undercloud to Store Events](#openstack-events-uc)
    for instructions. For more information, see [OpenStack Telemetry
    (ceilometer)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/architecture_guide/#comp-telemetry)
    in the Red Hat OpenStack Platform *Architecture Guide*.

  - To authenticate the provider using a self-signed Certificate
    Authority (CA), configure the CloudForms appliance to trust the
    certificate using the steps in
    [appendix\_title](#app-self_signed_CA) before adding the provider.

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
    
    5.  Click **Validate** to confirm Red Hat CloudForms can connect to
        the OpenStack provider.

8.  Next, configure how Red Hat CloudForms should receive events from
    the OpenStack provider. Click the **Events** tab in the
    **Endpoints** section to start.
    
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

Red Hat CloudForms requires that the `adminURL` endpoint for all
OpenStack services be on a non-private network. Accordingly, assign the
adminURL endpoint an IP address of something other than `192.168.x.x`.
The `adminURL` endpoint must be accessible to the Red Hat CloudForms
appliance that is responsible for collecting inventory and gathering
metrics from the OpenStack environment. Additionally, all the Keystone
endpoints must be accessible, otherwise refresh will fail.

</div>

## Configuring the Undercloud to Store Events

To allow Red Hat CloudForms to receive events from a Red Hat OpenStack
Platform environment, you must configure the **notification\_driver**
option for the Compute service and Orchestration service in that
environment. See [Installing the
Undercloud](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/director_installation_and_usage/#chap-Installing_the_Undercloud)
and [Configuring the
Director](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/director_installation_and_usage/#sect-Configuring_the_Director)
in Red Hat OpenStack Platform *Director Installation and Usage* for
related details.

# Adding an OpenStack Cloud Provider

Red Hat CloudForms supports operating with the OpenStack `admin` tenant.
When creating an OpenStack provider in Red Hat CloudForms, select the
OpenStack provider’s `admin` user because it is the default
administrator of the OpenStack `admin` tenant. When using the `admin`
credentials, a user in Red Hat CloudForms provisions into the `admin`
tenant, and sees images, networks, and instances that are associated
with the `admin` tenant.

<div class="note">

In OpenStack, you must add `admin` as a member of all tenants that users
want to access and use in CloudForms.

See [Cloud
Tenants](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/5.0-beta/html-single/managing_infrastructure_and_inventory/index#tenants)
in *Managing Infrastructure and Inventory* for information on working
with OpenStack tenants (projects) in CloudForms.

</div>

When adding an OpenStack cloud or infrastructure provider, enable
*tenant mapping* in CloudForms to map any existing tenants from that
provider.

This means CloudForms will create new cloud tenants to match each
existing OpenStack tenant; each new cloud tenant and its corresponding
OpenStack tenant will have identical resource assignments (including
user and role synchronization) with the exception of quotas. Tenant
quotas are not synchronized between CloudForms and OpenStack, and are
available for reporting purposes only. You can manage quotas in
CloudForms but this will not affect the quotas created in OpenStack.

During a provider refresh, CloudForms will also check for any changes to
the tenant list in OpenStack. CloudForms will create new cloud tenants
to match any new tenants, and delete any cloud tenants whose
corresponding OpenStack tenants no longer exist. CloudForms will also
replicate any changes to OpenStack tenants to their corresponding cloud
tenants.

If you leave tenant mapping disabled, CloudForms will not create cloud
tenants or tenant object hierarchy from OpenStack.

See
[Chargeback](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/monitoring_alerts_and_reporting/#sect_chargeback)
in *Managing Providers* for information on configuring OpenStack
providers.

<div class="note">

You can set whether Red Hat CloudForms should use the Telemetry service
or Advanced Message Queueing Protocol (AMQP) for event monitoring. If
you choose Telemetry, you should first configure the **ceilometer**
service on the overcloud to store events. See [Configuring the Overcloud
to Store Events](#openstack-events-oc) for instructions.

For more information, see [OpenStack Telemetry
(ceilometer)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/architecture_guide/components#comp-telemetry)
in the Red Hat OpenStack Platform *Architecture Guide*.

</div>

<div class="note">

To authenticate the provider using a self-signed Certificate Authority
(CA), configure the CloudForms appliance to trust the certificate using
the steps in [appendix\_title](#app-self_signed_CA) before adding the
provider.

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
    Red Hat CloudForms should use. This is the domain of the user
    account you will be specifying later in the **Default** tab. If
    domains are not configured in the provider, enter **default**.
    
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
    between the OpenStack cloud provider and CloudForms. By default,
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
    
    6.  Click **Validate** to confirm Red Hat CloudForms can connect to
        the OpenStack provider.

11. Next, configure how Red Hat CloudForms should receive events from
    the OpenStack provider. Click the **Events** tab in the
    **Endpoints** section to start.
    
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
    Red Hat CloudForms appliance requires that the adminURL endpoint for
    the OpenStack environment be on a non-private network. Hence, the
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

## Configuring the Overcloud to Store Events

By default, the Telemetry service does not store events emitted by other
services in a Red Hat OpenStack Platform environment. The following
procedure outlines how to enable the Telemetry service on your OpenStack
cloud provider to store such events. This ensures that events are
exposed to Red Hat CloudForms when a Red Hat OpenStack Platform
environment is added as a cloud provider.

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

# Performing a SmartState Analysis

Red Hat CloudForms can analyze a cloud Instance or infrastructure host
to collect metadata such as user accounts, applications, software
patches, and other internal information. This key CloudForms feature is
called SmartState Analysis. SmartState analysis can be initiated
manually or automatically using Control Policies.

To manually initiate SmartState analysis on an instance:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click on an instance in the **All Instances by Provider** nsection.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1942](images/1942.png) (**Perform SmartState Analysis**). A pop-up
    window will appear to confirm the action.

4.  Click **OK**. The SmartState analysis will be initiated for the
    selected instance.

To manually initiate SmartState analysis on an Infrastructure host:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Select a node in the **Nodes** section.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1942](images/1942.png) (**Perform SmartState Analysis**). A pop-up
    window will appear to confirm the action.

4.  Click **OK**. The SmartState analysis will be initiated for the
    selected node.

# Using the Topology Widget

The **Topology** widget is an interactive topology graph, showing the
status and relationships between the different resources and entities of
the OpenStack providers that Red Hat CloudForms has access to.

  - The topology graph includes instances, nodes, and other cloud
    resources within the overall OpenStack cloud provider environment.

  - Each entity in the graph displays a color indication of its status.

  - Hovering over any individual graph element will display a summary of
    details for the individual element.

  - Double-click the entities in the graph to navigate to their summary
    pages.

  - It is possible to drag elements to reposition the graph.

  - Click the legend at the top of the graph to show or hide entities.

  - Click **Display Names** on the right-hand side of the page to show
    or hide entity names.

To view an OpenStack provider through the **Topology** widget:

1.  Navigate to <span class="menuchoice">Compute \> Cloud \>
    Providers</span>.

2.  Click the desired OpenStack cloud provider for viewing the provider
    summary.

3.  On the provider summary page, click **Topology** in the **Overview**
    box on the right-hand side of the page.

# Managing Policies

Unresolved directive in master.adoc -
include::topics/managing-policies.adoc\[\]

# Managing Instances

Cloud instance provisioning goes through three phases:

1.  Request: This includes ownership information, tags, virtual hardware
    requirements, the operating system, and any customization required.
    See [Provisioning
    Requests](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/provisioning_virtual_machines_and_hosts/#provisioning-requests)
    from the [Provisioning Virtual Machines and
    Hosts](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/provisioning_virtual_machines_and_hosts/)
    guide for more details.

2.  Approval: Provisioning requests are then approved or denied. This
    phase can happen automatically or manually. See [Provisioning
    Request Approval
    Methods](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/provisioning_virtual_machines_and_hosts/#provisioning-request-approval-methods)
    from the [Provisioning Virtual Machines and
    Hosts](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/provisioning_virtual_machines_and_hosts/)
    guide for more details.

3.  Provision: Approved provisioning requests are executed. See [Working
    with Provisioning
    Requests](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/provisioning_virtual_machines_and_hosts/#working-with-provisioning-requests)
    from the [Provisioning Virtual Machines and
    Hosts](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/provisioning_virtual_machines_and_hosts/)
    guide for more details.

## Provisioning an OpenStack Instance from an Image

Create a request to provision Red Hat OpenStack Platform cloud instances
from images, volumes, and volume snapshots using Red Hat CloudForms.
Only bootable volumes not in use will be available.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click ![2007](images/2007.png)(**Lifecycle**), then click
    ![1862](images/1862.png)(**Provision Instances**).

3.  Select an OpenStack image, volume or volume snapshot from the list
    presented. These files must be available on your OpenStack provider.

4.  Click **Continue**.

5.  On the **Request** tab, enter information about this provisioning
    request. In **Request Information**, type in at least an email
    address. This email is used to send the requester status emails
    during the provisioning process for items such as auto-approval,
    quota, provision complete, retirement, request pending approval, and
    request denied. The other information is optional. If the Red Hat
    CloudForms Server is configured to use LDAP, you can use the **Look
    Up** button to populate the other fields based on the email address.
    
    <div class="note">
    
    Parameters with a \* next to the label are required to submit the
    provisioning request. To change the required parameters, see
    [appendix\_title](#provisioning-dialogs-customizing).
    
    </div>

6.  Click the **Purpose** tab to select the appropriate tags for the
    provisioned instance.

7.  Click the **Catalog** tab for basic instance options.
    
    1.  To change the source file to use as a basis for the instance,
        select it from the list of images, volumes, or volume snapshots.
    
    2.  Select the **Number of Instances** to provision.
    
    3.  Type a **Instance Name** and **Instance Description**.

8.  Click the **Environment** tab to select the instance’s **Cloud
    Tenant**, **Availabilty Zones**, **Cloud Network**, **Security
    Groups**, and **Public IP Address**. If no specific Cloud Tenant is
    required, select the **Choose Automatically** checkbox.

9.  Click the **Properties** tab to set provider options such as flavors
    and security settings.
    
    1.  Select a flavor from the **Instance Type** list.
    
    2.  Select a **Guest Access Key Pair** for access to the instance.
        For more information about key pairs, see
        [appendix\_title](#provision-keypairs).

10. Click the **Volumes** tab to provision any volumes with the
    instance. Volumes are useful for augmenting ephemeral storage of
    instances with persistent, general-purpose block storage:
    
    1.  Fill in the **Volume Name** and **Size (gigabytes)** fields.
    
    2.  If you want the volume to be deleted once the instance
        terminates (thereby making it non-persistent), check **Delete on
        Instance Terminate**.
    
    3.  To provision and add multiple volumes to the instance, click
        **Add Volume**. Doing so will add new fields you can fill in.
        
        For more information about persistent storage in OpenStack, see
        the Red Hat OpenStack Platform *Storage Guide*.

11. Click the **Customize** tab to set additional instance options.
    
    1.  Under **Credentials**, enter a **Root Password** for the
        **root** user access to the instance.
    
    2.  Enter a **IP Address Information** for the instance. Leave as
        **DHCP** for automatic IP assignment from the provider.
    
    3.  Enter any **DNS** information for the instance if necessary.
    
    4.  Select a **Customize Template** for additional instance
        configuration. Select from the Cloud-Init scripts stored on your
        appliance.

12. Click the **Schedule** tab to set the provisioning and retirement
    date and time.
    
    1.  In **Schedule Info**, choose whether the provisioning begins
        upon approval, or at a specific time. If you select
        **Schedule**, you will be prompted to enter a date and time.
    
    2.  In **Lifespan**, select whether to power on the instances after
        they are created, and whether to set a retirement date. If you
        select a retirement period, you will be prompted for when to
        receive a retirement warning.

13. Click **Submit**.

The provisioning request is sent for approval. For the provisioning to
begin, a user with the admin, approver, or super admin account role must
approve the request. The admin and super admin roles can also edit,
delete, and deny the requests. You will be able to see all provisioning
requests where you are either the requester or the approver.

After submission, the appliance assigns each provision request a
**Request ID**. If an error occurs during the approval or provisioning
process, use this ID to locate the request in the appliance logs. The
Request ID consists of the region associated with the request followed
by the request number. As regions define a range of one trillion
database IDs, this number can be several digits long.

**Request ID Format**

Request 99 in region 123 results in Request ID 123000000000099.

# Managing Storage

Two types of storage managers are currently available to Red Hat
CloudForms: OpenStack Block Storage (`openstack-cinder`) and OpenStack
Object Storage (`openstack-swift`). OpenStack Block Storage provisions
and manages block storage, whereas OpenStack Object Storage manages
object storage within the cloud. These storage managers are discovered
automatically by Red Hat CloudForms after adding an OpenStack cloud
provider.

For more information, see [Storage
Managers](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#storage_managers)
from the [Managing
Providers](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/)
guide.

## Managing Block Storage

The OpenStack Block Storage service (`openstack-cinder`) provides and
manages persistent block storage resources that OpenStack infrastructure
instances can consume. CloudForms provides an interface for managing
these resources (volumes, volume backups, and volume snapshots).

To create a volume:

<div class="important">

After creating a volume, only the volume name can be edited.

</div>

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![1862](images/1862.png) (**Add a new Cloud Volume**).

3.  Select the OpenStack Block Storage manager from the **Storage
    Manager** list.

4.  Enter a **Volume Name**.

5.  Enter the size of the volume in gigabytes (GB).

6.  Under **Placement**, select the cloud tenant to attach it to.

7.  Click **Add**.

The volume appears in the list of volumes after it has been provisioned.

To attach a volume to an instance (for example, one created through
[Provisioning an OpenStack Instance from an
Image](#provisioning-an-openstack-instance-from-an-image)):

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to attach.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Attach selected Cloud Volume to an
    Instance](images/volume-icon.png) (**Attach selected Cloud Volume to
    an Instance**) to open the **Attach Cloud Volume** screen.

4.  Select an instance from the list.

5.  Optionally, enter a **Device Mountpoint**.

6.  Click **Attach**.

To view a timeline of storage manager events:

1.  Navigate to <span class="menuchoice">Storage \> Storage
    Managers</span>.

2.  Select your OpenStack Cinder manager to go to the Cinder manager’s
    summary page.

3.  Click ![Monitoring](images/1994.png) (**Monitoring**), and then
    ![Timelines](images/1995.png) (**Timelines**) to view the events
    timeline for the manager.

4.  A timeline of either management events or policy events can be
    viewed.
    
    1.  To view management events, select **Management Events**.
    
    2.  Specify the type of event to view.
    
    3.  Specify the timeline for the events to view.
    
    4.  Click **Apply**.

5.  To view policy events, select **Policy Events**.
    
    1.  Specify if you want to view successful events, failed events, or
        both.
    
    2.  Specify the timeline for the events to view.
    
    3.  Click **Apply**.

To back up a volume:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click the volume you want to back up to open the volume’s summary
    page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Create a Backup of this Cloud
    Volume](images/volume-icon.png) (**Create a Backup of this Cloud
    Volume**).

4.  Enter a name for the backup in **Backup Name**.

5.  (Optional) Select **Incremental?** to take an incremental backup of
    the volume instead of a full backup.
    
    <div class="note">
    
    You can take an incremental backup of a volume if you have at least
    one existing full backup of the volume. An incremental volume saves
    resources by capturing only changes made to the volume since its
    last backup. See [Create an Incremental Volume
    Backup](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/storage_guide/ch-cinder#section-create-volume-backup-incremental)
    in the *Storage Guide* for more information.
    
    </div>

6.  (Optional) Select **Force?** to allow backup of a volume attached to
    an instance.
    
    <div class="note">
    
    Selecting the **Force** option will back up the volume whether its
    status is *available* or *in-use*. Backing up an *in-use* volume
    ensures data is crash-consistent.
    
    </div>

7.  Click **Save**.

View a volume’s backups by clicking **Cloud Volume Backups** on the
volume’s summary page.

<div class="note">

See [Back Up and Restore a
Volume](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/storage_guide/ch-cinder#section-volumes-advanced-backup)
in the *Storage Guide* for more information about backups.

</div>

To take a volume snapshot:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click the volume to snapshot to open the volume’s summary page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Create a Snapshot of this Cloud
    Volume](images/volume-icon.png) (**Create a Snapshot of this Cloud
    Volume**).

4.  Enter a name for the snapshot in **Snapshot Name**.

5.  Click **Save**.

Click **Cloud Volume Snapshots** on the summary page of a volume to view
the snapshots for that volume.

<div class="note">

See [Create, Use, or Delete Volume
Snapshots](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/storage_guide/#section-create-clone-delete-vol-snapshots)
in the *Storage Guide* for more information about snapshots.

</div>

For more information about available options for block storage resources
in CloudForms, see [OpenStack Block Storage
Managers](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#openstack_block_storage_managers)
(from the [Managing
Providers](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/)
guide).

## Managing Object Storage

The OpenStack Object Storage (`openstack-swift`) service provides cloud
object storage. The object store summary page shows details including
the object store’s size, parent cloud, storage manager, cloud tenant,
and the number of cloud objects on the object store.

To view the summary page of an object store:

1.  Navigate to <span class="menuchoice">Storage \> Object Stores</span>
    to display a list of object store containers.

2.  Click a container to open a summary page for that object store
    container.

3.  Click **Cloud Objects** to view a list of object stores in the
    object store container.

4.  Click an object store from the list to view the object store’s
    summary page.

# Catalogs and Services

Unresolved directive in master.adoc -
include::topics/catalogs-services.adoc\[\]

# Reports

Unresolved directive in master.adoc - include::topics/reports.adoc\[\]

# Chargeback

Unresolved directive in master.adoc -
include::topics/chargeback.adoc\[\]

# Using a Self-Signed CA Certificate

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
    `/etc/pki/ca-trust/source/anchors/` on your CloudForms appliance.

2.  Update the trust settings on the appliance:
    
        # update-ca-trust

3.  Restart the EVM processes on the server:
    
        # rake evm:restart

The CA certificate is added to the appliance, and you can add the
provider to CloudForms.

# Customizing Provisioning Dialogs

The default set of provisioning dialogs shows all possible options.
However, Red Hat CloudForms also provides the ability to customize which
tabs and fields are shown. You can decide what fields are required to
submit the provisioning request or set default values.

For each type of provisioning, there is a dialog that can be created to
adjust what options are presented. While samples are provided containing
all possible fields for provisioning, you can remove what fields are
shown but cannot add new fields or tabs.

Edit the dialogs to:

1.  Hide or show provisioning tabs.

2.  Hide or show fields. If you hide an attribute, the default will be
    used, unless you specify otherwise.

3.  Set default values for a field.

4.  Specify if a field is required to submit the request.

5.  Create custom dialogs for specific users.

# Creating Custom Buttons for Cloud Tenants

CloudForms also allows you to create *custom buttons* for cloud tenants.
This is useful for providing shortcuts to functionalities and features
frequently used by specific tenants.

<div class="note">

This capability is made possible through the *Automate* model. See
[Understanding the Automate
Model](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/scripting_actions_in_cloudforms/#understanding-the-automate-model)
from the [Scripting Actions in
CloudForms](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/scripting_actions_in_cloudforms/)
guide for more details.

</div>

The following subsections summarize the two main steps for creating a
custom button for cloud tenants.

# Creating a Custom Button Group

A *button group* is a label for a collection of buttons under an *object
type*. To create a button group:

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  Click the **Buttons** accordion.

3.  From the **Object Types** tree, select the type of object you want
    to create the button group for.
    
    <div class="note">
    
    When creating a button group for OpenStack tenants, select **Cloud
    Tenant** as your object type.
    
    </div>

4.  Click ![image](images/1847.png)(**Configuration**),
    ![image](images/1862.png) (**Add a new Button Group**).

5.  Type in a **Button Group Text** and **Button Group Hover Text**, and
    select the **Button Group Image** you want to use.

6.  If custom buttons have already been created, assign them to the
    button group. If not, see [Creating a Custom
    Button](#create-a-custom-button) to create custom buttons.

7.  Click **Add**.

The button group will show in the **Cloud Tenant** object type. When it
does, create a custom button for any tenant within the OpenStack Cloud
(see [Creating a Custom Button](#create-a-custom-button)).

# Creating a Custom Button

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  Click the **Buttons** accordion.

3.  From the **Object Types** tree, select the type of object you want
    to create the button for.
    
    <div class="note">
    
    When creating a button for OpenStack tenants, select **Cloud
    Tenant** as your object type.
    
    </div>

4.  Click **Unassigned Buttons**.

5.  Click ![image](images/1847.png)(**Configuration**), then
    ![image](images/1862.png) (**Add a new Button**).
    
    <div class="note">
    
    If ![image](images/1862.png) (**Add a new Button**) is not
    available, that means you have not created a button group for that
    object. To continue, create a button group first. See [Creating a
    Custom Button Group](#create-custom-button-group)
    
    </div>

6.  Under the **Options** tab:
    
    1.  Select the **Button** type from the list.
    
    2.  Enter button **Text** and **Hover Text**, and select the
        **Icon** and **Icon Color** to use.
    
    3.  Select a **Dialog** if applicable.
    
    4.  Check **Open URL** to open a browser window for the custom URL
        returned when the button is executed.
    
    5.  Choose a **Display For** option for the button.
    
    6.  Select a **Submit** parameter to choose how to submit objects to
        automate. Selecting *Submit All* will pass all objects at once
        when the button is executed, while choosing *One by one* will
        run execute the button action each time per object.

7.  Under the **Advanced** tab:
    
    1.  Set button **Enablement**. Click **Define Expression** to access
        the expression editor tool. Enter **Disabled Button Text** to
        display when the custom button is disabled.
    
    2.  Use **Visibility** to determine button appearance based on a
        custom expression. Click **Define Expression** to access the
        expression editor tool.
        
        <div class="note">
        
        For more about setting visibility and enablement for a custom
        button, see [???](#filtering-actions-custom-buttons).
        
        </div>
    
    3.  In **Object Details**, select **Request** from the
        `/System/Process/` dropdown. By default, the message is
        `create`. Do not change it.
    
    4.  Enter a **Request** name for the `/System/Process/Request`
        instance.
    
    5.  Enter the **Attribute/Value Pairs** fields if applicable.
    
    6.  Set **Role Access**. Selecting *\<By Role\>* will display
        available roles. Check applicable roles.

8.  Click **Add** when you have confirmed that the button accomplishes
    the task you want.

The button will show in the object type you added the button to. See
[Invoking
Automate](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/scripting_actions_in_cloudforms/#invoking-automate)
from the [Scripting Actions in
CloudForms](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/scripting_actions_in_cloudforms/)
guide for more in-depth coverage.

# Managing Keypairs

Key pairs allow you to manage SSH access between a user and provisioned
instance. For more information about key pairs in OpenStack, see [Manage
Key
Pairs](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/instances_and_images_guide/ch-manage_instances#section-manage-keypair)
in the *Instances and Images Guide*.

To manage key pairs, navigate to <span class="menuchoice">Compute \>
Clouds \> Key Pairs</span>. From there, you can view a list of available
key pairs. Click on a key pair to view its details.

To create a new key pair:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \> Key
    Pairs</span>.

2.  Click ![1847](images/1847.png)(**Configuration**),
    ![2345](images/2345.png)(**Add a new Key Pair**).

3.  Enter a **Name** for the key pair.

4.  If you want to use a public key, copy its contents into the **Public
    Key (optional)** field.

5.  Select which cloud provider on which to create the key pair. The key
    pair will then be available for use by instances in that provider.

6.  Click **Add**.
