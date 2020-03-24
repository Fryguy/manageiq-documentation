# Scaling a Highly Available {product-title\_short} Environment

After creating high availability for the database tier and the user
interface tier, the rest of the infrastructure should be sized
appropriately for the roles and the environments that they manage. These
roles and tiers use built-in high availability mechanisms like primary,
secondary, and tertiary failover.

You can configure additional worker appliances as needed using the steps
in [???](#installation_appliances_addl), and then assign zones and
server roles. The non-database {product-title\_short} appliances and
roles can be configured in any order.

The following diagram shows an example of a highly available database
configuration that contains worker appliances, providers, and the
HAProxy load balancer configured in [???](#configuring_HAProxy).

The worker appliances in the diagram are labeled by server role (**User
Interface**, **Management**, and **Database Ops**) and corresponding
zone to show how a highly available environment might be scaled with
server roles and zones.

![CloudForms HA Architecture 431939 0917 ECE
02](CloudForms_HA_Architecture_431939_0917_ECE-02.png)

See
[Regions](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.5/html-single/general_configuration/#regions)
and
[Servers](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.5/html-single/general_configuration/#servers)
in *General Configuration* for more information on configuring servers
and roles.

See [Deploying CloudForms at
Scale](https://access.redhat.com/documentation/en-us/reference_architectures/2017/html/deploying_cloudforms_at_scale/)
for further recommendations on scaling your {product-title\_short}
environment.
