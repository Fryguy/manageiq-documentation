The following questions can help you to estimate the resources and time
required for migration.

  - What am I migrating?
    
      - Identify the VMware virtual machines that you will be migrating.

  - What am I missing?
    
      - Identify resource gaps, such as bandwidth, storage, licenses, or
        a suitable maintenance window, before you begin the migration.

  - What is the maximum number of disks or virtual machines that I can
    migrate?
    
      - There is no maximum number of disks or virtual machines that you
        can migrate. However, you may not want to migrate all your
        virtual machines at the same time, in order to minimize the
        impact on your users.
        
        <div class="important">
        
        If you exceed the capabilities of your environment, the
        migration will fail. This situation could affect existing
        applications running on virtual machines attached to the network
        and storage.
        
        </div>

  - What impact will the migration have on my users?
    
      - Assess the effects the migration may have on a production
        environment.
        
        It may be possible to migrate your applications in phases,
        without downtime at the application layer, if the applications
        are distributed in a high-availability architecture.
    
      - Check whether users will lose access to critical applications.

# How long will the migration take?

There is no formula to estimate how long the actual migration will take.
Migration speed is determined by your hardware, network speed, and other
factors.

The following example is provided as a guide:

# What operating systems can I migrate?

You can migrate any guest operating system that is [certified and
supported](https://access.redhat.com/articles/973163).

# How many conversion hosts do I need?

The number of conversion hosts you create depends on the size of your
migration. All the virtual machines in a migration plan are migrated at
the same time, in parallel. The number of virtual machines that you can
migrate simultaneously depends on your infrastructure capabilities. Each
migration requires a certain amount of network bandwidth, I/O
throughput, and processing power for the conversion process.

Multiple conversion hosts provide load-balancing and better performance,
even for small migrations.

Conversion hosts are limited to a maximum of ten concurrent migrations,
unless you change the default values.

You should test your environment thoroughly before the migration to
determine how many migrations it can support without negative effects,
for example, five conversion hosts, each running ten concurrent
migrations.

# Should I migrate my virtual machines with VDDK or with SSH?

You can migrate your virtual machines with either the VMware Virtual
Disk Development Kit (VDDK) or SSH. VDDK is the default because it is
much faster than SSH and easier to configure.

VDDK is limited to 20 concurrent migrations per conversion host, because
of network limitations, and 10 concurrent migrations per VMware
hypervisor, unless you increase the hypervisor’s NFC service memory.

If you cannot use VDDK, SSH is a fallback option.
