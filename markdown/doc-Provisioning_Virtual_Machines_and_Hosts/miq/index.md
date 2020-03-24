# ManageIQ Lifecycle

This guide discusses lifecycle activities such as provisioning and
retirement that are part of the ManageIQ Automate component. ManageIQ
Automate enables real-time, bidirectional process integration and
adaptive automation for management events and administrative or
operational activities.

  - Operations Management with service level resource enforcement.

  - Resource Management including datastore cleanup, snapshot aging and
    enforcement, and virtual machine or instance aging and retirement.

  - Configuration and Change Management including enforced closed loop
    change management.

  - Lifecycle Management such as provisioning, customization,
    reconfiguration, approval, CMDB updates, and retirement.

<div class="important">

Provisioning requires the **Automation Engine** server role enabled.
Check your server role settings in the settings menu,
<span class="menuchoice">Configuration \> Server \> Server
Control</span>.

</div>

## Provisioning

When a virtual machine or cloud instance is provisioned, it goes through
multiple phases. First, the request must be made. The request includes
ownership information, tags, virtual hardware requirements, the
operating system, and any customization of the request. Second, the
request must go through an approval phase, either automatic or manual.
Finally, the request is executed. This part of provisioning consists of
pre-processing and post-processing. Pre-processing acquires IP addresses
for the user, creates CMDB instances, and creates the virtual machine or
instance based on information in the request. Post-processing activates
the CMDB instance and emails the user. The steps for provisioning may be
modified at any time using ManageIQ. ![2314](images/2314.png)

# Provisioning Requests

The following options are available when making provisioning requests:

  - Set an owner (User can do this using LDAP lookup)

  - Assign a purpose (tag)

  - Select a template or image from which to create a new virtual
    machine or instance respectively

  - Choose placement

  - Set hardware requirements

  - Specify the vLan

  - Customize the guest operating system

  - Schedule the provisioning ![2315](images/2315.png)

## Requirements for Provisioning Virtual Machines and Instances

ManageIQ supports the provisioning of VMware ESX hypervisors. To
provision a virtual machine from VMware providers, you must have an
appliance with the Automation Engine role enabled.

If you are using a Windows template, the following configuration is
required:

  - To customize settings that are inside the operating system, Sysprep
    must be copied to the appropriate directory on your vCenter
    computer. Usually this location is: `C:\Documents and Settings\All
    Users\Application Data\VMware\VMware VirtualCenter\sysprep`. Copy
    the Sysprep tools to the relevant operating system subdirectory. If
    you are running a standard Win2008 operating system, this step is
    unnecessary as Sysprep is included as standard.

  - The Windows template must have the latest version of VMware tools
    for its ESX Server. Check the VMware Site for more information. If
    you are creating a new password for the Administrator account, the
    Administrators password must be blank on the template. This is a
    limitation of Microsoft Sysprep.

See the VMware documentation for a complete list of customization
requirements.

## Requirements for Provisioning Virtual Machines from Red Hat Virtualization Manager

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Item</th>
<th>Requirements</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Red Hat Virtualization Manager version 4.0 or higher</p></td>
<td><p>Red Hat Virtualization Manager properly installed with API in default location <a href="https://server:8443/api">https://server:8443/api</a></p></td>
</tr>
<tr class="even">
<td><p>Red Hat Virtualization Manager History Database</p></td>
<td><p>Red Hat Virtualization Manager Data Warehouse (DWH) properly installed with access to the PostgreSQL database on the Red Hat Virtualization Manager server. Port 5432 open in iptables.</p>
<p>md5 authentication allowed to ManageIQ appliances in <code>pg_hba.conf</code>.</p>
<p>PostgreSQL set to listen for connections on <code>*:5432</code> in <code>postgresql.conf</code>.</p>
<p>Credentials provided during database setup to be used in ManageIQ UI.</p></td>
</tr>
<tr class="odd">
<td><p>Storage Supported for ManageIQ Virtual Machine Analysis</p></td>
<td><p>NFS - ManageIQ server must be able to mount NFS storage domain.</p>
<p>iSCSI / FCP - Cluster must use full Red Hat Enterprise Linux (not Red Hat Virtualization Hypervisor) Hosts.</p>
<p>DirectLUN Hook installed on each host and registered to Red Hat Virtualization Managers.</p>
<p>Must have ManageIQ appliance in each Cluster with this storage type.</p>
<p>ManageIQ appliance virtual machine container must have DirectLUN attribute set.</p>
<p>Local storage - Not yet supported (Red Hat does not recommend due to single point of failure).</p></td>
</tr>
</tbody>
</table>

## PXE Provisioning

PXE is a boot method that allows you to load files from across a network
link. ManageIQ uses it for files required for provisioning virtual
machines. PXE can be used for provisioning for either Red Hat
Virtualization Manager or VMware.

**Procedure Overview**

1.  Connect to the **PXE Server**.

2.  Create a **System Image Type**.

3.  Associate each **PXE** image with an image type.

4.  Create a customization template.

**Requirements for PXE Provisioning**

  - DHCP server configured with required PXE implementation

  - PXE implementation for Linux virtual machine provisioning

  - NFS or SAMBA read and write access to create and modify files on the
    PXE server

  - ManageIQ Server uses NFS mount to read and write the response files

  - HTTP read access to the NFS share location as virtual machines use
    this URL to access PXE images and Kickstart or Cloud-Init
    configuration files

  - Operating system installation media available to be streamed from
    PXE server

  - Images configured for desired operating systems

  - Kickstart or Cloud-Init templates to configure operating systems
    with desired packages

**Additional Requirements for Provisioning Linux Virtual Machines**

  - Linux distribution kernel and ramdisk available over HTTP

  - Linux sources available over HTTP

  - Sample PXE menu item that boots this kernel

**Additional Requirements for Provisioning Windows Virtual Machines**

  - WinPE ISO built with rhev-agent-tools (for RHEV-M environments) and
    configured to mount shares for Windows source files and Sysprep
    files and configured to run customization script

  - Windows based WIM file with operating system installed and
    configured with Sysprep

  - Sample Sysprep unattend file to be used with the operating system

  - Sample PXE menu item that downloads WinPE ISO, mount in memdisk and
    boot into WinPE environment

### Connecting to a PXE Server

The following procedure connects to a PXE server and adds its details to
ManageIQ.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    PXE</span>.

2.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a New PXE Server**).

3.  In **Basic Information**, type a **Name** that will be meaningful in
    your environment. ![2316](images/2316.png)

4.  For **Depot Type**, select either **Network File System** (NFS) or
    **Samba**. The fields to enter in the dialog depend on the **Depot
    Type**.
    
      - For NFS, type in the **URI**, **Access URL**, **PXE Directory**,
        **Windows Images Directory**, and **Customization Directory**.
        When you provision, ManageIQ writes a text file to the **PXE
        Directory**. The file is named after the MAC address of the NIC
        that is assigned to the virtual machine. It contains where to
        get the kernel and initrd image. This file is removed after a
        successful provision. The **Windows Images Directory** is where
        the files are located on your NFS for the provisioning of
        Windows operating systems. The **Customization Directory** is
        where your Kickstart and Sysprep files are located.
    
      - If using a **Depot Type** of **Samba**, you will not need
        **Access URL**, but you will need a **User ID**, and
        **Password**, in addition to the items required for NFS.

5.  For **PXE Image Menus**, type the **Filename** for the PXE Boot
    menu.

6.  Click **Add**.

7.  Select the new PXE server from the tree on the left, and click
    ![1847](images/1847.png)(**Configuration**), then
    ![2003](images/2003.png)(**Refresh**) to see your existing images.

<div class="informalexample">

Next, create PXE Image types to associate with the customization
templates and to specify if the image type is for a virtual machine, a
host, or both.

</div>

### Creating System Image Types for PXE

The following procedure creates a system image type for PXE servers.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    PXE</span>.

2.  Click the **System Image Types** accordion. ![2318](images/2318.png)

3.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1848](images/1848.png)(**Add a new System Image Type**).

4.  In **Basic Information**, type in a **Name** and select a **Type**.
    ![2317](images/2317.png)
    
      - Use **Vm** if you want this image type to only apply to virtual
        machines.

5.  Click **Add**.

<div class="informalexample">

After creating the System Image Types, assign the types to each image on
your PXE servers. To do this, you will select each image on the PXE
server and identify its type.

</div>

### Setting the PXE Image Type for a PXE Image

The following procedure sets the image type for a chosen PXE image.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    PXE</span>.

2.  Click the **PXE Servers** accordion and select the image that you
    want to set a type for.

3.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1851](images/1851.png)(**Edit this PXE Image**).

4.  From the **Basic Information** area, select the correct type. If
    this PXE image will be used as the **Windows Boot Environment**,
    check **Windows Boot Environment**. At the time of this writing,
    only one PXE Image can be identified as the **Windows Boot
    Environment**. Therefore, checking one as the **Windows Boot
    Environment**, will remove that from any other PXE image with that
    check. ![2319](images/2319.png) Click **Save**.
    ![2320](images/2320.png)

## ISO Provisioning

ManageIQ also allows ISO provisioning from Red Hat Virtualization
Manager datastores. To use this feature, you will need to do the
following before creating a provision request.

1.  Add the **ISO Datastore**. The Red Hat Virtualization Manager system
    must have already been discovered or added into the VMDB. For more
    information, see [Adding a Red Hat Enterprise Virtualization Manager
    Provider](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#adding_a_red_hat_enterprise_virtualization_manager_provider)
    in *Managing Providers*.

2.  Refresh the **ISO Datastore**.

3.  Create a **System Image Type**.

4.  Set the **ISO Image Type**.

5.  **Create** a customization template.

### Adding an ISO Datastore

The following procedure adds an ISO Datastore from your Red Hat
Virtualization environment.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    PXE</span>.

2.  Click the **ISO Datastores** accordion.

3.  Click ![1847](images/1847.png)(**Configuration**),
    ![1862](images/1862.png)(**Add a new ISO Datastore**).

4.  Select the Cloud or Infrastructure provider hosting the ISO
    Datastore.

5.  Click **Add**.

The ISO datastore is added to ManageIQ.

### Refreshing an ISO Datastore

The following procedure refreshes the chosen ISO datastore and updates
ManageIQ with available ISOs.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    PXE</span>.

2.  Click the **ISO Datastores** accordion, and select an ISO datastore.

3.  Click ![1847](images/1847.png)(**Configuration**), then click
    ![2003](images/2003.png)(**Refresh Relationships**).

### Creating System Image Types for ISO

The following procedure creates a system image type for ISO Servers.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    PXE</span>.

2.  Click the **System Image Types** accordion.

3.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a new System Image Type**).

4.  In **Basic Information**, type in a **Name** and select a **Type**.
    ![2317](images/2317.png)
    
      - Use **Vm** if you want this image type to only apply to virtual
        machines.

5.  Click **Add**. ![2322](images/2322.png)

<div class="informalexample">

After creating the system image types, assign the types to each image on
your ISO servers. To do this, you will select each image on the ISO
server and identify its type.

</div>

### Setting the Image Type for an ISO Image

The following procedure sets the image type for an ISO image.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    PXE</span>.

2.  Click the **ISO Datastores** accordion, and select the image that
    you want to set a type for.

3.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1851](images/1851.png)(**Edit this ISO Image**).

4.  From the **Basic Information** area, select the correct **Type**.
    ![2323](images/2323.png)

5.  Click **Save**.

## Customization Templates for Virtual Machine and Instance Provisioning

