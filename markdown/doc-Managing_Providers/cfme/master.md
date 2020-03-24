# 

Red Hat CloudForms can manage a variety of external environments, known
as providers and managers. A provider or manager is any system that
CloudForms integrates with for the purpose of collecting data and
performing operations.

In CloudForms, a *provider* is an external virtualization, cloud, or
containers environment that manages multiple virtual machines or
instances residing on multiple hosts. One example is Red Hat
Virtualization, a platform that manages multiple hosts and virtual
machines.

In CloudForms, a *manager* is an external management environment that
manages more than one type of resource. One example of a manager is
OpenStack, which manages infrastucture, cloud, network, and storage
resources.

This guide covers working with providers and managers in CloudForms,
which include:

  - Infrastructure providers

  - Configuration management providers

  - Automation management providers

  - Cloud providers

  - Networking management providers

  - Middleware management providers

  - Container providers

  - Storage managers

For information on working with the resources contained by a provider or
manager, see [Managing Infrastructure and
Inventory](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_infrastructure_and_inventory/).

Unresolved directive in master.adoc -
include::topics/Infrastructure\_Providers.adoc\[\]

Unresolved directive in master.adoc -
include::topics/Configuration\_Management\_Providers.adoc\[\]

Unresolved directive in master.adoc -
include::topics/Automation\_Management\_Providers.adoc\[\]

Unresolved directive in master.adoc -
include::topics/Cloud\_Providers.adoc\[\]

Unresolved directive in master.adoc -
include::topics/Networking\_Providers.adoc\[\]

Unresolved directive in master.adoc -
include::topics/Containers\_Providers.adoc\[\]

Unresolved directive in master.adoc -
include::topics/Storage\_Managers.adoc\[\]

# Appendix

## Using a Self-Signed CA Certificate

Adding a self-signed Certificate Authority (CA) certificate for SSL
authentication requires additional configuration on OpenStack Platform
and Microsoft System Center Virtual Machine Manager (SCVMM) providers.

<div class="note">

This procedure is not required for OpenShift Container Platform, Red Hat
Virtualization, or middleware manager providers, which have the option
to select **SSL trusting custom CA** as a **Security Protocol** in the
user interface. These steps are needed only for providers without this
option in the user interface.

</div>

Before adding the provider, configure the following:

1.  Copy your provider’s CA certificate in PEM format to
    `/etc/pki/ca-trust/source/anchors/` on your CloudForms appliance.

2.  Update the trust settings on the appliance:
    
        # update-ca-trust

3.  Restart the EVM processes on the server:
    
        # rake evm:restart

The CA certificate is added to the appliance, and you can add the
provider to CloudForms.
