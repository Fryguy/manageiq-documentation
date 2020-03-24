If you are migrating a virtual machine running RHEL or other Linux
operating system, you must create and run a `RHEL premigration` playbook
to call the Ansible `ims.rhel_premigration` role.

The `ims.rhel_premigration` role ensures that the virtual machine IP
addresses are accessible after migration.

  - The `rhel-<version>-server-rpms` repository must be enabled for the
    VMware virtual machines. If you have disabled it, you can re-enable
    it in the RHEL premigration playbook.

<!-- end list -->

1.  [Install the `ims.rhel_premigration`
    role](https://galaxy.ansible.com/fdupont_redhat/ims_rhel_pre_migration)
    with Ansible Galaxy.

2.  Create a `RHEL premigration` playbook according to the following
    example:
    
    ``` yaml
    ---
    - hosts: <hosts> 
      vars:
        rhsm_repositories:
          - "rhel-<version>-server-rpms" 
      roles:
        - role: ims.rhel_pre_migration
    ```
    
      - Specify the VMware hosts on which you are running this playbook.
    
      - Specify the RHEL version.

You will add this playbook when you create your migration plan.
