You can scan your VMware virtual machines in Red Hat CloudForms.

<div class="important">

Some virtual machines should not be analyzed because the snapshot
process may cause data corruption. See the VMware documentation about
[snapshot
limitations](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vm_admin.doc/GUID-53F65726-A23B-4CF0-A7D5-48E584B88613.html)
for details.

You can exclude a virtual machine from the scan by assigning to it the
[`exclusions` tag, with the `do_not_analyze`
value](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/5.0/html-single/managing_infrastructure_and_inventory/index#to_tag_virtual_machines_and_templates).

</div>

  - SmartState analysis and SmartProxy must be enabled.

  - You must have a valid VM analysis profile called `default`. If you
    create an analysis profile with a different name, you must [create a
    control
    policy](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/5.0/html-single/assigning_a_custom_analysis_profile_to_a_virtual_machine/index#create-vm-control-policy)
    and assign it to the vSphere provider.

<!-- end list -->

1.  Log in to the CloudForms user interface.

2.  Navigate to **Compute** → **Infrastructure** → **Virtual Machines**.

3.  Select the virtual machines that you want to scan.

4.  Click **Configuration** → **Perform SmartState Analysis**.
    
    Each virtual machine can take up to one minute to scan.

5.  Click your username ![user](user.png) → **Tasks**.
    
    The result of each SmartState analysis scan appears in **My Tasks**.
