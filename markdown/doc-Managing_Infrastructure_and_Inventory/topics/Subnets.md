# Creating and Administering Subnets

{product-title} enables creation and administration of subnets for your
cloud networks. Create subnets in pre-existing networks as means to
grant network connectivity to instances. Subnets are the means by which
instances are granted network connectivity. Each instance is assigned to
a subnet as part of the instance creation process.

Consider proper placement of instances to best accommodate their
connectivity requirements:

  - Tenant networks in OpenStack Networking can host multiple subnets.

  - Subnets are isolated from one another.

  - Host distinctly different systems on different subnets within the
    same network.

  - Instances on one subnet that wish to communicate with another subnet
    must have traffic directed by a router.

  - Place systems requiring a high volume of traffic amongst themselves
    in the same subnet, avoiding routing and subsequent latency and load
    issues.

Unresolved directive in Subnets.adoc -
include::Adding\_a\_Subnet.adoc\[\]

Unresolved directive in Subnets.adoc -
include::Editing\_a\_Subnet.adoc\[\]
