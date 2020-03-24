In {product-title\_short}, a configuration management provider is a
systems management product that you can add to a {product-title\_short}
appliance to manage the lifecycle of your resources. Configuration
management providers are useful for uniformly applying changes and
updates across providers, and for recording and reporting status and
change activity. They can also help eliminate the confusion and error
brought about by the existence of different providers.

This chapter describes the different types of configuration management
providers available to {product-title\_short}, and how to manage them.
Configuration management providers must be added individually to
{product-title\_short}.

# Red Hat Satellite 6

Satellite 6 is a subscription and system management tool that provides a
way to provision hosts (both virtual and bare metal) and configure them
using a set of Puppet modules. {product-title} provides functionality to
integrate with a Red Hat Satellite 6 server and take advantage of its
features. This includes:

  - Monitoring the inventory of your Red Hat Satellite 6 server,
    including independent hosts and hosts provisioned using hostgroups.

  - Reprovisioning existing bare metal system hosts to new host groups.

  - Applying {product-title} policy tags to hosts.

<div class="important">

{product-title} only reprovisions existing systems in a Red Hat
Satellite 6 environment. Provisioning systems from Red Hat Satellite 6’s
bare metal discovery service is planned for a future release.

</div>

Unresolved directive in Configuration\_Management\_Providers.adoc -
include::Defining\_the\_Workflow.adoc\[\]

Unresolved directive in Configuration\_Management\_Providers.adoc -
include::Defining\_the\_Hostgroup\_Hierarchy.adoc\[\]

Unresolved directive in Configuration\_Management\_Providers.adoc -
include::Adding\_a\_Satellite\_6\_Provider.adoc\[\]

Unresolved directive in Configuration\_Management\_Providers.adoc -
include::Triggering\_a\_Refresh\_of\_a\_Satellite\_6\_Provider.adoc\[\]

Unresolved directive in Configuration\_Management\_Providers.adoc -
include::Displaying\_Red\_Hat\_Satellite\_6\_Contents.adoc\[\]

Unresolved directive in Configuration\_Management\_Providers.adoc -
include::Reprovisioning\_a\_Bare\_Metal\_Host.adoc\[\]

Unresolved directive in Configuration\_Management\_Providers.adoc -
include::Tagging\_a\_Bare\_Metal\_Host.adoc\[\]
