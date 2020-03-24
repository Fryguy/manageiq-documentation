# Installing ManageIQ

Installing ManageIQ consists of the following steps:

1.  Downloading the appliance for your environment as a virtual machine
    image template.

2.  Setting up a virtual machine based on the appliance.

3.  Configuring the ManageIQ appliance.

After you have completed all the procedures in this guide, you will have
a working environment on which additional customizations and
configurations can be performed.

## Obtaining the ManageIQ Virtual Appliance

1.  In a browser, navigate to
    [manageiq.org/download](manageiq.org/download).

2.  Select **Microsoft Azure** from the **--Choose your platform--**
    list.

3.  Select **Stable** from the **--Choose a release--** list.

4.  Follow the instructions to download the appliance.

## Uploading and Provisioning the ManageIQ Virtual Appliance in Microsoft Azure

You can upload and provision the appliance in an Azure environment using
the following two methods:

  - Using the Azure PowerShell script

  - Using the Azure Command-Line Interface (Azure CLI)

To upload the ManageIQ appliance file in Microsoft Azure, ensure the
following requirements are met:

  - Approximately 2 GB of space for each VHD image; 44+ GB of space, 12
    GB RAM, and 4 VCPUs for the ManageIQ appliance.

  - [Microsoft Azure Account](https://azure.microsoft.com/en-us/free/).

  - Administrator access to the Azure portal.

  - Depending on your infrastructure, allow time for the upload.

<div class="important">

Azure requires that the uploaded Virtual Hard Disk (VHD) files are in a
fixed format. The ManageIQ virtual appliance image VHD file is dynamic
by default. Currently, the Azure Powershell script and Azure CLI do not
automatically convert the dynamic VHD file to fixed during upload. To
upload using either method, the ManageIQ virtual appliance image VHD
file must be first converted from dynamic to fixed, and properly aligned
to the nearest 1 MB boundary. Once converted and properly aligned, you
can then upload the appliance virtual image VHD file using either the
Azure PowerShell or Azure CLI method.

</div>

### Converting and Aligning the ManageIQ Virtual Appliance Image

Complete the following procedure to ensure the ManageIQ dynamic .vhd
file is properly aligned to the nearest 1 MB boundary, and is in a
fixed-size VHD format.

1.  Convert the dynamic VHD file you downloaded in [Obtaining the
    ManageIQ Virtual Appliance](#obtaining-the-appliance) to RAW format.
    
        $ qemu-img convert -f vpc -O raw <image-name.vhd> <image-name.raw>
        
        Example:
        
        $ qemu-img convert -f vpc -O raw example.vhd rexample.raw

2.  Copy and paste the script below into a new bash shell script file,
    for example, `aligned-size.sh`. Change *rawdisk="image-name"* to the
    image name for your file. This script will calculate the rounded
    file size to the nearest 1 MB boundary.
    
        #!/bin/bash
        rawdisk="example.raw"
        MB=$((1024 * 1024))
        size=$(qemu-img info -f raw --output json "$rawdisk" | gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
        rounded_size=$((($size/$MB + 1) * $MB))
        echo "rounded size = $rounded_size"
        export rounded_size

3.  Run the shell script. The file name `aligned-size.sh` is used in
    this example.
    
        $ sh aligned-size.sh
        
        rounded size = 34361835520

4.  Resize the virtual appliance image using the rounded size.
    
        $ qemu-img resize -f raw <image-name.raw> <rounded_size>
        
        Example:
        
        $ qemu-img resize -f raw example.raw 34361835520
        
        Image resized.

5.  Convert the appliance image to a fixed-size VHD file.
    
        $ qemu-img convert -f raw -o subformat=fixed -O vpc <image-name.raw> <image-name.vhd>
        
        Example:
        
        qemu-img convert -f raw -o subformat=fixed -O vpc example.raw example.vhd

6.  Get the virtual size for the VHD file.
    
        $ qemu-img info --output=json -f vpc <path-to-image>
        
        Example:
        
        $ qemu-img info --output=json -f vpc example.vhd
        
        {
          "virtual-size": 34361835520,
          "filename": "example.vhd",
          "cluster-size": 2097152,
          "format": "vpc",
          "actual-size": 2133401600,
          "dirty-flag": false
        }

7.  Divide the virtual-size value by 1024, twice. If the result is a
    whole number, the VHD file is aligned properly. The example below
    shows that the file is properly aligned.
    
        34361835520 / 1024 / 1024 = 32770

<div class="important">

qemu-img version 1.5.3 is used in this procedure. Check the qemu-img
version using the command: `yum info qemu-img`. If the version is 2.2.1
or later, add the option *force\_size* in the conversion command, for
example, *subformat=fixed,force\_size*.

</div>

The ManageIQ Azure virtual appliance image is ready for uploading and
provisioning in Microsoft Azure.

### Using the Azure PowerShell Script

<div class="note">

Make sure Azure Resource Manager cmdlets are available; see [Azure
Resource Manager
Cmdlets](https://msdn.microsoft.com/en-us/library/mt125356.aspx) for the
latest installation information.

</div>

1.  Log in to **Azure Resource Manager** using the cmdlet:
    
        ## Customize for Your Environment
        $SubscriptionName = "my subscription"
        
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
    
    When prompted, enter your user name and password for the Azure
    Portal.

2.  Upload the VHD file to a storage account. As shown in the example
    script below, you will first create a **Resource Group** through the
    Portal UI or PowerShell. Additionally, create the storage container
    defined in "BlobDestinationContainer" in advance.
    
        Example Script:
        
        ## Customize for Your Environment
        $SubscriptionName = "my subscription"
        
        $ResourceGroupName = "test"
        $StorageAccountName = "test"
        
        $BlobNameSource = "example.vhd"
        $BlobSourceContainer = "templates"
        $LocalImagePath = "C:\tmp\$BlobNameSource"
        
        ##
        
        # Upload VHD to a "templates" directory. You can pass a few arguments, such as `NumberOfUploaderThreads 8`. The default number of uploader threads is `8`. See https://msdn.microsoft.com/en-us/library/mt603554.aspx
        
        Add-AzureRmVhd -ResourceGroupName $ResourceGroupName -Destination https://$StorageAccountName.blob.core.windows.net/$BlobSourceContainer/$BlobNameSource -LocalFilePath $LocalImagePath -NumberOfUploaderThreads 8

3.  Create a virtual machine. Then, define your VM and VHD name, your
    system/deployment name and size. Next, you will set the appropriate
    Storage, Network and Configuration options for your environment.
    
        Example Script:
        
        ## Customize for Your Environment
        
        $BlobNameDest = "example.vhd"
        $BlobDestinationContainer = "vhds"
        $VMName = "example"
        $DeploySize= "Standard_A3"
        $vmUserName = "user1"
        
        $InterfaceName = "test-nic"
        $VNetName = "test-vnet"
        $PublicIPName = "test-public-ip"
        
        $SSHKey = <your ssh public key>
        
        ##
        
        $StorageAccount = Get-AzureRmStorageAccount -ResourceGroup $ResourceGroupName -Name $StorageAccountName
        
        $SourceImageUri = "https://$StorageAccountName.blob.core.windows.net/templates/$BlobNameSource"
        $Location = $StorageAccount.Location
        $OSDiskName = $VMName
        
        # Network
        $Subnet1Name = "default"
        $VNetAddressPrefix = "10.1.0.0/16"
        $VNetSubnetAddressPrefix = "10.1.0.0/24"
        $PIp = New-AzureRmPublicIpAddress -Name $PublicIPName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod Dynamic -Force
        $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $Subnet1Name -AddressPrefix $VNetSubnetAddressPrefix
        $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig -Force
        $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PIp.Id -Force
        
        # Specify the VM Name and Size
        $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $DeploySize
        
        # Add User
        $cred = Get-Credential -UserName $VMUserName -Message "Setting user credential - use blank password"
        $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Linux -ComputerName $VMName -Credential $cred
        
        # Add NIC
        $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
        
        # Add Disk
        $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + $BlobDestinationContainer + "/" + $BlobNameDest
        
        $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -CreateOption fromImage -SourceImageUri $SourceImageUri -Linux
        
        # Set SSH key
        Add-AzureRmVMSshPublicKey -VM $VirtualMachine -Path “/home/$VMUserName/.ssh/authorized_keys” -KeyData $SSHKey
        
        # Create the VM
        New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine
    
    <div class="note">
    
    These are the procedural steps as of the time of writing. For more
    information, see the following Azure documentation.
    
      - <https://azure.microsoft.com/en-us/documentation/articles/powershell-azure-resource-manager>
    
    The steps covered in the following article are for a Windows
    machine, however, most of the items are common between Windows and
    Linux.
    
      - <https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-create-powershell>
    
    </div>

### Using the Azure Command-Line Interface

Complete the following steps to upload and provision the ManageIQ
virtual appliance using the Azure CLI.

#### Installing the Azure Command-Line Interface

<div class="note">

For a complete Azure CLI 2.0 command reference, see [Azure CLI 2.0:
Command reference -
az](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest).

</div>

1.  Import the Microsoft repository key.
    
        $ sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

2.  Create a local Azure CLI repository entry.
    
        $ sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'

3.  Update the yum package index.
    
        $ yum check-update

4.  Install the Azure CLI.
    
        $ sudo yum install azure-cli

5.  Log in to Azure.
    
        $ az login
        
        Example:
        
        To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the code GJP8Y33XY to authenticate.
        
        [
          {
            "cloudName": "AzureCloud",
            "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "isDefault": true,
            "name": "Demo Azure account",
            "state": "Enabled",
            "tenantId": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "user": {
              "name": "clouduser",
              "type": "user"
            }
          }
        ]

#### Creating Resources for the Appliance in Microsoft Azure Using the Azure Command-Line Interface

Complete the following steps to create resources in Microsoft Azure
using the Azure CLI.

<div class="note">

  - If you already have resources you can use, you can skip this section
    and go directly to [Uploading and Provisioning the ManageIQ Virtual
    Appliance Using the Azure Command-Line
    Interface](#uploading-provisioning-appliance-using-azure-cli).

  - For a complete Azure CLI 2.0 command reference, see [Azure CLI 2.0:
    Command reference -
    az](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest).

</div>

1.  Create a resource group in an Azure region.
    
        $ az group create --name <resource-group> --location <azure-region>
        
        Example:
        
        [clouduser@localhost]$ az group create --name azrhelclirsgrp --location southcentralus
        {
          "id": "/subscriptions//resourceGroups/azrhelclirsgrp",
          "location": "southcentralus",
          "managedBy": null,
          "name": "azrhelclirsgrp",
          "properties": {
            "provisioningState": "Succeeded"
          },
          "tags": null
        }

2.  Create a storage account; see [SKU type
    descriptions](#storage-sku-types).
    
        $ az storage account create -l <azure-region> -n <storage-account-name> -g <resource-group --sku <sku_type>
        
        Example:
        
        [clouduser@localhost]$ az storage account create -l southcentralus -n azrhelclistact -g azrhelclirsgrp --sku Standard_LRS
        {
          "accessTier": null,
          "creationTime": "2017-04-05T19:10:29.855470+00:00",
          "customDomain": null,
          "encryption": null,
          "id": "/subscriptions//resourceGroups/azrhelclirsgrp/providers/Microsoft.Storage/storageAccounts/azrhelclistact",
          "kind": "Storage",
          "lastGeoFailoverTime": null,
          "location": "southcentralus",
          "name": "azrhelclistact",
          "primaryEndpoints": {
            "blob": "https://azrhelclistact.blob.core.windows.net/",
            "file": "https://azrhelclistact.file.core.windows.net/",
            "queue": "https://azrhelclistact.queue.core.windows.net/",
            "table": "https://azrhelclistact.table.core.windows.net/"
        },
        "primaryLocation": "southcentralus",
        "provisioningState": "Succeeded",
        "resourceGroup": "azrhelclirsgrp",
        "secondaryEndpoints": null,
        "secondaryLocation": null,
        "sku": {
          "name": "Standard_LRS",
          "tier": "Standard"
        },
        "statusOfPrimary": "available",
        "statusOfSecondary": null,
        "tags": {},
          "type": "Microsoft.Storage/storageAccounts"
        }

3.  Get the storage account connection string.
    
        $ az storage account show-connection-string -n <storage-account-name> -g <resource-group>
        
        Example:
        
        [clouduser@localhost]$ az storage account show-connection-string -n azrhelclistact -g azrhelclirsgrp
        {
          "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=azrhelclistact;AccountKey=NreGk...=="
        }

4.  Export the connection string. Copy the connection string and paste
    it into the following command. This connects your system to the
    storage account.
    
        $ export AZURE_STORAGE_CONNECTION_STRING="<storage-connection-string>"
        
        Example:
        
        [clouduser@localhost]$ export AZURE_STORAGE_CONNECTION_STRING="DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=azrhelclistact;AccountKey=NreGk...=="

5.  Create the storage container.
    
        $ az storage container create -n <container-name>
        
        Example:
        
        [clouduser@localhost]$ az storage container create -n azrhelclistcont
        {
          "created": true
        }

6.  Create a virtual network.
    
        $ az network vnet create -g <resource group> --name <vnet-name> --subnet-name <subnet-name>
        
        Example:
        
        [clouduser@localhost]$ az network vnet create --resource-group azrhelclirsgrp --name azrhelclivnet1 --subnet-name azrhelclisubnet1
        {
          "newVNet": {
            "addressSpace": {
              "addressPrefixes": [
              "10.0.0.0/16"
              ]
          },
          "dhcpOptions": {
            "dnsServers": []
          },
          "etag": "W/\"\"",
          "id": "/subscriptions//resourceGroups/azrhelclirsgrp/providers/Microsoft.Network/virtualNetworks/azrhelclivnet1",
          "location": "southcentralus",
          "name": "azrhelclivnet1",
          "provisioningState": "Succeeded",
          "resourceGroup": "azrhelclirsgrp",
          "resourceGuid": "0f25efee-e2a6-4abe-a4e9-817061ee1e79",
          "subnets": [
            {
              "addressPrefix": "10.0.0.0/24",
              "etag": "W/\"\"",
              "id": "/subscriptions//resourceGroups/azrhelclirsgrp/providers/Microsoft.Network/virtualNetworks/azrhelclivnet1/subnets/azrhelclisubnet1",
              "ipConfigurations": null,
              "name": "azrhelclisubnet1",
              "networkSecurityGroup": null,
              "provisioningState": "Succeeded",
              "resourceGroup": "azrhelclirsgrp",
              "resourceNavigationLinks": null,
              "routeTable": null
            }
          ],
          "tags": {},
          "type": "Microsoft.Network/virtualNetworks",
          "virtualNetworkPeerings": null
          }
        }

#### Uploading and Provisioning the ManageIQ Virtual Appliance Using the Azure Command-Line Interface

You can now upload and provision the appliance in an Azure environment
using the Azure Command-Line Interface (Azure CLI).

1.  Upload the image to the storage container. It may take several
    minutes. Note: Enter `az storage container list` to get the list of
    storage containers.
    
        $ az storage blob upload --account-name <storage-account-name> --container-name <container-name> --type page --file <path-to-vhd> --name <image-name>.vhd
        
        Example:
        
        $ az storage blob upload --account-name azrhelclistact --container-name azrhelclistcont --type page --file example.vhd --name example.vhd
        
        Finished[#############################################################]  100.0000%

2.  Get the URL for the uploaded VHD file using the following command.
    You will need to use this URL in the next step.
    
        $ az storage blob url -c <container-name> -n <image-name>.vhd
        
        Example:
        
        $ az storage blob url -c azrhelclistcont -n example.vhd
        
        "https://azrhelclistact.blob.core.windows.net/azrhelclistcont/example.vhd"

3.  Create a reusable image from a blob and then use a managed disk.
    
        Example:
        
        $ az image create -n <image-name> -g <miq-appliance-group> --os-type <linux> --source <https://miqstorageaccount.blob.core.windows.net/miqstoragecontainer/example.vhd>

4.  Create the virtual machine. Note that the following command uses
    `--generate-ssh-keys`. In this example, the private/public key pair
    `/home/clouduser/.ssh/id_rsa` and `/home/clouduser/.ssh/id_rsa.pub`
    are created.
    
        $ az vm create --resource-group <resource-group> --location <azure-region> --use-unmanaged-disk --name <vm-name> --storage-account <storage-account-name> --os-type linux --admin-username <administrator-name> --generate-ssh-keys --image <URL>
        
        Example:
        
        az vm create --resource-group azrhelclirsgrp --location southcentralus --use-unmanaged-disk --name miq-appliance-1 --storage-account azrhelclistact --os-type linux --admin-username clouduser --generate-ssh-keys --image https://azrhelclistact.blob.core.windows.net/azrhelclistcont/example.vhd
        
        {
          "fqdns": "",
          "id": "/subscriptions//resourceGroups/azrhelclirsgrp/providers/Microsoft.Compute/virtualMachines/miq-appliance-1",
          "location": "southcentralus",
          "macAddress": "00-0X-XX-XX-XX-XX",
          "powerState": "VM running",
          "privateIpAddress": "10.0.0.4",
          "publicIpAddress": "12.84.121.147",
          "resourceGroup": "azrhelclirsgrp"
        }
    
    Make a note of the public IP address. You will need this to log in
    to the virtual machine in the next step.

5.  Start an SSH session and log in to the appliance.
    
        $ ssh -i <path-to-ssh-key> <admin-username@public-IP-address>
        
        Example:
        
        $ ssh  -i /home/clouduser/.ssh/id_rsa clouduser@12.84.121.147
        The authenticity of host '12.84.121.147' can't be established.
        Are you sure you want to continue connecting (yes/no)? yes
        Warning: Permanently added '12.84.121.147' (ECDSA) to the list of known hosts.
        
        Welcome to the Appliance Console
        
        For a menu, please type: appliance_console

6.  Enter `sudo appliance_console` at the prompt. The summary screen
    appears.

You have successfully provisioned a ManageIQ virtual appliance in
Microsoft Azure.

<div class="note">

The exported storage connection string does not persist after a system
reboot. If any of the commands in the above steps fail, export the
storage connection string again using the following commands:

1.  Get the storage account connection string.
    
        $ az storage account show-connection-string -n <storage-account-name> -g <resource-group>
        
        Example:
        
        $ az storage account show-connection-string -n azrhelclistact -g azrhelclirsgrp
        {
          "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=azrhelclistact;AccountKey=NreGk...=="
        }

2.  Export the connection string. Copy the connection string and paste
    it into the following command. This connects your system to the
    storage account.
    
        $ export AZURE_STORAGE_CONNECTION_STRING="<storage-connection-string>"
        
        Example:
        
        $ export AZURE_STORAGE_CONNECTION_STRING="DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=azrhelclistact;AccountKey=NreGk...=="

</div>

  - You will need to create a data disk for the database; see
    <https://docs.microsoft.com/en-us/azure/virtual-machines/linux/add-disk>
    for information about how to add a persistent disk to store your
    data.

  - See [Database
    Requirements](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.5/html-single/deployment_planning_guide/#database-requirements)
    for some general guidelines for your database requirements.

  - For information about Azure ports used by ManageIQ, see
    <https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.5/html-single/appliance_hardening_guide/#chap_red_hat_cloudforms_security_guide_firewall>.

# Enabling ManageIQ User Interface Access

To access the ManageIQ virtual appliance user interface, you need to
enable access over ports `80` and `443` to the virtual machine. You can
do this using the CLI or from within the Azure portal.

  - To enable a port using the CLI, enter `az vm open-port --port
    <port-number> --resource-group <resource-group> --name <vm-name>`.

  - To enable a port using the Microsoft Azure portal, open the
    properties for the resource group where the appliance is located,
    click on **Network Security Group**, and add HTTP and HTTPS access.

# Configuring ManageIQ

After installing ManageIQ and running it for the first time, you must
perform some basic configuration. To configure ManageIQ, you must at a
minimum:

1.  Add a disk to the infrastructure hosting your appliance.

2.  Configure the database.

Configure the ManageIQ appliance using the internal appliance console.

## Accessing the Appliance Console

1.  Start the appliance and open a terminal console.

2.  Log in to the appliance using the SSH key.

3.  Enter the `appliance_console` command. The ManageIQ appliance
    summary screen displays.

4.  Press `Enter` to manually configure settings.

5.  Press the number for the item you want to change, and press `Enter`.
    The options for your selection are displayed.

6.  Follow the prompts to make the changes.

7.  Press `Enter` to accept a setting where applicable.

<div class="note">

The ManageIQ appliance console automatically logs out after five minutes
of inactivity.

</div>

## Configuring a Database

ManageIQ uses a database to store information about the environment.
Before using ManageIQ, configure the database options for it; ManageIQ
provides the following two options for database configuration:

  - Install an internal PostgreSQL database to the appliance

  - Configure the appliance to use an external PostgreSQL database

### Configuring an Internal Database

<div class="important">

Before installing an internal database, add a disk to the infrastructure
hosting your appliance. See the documentation specific to your
infrastructure for instructions for adding a disk. As a storage disk
usually cannot be added while a virtual machine is running, Red Hat
recommends adding the disk before starting the appliance. ManageIQ only
supports installing of an internal VMDB on blank disks; installation
will fail if the disks are not blank.

</div>

1.  Start the appliance and open a terminal console.

2.  Log in to the appliance using the SSH key.

3.  Enter the `appliance_console` command. The ManageIQ appliance
    summary screen displays.

4.  Press **Enter** to manually configure settings.

5.  Select **Configure Database** from the menu.

6.  You are prompted to create or fetch an encryption key.
    
      - If this is the first ManageIQ appliance, choose **Create key**.
    
      - If this is not the first ManageIQ appliance, choose **Fetch key
        from remote machine** to fetch the key from the first appliance.
        For worker and multi-region setups, use this option to copy key
        from another appliance.
        
        <div class="note">
        
        All ManageIQ appliances in a multi-region deployment must use
        the same key.
        
        </div>

7.  Choose **Create Internal Database** for the database location.

8.  Choose a disk for the database. This can be either a disk you
    attached previously, or a partition on the current disk.
    
    <div class="important">
    
    Red Hat recommends using a separate disk for the database.
    
    </div>
    
    If there is an unpartitioned disk attached to the virtual machine,
    the dialog will show options similar to the following:
    
        1) /dev/vdb: 20480
        2) Don't partition the disk
    
      - Enter **1** to choose `/dev/vdb` for the database location. This
        option creates a logical volume using this device and mounts the
        volume to the appliance in a location appropriate for storing
        the database. The default location is `/var/lib/pgsql`, which
        can be found in the environment variable
        `$APPLIANCE_PG_MOUNT_POINT`.
    
      - Enter **2** to continue without partitioning the disk. A second
        prompt will confirm this choice. Selecting this option results
        in using the root filesystem for the data directory (not advised
        in most cases).

9.  Enter **Y** or **N** for **Should this appliance run as a standalone
    database server?**
    
      - Select **Y** to configure the appliance as a database-only
        appliance. As a result, the appliance is configured as a basic
        PostgreSQL server, without a user interface.
    
      - Select **N** to configure the appliance with the full
        administrative user interface.

10. When prompted, enter a unique number to create a new region.
    
    <div class="important">
    
    Creating a new region destroys any existing data on the chosen
    database.
    
    </div>

11. Create and confirm a password for the database.

ManageIQ then configures the internal database. This takes a few
minutes. After the database is created and initialized, you can log in
to ManageIQ.

### Configuring an External Database

Based on your setup, you will choose to configure the appliance to use
an external PostgreSQL database. For example, we can only have one
database in a single region. However, a region can be segmented into
multiple zones, such as database zone, user interface zone, and
reporting zone, where each zone provides a specific function. The
appliances in these zones must be configured to use an external
database.

The `postgresql.conf` file used with ManageIQ databases requires
specific settings for correct operation. For example, it must correctly
reclaim table space, control session timeouts, and format the PostgreSQL
server log for improved system support. Due to these requirements, Red
Hat recommends that external ManageIQ databases use a `postgresql.conf`
file based on the standard file used by the ManageIQ appliance.

Ensure you configure the settings in the `postgresql.conf` to suit your
system. For example, customize the `shared_buffers` setting according to
the amount of real storage available in the external system hosting the
PostgreSQL instance. In addition, depending on the aggregate number of
appliances expected to connect to the PostgreSQL instance, it may be
necessary to alter the `max_connections` setting.

<div class="note">

  - ManageIQ requires PostgreSQL version 9.5.

  - Because the `postgresql.conf` file controls the operation of all
    databases managed by a single instance of PostgreSQL, do not mix
    ManageIQ databases with other types of databases in a single
    PostgreSQL instance.

</div>

1.  Start the appliance and open a terminal console.

2.  Log in to the appliance using the SSH key.

3.  Enter the `appliance_console` command. The ManageIQ appliance
    summary screen displays.

4.  Press **Enter** to manually configure settings.

5.  Select **Configure Database** from the menu.

6.  You are prompted to create or fetch a security key.
    
      - If this is the first ManageIQ appliance, choose **Create key**.
    
      - If this is not the first ManageIQ appliance, choose **Fetch key
        from remote machine** to fetch the key from the first appliance.
        
        <div class="note">
        
        All ManageIQ appliances in a multi-region deployment must use
        the same key.
        
        </div>

7.  Choose **Create Region in External Database** for the database
    location.

8.  Enter the database hostname or IP address when prompted.

9.  Enter the database name or leave blank for the default
    (`vmdb_production`).

10. Enter the database username or leave blank for the default (`root`).

11. Enter the chosen database user’s password.

12. Confirm the configuration if prompted.

ManageIQ will then configure the external database.

## Configuring a Worker Appliance

You can use multiple appliances to facilitate horizontal scaling, as
well as for dividing up work by roles. Accordingly, configure an
appliance to handle work for one or many roles, with workers within the
appliance carrying out the duties for which they are configured. You can
configure a worker appliance through the terminal. The following steps
demonstrate how to join a worker appliance to an appliance that already
has a region configured with a database.

1.  Start the appliance and open a terminal console.

2.  Log in to the appliance using the SSH key.

3.  Enter the `appliance_console` command. The ManageIQ appliance
    summary screen displays.

4.  Press **Enter** to manually configure settings.

5.  Select **Configure Database** from the menu.

6.  You are prompted to create or fetch a security key. Since this is
    not the first ManageIQ appliance, choose **2) Fetch key from remote
    machine**. For worker and multi-region setups, use this option to
    copy the security key from another appliance.
    
    <div class="note">
    
    All ManageIQ appliances in a multi-region deployment must use the
    same key.
    
    </div>

7.  Choose **Join Region in External Database** for the database
    location.

8.  Enter the database hostname or IP address when prompted.

9.  Enter the port number or leave blank for the default (`5432`).

10. Enter the database name or leave blank for the default
    (`vmdb_production`).

11. Enter the database username or leave blank for the default (`root`).

12. Enter the chosen database user’s password.

13. Confirm the configuration if prompted.

# Logging In After Installing ManageIQ

Once ManageIQ is installed, you can log in and perform administration
tasks.

Log in to ManageIQ for the first time after installing by:

1.  Navigate to the URL for the login screen. (<https://xx.xx.xx.xx> on
    the virtual machine instance)

2.  Enter the default credentials (Username: **admin** | Password:
    **smartvm**) for the initial login.

3.  Click **Login**.

## Changing the Default Login Password

Change your password to ensure more private and secure access to
ManageIQ.

1.  Navigate to the URL for the login screen. (<https://xx.xx.xx.xx> on
    the virtual machine instance)

2.  Click **Update Password** beneath the **Username** and **Password**
    text fields.

3.  Enter your current **Username** and **Password** in the text fields.

4.  Input a new password in the **New Password** field.

5.  Repeat your new password in the **Verify Password** field.

6.  Click **Login**.

# Appendix

# Appliance Console Command-Line Interface (CLI)

Currently, the `appliance_console_cli` feature is a subset of the full
functionality of the `appliance_console` itself, and covers functions
most likely to be scripted using the command-line interface (CLI).

1.  After starting the ManageIQ appliance, log in with a user name of
    `root` and the default password of `smartvm`. This displays the Bash
    prompt for the root user.

2.  Enter the `appliance_console_cli` or `appliance_console_cli --help`
    command to see a list of options available with the command, or
    simply enter `appliance_console_cli --option <argument>` directly to
    use a specific option.

|                  |                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------ |
| Option           | Description                                                                                |
| \--region (-r)   | region number (create a new region in the database - requires database credentials passed) |
| \--internal (-i) | internal database (create a database on the current appliance)                             |
| \--dbdisk        | database disk device path (for configuring an internal database)                           |
| \--hostname (-h) | database hostname                                                                          |
| \--port          | database port (defaults to `5432`)                                                         |
| \--username (-U) | database username (defaults to `root`)                                                     |
| \--password (-p) | database password                                                                          |
| \--dbname (-d)   | database name (defaults to `vmdb_production`)                                              |

Database Configuration Options

|                   |                                                            |
| ----------------- | ---------------------------------------------------------- |
| Option            | Description                                                |
| \--key (-k)       | create a new v2\_key                                       |
| \--fetch-key (-K) | fetch the v2\_key from the given host                      |
| \--force-key (-f) | create or fetch the key even if one exists                 |
| \--sshlogin       | ssh username for fetching the v2\_key (defaults to `root`) |
| \--sshpassword    | ssh password for fetching the v2\_key                      |

v2\_key Options

|                       |                                                                                                  |
| --------------------- | ------------------------------------------------------------------------------------------------ |
| Option                | Description                                                                                      |
| \--host (-H)          | set the appliance hostname to the given name                                                     |
| \--ipaserver (-e)     | IPA server FQDN                                                                                  |
| \--ipaprincipal (-n)  | IPA server principal (default: `admin`)                                                          |
| \--ipapassword (-w)   | IPA server password                                                                              |
| \--ipadomain (-o)     | IPA server domain (optional). Will be based on the appliance domain name if not specified.       |
| \--iparealm (-l)      | IPA server realm (optional). Will be based on the domain name of the ipaserver if not specified. |
| \--uninstall-ipa (-u) | uninstall IPA client                                                                             |

IPA Server Options

<div class="note">

  - In order to configure authentication through an IPA server, in
    addition to using **Configure External Authentication (httpd)** in
    the `appliance_console`, external authentication can be optionally
    configured via the `appliance_console_cli` (command-line interface).

  - Specifying **--host** will update the hostname of the appliance. If
    this step was already performed via the `appliance_console` and the
    necessary updates made to `/etc/hosts` if DNS is not properly
    configured, the **--host** option can be omitted.

</div>

|                              |                                                                                 |
| ---------------------------- | ------------------------------------------------------------------------------- |
| Option                       | Description                                                                     |
| \--ca (-c)                   | CA name used for certmonger (default: `ipa`)                                    |
| \--postgres-client-cert (-g) | install certs for postgres client                                               |
| \--postgres-server-cert      | install certs for postgres server                                               |
| \--http-cert                 | install certs for http server (to create certs/httpd\* values for a unique key) |
| \--extauth-opts (-x)         | external authentication options                                                 |

Certificate Options

<div class="note">

The certificate options augment the functionality of the `certmonger`
tool and enable creating a certificate signing request (CSR), and
specifying `certmonger` the directories to store the keys.

</div>

|                 |                                                                                     |
| --------------- | ----------------------------------------------------------------------------------- |
| Option          | Description                                                                         |
| \--logdisk (-l) | log disk path                                                                       |
| \--tmpdisk      | initialize the given device for temp storage (volume mounted at `/var/www/miq_tmp`) |
| \--verbose (-v) | print more debugging info                                                           |

Other Options

**Example Usage.**

    $ ssh root@appliance.test.company.com

To create a new database locally on the server using `/dev/sdb`:

    # appliance_console_cli --internal --dbdisk /dev/sdb --region 0 --password smartvm

To copy the v2\_key from a host *some.example.com* to local machine:

    # appliance_console_cli --fetch-key some.example.com --sshlogin root --sshpassword smartvm

You could combine the two to join a region where *db.example.com* is the
appliance hosting the database:

    # appliance_console_cli --fetch-key db.example.com --sshlogin root --sshpassword smartvm --hostname db.example.com --password mydatabasepassword

To configure external authentication:

    # appliance_console_cli --host appliance.test.company.com
                            --ipaserver ipaserver.test.company.com
                            --ipadomain test.company.com
                            --iparealm TEST.COMPANY.COM
                            --ipaprincipal admin
                            --ipapassword smartvm1

To uninstall external authentication:

    # appliance_console_cli  --uninstall-ipa

# Storage SKU Types

| SKU Type        | Description                                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Standard\_LRS   | Locally Redundant Storage: Synchronous copies of data are created within a single data center.                                                                     |
| Standard\_GRS   | Geographically Redundant Storage: Same as Standard\_LRS with additional asynchronous copies stored in a secondary data center in a separate geographical location. |
| Standard\_RAGRS | Read-Access Geographically Redundant Storage: Same as Standard\_GRS with additional read access to the secondary data center.                                      |
| Standard\_ZRS   | Zone Redundant Storage: For block blobs only. Stores three copies of data across multiple data centers within the region or across regions.                        |
| Premium\_LRS    | Premium Locally Redundant Storage: Same as Standard\_LRS, but uses Premium Storage disks.                                                                          |

Storage SKU types