Add a customization template to provide **Kickstart**, **Cloud-Init**,
or **Sysprep** files for the initial loading of the operating system.

  - When creating a template using Red Hat Virtualization, install the
    **cloud-init** package on the source virtual machine. This enables
    Cloud-Init to source configuration scripts when a virtual machine
    built on that template boots.

  - See [Using Cloud-Init to Automate the Configuration of Virtual
    Machines](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Virtualization/3.6/html-single/Virtual_Machine_Management_Guide/index.html#sect-Using_Cloud-Init_to_Automate_the_Configuration_of_Virtual_Machines)
    in the Red Hat Virtualization *Administration Guide* for more
    information on using Cloud-Init in a Red Hat Virtualization
    environment.

  - See the [Cloud-Init
    Documentation](http://cloudinit.readthedocs.org/en/latest/) web site
    for example scripts.

<!-- end list -->

  - The **Kickstart** file must be named **ks.cfg**.

  - Set the new virtual machine to power down after provisioning is
    complete.

  - ManageIQ must use the virtual machine payload feature of Red Hat
    Virtualization to create a floppy disk containing the data from the
    selected customization template.

  - Customize the installer to include the data written to the floppy
    disk payload.

<!-- end list -->

  - RHEL 7.5 and above

  - `isolinux.cfg` NDASH add **ks=cdrom** to the **append** line

  - `ks.cfg` NDASH which must minimally include:

<!-- end list -->

    ### Pre Install Scripts
    %pre
    
    # Mount the floppy drive
    modprobe floppy
    mkdir /tmp/floppy
    mount /dev/fd0 /tmp/floppy
    %end
    
    # Include ks.cfg file from the floppy (written by CFME based on selected customization template)
    %include /tmp/floppy/ks.cfg

## Customization Script Additions for Virtual Machine and Instance Provisioning

| Customization Type | Reason to Include                                                                                                                                                                                                         | Script entries                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Kickstart          | Takes the values from the **Customize** tab in **Provisioning Dialog** and substitutes them into the script.                                                                                                              | *Configure Networking based on values from provisioning dialog \<% if evm\[:addr\_mode\].first == *static* %\> \<% network\_string = "network --onboot yes --device=eth0 --bootproto=static --noipv6" %\> \<% \["ip", :ip\_addr, "netmask", :subnet\_mask, "gateway", :gateway, "hostname", :hostname, "nameserver", :dns\_servers\].each\_slice(2) do |ks\_key, evm\_key| %\> \<% network\_string \<\< " --*{ks\_key} \#{evm\[evm\_key\]}" unless evm\[evm\_key\].blank? %\> \<% end %\> \<%= network\_string %\> \<% else %\> network --device=eth0 --bootproto=dhcp \<% end %\> |
| Kickstart          | Encrypts the root password from the **Customize** tab in the **Provisioning Dialog**.                                                                                                                                     | rootpw --iscrypted \<%= ManageIQ::Password.md5crypt(evm\[:root\_password\]) %\>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Kickstart          | Sends status of the provision back to ManageIQ Server for display in the ManageIQ Console.                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Sysprep            | Encrypts the root password from the **Customize** tab in the **Provisioning Dialog**. The value for the **AdministratorPassword** line must be inserted to use the password from the **Provision Dialog** and encrypt it. | \<UserAccounts\> \<AdministratorPassword\> \<Value\>\<%= ManageIQ::Password.sysprep\_crypt(evm\[:root\_password\]) %\>\</Value\> \<PlainText\>false\</PlainText\> \</AdministratorPassword\> \</UserAccounts\>                                                                                                                                                                                                                                                                                                                                                                     |

## Adding a Customization Template

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    PXE</span>.

2.  Click the **Customization Templates** accordion.

3.  Click ![1847](images/1847.png)(**Configuration**),
    ![1862](images/1862.png)(**Add a new Customization Template**).

4.  In **Basic Information**, type in a **Name** and **Description**.
    ![2324](images/2324.png)

5.  Select the **Image Type**. This list should include the PXE image
    types you created.

6.  In **Type**, select **Kickstart** or **CloudInit** for Linux based
    systems, and **Sysprep** for Windows based system.

7.  In the **Script** area, either paste the script from another source
    or type the script directly into the ManageIQ interface.

8.  Click **Add**.

<div class="informalexample">

The default dialogs show all possible parameters for provisioning. To
limit the options shown, see [Customizing Provisioning
Dialogs](#provisioning-dialogs-customizing).

</div>

## Provisioning Virtual Machines

There are four types of provisioning requests available in ManageIQ:

1.  Provision a new virtual machine from a template

2.  Clone a virtual machine

3.  Publish a virtual machine to a template

4.  Provision a virtual machine using cloud-init via REST API.

### Provisioning a Virtual Machine from a Template

You can provision virtual machines through various methods. One method
is to provision a virtual machine directly from a template stored on a
provider.

<div class="important">

  - To provision a virtual machine, you must have the "Automation
    Engine" role enabled.

  - During virtual machine provisioning, the **Customize** tab is hidden
    if the template has an unknown operating system (OS) type. To make
    the **Customize** tab visible in the user interface, you will need
    to set the OS type from the provider or perform SmartState analysis
    on the template to detect the OS type.

</div>

To provision a virtual machine from a template:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click ![2007](images/2007.png)(**Lifecycle**), and then
    ![1862](images/1862.png)(**Provision VMs**).

3.  Select a template from the list.

4.  Click **Continue**.

5.  On the **Request** tab, enter the request information.
    
    ![request info](images/request-info.png)
    
    In **Request Information**, enter your name and email address. The
    requester will receive status emails about the provisioning request
    such as auto-approval, quota, provision complete, retirement,
    request pending approval, and request denied.
    
    <div class="note">
    
    Parameters with a \* next to the label are required to submit the
    provisioning request. To change the required parameters, see
    [Customizing Provisioning
    Dialogs](#provisioning-dialogs-customizing).
    
    </div>

6.  Click the **Purpose** tab to select the appropriate tags for the
    provisioned virtual machines.

7.  Click the **Catalog** tab to select the template to provision from.
    This tab is context sensitive based on provider.

8.  For templates on VMware providers: ![2328](images/2328.png)
    
    1.  For **Provision Type**, select **VMware** or **PXE**.
        
        1.  If **VMware** is selected, select **Linked Clone** to create
            a linked clone to the virtual machine instead of a full
            clone. Since a snapshot is required to create a linked
            clone, this box is only enabled if a snapshot is present.
            Select the snapshot you want to use for the linked clone.
        
        2.  If **PXE** is selected, select a PXE **Server** and
            **Image** to use for provisioning.
    
    2.  Under **Count**, select the number of virtual machines to create
        in this request.
    
    3.  Use **Naming** to specify a virtual machine name and virtual
        machine description. When provisioning multiple virtual
        machines, a number will be appended to the virtual machine name.

9.  For templates on Red Hat providers:
    
    1.  Select the **Name** of a template to use.
    
    2.  For **Provision Type**, select either **ISO**, **PXE**, or
        **Native Clone**. You must select **Native Clone** in order to
        use a Cloud-Init template.
        
        1.  If **Native Clone** is selected, select **Linked Clone** to
            create a linked clone to the virtual machine instead of a
            full clone. This is equivalent to *Thin Template
            Provisioning* in Red Hat Virtualization. Since a snapshot is
            required to create a linked clone, this box is only enabled
            if a snapshot is present. Select the snapshot to use for the
            linked clone.
        
        2.  If **ISO** is selected, select an ISO **Image** to use for
            provisioning.
        
        3.  If **PXE** is selected, select a PXE **Server** and
            **Image** to use for provisioning.
    
    3.  Under **Count**, select the number of virtual machines you want
        to create in this request.
    
    4.  Use **Naming** to specify a **VM Name** and **VM Description**.
        When provisioning multiple virtual machines, a number will be
        appended to the **VM Name**.

10. Click the **Environment** tab to decide where you want the new
    virtual machines to reside.
    
    1.  If provisioning from a template on VMware, you can either let
        ManageIQ decide for you by checking **Choose Automatically**, or
        select a specific cluster, resource pool, folder, host, and
        datastore. VMware virtual machines can also be provisioned to a
        clustered datastore by selecting it under **Datastore**.
        Additionally, you can assign a storage profile to a VMware
        virtual machine under **Datastore** to configure the virtual
        machine to operate using a storage profile from that datastore.
        
        Note, read-only datastores are excluded when provisioning a
        virtual machine.
    
    2.  If provisioning from a template on Red Hat, you can either let
        ManageIQ decide for you by checking **Choose Automatically**, or
        select a datacenter, cluster, host and datastore.

11. Click the **Hardware** tab to set hardware options. ![provision
    vms](images/provision-vms.png)
    
    1.  In **Hardware**, set the number of sockets, cores per socket,
        memory in MB, and disk format: thin, pre-allocated/thick or same
        as the provisioning template (default).
    
    2.  For VMware provisioning, set the **VM Limits** of CPU and memory
        the virtual machine can use.
    
    3.  For VMware provisioning, set the **VM Reservation** amount of
        CPU and memory.

12. Click **Network** to set the vLan adapter. Additional networking
    settings that are internal to the operating system appear on the
    **Customize** tab. ![2335](images/2335.png)
    
    1.  In **Network Adapter Information**, select the **vLan**.
        
        <div class="note">
        
        A VMware virtual machine can be provisioned to a DVPortgroup by
        selecting it from the **vLan** list. Prior to provisioning a
        virtual machine, the DVPortgroup must be created on a vSphere
        Distributed Switch (VDS) in VMware vCenter in order for ManageIQ
        to list the DVPortgroup under **vLan**.
        
        </div>

13. Click **Customize** to customize the operating system of the new
    virtual machine. These options vary based on the operating system of
    the template. ![2336](images/2336.png)

14. For Windows provisioning:
    
    1.  To use a custom specification from the provider, click
        **Specification**. To select an appropriate template, choose
        from the list in the custom specification area. The values that
        are honored by ManageIQ display.
        
        <div class="note">
        
        Any values in the specification that do not show in the ManageIQ
        console’s request dialogs are not used by ManageIQ. For example,
        for Windows operating systems, if you have any run once values
        in the specification, they are not used in creating the new
        virtual machines. Currently, for a Windows operating system,
        ManageIQ honors the unattended GUI, identification, workgroup
        information, user data, windows options, and server license. If
        more than one network card is specified, only the first is used.
        
        </div>
        
        ![2337](images/2337.png)
        
        To modify the specification, select **Override Specification
        Values**.
    
    2.  Select **Sysprep Answer File**, to upload a Sysprep file or use
        one that exists for a custom specification on the Provider where
        the template resides. To upload a file, click **Browse** to find
        the file, and then upload. To use an answer file in
        **Customization Specification**, click on the item. The answer
        file will automatically upload for viewing. You cannot make
        modifications to it.

15. For Linux provisioning:
    
    1.  Under **Credentials**, enter a **Root Password** for the
        **root** user to access the instance.
    
    2.  Enter a **IP Address Information** for the instance. Leave as
        **DHCP** for automatic IP assignment from the provider.
    
    3.  Enter any **DNS** information for the instance if necessary.
    
    4.  Select **Customize Template** for additional instance
        configuration. Select from the Kickstart or Cloud-Init
        customization templates stored on your appliance.

16. Click the **Schedule** tab to select when provisioning begins.
    
    1.  In **Schedule Info**, select when to start provisioning. If you
        select **Schedule**, you will be prompted to enter a date and
        time. Select **Stateless** if you do not want the files deleted
        after the provision completes. A stateless provision does not
        write to the disk so it requires the PXE files on the next boot.
    
    2.  In **Lifespan**, select to power on the virtual machines after
        they are created, and to set a retirement date. If you select a
        retirement period, you will be prompted for when you want a
        retirement warning. ![2338](images/2338.png)

17. Click **Submit**.

The provisioning request is sent for approval. For the provisioning to
begin, a user with the administrator, approver, or super administrator
account role must approve the request. The administrator and super
administrator roles can also edit, delete, and deny the requests. You
will be able to see all provisioning requests where you are either the
requester or the approver.

After submission, the appliance assigns each provision request a
**Request ID**. If an error occurs during the approval or provisioning
process, use this ID to locate the request in the appliance logs. The
Request ID consists of the region associated with the request followed
by the request number. As regions define a range of one trillion
database IDs, this number can be several digits long.

**Request ID Format**

Request 99 in region 123 results in Request ID 123000000000099.

### Provisioning a Virtual Machine using Cloud-Init via REST API

Cloud-init is a tool for automating the initial setup of virtual
machines. In ManageIQ, you can use cloud-init via REST API to provision
a virtual machine that was created based on a template.

<div class="note">

To use cloud-init, the template from which the virtual machine is
provisioned must have cloud-init package installed, and have the **Use
Cloud-Init/Sysprep** option selected.

</div>

For a virtual machine provision request via REST API, ensure the
following two fields in the request’s body are set correctly, otherwise
cloud-init may not work.

  - VLAN

  - sysprep\_enabled

**VLAN.**

The value of **VLAN** in the API request can be one of the following
options:

| VLAN value                    | Note                                                                                                                       | vNIC profile                                                                    |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| \<empty\>                     | Must be written within the \<..\>                                                                                          | No vNIC profile                                                                 |
| \<Template\>                  | Must be written within the \<..\>                                                                                          | Use the template’s default vNIC profile                                         |
| profile\_name (network\_name) | Must include a space between profile\_name (network\_name), otherwise it will fail. For example, **ovirtmgmt (ovirtmgmt)** | Set the specified vNIC profile.                                                 |
| vNIC profile ID               |                                                                                                                            | Set the specified vNIC profile, such as `3a8dce01-dd59-4a46-8a6f-823acccda79f`. |

**sysprep\_enabled.**

The value of sysprep\_enabled in the API request must be in the
following format.

<div class="note">

Sysprep\_enabled is written in the order: \[value\] - \[it’s meaning\] -
\[how it appears in the ManageIQ user interface virtual machine
provision dialog’s **Customize** tab\]

</div>

**For Windows template**:

  - **"fields"** - Sysprep Specification  
    In the ManageIQ user interface, when you navigate to the virtual
    machine provision dialog (<span class="menuchoice">Compute \>
    Infrastructure \> Virtual Machine</span>), this option located under
    the **Customize** tab’s **Customize** drop-down list is called
    **Sysprep Specification**.

  - **"file"** - Sysprep answer file  
    In the ManageIQ user interface, when you navigate to the virtual
    machine provision dialog (<span class="menuchoice">Compute \>
    Infrastructure \> Virtual Machine</span>), this option located under
    the **Customize** tab’s **Customize** drop-down list is called
    **Sysprep answer file**.

**For Linux template**:

  - **“fields”** - Customized template and any Customized parameters
    will be used  
    In the ManageIQ user interface, when you navigate to the virtual
    machine provision dialog (<span class="menuchoice">Compute \>
    Infrastructure \> Virtual Machine</span>), this option located under
    the **Customize** tab’s **Customize** drop-down list is called
    **Specification**.

<div class="note">

For cloud-init to work *(that is, to have the provisioned virtual
machine marked with **Use cloud-init** and the customized template as
well as customized parameters, if any, will be used)* "sysprep\_enabled"
must be set to “fields”. If you do not set it correctly, the customized
template will be ignored and the provisioned virtual machine will not be
marked with **Use cloud-init**; although, the template from which the
virtual machine is provisioned has it marked.

</div>

**For both Windows and Linux template**:

  - **“disabled”** - Do not customize  
    In the ManageIQ user interface, when you navigate to the virtual
    machine provision dialog (<span class="menuchoice">Compute \>
    Infrastructure \> Virtual Machine</span>), this option located under
    the **Customize** tab’s **Customize** drop-down list is called
    **\<None\>**. The customized template will be ignored, and the
    provisioned virtual machine will not be marked with **Use
    cloud-init**, even though the template from which the virtual
    machine was provisioned, has it marked. The default value is
    *disabled*.

<div class="note">

For an example of virtual machine provisioning request using cloud-init
via REST API, see *Provisioning a Virtual Machine Using Cloud-init* in
the [ManageIQ REST
API](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/red_hat_cloudforms_rest_api/index)
guide.

</div>

### Cloning a Virtual Machine

Virtual machines can be cloned in other providers as well.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>, and select the virtual machine you want to
    clone.

2.  Click ![2007](images/2007.png)(**Lifecycle**), and then
    ![2339](images/2339.png)(**Clone selected item**).

3.  Enter the requested information in the dialogs. Be sure to check the
    **Catalog** tab.

4.  Schedule the request on the **Schedule** tab.

5.  Click **Submit**.

### Publishing a Virtual Machine to a Template (VMware Virtual Machines Only)

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>, and select the virtual machine you want to
    publish as a template.

2.  Click ![2007](images/2007.png)(**Lifecycle**), and then
    ![2340](images/2340.png)(**Publish selected VM to a Template**).

3.  Enter the requested information in the dialogs. Be sure to check the
    **Catalog** tab.

4.  Schedule the request on the **Schedule** tab.

5.  Click **Submit**.

### Renaming a Provisioned Virtual Machine (VMware Virtual Machines Only)

ManageIQ allows you to rename a VMware virtual machine without having to
reprovision it.

To rename a VMware virtual machine:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>, and select the VMware virtual machine you
    want to rename.

2.  Click ![1847](images/1847.png)(**Configuration**),
    ![1851](images/1851.png)(**Rename selected item**).

3.  In the **Basic Information** screen, provide a new **name**.

4.  Click **Save**.

The renamed virtual machine will appear in the inventory view.

## Provisioning Instances

Cloud instances follow the same process (Request, Approval, Deployment)
as a standard virtual machine from virtualization infrastructure. First,
a user makes a request for instances and specifies the image, volume or
volume snapshot, tags, availability zone and hardware profile flavor.
Second, the request goes through the approval phase. Finally, ManageIQ
executes the request.

### Provisioning an EC2 Instance from an Image

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click ![2007](images/2007.png)(**Lifecycle**), then click
    ![1862](images/1862.png)(**Provision Instances**).

3.  Select an image from the list presented.

4.  Click **Continue**.

5.  On the **Request** tab, enter information about this provisioning
    request. In **Request Information**, type in at least a first and
    last name and an email address. This email is used to send the
    requester status emails during the provisioning process for items
    such as auto-approval, quota, provision complete, retirement,
    request pending approval, and request denied. The other information
    is optional. If the ManageIQ Server is configured to use LDAP, you
    can use the **Look Up** button to populate the other fields based on
    the email address.
    
    <div class="note">
    
    Parameters with a \* next to the label are required to submit the
    provisioning request. To change the required parameters, see
    [Customizing Provisioning
    Dialogs](#provisioning-dialogs-customizing).
    
    </div>

6.  Click the **Purpose** tab to select the appropriate tags for the
    provisioned instance.

7.  Click the **Catalog** tab for basic instance options.
    
    1.  To change the image to use as a basis for the instance, select
        it from the list of images.
    
    2.  Select the **Number of VMs** to provision.
    
    3.  Type a **VM Name** and **VM Description**.

8.  Click the **Environment** tab to select the instance’s
    **Availability Zone**, **Virtual Private Cloud**, **Cloud Subnet**,
    **Security Groups**, and **Elastic IP Address**. If no specific
    availability zone is required, select the **Choose Automatically**
    checkbox.

9.  Click the **Properties** tab to set provider options such as
    hardware flavor and security settings.
    
    1.  Select a flavor from the **Instance Type** list.
    
    2.  Select a **Guest Access Key Pair** for access to the instance.
    
    3.  Select the **CloudWatch** monitoring level. Leave as **Basic**
        for the default EC2 monitoring.

10. Click the **Customize** tab to set additional instance options.
    
    1.  Under **Credentials**, enter a **Root Password** for the
        **root** user access to the instance.
    
    2.  Enter a **IP Address Information** for the instance. Leave as
        **DHCP** for automatic IP assignment from the provider.
    
    3.  Enter any **DNS** information for the instance if necessary.
    
    4.  Select a **Customize Template** for additional instance
        configuration. Select from the Cloud-Init scripts stored on your
        appliance.

11. Click the **Schedule** tab to set the provisioning and retirement
    date and time.
    
    1.  In **Schedule Info**, choose whether the provisioning begins
        upon approval, or at a specific time. If you select
        **Schedule**, you will be prompted to enter a date and time.
    
    2.  In **Lifespan**, select whether to power on the instances after
        they are created, and whether to set a retirement date. If you
        select a retirement period, you will be prompted for when to
        receive a retirement warning.

12. Click **Submit**.

The provisioning request is sent for approval. For the provisioning to
begin, a user with the admin, approver, or super admin account role must
approve the request. The admin and super admin roles can also edit,
delete, and deny the requests. You will be able to see all provisioning
requests where you are either the requester or the approver.

After submission, the appliance assigns each provision request a
**Request ID**. If an error occurs during the approval or provisioning
process, use this ID to locate the request in the appliance logs. The
Request ID consists of the region associated with the request followed
by the request number. As regions define a range of one trillion
database IDs, this number can be several digits long.

**Request ID Format**

Request 99 in region 123 results in Request ID 123000000000099.

### Provisioning an OpenStack Instance from an Image, Volume or Volume Snapshot

Create a request to provision Red Hat OpenStack Platform cloud instances
from images, volumes, and volume snapshots using ManageIQ. Only bootable
volumes not in use will be available.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click ![2007](images/2007.png)(**Lifecycle**), then click
    ![1862](images/1862.png)(**Provision Instances**).

3.  Select an OpenStack image, volume or volume snapshot from the list
    presented. These files must be available on your OpenStack provider.

4.  Click **Continue**.

5.  On the **Request** tab, enter information about this provisioning
    request. In **Request Information**, type in at least an email
    address. This email is used to send the requester status emails
    during the provisioning process for items such as auto-approval,
    quota, provision complete, retirement, request pending approval, and
    request denied. The other information is optional. If the ManageIQ
    Server is configured to use LDAP, you can use the **Look Up** button
    to populate the other fields based on the email address.
    
    <div class="note">
    
    Parameters with a \* next to the label are required to submit the
    provisioning request. To change the required parameters, see
    [Customizing Provisioning
    Dialogs](#provisioning-dialogs-customizing).
    
    </div>

6.  Click the **Purpose** tab to select the appropriate tags for the
    provisioned instance.

7.  Click the **Catalog** tab for basic instance options.
    
    1.  To change the source file to use as a basis for the instance,
        select it from the list of images, volumes, or volume snapshots.
    
    2.  Select the **Number of Instances** to provision.
    
    3.  Type a **Instance Name** and **Instance Description**.

8.  Click the **Environment** tab to select the instance’s **Cloud
    Tenant**, **Availabilty Zones**, **Cloud Network**, **Security
    Groups**, and **Public IP Address**. If no specific Cloud Tenant is
    required, select the **Choose Automatically** checkbox.

9.  Click the **Properties** tab to set provider options such as flavors
    and security settings.
    
    1.  Select a flavor from the **Instance Type** list.
    
    2.  Select a **Guest Access Key Pair** for access to the instance.
        For more information about key pairs, see [Managing Key
        Pairs](#provision-keypairs).

10. Click the **Volumes** tab to provision any volumes with the
    instance. Volumes are useful for augmenting ephemeral storage of
    instances with persistent, general-purpose block storage:
    
    1.  Fill in the **Volume Name** and **Size (gigabytes)** fields.
    
    2.  If you want the volume to be deleted once the instance
        terminates (thereby making it non-persistent), check **Delete on
        Instance Terminate**.
    
    3.  To provision and add multiple volumes to the instance, click
        **Add Volume**. Doing so will add new fields you can fill in.
        
        For more information about persistent storage in OpenStack, see
        the Red Hat OpenStack Platform *Storage Guide*.

11. Click the **Customize** tab to set additional instance options.
    
    1.  Under **Credentials**, enter a **Root Password** for the
        **root** user access to the instance.
    
    2.  Enter a **IP Address Information** for the instance. Leave as
        **DHCP** for automatic IP assignment from the provider.
    
    3.  Enter any **DNS** information for the instance if necessary.
    
    4.  Select a **Customize Template** for additional instance
        configuration. Select from the Cloud-Init scripts stored on your
        appliance.

12. Click the **Schedule** tab to set the provisioning and retirement
    date and time.
    
    1.  In **Schedule Info**, choose whether the provisioning begins
        upon approval, or at a specific time. If you select
        **Schedule**, you will be prompted to enter a date and time.
    
    2.  In **Lifespan**, select whether to power on the instances after
        they are created, and whether to set a retirement date. If you
        select a retirement period, you will be prompted for when to
        receive a retirement warning.

13. Click **Submit**.

The provisioning request is sent for approval. For the provisioning to
begin, a user with the admin, approver, or super admin account role must
approve the request. The admin and super admin roles can also edit,
delete, and deny the requests. You will be able to see all provisioning
requests where you are either the requester or the approver.

After submission, the appliance assigns each provision request a
**Request ID**. If an error occurs during the approval or provisioning
process, use this ID to locate the request in the appliance logs. The
Request ID consists of the region associated with the request followed
by the request number. As regions define a range of one trillion
database IDs, this number can be several digits long.

**Request ID Format**

Request 99 in region 123 results in Request ID 123000000000099.

### Customizing Provisioning Dialogs

The default set of provisioning dialogs shows all possible options.
However, ManageIQ also provides the ability to customize which tabs and
fields are shown. You can decide what fields are required to submit the
provisioning request or set default values.

For each type of provisioning, there is a dialog that can be created to
adjust what options are presented. While samples are provided containing
all possible fields for provisioning, you can remove what fields are
shown but cannot add new fields or tabs.

Edit the dialogs to:

1.  Hide or show provisioning tabs.

2.  Hide or show fields. If you hide an attribute, the default will be
    used, unless you specify otherwise.

3.  Set default values for a field.

4.  Specify if a field is required to submit the request.

5.  Create custom dialogs for specific users.

#### Adding a Provision Dialog for All Users

1.  Login to the ManageIQ console for the ManageIQ server where you want
    to change the dialog.

2.  Navigate to <span class="menuchoice">Automate \>
    Customization</span>.

3.  Click the **Provisioning Dialogs** accordion.

4.  Click the type of dialog you want to create: **Host Provision**,
    **VM Provision** or **VM Migrate**.

5.  Select one of the default dialogs.

6.  Click ![1847](images/1847.png)**(Configuration)**, and then
    ![1859](images/1859.png)**(Copy this Dialog)**.

7.  Type a new **Name** and **Description** for the dialog.

8.  In the **Content** field,
    
      - To remove a tab from display, change its display value to
        ignore. By choosing ignore, you not only hide the tab, but also
        skip any fields on that tab that were required. To show the tab,
        change the display value to show.
    
      - To hide a field, change its `:display:` value from `:edit` to
        `:hide`. To display fields of most data types, use `:edit`. To
        display a button, use `:show`. To set a default value for a
        field, add `:default: defaultvalue` to the list of parameters
        for the field. Set the `:required:` parameter to either `true`
        or `false` based on your needs.
        
        <div class="note">
        
        If you set `:required:` to `true`, the field must have a value
        for the provision request to be submitted.
        
        </div>

9.  Click **Add**.

If you are using **Provisioning Profiles**, you can specify a specific
file that holds the customizations. To do this, you must create an
instance mapping to this file in the ManageIQ
**Applications/provisioning/profile/VM provisioning by group** class. By
default, if you are using provisioning profiles and the group does not
have a defined instance, the appropriate default dialog file will be
used based on the type of provisioning selected.

#### Creating a Custom Provision Dialog

1.  Navigate to <span class="menuchoice">Automate \>
    Customization</span>.

2.  Click on the **Provisioning Dialogs** accordion.

3.  Click on the type of dialog you want to create, **Host Provision**,
    **VM Provision** or **VM Migrate**.

4.  Select one of the default dialogs.

5.  Click ![1847](images/1847.png)(**Configuration**), and then
    ![1859](images/1859.png)(**Copy this Dialog**).

6.  Rename the dialog as shown in the examples below.
    
    | Type of Provision                         | Dialog Name                                                                                                                                   |
    | ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
    | Provision Virtual Machine from a template | miq\_provision\_dialogs\_groupname\_template Example: miq\_provision\_dialogs\_ EvmGroup-user\_self\_service \_template                       |
    | Clone a Virtual Machine                   | miq\_provision\_dialogs\_groupname\_clone\_to\_vm Example: miq\_provision\_dialogs\_ EvmGroup-user\_self\_service \_clone\_to\_vm             |
    | Publish a Virtual Machine to a template   | miq\_provision\_dialogs\_groupname\_clone\_to\_template Example: miq\_provision\_dialogs\_ EvmGroup-user\_self\_service \_clone\_to\_template |
    

7.  Make any changes you need.

8.  In the **Content** field,
    
      - To remove a tab from display, change its display value to
        ignore. By choosing ignore, you not only hide the tab, but also
        skip any fields on that tab that were required. To show the tab,
        change the display value to show.
    
      - To hide a field, change its `:display:` value from `:edit` to
        `:hide`. To ensure the field does not get turned back on by a
        workflow model, use `:display_override: :hide`. To display
        fields of most data types, use `:edit`. To display a button, use
        `:show`. To set a default value for a field, add `:default:
        defaultvalue` to the list of parameters for the field. Set the
        `:required:` parameter to either `true` or `false` based on your
        needs.
        
        <div class="note">
        
        If you set `:required:` to `true`, the field must have a value
        for the provision request to be submitted.
        
        </div>

9.  Click **Add**.

Enter the name of the new dialog into the dialog name field in the
appropriate ManageIQ **Applications/provisioning/profile instance**.
This dialog can now be referred to in an instance in the Provisioning
Profiles class so that it can be used for groups of users.

### Provisioning Profiles

Provisioning profiles can be used to customize the dialogs and the state
machine (steps used to provision the machine). Profiles can be created
for LDAP or ManageIQ groups. To use provisioning profiles:

  - Create a **Provisioning Profile** instance for the LDAP or ManageIQ
    group. If no instance exists, then default settings will be used.

  - If customizing dialogs, create a custom dialog file, and specify the
    name of that file in the provisioning profile instance. If
    customizing the states for provisioning, create a state instance and
    set the name of the state instance in the provisioning profile
    instance.

The diagram below shows where provisioning profiles are called during
the entire provisioning process. ![2344](images/2344.png)

#### Creating a Provisioning Profile Instance

1.  Navigate to <span class="menuchoice">Automate \> Explorer</span>.

2.  Using the tree located in the accordion, click
    <span class="menuchoice">DOMAIN \> Cloud \> VM \> Provisioning \>
    Profile</span>.
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    This example uses the **Cloud** Namespace, but can also use the
    **Infrastructure** namespace.
    
    </div>

3.  Click ![1847](images/1847.png)(**Configuration**),
    ![2345](images/2345.png)(**Add a New Instance**).

4.  Make the name of the tag identical to the name of the LDAP or
    ManageIQ group you are creating the instance for, replacing spaces
    in the group name with underscores. For example, change
    **ManageIQ-test group** to **ManageIQ-test\_group**.
    ![6278](images/6278.png)

5.  In the dialog name field, enter the name of the customized dialog
    file. This file must reside on the ManageIQ appliance in the
    `/var/www/miq/vmdb/db/fixtures` directory. Red Hat recommends naming
    the file in the format `miq_provision_dialogs-groupname.rb` and
    copying this file to all ManageIQ appliances. For instructions on
    creating a custom dialog file, see [Customizing Provisioning
    Dialogs](#provisioning-dialogs-customizing).
    
    <div class="note">
    
    Be sure that the custom dialog file exists. If it does not, an error
    will appear when the user clicks on the **Provisioning** button in
    the ManageIQ console.
    
    </div>

6.  Click **Add**.

#### Setting Provisioning Scope Tags

Some non-default placement methods, for example the
**redhat\_best\_placement\_with\_scope** or
**vmware\_best\_fit\_with\_scope** methods, may require you to set
**Provisioning Scope** tags for a host and a datastore.

To enable these resources for all groups, set the scope to **All**. To
limit access to a select group, create a tag in the **Provisioning
Scope** category with the exact name of the user group and set this tag
on the desired resources. See
[Tags](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/general_configuration/#regions)
in *General Configuration* for information on creating tags.

To set the scope for a datastore:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Datastores</span>.

2.  Select the datastore to set the provisioning scope for.

3.  Click ![1941](images/1941.png)(**Policy**), and then
    ![1851](images/1851.png)(**Edit Tags**).

4.  From the **Select a customer tag to assign** drop down, select
    **Provisioning Scope** and then a value for the tag from the next
    drop down menu.

5.  Click **Save**.

### Managing Key Pairs

Key pairs allow you to manage SSH access between a user and provisioned
instance. For more information about key pairs in OpenStack, see [Manage
Key
Pairs](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/instances_and_images_guide/ch-manage_instances#section-manage-keypair)
in the *Instances and Images Guide*.

To manage key pairs, navigate to <span class="menuchoice">Compute \>
Clouds \> Key Pairs</span>. From there, you can view a list of available
key pairs. Click on a key pair to view its details.

To create a new key pair:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \> Key
    Pairs</span>.

2.  Click ![1847](images/1847.png)(**Configuration**),
    ![2345](images/2345.png)(**Add a new Key Pair**).

3.  Enter a **Name** for the key pair.

4.  If you want to use a public key, copy its contents into the **Public
    Key (optional)** field.

5.  Select which cloud provider on which to create the key pair. The key
    pair will then be available for use by instances in that provider.

6.  Click **Add**.

# Working with Requests

## Provisioning Request Approval Methods

In this chapter, you will learn about the different approval methods.
The request can be approved manually in the ManageIQ console, set for
automatic approval by setting options in the **Automate Explorer**, or
by using an external method. ![2348](images/2348.png) When using an
external method, the approval actually takes place on the external
system and is sent directly for execution. This chapter discusses how to
view and edit requests in the ManageIQ Console, how to approve a
request, and how to set automatic approval parameters.

## Working with Provisioning Requests

After a provisioning request is sent, if you have proper authority, you
can copy, edit, delete, approve, or deny a request.

After submission, the appliance assigns each provision request a
**Request ID**. If an error occurs during the approval or provisioning
process, use this ID to locate the request in the appliance logs. The
**Request ID** consists of the region associated with the request
followed by the request number. As regions define a range of one
trillion database IDs, this number can be several digits long.

**Request ID Format**

**Request 99** in **region 123** results in **Request ID
123000000000099**.

### Reloading the Status of Provisioning Requests

1.  Navigate to <span class="menuchoice">Services \> Requests</span>.

2.  Click ![2106](images/2106.png)(**Reload the current display**).

### Approving a Provisioning Request

After a user creates provisioning request, administrators have the
ability to approve the request and allow ManageIQ to complete virtual
machine or instance creation.

1.  Navigate to <span class="menuchoice">Services \> Requests</span>.

2.  Click on the request you want to approve.

3.  Type in a **Reason** for the approval.

4.  Click ![1852](images/1852.png)(**Approve this request**).

### Denying a Provisioning Request

1.  Navigate to <span class="menuchoice">Services \> Requests</span>.

2.  Click on the request you want to deny.

3.  Type in a **Reason** for the denial.

4.  Click ![2009](images/2009.png)(**Deny this request**).

### Copying a Provisioning Request

1.  Navigate to <span class="menuchoice">Services \> Requests</span>.

2.  Click on the request you want to copy.

3.  Click ![1859](images/1859.png)(**Copy original provision request**).

4.  Make changes to the request.

5.  Click **Submit**.

<div class="informalexample">

If the logged in user is not same as the requester or the request has
been already approved or denied, you cannot edit or delete the request.

</div>

### Editing a Provisioning Request

1.  Navigate to <span class="menuchoice">Services \> Requests</span>.

2.  Click on the request you want to edit.

3.  Click ![1851](images/1851.png)(**Edit the original provision
    request**).

4.  Make changes to the request.

5.  Click **Submit**.

### Deleting a Provisioning Request

1.  Navigate to <span class="menuchoice">Services \> Requests</span>.

2.  Click on the request you want to delete.

3.  Click ![1861](images/1861.png)(**Delete this request**).

4.  Click **OK** to confirm.

### Automatically Approving Requests

You can set thresholds for automatic approval of provisioning requests
and, therefore, remove the requirement to manually approve the request.
You can do this either as a global default or on a per template basis.

#### Enabling Global Defaults for Automatic Approval

To enable a global set of default approval values, edit the defaults
instance by navigating to <span class="menuchoice">Automate \>
Explorer</span>, then <span class="menuchoice">DOMAIN \>
Cloud|Infrastructure \> VM \> Provisioning \> StateMachines \>
ProvisionRequestApproval</span> in the accordion menu. The parameters in
this instance are used by the methods in that same class. By default,
the maximum number of virtual machines or instances that can be
automatically approved for provisioning is 1. To skip the check for the
maximum number of virtual machines, set this field to 0. Set this field
to -1 to force manual approval. At a minimum, you must change this
parameter for all others to be validated.

1.  Navigate to <span class="menuchoice">Automate \> Explorer</span>.

2.  From the tree in the accordion menu, select
    <span class="menuchoice">DOMAIN \> Cloud \> VM \> Provisioning \>
    StateMachines \> ProvisionRequestApproval Class</span>.
    
    <div class="note">
    
    DOMAIN must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    This example uses the **Cloud** Namespace but can also use the
    **Infrastructure** namespace.
    
    </div>

3.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1851](images/1851.png)(**Edit this instance**).
    ![6280](images/6280.png)
    
    <div class="note">
    
    Do not change any values other than those listed below. Doing so may
    prevent the automatic approval process from running.
    
    </div>
    
      - Use **max\_cpus** to set the number of CPUs allowed to approve
        automatically the provisioning request.
    
      - Use **max\_vms** to set the maximum number of virtual machines
        or instances that are allowed to be provisioned automatically
        approve the request. If this is set to blank, no requests will
        be automatically approved.
    
      - Use **max\_memory** to set the maximum memory allowed to approve
        automatically the provisioning request.
    
      - Use **max\_retirement\_days** to set the maximum number of days
        until the virtual machine or instance is retired to
        automatically approve this request.
    
      - If a value is blank or **0**, the parameter is ignored.

4.  Click **Save**.

The thresholds for automatic approval are set. The next time a provision
request is created these thresholds will be checked. If the requirements
are met, the provisioning request will be approved with no user
intervention.

#### Template Specific Approval Defaults

ManageIQ provides tags that can be used to set default automatic
approval values on a per template or image basis. These values
**supersede** those in the **Automate** model. Use these tags to
eliminate the need for manual approval for all provisioning requests. To
enable automatic approval, assign the tags directly to templates or
images.

| Category Display Name (Name)                                   | Use (Sample values)                                                                                                                                            |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Auto Approve Max CPU (prov\_max\_cpus)                         | Sets the maximum number of CPUs that can be automatically approved in a single provisioning request. Sample Values: 1, 2, 3, 4, 5                              |
| Auto Approve Max Memory (prov\_max\_memory)                    | Sets the maximum number of memory that can be automatically approved in a single provisioning request. Sample Values: 1, 2, 4, 8 (in GB)                       |
| Auto Approve Max Retirement Days (prov\_max\_retirement\_days) | Sets the maximum number of days until retirement that can be automatically approved in a single provisioning request. Sample Values: 30, 60, 90, 180 (in days) |
| Auto Approve Max VM (prov\_max\_vms)                           | Sets the maximum number of virtual machines or instances that can be automatically approved in a single provisioning request. Sample Values: 1, 2, 3, 4, 5     |

#### Assigning Tags to a Template for Auto Approval

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the **Templates** accordion, and select the templates that you
    want to tag.

3.  Click ![1941](images/1941.png)(**Policy**), and then
    ![1851](images/1851.png)(**Edit Tags**).

4.  Select a customer tag from the first dropdown, and then a value for
    the tag.

The thresholds for automatic approval for a specific template are set.
The next time a provision request is created for this template these
thresholds will be checked. If the requirements are met, the
provisioning request will be approved with no user intervention.

#### Setting Provisioning Notification Email Addresses

ManageIQ contains a set of Automate instances for provisioning. These
Automate instances also include email fields to set the sender and
recipient of provisioning notifications, such as requests. These fields
are set to **evmadmin@company.com** as a default.

1.  Navigate to <span class="menuchoice">Automate \> Explorer</span>.

2.  Choose the following Namespace: <span class="menuchoice">DOMAIN \>
    Cloud \> VM \> Provisioning \> Email</span>.
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    This example uses the **Cloud** Namespace, but can also use the
    **Infrastructure** namespace.
    
    </div>

3.  Select an instance within the chosen class.

4.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1851](images/1851.png)(**Edit this instance**).

5.  Type the desired email addresses in the **to\_email\_address** and
    **from\_email\_address** fields.

6.  Click **Save**.
    
    ![6282](images/6282.png)

# Fulfilling Requests

## Fulfilling a Request

After a request has been approved, ManageIQ then goes through the steps
required to complete the request. The steps followed for a regular
provision from a virtual machine to a virtual machine (not to a
template) are found by navigating to <span class="menuchoice">Automate
\> Explorer</span>, then listed under <span class="menuchoice">DOMAIN \>
Cloud|Infrastructure \> VM \> Provisioning \> VMProvision\_VM \>
Provision VM from Template (template)</span>. The value for each state
shows where the instance resides in the **Datastore** accordion. The
default set of execution steps is shown below. For more information on
state machines, see [State Machines](#state-machines).

## Default Execution Steps in States Instance

| Step                | Description                                                                         |
| ------------------- | ----------------------------------------------------------------------------------- |
| Customize Request   | Apply customizations.                                                               |
| Acquire IP Address  | Integrates with IPAM (IP Address Management) to get an IP Address.                  |
| Acquire MAC Address | Integrates with IPAM to get a MAC Address.                                          |
| Register DNS        | Integrates with IPAM to register with DNS.                                          |
| Register CMDB       | Integrates with CMDB (Configuration Management Database) to register with the CMDB. |
| Register AD         | Integrates with IPAM to register with active directory.                             |
| PreProvision        | Pre-provisioning steps.                                                             |
| Provision           | Create the virtual machine or instance.                                             |
| CheckProvisioned    | Check that the new virtual machine or instance is in the VMDB.                      |
| PostProvision       | Post-provisioning steps.                                                            |
| Register DHCP       | Integrate with IPAM to register the IP address with DHCP Server.                    |
| Activate CMDB       | Integrate with IPAM to activate the virtual machine or instance in the CMDB.        |
| Email owner         | Send email to owner that the virtual machine or instance has been provisioned.      |

### Quotas

Quotas allow you to establish maximum usage thresholds for an user,
group, or tenant for provisioned virtual machines or instances and are
integrated into provisioning profiles. These maximums are checked after
the approval but before the actual provision request is started. The
quota is set for the tenant or group as a whole.

#### Applying User or Group Quotas

1.  Log in as a user with administrator or super administrator rights to
    the ManageIQ console.

2.  Navigate to <span class="menuchoice">Automate \> Explorer</span>.

3.  Copy the <span class="menuchoice">ManageIQ \> System \>
    CommonMethods \> QuotaStateMachine \> quota</span> instance to a
    custom DOMAIN.

4.  From the accordion menu, click <span class="menuchoice">DOMAIN \>
    System \> CommonMethods \> QuotaStateMachine \> quota</span>.
    
    <div class="note">
    
    By default, quotas are applied to tenants and do not require any
    change in <span class="menuchoice">Automate \> Explorer</span>.
    
    </div>

5.  Click ![1847](images/1847.png)(**Configuration**),
    ![1851](images/1851.png)(**Edit this instance**).
    ![6300](images/6300.png)
    
    1.  Set the value for **Quota Source Type** to *user* or *group*.
        
        <div class="important">
        
        A user creating a provisioning request must have an email
        address saved in their profile, or provisioning may fail. See
        [Creating a
        User](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/general_configuration/#creating_a_user)
        in *General Configuration* for details on configuring users.
        
        </div>
    
    2.  Set the values for **VM Warning Count**, **VM Maximum Count**,
        **Storage Warning Limit**, **Storage Maximum Limit**, **CPU
        Warning Count**, **CPU Maximum Count**, **Memory Warning
        Limit**, or **Memory Maximum Limit** to be the maximums for a
        specific user or group.

6.  Click **Save**.

#### Using Tags for Owner and Group Quotas

ManageIQ provides tags for enforcing quotas for the owners of virtual
machines or instances. Ownership of a virtual machine or instance can be
set either during the provisioning process or by using the
**Configuration Set Ownership** button. If a virtual machine or instance
has an owner, the value is displayed in the **Lifecycle** section of the
virtual machine or instance summary page.

Quota tags can be assigned directly to **either** a group or owner
**not** to a configuration item. The table below shows the tags for use
in quotas.

| Category Display Name (Name)            | Use                                                                                                                                                                          |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Quota Max CPU (quota\_max\_cpu)         | Sets the maximum number of CPUs summed over all virtual machines and instances owned by the group or user. Sample Values: 1, 2, 3, 4, 5, 10, 20, 30, 40, 50                  |
| Quota Max Memory (quota\_max\_memory)   | Sets the maximum memory summed over all virtual machines and instances owned by the group or user. Sample Values: 1024, 2048, 4096, 8192, 10240, 20480, 40960, 81920 (in MB) |
| Quota Max Storage (quota\_max\_storage) | Sets the maximum storage summed over virtual machines and instances owned by the group or user. Sample Values: 10, 100, 1000, 20, 200, 40, 400 (in GB)                       |

#### Applying a Tag to a User or User Group

1.  Click ![config gear](images/config-gear.png) (**Configuration**).

2.  Click the **Access Control** accordion, and select the user or group
    that you want to tag.

3.  Click ![1941](images/1941.png)(**Policy**), then click
    ![1851](images/1851.png)(**Edit Tags**).

4.  Select the appropriate customer tag to assign, then the value.

5.  Click **Save**.

<div class="note">

When quotas are applied by both automate instance and tagging, the
tagged values will have higher precedence.

</div>

#### State Machines

The automate state machine processes an ordered list of states. It can
ensure the successful completion of a step before the next step is run,
permit steps to be retried, allow setting a maximum time to retry the
state before exiting, and number of retries before exiting the state.
Before each state is executed, the `On_Entry` method is executed and
after the state ends the `On_Exit` or `On_Error` method is executed
based on how the state ends.

The following components make up a ManageIQ automate state machine:

| Component     | Description                                                                                                                                                                                                     |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| On\_Entry     | Method to run when entering the state. It enables you to execute an automate method to do some pre-processing before the state of the state machine is processed.                                               |
| On\_Exit      | Method to run when exiting the state.                                                                                                                                                                           |
| On\_Error     | Method to run if an error is encountered when running the state. It enables you to execute an automate method to do some final processing before the state machine finally exits (MIQ\_ABORT) due to the error. |
| Default Value | Runs after the On\_Entry method completes (The actual state being processed).                                                                                                                                   |
| Max Retries   | Maximum number of times to retry the state before exiting.                                                                                                                                                      |
| Max Time      | Maximum time in seconds to retry the state before exiting.                                                                                                                                                      |

In the diagram below, you can see how these components combine to create
a state machine workflow.

<div class="note">

The retry logic, `On_Entry` and `On_Error` are distinct cases in the
program flow.

</div>

![2353](images/2353.png)

**Code snippet demonstrating the state machine retry logic:**

    # Get current provisioning status
    task = $evm.root['service_template_provision_task']
    task_status = task['status']
    result = task.status
    
    Then check the result to see how it should proceed:
    
    case result
    when 'error'
      $evm.root['ae_result'] = 'error'
    .....
    when 'retry'
      $evm.root['ae_result'] = 'retry'
      $evm.root['ae_retry_interval'] = '1.minute'
    when 'ok'
      $evm.root['ae_result'] = 'ok'
    end
    
    When the result is "retry", it sets:
      $evm.root['ae_result'] = 'retry'
      $evm.root['ae_retry_interval'] = '1.minute'

The following image shows a simple state machine pertaining to approving
a provision request. This instance can be found in
<span class="menuchoice">Datastore \> ManageIQ \> Infrastructure \> VM
\> Provisioning \> StateMachines \> ProvisioningRequestApproval \>
Default</span>. ![2354](images/2354.png)

1.  The attribute **max\_vms** has a value of 1. State machine
    processing can use the attributes of the state machine instance to
    make logic decisions. In this case, the **validate\_request**
    method, which is processed during the **On\_Entry** portion of the
    **ValidateRequest** state, evaluates the **max\_vms** attribute. If
    the number of virtual machines requested is less than the
    **max\_vms** value, the request can be auto-approved.

2.  **ValidateRequest** is the first state to be executed.

3.  **ApproveRequest** is the next state to be executed.

<div class="note">

Grayed out items reflect values that are set in the class schema. These
values can be overwritten on a per instance basis.

</div>

#### Customizing Provisioning States

The steps followed when provisioning a virtual machine or cloud instance
are completed based on instances from the
<span class="menuchoice">DOMAIN \> Cloud|Infrastructure \> VM \>
Provisioning \> StateMachines \> VMProvision\_VM</span> class. Depending
on your environment you can remove, change, or add steps to the
provisioning process. For example, if you are not integrating with IPAM
or a CMDB, then you can remove those execution steps.
![6281](images/6281.png)

#### Editing the Default State Instance

1.  Navigate to <span class="menuchoice">Automate \> Explorer</span>.

2.  From the accordion menu, click <span class="menuchoice">DOMAIN \>
    Cloud \> VM \> Provisioning \> StateMachines \>
    VMProvision\_VM</span>.
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    This example uses the **Cloud** Namespace, but can also use the
    **Infrastructure** namespace.
    
    </div>

3.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1851](images/1851.png)(**Edit this instance**).
    ![6281](images/6281.png)

4.  For each step that you want to remove, clear the entries in the
    **Value**, **On Entry**, **On Exit**, and **On Error** columns.

5.  Click **Save**.

#### Viewing the Status of a Provisioning Request

After a request has been approved, the various stages of fulfillment are
executed. You can see the progress of the provisioning process by
viewing its status.

1.  Navigate to <span class="menuchoice">Services \> Requests</span>.
    The list of requests is shown.

2.  Click on a specific request for more information. Once the
    provisioning begins, if the request was supposed to create more than
    one virtual machine or instance, a field will appear called
    **Provisioned VMs**. Click on the number that appears next to it for
    information on each of the individual provisions.

#### Viewing a Provisioned Virtual Machine or Instance

When a virtual machine or instance is created as a result of a
provisioning request, its summary screen will show when it was
provisioned in the **Lifecycle** area of the respective summary.

1.  From <span class="menuchoice">Services \> Workloads</span>, click
    the virtual machine or instance that you want to view.
    ![2356](images/2356.png)

#### Viewing a Virtual Machine or Instance Summary

From <span class="menuchoice">Services \> Workloads</span>, click the
virtual machine or instance that you want to view.

# Catalogs and Services

Through the use of catalogs, ManageIQ provides support for multi-tier
service provisioning to deploy layered workloads across hybrid
environments. You can create customized dialogs that will give consumers
of the services the ability to input just a few parameters and provision
the entire service. The following table lists the terminology associated
with catalogs that you will use within the CloudForms user interface for
service provisioning.

| Type                 | Information                                                                                                                                                                                             |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Catalog Bundle       | A group of templates.                                                                                                                                                                                   |
| Catalog Item         | A single template.                                                                                                                                                                                      |
| Template             | A template is a copy of a preconfigured virtual machine, designed to capture the installed software and software configurations, as well as the hardware configuration of the original virtual machine. |
| Dialog Tabs          | Part of a service dialog.                                                                                                                                                                               |
| Element              | An item on a tab in a dialog. It can be a button, check box, drop down list, radio button, tag control, text area box, or a text box.                                                                   |
| Provisioning Dialogs | Dialogs created for host provisioning, virtual machine migration, or virtual machine provisioning. The dialog name must be added to the appropriate provision instance to be processed.                 |
| Service Catalog      | A catalog item or catalog bundle that is available for provisioning.                                                                                                                                    |
| Service Dialogs      | Made up of fully customizable tabs, items, and values for use with service provisioning.                                                                                                                |

Terminology

## Generic Objects

Generic Objects are object-like entities, defined at runtime, that have
unique names and user-defined attributes and relationships. Residing in
the Automate Engine datastore, generic objects are designed to manage
objects other than those related to private infrastructure, and public
or private cloud providers.

Using automate requests, services and catalog items, generic objects can
be directly accessed or passed, during any step, as a parameter to a
service state machine. As a result, generic objects can be used to
quickly add the capability to provision and collect data on resources
not supported by ManageIQ.

### Viewing Generic Objects Classes

View a list of generic objects and click through to see detailed summary
information for each object.

1.  Navigate to <span class="menuchoice">Automate \> Generic
    Objects</span>.

2.  Click on a generic object class in the table to view its summary
    information.

### Creating Generic Objects Classes

Model a new resource by creating a generic object class and adding it to
your ManageIQ inventory. Each generic object class can have attributes,
associations, and methods. Once created, generic object classes are
visible to users of the Self Service user interface at the resource
level.

Create a generic object class using the following steps:

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Generic Objects</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Add a New Generic Object Class](images/1862.png) (**Add a
    New Generic Object Class**).

3.  Provide a **Name** and **Description** for the new object class.

4.  In the **Attributes** field, enter a **Name** and choose a **Type**
    from the drop-down list. Click the ![Add](images/1848.png) button to
    add attributes.

5.  Enter a **Name** and select a **Class** for the object class’s
    **Associations**. Click the ![Add](images/1848.png) button to create
    additional associations.

6.  Provide a **Name** for the **Methods**. Click the
    ![Add](images/1848.png) button to add methods.

7.  Click **Add**.

### Editing Generic Object Classes

Edit existing generic object classes using the following steps:

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Generic Objects</span>.

2.  Click on a generic object class in the list view.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Edit this Generic Object Class](images/1851.png) (**Edit
    this Generic Object Class**).

4.  Make required changes to the generic object class fields.

5.  Click **Save**.

### Removing Generic Objects Classes

Remove generic object classes from your inventory using the following
steps:

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Generic Objects</span>.

2.  Check the generic objects classes from the table to remove.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Remove selected Generic Object Classes from
    Inventory](images/2098.png) (**Remove selected Generic Object
    Classes from Inventory**).

4.  Click **OK** to confirm.

### Exporting Generic Objects

Export generic objects from ManageIQ to create a shared library.

Exporting a generic object requires the object has been created in
ManageIQ.

Procedure

1.  ssh to the ManageIQ appliance as `root`.

2.  Navigate to `/var/www/miq/vmdb`:
    
        # cd /var/www/miq/vmdb

3.  Create a temporary directory to store the generic object
    definitions:
    
        # mkdir tmp/generic_object_definitions

4.  Export the generic object definitions using the following `bin/rake`
    command:
    
        # bin/rake evm:export:generic_object_definitions -- --directory tmp/generic_object_definitions

Locate the exported yaml file containing the generic object properties
in the temporary folder.

### Importing Generic Objects

Import generic objects to ManageIQ from a shared library.

Procedure

1.  ssh to the ManageIQ appliance as `root`.

2.  Navigate to `/var/www/miq/vmdb`:
    
        # cd /var/www/miq/vmdb

3.  Create a temporary directory to store the generic object
    definitions:
    
        # mkdir tmp/generic_object_definitions

4.  Copy the yaml file containing the generic object definitions to the
    temporary folder:
    
        # cp generic_objects.yaml tmp/generic_object_definitions

5.  Import the generic object definitions to the ManageIQ appliance
    using the following `bin/rake` command:
    
        # bin/rake evm:import:generic_object_definitions -- --source tmp/generic_object_definitions

Confirm the generic objects have imported successfully by [Viewing
Generic Objects Classes](#view-generic-objects) in the ManageIQ user
interface.

## Service Dialogs

When provisioning a service, input will be needed from the requester.
Service dialogs are used to take input from the user. This input is
connected to a method in the Automate model that defines how the user’s
input is translated into the provision request. Before creating a
service dialog, be sure to plan what items you need the user to input.

### Adding a Service Dialog

<div class="important">

  - When creating a service dialog for use with Ansible playbook catalog
    items, variable elements must use the prefix **param\_** when
    assigning the value. For example, a new variable labeled **key1**
    should have its value set as **param\_key1**.

  - Using Ansible playbooks to populate dynamic dialog fields is not
    recommended due to delay times caused by the overhead of interaction
    between systems.

  - If you add the playbook automate method to a service dialog, only
    users with admin privileges can run the dialog.

</div>

ManageIQ includes a drag-and-drop service dialog editor to create
service dialogs. The editor, with its drag-and-drop feature, provides a
visual representation of the components that comprise a service dialog.
You can easily design your service dialog utilizing dialog tabs,
sections (previously referred to as boxes), and elements.

When users access a service, the majority of options available to them
are preset and cannot be altered. The requirements for the service
determine the options and fields that need to be present in the dialog
for user input. A service dialog exposes some of those options to the
user so that even if they are ordering a basic Red Hat Enterprise Linux
7 machine, for example, they can at least choose the amount of memory,
virtual CPUs, or other options available to the instance they order. In
cases where certain fields must be unique, such as the name of virtual
machines in Red Hat Virtualization, users must enter their own unique
name for the virtual machine they choose or the operation will fail, so
this field must be exposed.

A service dialog contains three components:

  - One or more **Tabs**.

  - Inside the tabs, one or more **Sections**. Note that in the previous
    method of creating service dialogs using the ManageIQ user
    interface, **Sections** were referred to as **Boxes**.

  - Inside the sections, one or more **Elements**. Elements are controls
    that accept input. Elements contain methods, like check boxes,
    drop-down lists or text fields, to fill in the options on the
    provisioning dialog.

<div class="important">

The names of the elements must correspond to the options used in the
provisioning dialog.

</div>

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  Click the **Service Dialogs** accordion.

3.  Click ![1847](images/1847.png)(**Configuration**), and then
    ![1862](images/1862.png)(**Add a new Dialog**).
    
    ![edit section1](images/edit-section1.png)

4.  Enter basic details under **General**:
    
    1.  Enter the **Dialog’s name** and **Dialog’s description**.

5.  Add a new tab to the dialog:
    
    1.  Click ![1862](images/1862.png)**Create Tab**. Then, click the
        ![pencil](images/1851.png)icon on the new tab to edit tab
        information.
    
    2.  Enter a **Label**.
    
    3.  Optional: Enter a description for the tab in **Description**.
    
    4.  Click **Save**.

6.  Add a new section to the tab:
    
    1.  Click ![1862](images/1862.png)**Add Section**. Then, click the
        ![pencil](images/1851.png)icon on the upper-right to edit
        section details.
    
    2.  Enter a **Label**.
    
    3.  Optional: Enter a description for the section in
        **Description**.
    
    4.  Click **Save**.

7.  Add elements to the section:
    
    1.  From the list of elements on the left, click an element you want
        to add, then drag-and-drop it inside the section. Then, click
        the ![pencil](images/1851.png)icon next to the element to edit
        its field details.
        
        | Element Types | Additional Info                                                                                                                                                                                                                                                                |
        | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
        | Text Area     | Provides text area for users to enter text. You can enter the default text in **Default Value**, or leave it as blank.                                                                                                                                                         |
        | Text Box      | Text box is similar to a text area with the added option to enable **Protected** so the text is shown as asterisks(\*), instead of plain text.                                                                                                                                 |
        | Check Box     | Enable **Default Value** if you want the box checked by default.                                                                                                                                                                                                               |
        | Drop Down     | Use drop down to create list entries either manually or using automate methods. Enable **Dynamic** to create lists using automate methods; use **Entry Point** to select an automate instance. Enable **Show Refresh Button** to allow users to refresh list options manually. |
        | Radio Button  | Similar to a drop down but displays options using radio buttons.                                                                                                                                                                                                               |
        | Datepicker    | Use this to enable users to pick a date by clicking the calendar icon.                                                                                                                                                                                                         |
        | Timepicker    | use this to enable users to pick a date and time.                                                                                                                                                                                                                              |
        | Tag Control   | Select a **Category** of tags you want assigned to virtual machines associated with the service dialog. Enable **Single Select** if only one tag can be selected.                                                                                                              |
        

    2.  Enter a **Label**, **Name**, and **Description** for the
        element.
        
        <div class="important">
        
        Element names must correspond to the options used in the
        provisioning dialog. **Name** must use only alphanumeric
        characters and underscores without spaces. It is also used to
        retrieve the value of this element in the method used with the
        dialog and must start with **dialog\_service\_type**.
        
        </div>
    
    3.  Optional: Add additional information in **Help** to assist the
        user to complete the fields in the service dialog. This field is
        useful for explaining unfamiliar terminology or providing
        configuration tips. This information is presented when you hover
        over the \[\!\] exclamation mark in the Service Dialog while
        ordering a Service Catalog later.
    
    4.  Set other options as required.
    
    5.  Click **Save**.

8.  Optional: Repeat the above step to add more elements to the existing
    section, or create and add elements to a new section as required.

9.  Optional: Repeat the step to add a new tab to the dialog, and
    subsequent steps to add sections and elements to it as required.

10. Click **Save** to create the dialog.

The service dialog is now created, and added to the **Service Dialogs**
accordion.

### Creating a Service Dialog from a Container Template

Complete the following procedure to create a Service Dialog from a
Container Template.

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Container Templates</span> and select the template for provisioning.

2.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Create Service Dialog from Container
    Template**).

3.  Enter a name for the dialog in **Service Dialog Name**.

4.  Click **Save**.

You can use this service dialog when creating a catalog item for
container template provisioning; see [Creating an OpenShift Template
Catalog Item](#create-container-template-catalog-item).

### Importing Service Dialogs

You can share service dialogs between appliances using the export and
import features.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  In the **Import/Export** accordion, click **Service Dialog
    Import/Export**.

3.  In the **Import** area, click **Browse** to select an import file.

4.  Click **Upload**.

### Exporting Service Dialogs

You can share service dialogs between appliances using the export and
import features.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  In the **Import/Export** accordion, click **Service Dialog
    Import/Export**.

3.  In the **Export** area, select the service dialogs that you want to
    export.

4.  Click **Export**.

## Methods

### Creating a Method to Associate with the Dialog

You will need to create a method that connects the values in the dialog
with the provisioning request. The method should be created in the
`DOMAIN/Service/Provisioning/StateMachines/ServiceProvision_Template`
class of the **Automate** model.

<div class="note">

**DOMAIN** must be a user-defined Domain and not the locked ManageIQ
Domain. If necessary, you can copy the class from the ManageIQ domain
into a custom domain.

</div>

A method is provided below that was created for the following scenario:

  - You want to provision a three-tiered service that contains catalog
    items of web, app and DB. Each of these virtual machines (or cloud
    instances) has been tagged under the **Service** category with the
    appropriate value. Then, added as a catalog item and combined into a
    catalog bundle.

  - The **Service Dialog** captures the selection of small, medium or
    large application in a dropdown called **service\_type**. When
    referring to a value captured in an element in a dialog, the name of
    the element should be prefixed with **dialog\_**. For example,
    **service\_type** becomes **dialog\_service\_type** when used in the
    method.

  - The method will set the memory sizes for each of the catalog items
    based on the **service\_type** selection.

<!-- end list -->

    #            Automate Method
    #
    $evm.log("info", "Automate Method ConfigureChildDialog Started")
    #
    #            Method Code Goes here
    #
    $evm.log("info", "===========================================")
    $evm.log("info", "Listing ROOT Attributes:")
    $evm.root.attributes.sort.each { |k, v| $evm.log("info", "\t#{k}: #{v}")}
    $evm.log("info", "===========================================")
    
    stp_task = $evm.root["service_template_provision_task"]
    $evm.log("info", "===========================================")
    $evm.log("info", "Listing task Attributes:")
    stp_task.attributes.sort.each { |k, v| $evm.log("info", "\t#{k}: #{v}")}
    $evm.log("info", "===========================================")
    
    #############################################################
    #### This is how the method would look for dialog variables
    #############################################################
    dialog_service_type = $evm.root['dialog_service_type']
    $evm.log("info","User selected Dialog option = [#{dialog_service_type}]")
    
    stp_miq_request_task = stp_task.miq_request_task
    #$evm.log("info","(parent) miq_request_task:  = [#{stp_miq_request_task}]")
    
    #############################################################
    #### This is how you get the catalog items for the catalog bundle
    #############################################################
    
    stp_miq_request_tasks = stp_task.miq_request_tasks
    #$evm.log("info","(children) miq_request_tasks count:  = [#{stp_miq_request_tasks.count}]")
    
    #############################################################
    #### By going through the children, you can set the dialog variable for each of the children (we based our values on the childrens service tags)
    #############################################################
    
    stp_miq_request_tasks.each do |t|
    
      $evm.log("info"," Setting dialog for: #{t.description}")
      service = t.source
      service_resource = t.service_resource
      #$evm.log("info"," Child service resource name: #{service_resource.resource_name}")
      #$evm.log("info"," Child service resource description: #{service_resource.resource_description}")
    
      service_tag_array = service.tags(:app_tier)
      service_tag = service_tag_array.first.to_s
    
      memory_size = nil
    
    #############################################################
    #### The dialog_service_type is the attribute set on the service dialog
    #### We use the service_tag to decide what child gets what dialog
    #############################################################
    
      case dialog_service_type
      when "Small"
        case service_tag
        when "app"
          memory_size = 1024
        when "web"
          memory_size = 1024
        when "db"
          memory_size = 4096
        else
          $evm.log("info","Unknown Dialog type")
        end
      when "Large"
        case service_tag
        when "app"
          memory_size = 4096
        when "web"
          memory_size = 4096
        when "db"
          memory_size = 8192
        else
          $evm.log("info","Unknown Dialog type")
        end
      else
        $evm.log("info","Unknown Dialog type - setting Dialog options here")
      end
    
    #############################################################
    #### set_dialog_option sets the dialog for the child
    #############################################################
    
      t.set_dialog_option('memory',memory_size) unless memory_size.nil?
      $evm.log("info","Set dialog for selection: [#{dialog_service_type}]  Service_Tier: [#{service_tag}] Memory size: [#{memory_size}]")
    
    end
    #
    #
    #
    $evm.log("info", "Automate Method ConfigureChildDialog Ended")
    exit MIQ_OK

### Creating a Method in the Service Class

Service methods have been split based on purpose.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>.

2.  Service Class is located at <span class="menuchoice">DOMAIN \>
    Service \> Provisioning \> StateMachines \> Methods</span> and
    <span class="menuchoice">Domain \> Service \> Retirement \>
    StateMachines \> Methods</span>.
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>

3.  Click the **Methods** tab.

4.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a New Method**).

5.  Enter a **Name** and **Display Name**.

6.  In the **Data** field, enter the method contents.

7.  Click **Validate** and wait for your data entry to be successfully
    validated.

8.  Click **Add**. ![6297](images/6297.png)

### Creating an Instance in the Service Class

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>.

2.  Service Class is located at <span class="menuchoice">DOMAIN \>
    Service \> Provisioning \> StateMachines \> Methods</span> and
    <span class="menuchoice">Domain \> Service \> Retirement \>
    StateMachines \> Methods</span>.
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>

3.  Click the **Instances** tab.

4.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a new Instance**).

5.  Enter a **Name** and **Display Name**.

6.  In the **Fields** area, enter the method’s name in **Value**.

7.  Click **Add**.

The instance is created so that it can be called from the
**ServiceProvision** class.

![6298](images/6298.png)

<div class="note">

After the method has been created, it must be mapped to an instance in
the `DOMAIN/Service/Service/Provisioning/StateMachines` class. The name
of the instance must be specified as the **Entry Point**. This method
must be called before the provision job begins.

</div>

### Associating a Method with an Automate Instance

Service methods have been split based on purpose.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>.

2.  From the accordion menu, click the required service method.

3.  Service Class is located at <span class="menuchoice">DOMAIN \>
    Service \> Provisioning \> StateMachines \> Methods</span> and
    <span class="menuchoice">Domain \> Service \> Retirement \>
    StateMachines \> Methods</span>.
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>

4.  Either create a new instance or select the **clone\_to\_service**
    instance.

5.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1851](images/1851.png)(**Edit Selected Instance**).

6.  In the **configurechilddialog** value, put the path to the method.

7.  Click **Save** or **Add** if you are adding this to a new instance.

## Catalogs

Catalogs are used to create groups of virtual machines or instances for
provisioning. For example, a complete package of a database server,
desktop with specialized software already on it, and a firewall. You
will need to complete the following steps to create and provision a
service catalog.

1.  Create **Catalog Items** for each virtual machine or instance that
    will be part of the service.

2.  Create a **Service** dialog. For example, create a dropdown with
    three options small, medium, and large.

3.  Create a method for the Service Dialog. This method defines what
    each of the options means to each of the individual virtual machines
    or cloud instances for the service. This method is called from a
    service provisioning instance in the Automate model.

4.  Create an instance in the
    `DOMAIN/Service/Provisioning/StateMachines/ServiceProvision_Template`
    class that calls the method.
    
    <div class="note">
    
    DOMAIN must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>

5.  Associate method with Automate instance.

6.  Create a **Catalog Bundle**, adding each of the catalog items to it.
    Select the **Service Dialog** you created. Use the instance created
    in the
    `DOMAIN/Service/Provisioning/StateMachines/ServiceProvision_Template`
    class as the **Entry Point**. Check **Display in Catalog** box.

7.  Provision a service.

### Creating a Catalog Bundle

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  Click the **Catalog Items** accordion.

3.  Click ![1847](images/1847.png)(**Configuration**), and then
    ![1862](images/1862.png)(**Add a New Catalog Bundle**).

4.  Enter a name and description for the bundle. Select **Display in
    Catalog**.

5.  Select the required **Catalog**.

6.  Select the required **Dialog**.

7.  Select chargeback currency.

8.  Enter **Price / Month**.

9.  Select the provisioning and retirement entry points.

10. Select **Additional Tenants**.

11. Click on the **Resources** tab, then select the catalog item you
    want to add to the bundle from the **Add a Resource** dropdown.

12. Click **Add**.

A catalog bundle is created and visible in the **Service Catalog**
accordion.

<div class="note">

You should also create and specify an Entry Point in the
`DOMAIN/Service/Provisioning/StateMachines/Methods/CatalogBundle` class
for each catalog item that is part of a bundle. If you do not, then the
pre and post provision processing will occur for each item in the bundle
in addition to processing for the **Catalog Bundle**. To set the entry
point, go into each **Catalog Item** and check **Display in Catalog**.
Then, you will see the **Entry Point** field.

</div>

### Copying a Catalog Bundle

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  Click the **Catalog Items** accordion.

3.  Select the catalog bundle you want to copy from **All Catalog
    Items**.

4.  Click ![1847](images/1847.png)(**Configuration**), and then
    ![Edit\_Sign](images/1851.png)(**Copy Selected Item**).

5.  Enter a name for the copy of catalog bundle you are creating. Note
    that this name must not already be in use.

6.  Click **Add**.

A copy of the catalog bundle is saved. You can now select this new copy
of the catalog bundle and edit as required by navigating to
![1847](images/1847.png)(**Configuration**), then clicking
![Edit\_Sign](images/1851.png)(**Edit this Item**).

### Creating a Catalog Item

Create a catalog item for each virtual machine or cloud instance that
will be part of the service.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  Click the **Catalog Items** accordion.

3.  Click ![1847](images/1847.png)(**Configuration**), and then
    ![1862](images/1862.png)(**Add a New Catalog Item**).

4.  Select the **Catalog Item Type** you are adding. This list only
    shows items related to providers available or options activated in
    the appliance (for example, **Ansible Playbook** is available as a
    **Catalog Item Type** option if the Embedded Ansible server role is
    enabled on the appliance).

5.  Enter a name and description for the bundle. Select **Display in
    Catalog**.

6.  Select a **Catalog**.

7.  Select a **Dialog**.
    
    <div class="note">
    
    You can only choose from the catalogs and dialogs you have already
    created. If you haven’t done so, leave the values blank and edit
    later.
    
    </div>

8.  Select a **Zone**.

9.  Select the chargeback currency.

10. Enter **Price / Month**.

11. Select the catalog item’s **Subtype**.

12. Select the provisioning and retirement entry points, that is the
    Automate instance to run upon provisioning and retirement.
    
    <div class="note">
    
    The entry point must be a State Machine since the **Provisioning
    Entry Point** list is filtered to only show State Machine class
    instances. No other entry points will be available from the
    **Provisioning Entry Point** field.
    
    </div>

13. Select **Additional Tenants**.

14. Click **Add**.

### Copying a Catalog Item

<div class="note">

When copying a catalog item for reuse, you must click **Display in
Catalog** in the copied catalog item for the item to appear in the
catalog.

</div>

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  Click the **Catalog Items** accordion.

3.  Select the catalog item you want to copy from **All Catalog Items**.

4.  Click ![1847](images/1847.png)(**Configuration**), and then
    ![Edit\_Sign](images/1851.png)(**Copy Selected Item**).

5.  Enter a name for the copy of catalog item you are creating. Note
    that this name must not already be in use.

6.  Click **Add**.

A copy of the catalog item is saved. You can now select this new copy of
the catalog item and edit as required by navigating to
![1847](images/1847.png)(**Configuration**), then clicking
![Edit\_Sign](images/1851.png)(**Edit this Item**).

### Creating a Generic Catalog Item

Create generic catalog items for services non-specific to virtualization
or cloud environments. This catalog item type can serve a wide array of
needs, from creating a vLAN across a network to accessing virtual
machine IP addresses and adding them to a load balancer pool.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  Click the **Catalog Items** accordion.

3.  Click ![1847](images/1847.png)(**Configuration**), and then
    ![1862](images/1862.png)(**Add a New Catalog Item**).

4.  Select **Generic** from the Catalog Item Type list.

5.  In the **Basic Info** subtab:
    
    1.  Type a **Name/Description**.
    
    2.  Check **Display in Catalog** to display the item in the catalog.
        A **Dialog** will be required if you select **Display in
        Catalog**.
    
    3.  Choose a **Catalog** to which to add the new item.
    
    4.  Select a **Dialog** from the available options.
    
    5.  Choose a **Subtype** from the list menu.
    
    6.  Add **Entry Point(NS/Cls/Inst)** options.
        
        1.  **Provisioning Entry Point (Domain/NS/Cls/Inst)** requires
            you to select an Automate instance to run upon provisioning.
        
        2.  **Retirement Entry Point (Domain/NS/Cls/Inst)** requires you
            to select an Automate instance to run upon retirement.
            
            <div class="note">
            
            The entry point must be a State Machine since the
            **Provisioning Entry Point** list is filtered to only show
            State Machine class instances. No other entry points will be
            available from the **Provisioning Entry Point** field.
            
            </div>

6.  In the **Details** subtab, write a **Long Description** for the
    catalog item.

7.  Click **Add**.

### Creating an Ansible Playbook Service Catalog Item

Create a catalog item that uses an Ansible Playbook to back it.

<div class="note">

  - Before creating an Ansible service, at least one repository, one
    playbook, and one credential must exist in the ManageIQ inventory.
    Check your inventory and add the appropriate resources before
    creating an Ansible service. For more information, see [Automation
    Management
    Providers](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.5/html-single/managing_providers/#automation_management_providers)
    in *Managing Providers*.

  - Debugging verbosity is available for Ansible playbook catalog items.
    Selecting a higher verbosity value provides more detailed output as
    the playbook executes. **0 (Normal)** is the default value. **1
    (Verbose)** will yield return data while a value of **3 (Debug)**
    provides connection attempt and task invocation details. Higher
    levels, such as **4 (Connection)** can be useful for debugging SSH
    connections. Use **5 (WinRM Debug)** when debugging WinRM
    connections.

  - Using Ansible playbooks to populate dynamic dialog fields is not
    recommended due to delay times caused by the overhead of interaction
    between systems.

  - Only users with administrator privileges can run a service dialog
    based on a playbook.

</div>

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  In the **Catalog Items** accordion, click on the **All Catalog
    Items**.

3.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a New Catalog Item**).

4.  Select **Ansible Playbook** from the **Catalog Item Type** drop-down
    list.

5.  Type a **Name** and **Description** for the new service catalog
    item.

6.  Click **Display in Catalog**.

7.  Select the appropriate **Catalog** from the drop-down list.

8.  In the **Provisioning** tab, set parameters for your catalog item to
    use by configuring a Playbook to back your service item:
    
    1.  Choose a **Repository** from the drop-down list.
    
    2.  Select the **Ansible Playbook** to use.
    
    3.  Assign the appropriate **Machine Credentials** from the
        drop-down list.
    
    4.  Add **Cloud** or **Network Credentials** from the drop-down
        lists.
    
    5.  Choose the **Host** against which to run the service item.
    
    6.  Set the **Max TTL** in minutes. The Time To Live (TTL) field
        allows you to set the maximum execution time for the playbook to
        run.
    
    7.  Use the **Escalate Privilege** toggle switch to enable user
        privilege escalation if called for in credentials during the
        playbook run.
    
    8.  Choose a **Verbosity** value to set the debug level for playbook
        execution.
    
    9.  Add key value pairs for **Variables** and their corresponding
        **Default Values**.
    
    10. In the **Dialog** options, choose an existing dialog from the
        **Use Existing** drop-down list or select **Create New** to add
        a new dialog.

9.  In the **Retirement** tab, set parameters for your catalog item to
    use by selecting values for the following:
    
    1.  Choose a **Repository** from the drop-down list.
    
    2.  Select the **Ansible Playbook** to use.
    
    3.  Assign the appropriate **Machine Credentials** from the
        drop-down list.
    
    4.  Add **Cloud** or **Network Credentials** from the drop-down
        lists.
    
    5.  Choose the **Host** against which to run the service item.
    
    6.  Set the **Max TTL** in minutes. The Time To Live (TTL) field
        allows you to set the maximum execution time for the playbook to
        run.
    
    7.  Use the **Escalate Privilege** toggle switch to enable user
        privilege escalation if called for in credentials during the
        playbook run.
    
    8.  Choose a **Verbosity** value to set the debug level for playbook
        execution.
    
    9.  Add key value pairs for **Variables** and their corresponding
        **Default Values**.
    
    10. In the **Dialog** options, choose an existing dialog from the
        **Use Existing** drop-down list or select **Create New** to add
        a new dialog.

10. Click **Add**.

### Creating an Ansible Tower Service Catalog Item

Create a service catalog item from an Ansible Tower template you can use
to execute an Ansible Tower playbook in ManageIQ.

<div class="important">

You must first create the job or workflow template in Ansible Tower. The
job or workflow templates are automatically discovered by ManageIQ when
refreshing your Ansible Tower provider’s inventory.

</div>

First, create a catalog:

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Add a New Catalog](images/1862.png) (**Add a New Catalog**)

3.  Enter a **Name** and **Description** for the catalog.

4.  Click **Add**.

Then, create an Ansible Tower service catalog item:

1.  Navigate to <span class="menuchoice">Automation \> Ansible Tower \>
    Explorer</span>, then click on the **Templates** accordion menu.

2.  Click **Ansible Tower Templates** and select an Ansible Tower job or
    workflow template.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Create Service Dialog from Template](images/1862.png) (**Create
    Service Dialog from this Template**).

4.  Enter a **Service Dialog Name** (for example,
    *ansible\_tower\_job*)and click **Save**.

5.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.
    Click **Catalog Items**.

6.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Add a New Catalog Item](images/1862.png) (**Add a New Catalog
    Item**) to create a new catalog item with the following details, at
    minimum:
    
      - For **Catalog Item type**, select **Ansible Tower**.
    
      - Enter a **Name** for the service catalog item.
    
      - Select **Display in Catalog**.
    
      - In **Catalog**, select the catalog you created previously.
    
      - In **Dialog**, select the service dialog you created previously
        (in this example, *ansible\_tower\_job*). To ask the user to
        enter extra information when running the task, **Service
        Dialog** must be selected. A dialog is required if **Display in
        Catalog** is chosen.
    
      - In **Provider**, select your Ansible Tower provider. This brings
        up the **Ansible Tower Template** option and configures the
        **Provisioning Entry Point State Machine** automatically.
    
      - Add configuration information for **Reconfigure Entry Point**
        and **Retirement Entry Point** as applicable.
    
      - Select your desired **Ansible Tower Template** from the list.
        Generally, this is the Ansible Tower job or workflow template
        previously used to create the service dialog.

7.  Click **Add**. The catalog item you created will appear in the **All
    Service Catalog Items** list.

### Creating an Amazon Service Catalog Item

Use the following procedure to create an Amazon catalog item. Once
created, the catalog item and service dialog combine with all of the
options in the provisioning dialog. Users can then order Red Hat
Enterprise Linux instances from the **Service Catalog** in the ManageIQ
Service user interface.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>,
    then click on the **Catalog Items** accordion.

2.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a New Catalog Item**).

