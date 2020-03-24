The following are known issues:

  - BZ\#1726939: [Run the preflight check of migration task before
    waiting for a conversion
    host](https://bugzilla.redhat.com/show_bug.cgi?id=1726939).
    Currently, the preflight check that monitors the migration is
    performed after a conversion host is assigned to the task. As a
    result, the total volume of the datastores reported in **Migration
    Plans In Progress** reflects the total volume of the virtual
    machines that are currently migrating, not the total volume of the
    migration plan. When all the virtual machines have started to
    migrate, the correct value of the total volume is displayed.
