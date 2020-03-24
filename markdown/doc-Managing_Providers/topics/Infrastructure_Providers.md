In {product-title}, an infrastructure provider is a virtual
infrastructure environment that you can add to a {product-title\_short}
appliance to manage and interact with the resources in that environment.
This chapter describes the different types of infrastructure providers
that you can add to {product-title\_short}, and how to manage them.
Infrastructure providers can be either discovered automatically by
{product-title\_short}, or added individually.

The web interface uses virtual thumbnails to represent infrastructure
providers. Each thumbnail contains four quadrants by default, which
display basic information about each provider:

![2189](2189.png)

1.  Number of hosts

2.  Management system software

3.  Currently unused

4.  Authentication status

| Icon              | Description                                                                    |
| ----------------- | ------------------------------------------------------------------------------ |
| ![2190](2190.png) | Validated: Valid authentication credentials have been added.                   |
| ![2191](2191.png) | Invalid: Authentication credentials are invalid.                               |
| ![2192](2192.png) | Unknown: Authentication status is unknown or no credentials have been entered. |

Provider authentication status

Unresolved directive in Infrastructure\_Providers.adoc -
include::Discovering\_Multiple\_Management\_Systems.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Discovering\_Physical\_Infra\_Providers.adoc\[\]

# Red Hat Virtualization Providers

To use a Red Hat Virtualization provider, add it to the appliance and
authenticate its hosts. You can also configure capacity and utilization
data collection to help track usage and find common issues.

Unresolved directive in Infrastructure\_Providers.adoc -
include::Enabling\_Red\_Hat\_Virtualization\_CU.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Adding\_a\_Red\_Hat\_Virtualization\_Provider.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Authenticating\_Red\_Hat\_Virtualization\_Hosts.adoc\[\]

# OpenStack Infrastructure Providers

Enable an OpenStack Infrastructure provider by adding it to the
appliance.

Unresolved directive in Infrastructure\_Providers.adoc -
include::Adding\_an\_OpenStack\_Infrastructure\_Provider.adoc\[\]

## Discovering OpenStack Infrastructure Providers

{product-title} has the ability to discover OpenStack infrastructure
providers. In this process, {product-title\_short} scans a network
segment and searches for the Bare Metal (Ironic) service which runs on
port `6385` by default. Note that, currently, the discovery does not
work if the Bare Metal service has been moved to a different port.

1.  Navigate to menu:Compute\[Infrastructure \> Providers\].

2.  Click ![Configuration](1847.png) (**Configuration**), then click
    ![Discover Infrastructure Providers](1942.png) (**Discover
    Infrastructure Providers**).

3.  Select **OpenStack Infrastructure** under **Discover**.

4.  Provide a **Subnet Range**. Enter the **From Address** and **To
    Address** of the address range.

5.  Click **Start**.

# VMware vCenter Providers

To use a VMware vCenter provider, add it to the appliance and
authenticate its hosts.

Unresolved directive in Infrastructure\_Providers.adoc -
include::Adding\_a\_VMware\_vCenter\_Provider.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Nonadmin\_VMware\_vCenter\_Auth.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Authenticating\_VMware\_vCenter\_Hosts.adoc\[\]

# Microsoft SCVMM Providers

To use a Microsoft System Center Virtual Machine Manager (SCVMM)
provider, add it to the appliance and set up the SCVMM server for
authentication.

<div class="note">

To use a SCVMM provider, you must have at least one network adapter
available for communication between the host and the SCVMM management
server. Make sure that **Used by Management** is checked for this
network adapter in the SCVMM host properties.

</div>

Unresolved directive in Infrastructure\_Providers.adoc -
include::Authenticating\_to\_Microsoft\_SCVMM.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Adding\_a\_Microsoft\_System\_Center\_Virtual\_Machine\_Manager\_Provider.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Refreshing\_Multiple\_Management\_Systems.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Tagging\_Multiple\_Management\_Systems.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Reviewing\_a\_Management\_System.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::To\_remove\_Management\_Systems.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Viewing\_the\_Management\_System\_Timeline.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Viewing\_Hosts\_and\_Clusters.adoc\[\]

Unresolved directive in Infrastructure\_Providers.adoc -
include::Viewing\_Virtual\_Machines\_and\_Templates.adoc\[\]
