# Migrating Custom Buttons

This workflow demonstrates how to export custom buttons from one
{product-title} appliance and import them in another
{product-title\_short} appliance.

1.  Export custom buttons from the source {product-title\_short}
    appliance:
    
    1.  SSH into the {product-title} appliance as `root`.
    
    2.  Create a temporary directory:
        
            # mkdir /tmp/custom_buttons
    
    3.  Navigate to the Virtual Management Database (VMDB) directory:
        
            # vmdb
    
    4.  Export custom buttons using the following `rake` command:
        
            # rake evm:export:custom_buttons -- --directory /tmp/custom_buttons
    
    5.  Confirm the `yaml` file was created by navigating to the new
        directory:
        
            # cd /tmp/custom_buttons

2.  Copy the directory to the target {product-title\_short} appliance:
    
        scp -r /tmp/custom_buttons/ hostname:/tmp/custom_buttons

3.  Import custom buttons on the target {product-title\_short}
    appliance:
    
    1.  SSH to the target {product-title\_short} appliance as `root`.
    
    2.  Navigate to the VMDB directory:
        
            # vmdb
    
    3.  Import custom buttons using the following `rake` command:
        
            # rake evm:import:custom_buttons -- --source /tmp/custom_buttons

To verify successful import of custom buttons:

1.  Log in to the target {product-title\_short} appliance.

2.  Navigate to menu:Automation\[Automate \> Customization\].

3.  Click **Buttons** in the accordion menu.

Imported buttons will appear under the parent **Object Type**.
