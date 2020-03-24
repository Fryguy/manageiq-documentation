A tenant is an OpenStack term for an organizational unit or project.
{product-title\_short} creates cloud tenants to match existing OpenStack
tenants for managing resources and controlling visibility of objects.

<div class="note">

OpenStack tenant mapping must be enabled for cloud tenants to be
created. See [Tenant Mapping](#tenant-mapping) for details.

</div>

OpenStack uses tenants for the following reasons:

  - Assigning users to a project

  - Defining quotas for a project

  - Applying access and security rules for a project

  - Managing resources and instances for a project

This helps administrators and users organize their OpenStack environment
and define limits for different groups of people. For example, one
project might require higher quotas and another project might require
restricted access to certain ports. OpenStack allows you to define these
limits and apply them to a project.

{product-title} can abstract information from tenants including quotas
and relationships to other OpenStack objects.

To see multiple tenants in {product-title}, the user authenticating to
your OpenStack environment from {product-title} must be configured to
have visibility into these tenants.

<div class="note">

This section describes OpenStack cloud tenant usage. For information
about tenants created in {product-title\_short} for access and resource
control, see [Access
Control](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/general_configuration/#access-control)
in *General Configuration*.

</div>

# Tenant Mapping

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

Unresolved directive in Tenants.adoc -
include::Viewing\_a\_Tenant.adoc\[\]
