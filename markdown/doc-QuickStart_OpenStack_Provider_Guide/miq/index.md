Unresolved directive in index.adoc -
include::topics/common/introduction.adoc\[\]

# Installing ManageIQ

Unresolved directive in index.adoc - include::topics/installing.adoc\[\]

## Obtaining the ManageIQ Appliance

1.  In a browser, navigate to
    [manageiq.org/download](manageiq.org/download).

2.  Select **OpenStack** from the **--Choose your platform--** list.

3.  Select **Stable (fine-2)** from the **--Choose a release--** list.

4.  Follow the instructions to download the appliance.

## Deploying the Appliance as a Virtual Machine

Upon obtaining the ManageIQ appliance, deploy it in a network where it
can communicate with the OpenStack management network. You can deploy
the appliance on bare metal or as a virtual machine.

To deploy the appliance as a virtual machine, perform the following
steps:

1.  Log in as `root` to the virtual machine host.

2.  Copy the appliance to `/var/lib/libvirt/images/`.

3.  Run `virt-manager`. Doing so will launch the Virtual Machine
    Manager.

4.  Enter a name for the virtual machine in the **Name** field; for
    example, use `my-cfme`. Select **Import existing disk image** and
    click **Forward**.
    
    ![virt manager install step1](images/virt-manager-install-step1.png)

5.  Click **Browse** to select the copy of the appliance stored in
    `/var/lib/libvirt/images/`.
    
    ![virt manager install step2](images/virt-manager-install-step2.png)
    
    Select **Linux** from the **OS type** drop-down. For **Version**,
    select **Red Hat Enterprise Linux 7 or later**. Click **Forward**.

6.  Configure the appliance with 4 CPUs and 8192MiB or memory. Select
    **Customize configuration before install** then click **Finish**.
    
    ![virt manager install step3](images/virt-manager-install-step3.png)

7.  Add a second network interface for the virtual machine. Select
    **virtio** as its **Device Model**.
    
    ![virt manager install step4](images/virt-manager-install-step4.png)

8.  Configure the virtual machine with two additional virtual disks. One
    will be used for the internal database
    ([???](#configuring_a_database)), while the other will be used for
    mounting images and SmartState analysis.
    
    ![virt manager install step5](images/virt-manager-install-step5.png)

9.  Click **Finish** to launch the virtual machine.

# Configuring ManageIQ

Unresolved directive in index.adoc -
include::topics/configuration-quick.adoc\[\]

# Adding an OpenStack Infrastructure Provider

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
    certificate using the steps in [???](#app-self_signed_CA) before
    adding the provider.

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

## Configuring the Undercloud to Store Events

To allow ManageIQ to receive events from a Red Hat OpenStack Platform
environment, you must configure the **notification\_driver** option for
the Compute service and Orchestration service in that environment. See
[Installing the
Undercloud](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/director_installation_and_usage/#chap-Installing_the_Undercloud)
and [Configuring the
Director](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/director_installation_and_usage/#sect-Configuring_the_Director)
in Red Hat OpenStack Platform *Director Installation and Usage* for
related details.

# Adding an OpenStack Cloud Provider

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
the steps in [???](#app-self_signed_CA) before adding the provider.

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

## Configuring the Overcloud to Store Events

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

# Performing a SmartState Analysis

ManageIQ can analyze a cloud Instance or infrastructure host to collect
metadata such as user accounts, applications, software patches, and
other internal information. This feature is called SmartState Analysis.
SmartState analysis can be initiated manually or automatically using
Control Policies.

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

# Managing Policies

Unresolved directive in index.adoc -
include::topics/managing-policies.adoc\[\]

# Managing Instances

Cloud instance provision goes through three phases:

1.  Request: This includes ownership information, tags, virtual hardware
    requirements, the operating system, and any customization required.

2.  Approval: Provisioning requests are then approved or denied. This
    phase can happen automatically or manually.

3.  Provision: Approved provisioning requests are executed.

## Provisioning an OpenStack Instance from an Image

Create a request to provision Red Hat OpenStack Platform cloud instances
from images, volumes, and volume snapshots using ManageIQ. Only bootable
volumes not in use will be available.

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
    request denied. The other information is optional. If the ManageIQ
    Server is configured to use LDAP, you can use the **Look Up** button
    to populate the other fields based on the email address.
    
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

# Catalogs and Services

Unresolved directive in index.adoc -
include::topics/catalogs-services.adoc\[\]

# Reports

Unresolved directive in index.adoc - include::topics/reports.adoc\[\]

# Chargeback

Unresolved directive in index.adoc - include::topics/chargeback.adoc\[\]

# Customizing Provisioning Dialogs

The default set of provisioning dialogs shows all possible options.
However, ManageIQ also provides the ability to customize which tabs and
fields are shown. You can decide what fields are required to submit the
provisioning request or set default values.

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
