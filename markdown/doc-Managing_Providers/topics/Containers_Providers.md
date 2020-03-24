A containers provider is a service that manages container resources,
that can be added to the {product-title} appliance.

{product-title\_short} can connect to OpenShift Container Platform
containers providers and manage them similarly to infrastructure and
cloud providers. This allows you to gain control over different aspects
of your containers environment and answer questions such as:

  - How many containers exist in my environment?

  - Does a specific node have enough resources?

  - How many distinct images are used?

  - Which image registries are used?

When {product-title\_short} connects to a container’s environment, it
collects information on different areas of the environment:

  - Entities such as pods, nodes, or services.

  - Basic relationships between the entities, for example: Which
    services are serving which pods?

  - Advanced insight into relationships, for example: Which two
    different containers are using the same image?

  - Additional information, such as events, projects, routes, and
    metrics.

You can manage policies for containers entities by adding tags. All
containers entities except volumes can be tagged.

<div class="note">

This chapter provides details on managing containers providers. For
details on working with the resources within a container environment,
see [Container
Entities](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_infrastructure_and_inventory/#container_entities)
in *Managing Infrastructure and Inventory*.

</div>

The {product-title\_short} user interface uses virtual thumbnails to
represent containers providers. Each thumbnail contains four quadrants
by default, which display basic information about each provider:

![cp quad icon](cp-quad-icon.png)

1.  Number of nodes

2.  Container provider software

3.  Power state

4.  Authentication status

| Icon              | Description                                                                    |
| ----------------- | ------------------------------------------------------------------------------ |
| ![2190](2190.png) | Validated: Valid authentication credentials have been added.                   |
| ![2191](2191.png) | Invalid: Authentication credentials are invalid.                               |
| ![2192](2192.png) | Unknown: Authentication status is unknown or no credentials have been entered. |

Containers provider authentication status

# Obtaining an OpenShift Container Platform Management Token

When deploying OpenShift using `openshift-ansible-3.0.20` (or later
versions), the OpenShift Container Platform [service
account](https://docs.openshift.com/container-platform/latest/admin_guide/service_accounts.html)
and
[roles](https://docs.openshift.com/container-platform/latest/admin_guide/manage_authorization_policy.html)
required by {product-title} are installed by default.

<div class="note">

See the [OpenShift Container Platform
documentation](https://docs.openshift.com/container-platform/latest/architecture/additional_concepts/authorization.html#roles)
for a list of the default roles.

</div>

Run the following to obtain the token needed to add an OpenShift
Container Platform provider:

    # oc sa get-token -n management-infra management-admin
    eyJhbGciOiJSUzI1NiI...

# Enabling OpenShift Cluster Metrics

Use the OpenShift Cluster Metrics plug-in to collect node, pod, and
container metrics into one location. This helps track usage and find
common issues.

  - Configure {product-title} to allow for all three [**Capacity &
    Utilization** server
    roles](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.1/deployment-planning-guide/#assigning_the_capacity_and_utilization_server_roles).

  - Enable cluster metrics using the [OpenShift Container Platform
    documentation](https://access.redhat.com/documentation/en-us/openshift_container_platform/3.5/html-single/installation_and_configuration/#install-config-cluster-metrics).

Unresolved directive in Containers\_Providers.adoc -
include::Adding\_an\_OpenShift\_Provider.adoc\[\]

Unresolved directive in Containers\_Providers.adoc -
include::Tagging\_Containers\_Providers.adoc\[\]

Unresolved directive in Containers\_Providers.adoc -
include::Removing\_Containers\_Providers.adoc\[\]

Unresolved directive in Containers\_Providers.adoc -
include::Pause\_Resume\_Containers\_Providers.adoc\[\]

Unresolved directive in Containers\_Providers.adoc -
include::Editing\_a\_Containers\_Provider.adoc\[\]

Unresolved directive in Containers\_Providers.adoc -
include::Hide\_Environment\_Vars.adoc\[\]

Unresolved directive in Containers\_Providers.adoc -
include::Viewing\_a\_Containers\_Providers\_Timeline.adoc\[\]
