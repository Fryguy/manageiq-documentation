# Environment Overview

This guide describes how to configure and manage database high
availability in a {product-title} environment. This configuration allows
for disaster mitigation: a failure in the primary database does not
result in downtime, as the standby database takes over the failed
database’s processes. This is made possible by database replication
between two or more database servers. In {product-title\_short}, these
servers are *database-only {product-title\_short} appliances* which do
not have `evmserverd` processes enabled. This is configured from the
`appliance_console` menu at the time of deployment.

This guide describes two types of appliances used in high availability:

  - *Database-only {product-title\_short} appliances*, which do not have
    `evmserverd` processes enabled or a user interface.

  - *Non-database {product-title\_short} appliances*, which are standard
    appliances containing a user interface and which have `evmserverd`
    processes enabled.

In this configuration, a failover monitor daemon is configured and
running on each non-database {product-title\_short} appliance. The
failover monitor watches the `repmgr` metadata about the database-only
appliances present in the cluster. When the primary database-only
appliance goes down, the non-database {product-title\_short} appliances
start polling each of the configured standby database-only appliances to
monitor which one comes up as the new primary. The promotion is
orchestrated either by `repmgrd` on the database-only appliances or is
done manually. When the non-database {product-title\_short} appliances
find that a standby has been promoted, {product-title\_short}
reconfigures the setup by writing the new IP address in the
`database.yml` file to point to the new primary.

<div class="note">

Manual steps are required to reintroduce the failed database node back
as the standby server. See [???](#reintroducing_the_failed_node).

</div>

Note, this procedure also does not provide scalability or a multi-master
database setup. While a {product-title\_short} environment is comprised
of an engine tier and a database tier, this configuration affects only
the database tier and does not provide load balancing for the
appliances.

## Requirements

For a high availability {product-title} environment, you need a
virtualization host containing at minimum four virtual machines with
{product-title\_short} installed, consisting of:

  - One virtual machine for the primary external database containing a
    minimum of 4GB dedicated disk space

  - One virtual machine for the standby external database containing a
    minimum of 4GB dedicated disk space

  - Two virtual machines for the non-database {product-title\_short}
    appliances

The database-only appliances should reside on a highly reliable local
network in the same location.

<div class="important">

It is essential to use the same {product-title} appliance template
version to install each virtual machine in this environment.

</div>

Correct time synchronization is required before installing the cluster.
After installing the appliances, configure time synchronization on all
appliances using `chronyd`.
