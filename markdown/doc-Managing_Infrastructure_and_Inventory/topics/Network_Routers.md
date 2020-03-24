# Configuring Network Routers

{product-title} enables configuration for Red Hat OpenStack Platform
provider cloud network routing services using an SDN-based virtual
router.

  - Routers are a requirement for your instances to communicate with
    external subnets, including those out in the physical network.

  - Routers and subnets connect using interfaces, with each subnet
    requiring its own interface to the router.

  - A router’s default gateway defines the next hop for any traffic
    received by the router.

  - A router’s network is typically configured to route traffic to the
    external physical network using a virtual bridge.

Unresolved directive in Network\_Routers.adoc -
include::Adding\_Network\_Router.adoc\[\]

Unresolved directive in Network\_Routers.adoc -
include::Editing\_a\_Network\_Router.adoc\[\]

Unresolved directive in Network\_Routers.adoc -
include::Adding\_an\_Interface\_to\_Network\_Router.adoc\[\]

Unresolved directive in Network\_Routers.adoc -
include::Removing\_an\_Interface.adoc\[\]

Unresolved directive in Network\_Routers.adoc -
include::Deleting\_a\_Router.adoc\[\]
