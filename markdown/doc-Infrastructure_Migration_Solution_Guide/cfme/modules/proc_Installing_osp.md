You can install and configure your Red Hat OpenStack Platform 13 (or
later).

1.  Set the BIOS settings of the bare metal hosts for optimal
    performance, rather than power-saving, according to the vendor’s
    recommendations.

2.  Disable CPU enhanced halt (C1E) in the BIOS settings, if applicable.

3.  Check the firewall and security group rules to ensure that the ports
    required for migration are open.

**Procedure.**

You can install and configure Red Hat OpenStack Platform (RHOSP) for
migration.

1.  Set the BIOS settings of bare metal hosts for optimal performance,
    rather than power-saving, according to the vendor’s recommendations.

2.  Disable CPU enhanced halt (C1E) in the BIOS settings, if applicable.

3.  Check the firewall and security group rules to ensure that the ports
    required for migration are open.

<!-- end list -->

1.  Install [Red Hat OpenStack
    Platform](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.0/html-single/director_installation_and_usage/).

2.  [Create provider
    networks](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.0/html-single/networking_guide/#create_a_network)
    for the target instances to preserve the IP addresses of the source
    virtual machines.

3.  [Create a
    project](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.0/html-single/users_and_identity_management_guide/#create_a_project)
    for the conversion hosts and any target projects you require for the
    target instances.

4.  [Ensure that the `admin` user has `member` and `admin`
    roles](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.0/html-single/users_and_identity_management_guide/#edit_a_project)
    in the conversion host and target projects.

5.  [Create a
    volume](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.0/html-single/storage_guide/#section-create-volume)
    and [set at least one volume
    type](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.0/html-single/storage_guide/#section-volume-retype)
    for the target block storage. Otherwise, CloudForms will not detect
    the storage when you create the infrastructure mapping.

6.  Ensure that the storage backends have sufficient space for the
    migrated virtual machines.
    
    <div class="important">
    
    If you are using Red Hat Ceph Storage, you will require three times
    the space of the source virtual machines for the migrated virtual
    machines. A Ceph storage cluster, by default, [creates two copies of
    an object in a replicated storage
    pool](https://access.redhat.com/documentation/en-us/red_hat_ceph_storage/3/html-single/architecture_guide/index#concept-arch-data-copies-arch),
    for a total of three copies.
    
    The migrated disks use all of the space because it is preallocated.
    For example, a source virtual machine with a 100 GB disk requires
    300 GB of storage, regardless of how much data the disk actually
    contains. To save storage space, you can use the `fstrim` command on
    the migrated virtual machines as a postmigration task or playbook.
    
    </div>

7.  Create flavors for the source virtual machines. If you do not create
    custom flavors, CloudForms will try to map each source virtual
    machine to an existing flavor.
