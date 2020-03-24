In {product-title}, a network manager is an inventory of networking
entities on existing cloud and infrastructure providers managed by your
{product-title\_short} appliance.

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
to {product-title\_short}, and how to manage them. Network managers are
discovered automatically by {product-title\_short} from other connected
providers.

Unresolved directive in Networking\_Providers.adoc -
include::Adding\_Viewing\_Network\_Providers.adoc\[\]

Unresolved directive in Networking\_Providers.adoc -
include::Refreshing\_Network\_Providers.adoc\[\]

Unresolved directive in Networking\_Providers.adoc -
include::Tagging\_Network\_Providers.adoc\[\]

Unresolved directive in Networking\_Providers.adoc -
include::Removing\_Network\_Providers.adoc\[\]

Unresolved directive in Networking\_Providers.adoc -
include::Viewing\_Network\_Providers\_Timeline.adoc\[\]

You can also assign policy profiles to network providers, or remove
them. The method for doing so is similar to that of any normal policy
profile.

Unresolved directive in Networking\_Providers.adoc -
include::Network\_Topology.adoc\[\]
