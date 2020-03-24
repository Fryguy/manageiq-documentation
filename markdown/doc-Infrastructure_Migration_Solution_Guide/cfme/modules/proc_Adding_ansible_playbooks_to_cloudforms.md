You can add Ansible playbooks to CloudForms to perform automated
premigration and postmigration tasks on specific virtual machines, for
example:

  - Removing web servers from a load-balancing pool before migration and
    returning them to the pool after migration

  - Preserving the IP addresses of VMware virtual machines running RHEL
    or other Linux operating system

<!-- end list -->

1.  Log in to the CloudForms user interface.

2.  [Enable the `Embedded Ansible` server
    role](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html/managing_providers/automation_management_providers#enabling-embedded-ansible-server-role).

3.  [Add an Ansible playbook
    repository](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html/managing_providers/automation_management_providers#adding-a-playbook-repository).

4.  [Add the
    credentials](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html/managing_providers/automation_management_providers#ansible-credentials)
    of each virtual machine that you are migrating.

5.  [Add your playbook as an Ansible service catalog
    item](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/provisioning_virtual_machines_and_instances/#create-playbook-service-catalog-item).

You will select the playbooks and the virtual machines on which they run
in the **Advanced Options** screen when you create the migration plan.
