  - If you are configuring a previously configured host, you must remove
    its existing entry in the CloudForms database with the
    `conversion_host_disable` playbook, to avoid multiple entries for
    the same host:
    
        $ ansible-playbook /usr/share/ovirt-ansible-v2v-conversion-host/playbooks/conversion_host_disable.yml

<!-- end list -->

1.  Install the `ovirt-ansible-v2v-conversion-host` package:
    
        $ yum install ovirt-ansible-v2v-conversion-host

2.  Create the `extra_vars.yml` file with the following parameters:
    
    ``` yaml
    ---
    v2v_transport_methods:
    v2v_max_concurrent_conversions: "10" 
    
    # Empty vmware_hosts variable for conversion_host_disable.yml
    # Do not change this parameter
    vmware_hosts: ""
    
    manageiq_providers:
    ```
    
      - `v2v_max_concurrent_conversions` is the maximum number of
        concurrent conversions per host. The default value is `10`. Do
        not set this value higher than `20`.

3.  Create an encrypted `secure_vars.yml` file:
    
        $ ansible-vault create secure_vars.yml

4.  Add the following parameters and save the file:
    
    ``` yaml
    ---
    manageiq_username: "<username>" 
    manageiq_password: "<password>" 
    ```
    
      - Specify the CloudForms admin user, for connecting to CloudForms.
    
      - Specify the CloudForms admin password.

5.  Run the `conversion_host_enable.yml` playbook to configure each
    conversion host:
    
        $ ansible-playbook -i <conversion_host>, -b \ 
            -e "ansible_ssh_private_key_file=/etc/pki/ovirt-engine/keys/engine_id_rsa" \
            -e @extra_vars.yml -e @secure_vars.yml --ask-vault-pass \
            /usr/share/ovirt-ansible-v2v-conversion-host/playbooks/conversion_host_enable.yml
    
      - Specify the FQDN or IP address of the conversion host.

6.  Run the `conversion_host_check.yml` playbook to verify the
    configuration:
    
        $ ansible-playbook --ask-vault-pass -i <conversion_host>, -c local \ 
            -e @extra_vars.yml -e @secure_vars.yml conversion_host_check.yml
    
      - Specify the FQDN or IP address of the conversion host.
