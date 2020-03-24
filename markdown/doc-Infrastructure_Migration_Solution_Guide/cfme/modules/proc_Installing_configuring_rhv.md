You can install and configure Red Hat Virtualization (RHV) for
migration.

1.  Set the BIOS settings of bare metal hosts for optimal performance,
    rather than power-saving, according to the vendor’s recommendations.

2.  Disable CPU enhanced halt (C1E) in the BIOS settings, if applicable.

**Procedure.**

\+

<div class="note">

You can only migrate to shared storage, such as NFS, iSCSI, or FCP.
Local storage is not supported.

Although the ISO storage domain has been deprecated, it is required for
migration.

</div>

\+

<div class="important">

If the Red Hat Virtualization MAC address pool range overlaps the VMware
MAC address range, you must ensure that the MAC addresses of the
migrating virtual machines do not duplicate those of existing virtual
machines. Otherwise, the migration will fail.

If you do not create a MAC address pool, the migrated virtual machines
will not have MAC addresses in the same range as virtual machines
created in Red Hat Virtualization.

</div>
