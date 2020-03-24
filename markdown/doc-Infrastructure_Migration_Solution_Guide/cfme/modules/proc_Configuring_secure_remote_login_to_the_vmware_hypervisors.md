You can configure secure remote login to the VMware hypervisors by using
`ssh-agent` and `ssh-add`.

Secure remote login must be verified for **each** VMware hypervisor. If
secure remote login fails, all migrations from that hypervisor will
fail.

1.  On the Manager machine, create an `ssh-agent` session for the `vdsm`
    user:
    
        $ sudo -u vdsm ssh-agent
        SSH_AUTH_SOCK=<ssh_auth_sock>; export SSH_AUTH_SOCK;
        SSH_AGENT_PID=139150; export SSH_AGENT_PID;
        echo Agent pid 139150;

2.  Copy the `<ssh_auth_sock>` value from the output.

3.  Run `ssh-add` to authorize the `vdsm` user’s private key for the
    `ssh-agent` session:
    
        $ sudo -u vdsm SSH_AUTH_SOCK=<ssh_auth_sock> ssh-add 
    
      - Specify the `<ssh_auth_sock>` value.

4.  Connect to a VMware hypervisor to verify the secure remote login:
    
    ``` 
    $ sudo -u vdsm \
        SSH_AUTH_SOCK=<ssh_auth_sock> ssh root@<Vmware_host_name>  
    ```
    
      - Specify the `<ssh_auth_sock>` value.
    
      - Specify the host name of the VMware hypervisor.