3.  Select **Amazon** from the **Catalog Item Type** list.

4.  Enter the basic details in the **Basic Info** tab:
    
    1.  Enter a **Name** and **Description** for the new service catalog
        item.
    
    2.  Select **Display in Catalog**.
    
    3.  Select the appropriate catalog from the **Catalog** list.
    
    4.  Select the appropriate service dialog from the **Dialog** list.

5.  Click the **Request Info** tab to enter request details:
    
    1.  On the **Catalog** tab, select your Amazon AWS image name from
        the **Name** list, and the number of instances from the
        **Count** list. The **VM Name** will be overwritten during the
        provisioning process, but you can enter it as *changeme* for
        now.
    
    2.  On the **Properties** tab, select *T2 Micro* from the **Instance
        Type** list, and *Basic* or *Advanced* for **CloudWatch**. If
        you plan to access the instance, select a **Guest Access Key
        Pair**, too.
    
    3.  On the **Customize** tab, set the **Root Password** under
        **Credentials**, then select the *Basic root pass template* as a
        script for cloud-init under **Customize Template**.

6.  Click **Add**.

### Creating an Azure Service Catalog Item

Use the following procedure to create an Azure catalog item.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>,
    then click on the **Catalog Items** accordion.

2.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a New Catalog Item**).

