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
