# Creating Floating IPs

Floating IP addresses allow you to direct ingress network traffic to
your cloud network instances. Define a pool of validly routable external
IP addresses, which can then be dynamically assigned to an instance. All
incoming traffic destined for that floating IP is routed to the instance
to which it has been assigned.

<div class="note">

Red Hat OpenStack Networking allocates floating IP addresses to all
projects (tenants) from the same IP ranges/CIDRs. As a result, every
subnet of floating IPs is consumable by any and all projects. Manage
this behavior using quotas for specific projects.

</div>

Unresolved directive in Floating\_IPs.adoc -
include::Adding\_Floating\_IPs.adoc\[\]

Unresolved directive in Floating\_IPs.adoc -
include::Editing\_a\_Floating\_IP.adoc\[\]

Unresolved directive in Floating\_IPs.adoc -
include::Deleting\_a\_FloatingIP.adoc\[\]