3.  Select **Azure** from the **Catalog Item Type** list.

4.  Enter the basic details in the **Basic Info** tab:
    
    1.  Enter a **Name** and **Description** for the new service catalog
        item.
    
    2.  Select **Display in Catalog**.
    
    3.  Select the appropriate catalog from the **Catalog** list.
    
    4.  Select the appropriate service dialog from the **Dialog** list.

5.  Click the **Request Info** tab to enter request details:
    
    1.  On the **Catalog** tab, select your Azure image name from the
        **Name** list, and the number of instances from the **Count**
        list. The **VM Name** will be overwritten during the
        provisioning process, but you can enter it as *changeme* for
        now.
    
    2.  Select appropriate **Environment** settings that are known to
        work for your Azure environment.
    
    3.  On the **Customize** tab, set the **Username** and **Password**
        under **Credentials**, then select the appropriate script under
        **Customize Template**.

6.  Click **Add**.

### Creating an OpenShift Template Catalog Item

<div class="note">

Before adding a new catalog item for container template provisioning,
create a service dialog from a container template. See [Creating a
Service Dialog from a Container
Template](#creating-a-service-dialog-from-container-template) for
details.

</div>

Complete the following procedure to create an OpenShift Template catalog
item.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>,
    then click on the **Catalog Items** accordion.

2.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a New Catalog Item**).

