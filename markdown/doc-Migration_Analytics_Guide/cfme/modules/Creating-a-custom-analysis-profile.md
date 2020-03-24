You can create a customized analysis profile so that custom workloads
and instances are detected, added to the inventory data file, and
included in the Migration Analytics report.

  - If there is an existing `default` analysis profile in CloudForms,
    you must delete it.
    
    Importing a new `default` profile does not overwrite an existing
    `default` profile. The import process concatenates the `default`
    profiles.

<!-- end list -->

1.  Log in to the CloudForms machine as root.

2.  Create a `/root/custom_profile.yaml` file, using the
    `custom_profile.yaml` file as a template.

3.  Edit the `custom_profile.yaml` file for your workloads by updating
    the `target` parameters.
    
    For example, you can modify the paths to startup scripts and
    configuration files for custom Oracle WebLogic instances:
    
    ``` yaml
    ---
    name: default 
    definition:
    - name: default_file
      guid:
      item_type: file
      definition:
        stats:
        - target: /u01/app/oracle/domains/base/bin/startNodeManager.sh
        - target: /u01/app/oracle/domains/base/startWebLogic.sh
        - target: /home/oracle/oraInventory
        - target: /u01/app/oracle/domains/base/config/config.xml
    ```
    
      - The imported analysis profile is called `default`. If you change
        the profile name, you must [create a control
        policy](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/5.0/html-single/assigning_a_custom_analysis_profile_to_a_virtual_machine/index#create-vm-control-policy)
        and add it to the vSphere provider.

4.  Save the `custom_profile.yaml` file.

5.  Go to the vmdb directory:
    
        # cd /var/www/miq/vmdb

6.  Import the `custom_profile.yaml` file:
    
        # bundle exec rake evm:import:scan_profiles -- --source /root/custom_profile.yaml

7.  In the CloudForms user interface, verify that the `default` profile
    appears under **Analysis Profiles**.
