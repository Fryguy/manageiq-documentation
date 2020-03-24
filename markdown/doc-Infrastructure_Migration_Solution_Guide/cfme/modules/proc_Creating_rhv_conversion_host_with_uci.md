You can create a Red Hat Virtualization conversion host with the
Universal Conversion Host Image (UCI) in the Administration Portal.

  - The host on which you are deploying the conversion host must have
    [nested
    virtualization](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html-single/virtualization_deployment_and_administration_guide/index#sect-nested_virt_setup)
    enabled.

  - A network must be created and configured for the conversion host.
    See the migration network requirements for details.

<!-- end list -->

1.  Log in to the Administration Portal.

2.  [Upload the
    UCI](https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.3/html-single/administration_guide/index#Uploading_Images_to_a_Data_Storage_Domain_storage_tasks)
    to the data storage domain.

3.  Click **Compute** → **Virtual Machines**.

4.  Click **New** to open the **New Virtual Machine** dialog.

5.  In the **General** tab, specify the following options:
    
      - **Cluster**: Specify the cluster where the conversion host will
        run. The cluster must contain a RHV host that is configured for
        nested virtualization.
    
      - **Operating System**: Select **Red Hat Enterprise Linux 8.x
        x64**.
    
      - **Optimized for**: Select **Server**.
    
      - **Name**: Specify the conversion host name that will be
        displayed in the Administration Portal.
    
      - In the **Instance Images** section:
        
        1.  Click **Attach**.
        
        2.  Click **Image**.
        
        3.  Select the UCI from the list of available images and select
            the **OS** check box.
        
        4.  Click **OK**.
    
      - Select a vNIC profile for the network interface.

6.  In the **System** tab, specify the following options:
    
      - **Memory Size**: `10240 MB` or more
    
      - **Total Virtual CPUs**: `4` or more

7.  In the **Initial Run** tab, specify the following options:
    
      - Select **Use Cloud-Init/Sysprep**.
    
      - **VM Hostname**: Specify the conversion host’s FQDN.
    
      - Expand the **Authentication** section and paste the SSH public
        key in the **SSH Authorized Keys** field.
        
        This public key is associated with the SSH private key that
        CloudForms uses to connect to the conversion host.
    
      - The network interfaces use DHCP by default. If you do not want
        to use DHCP, expand the **Network** section and specify the
        following options:
        
        1.  Select **In-guest Network Interface Name**.
        
        2.  Enter the network interface name, for example, `eth0`, in
            the text field.
        
        3.  For **IPv4 Boot Protocol**, select `Static`.
        
        4.  Specify the **IPv4 Address**, **IPv4 Netmask**, and **IPv4
            Gateway**.

8.  In the **Host** tab, specify the following options:
    
      - In the **Start Running On** section, select **Specific Host(s)**
        and select a RHV host with nested virtualization enabled.
    
      - Select **Pass-Through Host CPU**.

9.  Click **OK** to create the virtual machine.
    
    The conversion host is displayed in the list of virtual machines.

10. Click **Run** to start the virtual machine.