3.  Select **OpenShift Template** from the **Catalog Item Type** list.

4.  Enter a **Name** and **Description** for the new service catalog
    item. Select **Display in Catalog**.

5.  Select the appropriate catalog from the **Catalog** list.

6.  From the **Dialog list**, select the service dialog you have created
    from a container template.

7.  Select your provider from the **Provider** list.

8.  Set the **Provisioning Entry Point**.

9.  Click **Add**.

### Creating an Orchestration Catalog Item

Use the following procedure to create an Orchestration catalog item.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span> and
    select **Catalog Items** in the accordion menu.

2.  Click ![Configuration](images/1847.png) **Configuration**, then
    click ![Green\_Plus\_Sign](images/1848.png) **Add a New Catalog
    Item**. The **Adding a new Service Catalog Item** window is
    displayed.

3.  Select **Orchestration** from the **Catalog Item Type** list.

4.  Enter the basic details in the **Basic Info**:
    
    1.  Enter a **Name** and **Description** for the new service catalog
        item.
    
    2.  Select **Display in Catalog** box.
    
    3.  Select the appropriate catalog from the **Catalog** list.
    
    4.  Select the appropriate dialog from the **Dialog** list.
    
    5.  Select the **Orchestration Template** from the list.

5.  Click **Add**.

