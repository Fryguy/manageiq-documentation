![25](circle_step_numbers/1.png) You create and run a migration plan in
the CloudForms user interface.

![25](circle_step_numbers/2.png) CloudForms uses the migration plan to
locate the VMware virtual machines.

![25](circle_step_numbers/3.png) CloudForms captures the VMware ESXi
host fingerprint for authentication during the migration process.

![25](circle_step_numbers/5.png) The `virt-v2v-wrapper` connects to the
VMware datastore through the ESXi host. `virt-v2v` streams the VMware
virtual disks to the Red Hat data domain and converts the disks.

The migration process is complete and the migration plan status is
displayed in the CloudForms user interface.
