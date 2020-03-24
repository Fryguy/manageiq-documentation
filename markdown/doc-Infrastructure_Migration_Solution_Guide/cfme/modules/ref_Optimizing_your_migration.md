You can minimize the impact of the migration on your environment and
improve performance.

For details on performance-related configurations, see [Performance
recommendations for migrating from VMware to Red Hat Virtualization or
Red Hat OpenStack Platform with
IMS](https://access.redhat.com/articles/4713391).

# Optimizing the migration environment

You can configure the VMware and Red Hat environments to optimize your
migration.

**VMware environment.**

You can improve performance with the following configurations:

  - Extend the VMware virtual machine network to the Red Hat
    environment.

  - Ensure that the VMware network provides high throughput.
    
    VMware and Red Hat hosts often have multiple network interfaces. By
    default, the conversion hosts use the VMware hosts' admin interface
    to import virtual machines. Configure your routing for the fastest
    possible connection between the VMware and Red Hat environment. You
    can use host routes or IP table filtering to control the traffic
    flow.

  - Ensure that the VMware network does not affect production machines,
    for example, by using a backup network to avoid overload.

  - Divide the VMware virtual machines equally between two VMware hosts,
    if possible.

  - Remove unnecessary data from the VMware disks.

**Red Hat environment.**

You can improve performance with the following configurations:

  - Update your Red Hat environment to the latest z-stream release and
    install required patches.

  - Use fast, full SSD storage.

  - Ensure that the network connection between the bare metal hosts and
    storage is at least 10 GbE.

  - Use Fibre Channel interfaces between the hosts and storage.

  - Configure multipath access between the hosts and storage.

# Optimizing conversion host performance

You can improve performance with the following conversion host
configurations:

  - Enable high performance and disable power-saving in the BIOS
    settings of the bare metal hosts.

  - Deploy multiple conversion hosts (up to 5) for load-balancing and
    improved performance.
    
    The virtual machines in a migration plan are automatically
    distributed among the conversion hosts. This decreases the load on
    the conversion hosts and allows you to increase the concurrent
    migrations beyond the limits of a single conversion host.

# Scheduling the migration

You can improve performance and minimize the impact on your users by
scheduling the migration carefully:

  - Stagger the migration schedules.

  - Move critical applications during maintenance windows.

  - Schedule the migration when storage input/output usage is low.

  - Create multiple migration plans for finer control.

# Grouping virtual machines for migration

You can improve performance and minimize the impact on your users by
creating migration groups of virtual machines:

  - Create migration groups for your virtual machines, so that you are
    not migrating all of them at the same time.

  - Migrate virtual machines as a group, rather than individually.
    
    You can deploy up to 5 conversion hosts, with each host migrating up
    to 20 virtual machines concurrently. **These limits should not be
    exceeded.**

  - Consider the following questions when creating migration groups:
    
      - How are the virtual machines grouped now?
    
      - Which virtual machines should be migrated together?
    
      - Which workloads or linked applications should be migrated
        together?
    
      - What applications must remain available?

  - Consider which parts of the workload to migrate first:
    
      - Databases
    
      - Applications
    
      - Web servers
    
      - Load balancers