### Provisioning a Service

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span>.

2.  Click the **Service Catalogs** accordion, and select the service to
    provision.

3.  Click **Order**.

The parameters are passed to the children based on the method tied to
the choices made in the dialog.

## Orchestration Stacks

Cloud orchestration is a service that allows you to create, update, and
manage cloud resources and their software components as a single unit
and then deploy them in an automated, repeatable way through a template.
Templates use a human-readable syntax and can be defined in text files,
thereby allowing users to check them into version control. Templates
allow you to easily deploy and reconfigure infrastructure for
applications within your cloud. A user can author the stack templates,
or can upload them from other sources.

ManageIQ supports adding Amazon CloudFormation, OpenStack Heat,
Microsoft Azure, VNF, and VMware vApp template type, and provides the
ability to:

  - Inventory stacks and elements of each type into the ManageIQ VMDB.

  - Model the relationships of instances to their stacks, inclusive of
    the user interface. For example, selecting an instance within a
    region that is within a stack, the user interface shows this on the
    standard instance view.

  - Model the stack and its elements in the user interface.

<div class="note">

When importing a template into ManageIQ, the selected elements are
converted according to their type. For example, lists convert to list
boxes, and single items convert to text boxes.

</div>

### Creating an Orchestration Template

Complete the following procedure to add an orchestration template.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span> and
    select **Orchestration Templates** in the accordion menu.

