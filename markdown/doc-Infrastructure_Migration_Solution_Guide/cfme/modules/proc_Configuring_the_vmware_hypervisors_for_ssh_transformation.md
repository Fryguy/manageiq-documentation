For SSH transformation, you must enable SSH access and copy a public SSH
key to each VMware hypervisor. The corresponding private key will be
used to configure the conversion hosts.

<div class="important">

A single SSH key pair is recommended because this key pair is used only
for virtual machine conversion and it simplifies conversion host
management.

If you wish to use a dedicated SSH key pair for each conversion host,
you can copy the public key of each conversion host to all the VMware
hypervisors.

</div>

1.  Enable SSH access on each VMware hypervisor, according to the VMware
    documentation:
    
    1.  In a browser, navigate to [VMware vSphere
        Documentation](https://docs.vmware.com/en/VMware-vSphere/index.html).
    
    2.  Enter `Enable ESXi Shell and SSH Access with the Direct Console
        User Interface` in the **Search** field and select your VMware
        version.
    
    3.  Click the `HTML` icon to view the procedure.
        
        You can collect the SSH public keys of the VMware hypervisors at
        this stage, to copy to the conversion hosts.

2.  Generate an SSH key pair without a passphrase:
    
        # ssh-keygen -N ''

3.  Copy the public SSH key to `/etc/ssh/keys-root/authorized_keys` on
    **each** VMware hypervisor.
    
    You will use the private SSH key to configure the conversion hosts.
