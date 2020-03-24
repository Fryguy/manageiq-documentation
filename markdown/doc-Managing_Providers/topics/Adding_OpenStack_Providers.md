{product-title} supports operating with the OpenStack `admin` tenant.
When creating an OpenStack provider in {product-title}, select the
OpenStack provider’s `admin` user because it is the default
administrator of the OpenStack `admin` tenant. When using the `admin`
credentials, a user in {product-title} provisions into the `admin`
tenant, and sees images, networks, and instances that are associated
with the `admin` tenant.

<div class="note">

In OpenStack, you must add `admin` as a member of all tenants that users
want to access and use in {product-title\_short}.

See [Cloud
Tenants](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/5.0-beta/html-single/managing_infrastructure_and_inventory/index#tenants)
in *Managing Infrastructure and Inventory* for information on working
with OpenStack tenants (projects) in {product-title\_short}.

</div>

When adding an OpenStack cloud or infrastructure provider, enable
*tenant mapping* in {product-title\_short} to map any existing tenants
from that provider.

This means {product-title\_short} will create new cloud tenants to match
each existing OpenStack tenant; each new cloud tenant and its
corresponding OpenStack tenant will have identical resource assignments
(including user and role synchronization) with the exception of quotas.
Tenant quotas are not synchronized between {product-title\_short} and
OpenStack, and are available for reporting purposes only. You can manage
quotas in {product-title\_short} but this will not affect the quotas
created in OpenStack.

During a provider refresh, {product-title\_short} will also check for
any changes to the tenant list in OpenStack. {product-title\_short} will
create new cloud tenants to match any new tenants, and delete any cloud
tenants whose corresponding OpenStack tenants no longer exist.
{product-title\_short} will also replicate any changes to OpenStack
tenants to their corresponding cloud tenants.

If you leave tenant mapping disabled, {product-title\_short} will not
create cloud tenants or tenant object hierarchy from OpenStack.

<div class="note">

You can set whether {product-title} should use the Telemetry service or
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
(CA), configure the {product-title\_short} appliance to trust the
certificate using the steps in [???](#app-self_signed_CA) before adding
the provider.

</div>

1.  Navigate to menu:Compute\[Clouds \> Providers\].

2.  Click ![1847](1847.png) (**Configuration**), then click
    ![1862](1862.png) (**Add a New Cloud Provider**).

3.  Enter a **Name** for the provider.

4.  From the **Type** list, select **OpenStack**.

5.  Select the appropriate **API Version** from the list. The default is
    `Keystone v2`.
    
    If you select `Keystone v3`, enter the `Keystone V3 Domain ID` that
    {product-title} should use. This is the domain of the user account
    you will be specifying later in the **Default** tab. If domains are
    not configured in the provider, enter **default**.
    
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
    between the OpenStack cloud provider and {product-title\_short}. By
    default, tenant mapping is disabled.

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
    
    6.  Click **Validate** to confirm {product-title} can connect to the
        OpenStack provider.

11. Next, configure how {product-title} should receive events from the
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
    {product-title} appliance requires that the adminURL endpoint for
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

# Configuring the Overcloud to Store Events

By default, the Telemetry service does not store events emitted by other
services in a Red Hat OpenStack Platform environment. The following
procedure outlines how to enable the Telemetry service on your OpenStack
cloud provider to store such events. This ensures that events are
exposed to {product-title} when a Red Hat OpenStack Platform environment
is added as a cloud provider.

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