2.  Click ![Configuration](images/1847.png)**Configuration**, then click
    ![Green\_Plus\_Sign](images/1848.png)**Create a new Orchestration
    Template**.

3.  Enter a **Name** and **Description** for your template.

4.  Select the template type from the **Template Type** list. The
    default is Amazon CloudFormation.

5.  Select **Draft** to create a draft template.

6.  Add your template in the area below for the selected **Template
    Type**.

7.  Click **Add**.

### Editing Orchestration Templates

Complete the following procedure to edit orchestration templates.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span> and
    select **Orchestration Templates** in the accordion menu.

2.  Select the orchestration template you want to edit from the **All
    Orchestration Templates** list.

3.  Click ![Configuration](images/1847.png)**Configuration**, then click
    ![Edit\_Sign](images/1851.png)**Edit this Orchestration Template**.

4.  Edit the template as needed.
    
    <div class="note">
    
    You can only edit the name and description of a read-only template
    as there can be stacks associated with the template.
    
    </div>

5.  Click **Save**.

### Copying Orchestration Templates

Complete the following procedure to copy an orchestration template to
create a new template.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span> and
    select **Orchestration Templates** in the accordion menu.

2.  Click ![Configuration](images/1847.png)**Configuration**, then click
    ![Copy](images/1859.png) **Copy this Orchestration Template**.

