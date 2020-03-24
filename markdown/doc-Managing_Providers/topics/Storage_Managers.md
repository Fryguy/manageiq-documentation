In {product-title}, a storage manager is a service providing storage
resources that you can manage from a {product-title} appliance. This
chapter describes the different types of storage managers used by
{product-title}, and how they are added to {product-title}.

There are three types of storage managers currently available to
{product-title}:

  - Amazon Elastic Block Store

  - OpenStack Block Storage (`openstack-cinder`)

  - OpenStack Object Storage (`openstack-swift`)

# Amazon Elastic Block Store Managers

The Amazon Elastic Block Store service provides and manages persistent
block storage resources that Amazon EC2 instances can consume.

To use the Amazon Elastic Block Store service as a storage manager, you
must first add an Amazon EC2 cloud provider to your {product-title}
appliance. The Amazon Elastic Block Store service is automatically
discovered by {product-title}, and added to the **Storage Managers**
list. See [???](#adding-amazon-ec2-providers) for instructions on adding
an Amazon EC2 cloud provider.

# OpenStack Block Storage Managers

The OpenStack Block Storage service (`openstack-cinder`) provides and
manages persistent block storage resources that OpenStack infrastructure
instances can consume.

To use OpenStack Block Storage as a storage manager, you must first add
an OpenStack cloud provider to your {product-title} appliance and enable
events. The Block Storage service will be automatically discovered by
{product-title} and added to the **Storage Managers** list in
{product-title}. See [???](#adding_openstack_cloud_providers) for
instructions on adding a cloud provider and enabling events.

# OpenStack Object Storage Managers

The OpenStack Object Storage (`openstack-swift`) service provides cloud
object storage.

To use the OpenStack Object Storage service as a storage manager, you
must first add an OpenStack cloud provider to your {product-title}
appliance and enable events. The Object Storage service will be
automatically discovered by {product-title} and added to the **Storage
Managers** list in {product-title}. See
[???](#adding_openstack_cloud_providers) for instructions on adding a
cloud provider and enabling events.

Unresolved directive in Storage\_Managers.adoc -
include::Viewing\_Swift\_Object\_Stores.adoc\[\]
