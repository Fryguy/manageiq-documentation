VMware storage profiles allow you to assign policies to datastores.
Storage profiles are used to tag virtual machines to ensure they operate
in compliance with settings in the datastore.

{product-title} retrieves VMware virtual machine storage profile
information in the inventory, and associates the virtual machines and
disks with them.

To view a virtual machine’s storage profile:

1.  Navigate to menu:Compute\[Infrastructure \> Virtual Machines\].

2.  Click a VMware virtual machine to open its summary page.

3.  The VMware **Storage Profile** is listed under **Properties**.

You can assign a storage profile when provisioning a VMware virtual
machine in {product-title}, by using the virtual machine as a template
to clone. See [Provisioning Virtual
Machines](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.7/single/provisioning-virtual-machines-and-hosts/#provisioning-virtual-machines)
in *Provisioning Virtual Machines and Hosts* for instructions.