3.  Change the **Description** and the actual content of the template as
    required. ManageIQ automatically prefixes *Copy of* to the old
    template **Name**.
    
    <div class="note">
    
    To create a copy of an orchestration template into a new template,
    the old and new template content must differ.
    
    </div>

4.  Click **Add**.

### Deleting Orchestration Templates

Complete the following procedure to delete orchestration templates.

1.  Navigate to <span class="menuchoice">Services \> Catalogs</span> and
    select **Orchestration Templates** in the accordion menu.

2.  Select the orchestration template you want to delete from the **All
    Orchestration Templates** list.

3.  Click ![Configuration](images/1848.png)**Configuration**, then click
    ![Delete](images/1861.png)**Remove this Orchestration Template from
    Inventory**.

4.  Click **OK**.

<div class="note">

Read-only templates cannot be deleted.

</div>

# Retirement

## Retiring Virtual Machines

### Retiring Virtual Machines and Instances

When a virtual machine or instance is no longer required, it can be
retired. Once a virtual machine or instance reaches its retirement date,
it is immediately shut down and not allowed to restart. If an attempt to
restart is made, ManageIQ will shut down the virtual machine or
instance.

There are three built-in policies involved with retirement:

  - If the virtual machine or instance reaches its retirement date, it
    will be stopped even if it is running.

  - If a retired virtual machine or instance is requested to start
    through ManageIQ, the virtual machine or instance will not be
    allowed to start.

  - If a provider starts a retired virtual machine or instance outside
    of ManageIQ, the virtual machine or instance will be stopped.

ManageIQ provides a number of ways to retire a virtual machine or
instance:

  - By using the allocated buttons in the ManageIQ console.

  - When creating a provision request, a retirement date can be set up.

### Using the Console to Retire a Virtual Machine

Through the ManageIQ console, you can retire a virtual machine on a
specific date or immediately.

### Retiring a Virtual Machine Immediately

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the virtual machine or instance that you want to retire.

3.  Click ![2007](images/2007.png)(**Lifecycle**), then
    ![2010](images/2010.png)(**Retire this VM/Instance**).

The virtual machine or instance is immediately stopped, and will be shut
down if an attempt is made to restart it.

### Setting a Retirement Date and Time for a Virtual Machine or Instance

You can schedule virtual machine retirement by specifying a date and
time, or by selecting a relative time a number of months, weeks, days or
hours ahead of the present time.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the virtual machine or instance that you want to set a
    retirement date for.

3.  Click ![2007](images/2007.png)(**Lifecycle**), then
    ![2010](images/2010.png)(**Set Retirement Dates**).

4.  From **Enter Retirement Date as**, select **Specific Date and Time**
    or **Time Delay from Now** to schedule retirement.
    
    1.  To choose a **Specific Date and Time**, click the **Retirement
        Date and Time** field to open the calendar.
        
        1.  Select a retirement date using the calendar control.
        
        2.  Click ![clock](images/clock.png) then select a retirement
            time (in UTC) using the arrows.
    
    2.  To retire the virtual machine using a relative time, select
        **Time Delay from Now**.
        
        1.  From **Time Delay**, specify a retirement time any number of
            months, weeks, days, or hours in the future using the
            arrows.

5.  Select a **Retirement Warning** if desired.

6.  Click **Save**.

The scheduled retirement date and time display in the virtual machine
summary screen.

### Removing a Retirement Date for a Virtual Machine or Instance

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the virtual machine or instance that you want to remove the
    retirement date from.

3.  Click ![2007](images/2007.png)(**Lifecycle**), then click
    ![2010](images/2010.png)(**Set Retirement Date**).

4.  Click ![remove retirement date](images/remove-retirement-date.png)
    to remove the retirement date.

## Setting Retirement in a Provision Request

If you are using ManageIQ to provision, you can set when you want
retirement in the provision request. To see how to create a request, see
[Provisioning Requests](#provisioning-requests). A warning email will be
sent to the owner before the retirement.

### Scheduling Retirement in a Provision Request

When provisioning a cloud instance or virtual machine, a multi-tabbed
screen appears where you can set up your provision requests.

1.  Click the **Schedule** tab to set when to provision your request and
    the lifespan of the virtual machine or instance.

2.  In **Lifespan**, you can choose to power on the virtual machines or
    instances after creation and set the **Time until Retirement**. If
    you select the time until retirement, you will select **Retirement
    Warning** accordingly.

3.  Click **Submit**.
    
    ![vm instance retirement](images/vm-instance-retirement.png)

## Extending Retirement Dates

ManageIQ **Automate** includes a method to extend the retirement of a
virtual machine or instance by 14 days. This section describes how to
create a button that invokes this method and how to edit the method to
change the number of days.

### Creating a Custom Button to Extend Retirement

1.  Navigate to <span class="menuchoice">Automate \>
    Customization</span>.

2.  Click the **Buttons** accordion.

3.  From the **Object Types** tree, select **VM and Instance**.

4.  Navigate to the button group to which you want to add this button.
    (If you do not have a button group, add one and then create the
    button.)

5.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1862](images/1862.png)(**Add a new Button**).

6.  Type in a button text and button hover text, and select the image
    you want to use.

7.  In **Object Details**, select **Request** from the
    **/System/Process/** dropdown. By default, the message is `create`.
    Do not change it.

8.  In **Request**, type `vm_retire_extend`.

9.  Click **Add**.

### Changing the Number of Days to Extend Retirement

1.  Navigate to <span class="menuchoice">Automate \> Explorer</span>.

2.  Click <span class="menuchoice">DOMAIN \> Cloud \> VM \> Retirement
    \> Email \> vm\_retire\_extend</span>.
    
    <div class="note">
    
    DOMAIN must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    This example uses the **Cloud** Namespace, but you can also use the
    **Infrastructure** namespace.
    
    </div>

3.  Click ![1847](images/1847.png)(**Configuration**), then
    ![1851](images/1851.png)(**Edit this Instance**).

4.  In the Value field, change the **vm\_retire\_extend\_days**
    attribute to the new value.

5.  Click **Save**. ![6299](images/6299.png)
