After deploying the appliance, log in with the root password `smartvm`.
If you deployed the appliance as a virtual machine, you can log in
through `virsh`:

    [root@kvm-host ~]# virsh console my-cfme
    Connected to domain my-cfme
    ...
    Welcome to the CFME Virtual Appliance.
    
    You can browse to http://localhost.localdomain/
    
    Red Hat Enterprise Linux Server 7.2 (Maipo)
    Kernel 3.10.0-327.36.1.el7.x86_64 on an x86_64
    localhost login: root
    Password:
    Last login: Thu Oct 13 23:03:53 on tty2
    Welcome to the Appliance Console
    
    For a menu, please type: appliance_console
    [root@localhost ~]#

# Configuring General Appliance Settings

After logging in, you can use the following menu items for advanced
configuration of the appliance:

<table>
<caption>Appliance Console Advanced Settings</caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Option</p></td>
<td><p>Description</p></td>
</tr>
<tr class="even">
<td><p><strong>Configure Network</strong></p></td>
<td><p>Provides options for configuring the network for your {product-title_short} appliance. The appliance is initially configured as a DHCP client with bridged networking.</p>
<p>You can use DHCP to obtain the IP address and network configuration for your {product-title_short} appliance, or use an IPv4 or IPv6 static network configuration by providing specific IP address and network settings.</p>
<p>This menu also provides options to test the network configuration to check that name resolution is working correctly, and to set the appliance’s host name.</p>
<div class="important">
<p>A valid fully qualified hostname for the {product-title_short} appliance is required for SmartState analysis to work correctly.</p>
</div></td>
</tr>
<tr class="odd">
<td><p><strong>Restore Database from Backup</strong></p></td>
<td><p>Restore the Virtual Management Database (VMDB) from a previous backup.</p></td>
</tr>
<tr class="even">
<td><p><strong>Configure Database</strong></p></td>
<td><p>Configure the VMDB. Use this option to configure the database for the appliance after installing and running it for the first time.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Configure Database Replication</strong></p></td>
<td><p>Configure a primary or standby server for VMDB replication.</p></td>
</tr>
<tr class="even">
<td><p><strong>Configure Database Maintenance</strong></p></td>
<td><p>Configure the VMDB maintenance schedule.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Logfile Configuration</strong></p></td>
<td><p>Provides options for configuring a new logfile disk volume, and changing the saved logrotate count.</p></td>
</tr>
<tr class="even">
<td><p><strong>Configure Application Database Failover Monitor</strong></p></td>
<td><p>Start or stop VMDB failover monitoring.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Extend Temporary Storage</strong></p></td>
<td><p>Add temporary storage to the appliance. The appliance formats an unpartitioned disk attached to the appliance host and mounts it at <code>/var/www/miq_tmp</code>. The appliance uses this temporary storage directory to perform certain image download functions.</p></td>
</tr>
<tr class="even">
<td><p><strong>Configure External Authentication (httpd)</strong></p></td>
<td><p>Configure authentication through an IPA server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Update External Authentication Options</strong></p></td>
<td><p>Enable or disable external authentication methods: single sign-on, SAML, and local login. For example, if the current state is <code>Enabled</code>, the prompt indicates the option should be <code>Disabled</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Generate Custom Encryption Key</strong></p></td>
<td><p>Regenerate the encryption key used to encode plain text password.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Harden Appliance Using SCAP Configuration</strong></p></td>
<td><p>Apply Security Content Automation Protocol (SCAP) standards to the appliance. You can view these SCAP rules in the <code>/var/www/miq/lib/appliance_console/config/scap_rules.yml</code> file.</p></td>
</tr>
<tr class="even">
<td><p><strong>Stop EVM Server Processes</strong></p></td>
<td><p>Stop all server processes. You may need to do this to perform maintenance.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Start EVM Server Processes</strong></p></td>
<td><p>Start the server. You may need to do this after performing maintenance.</p></td>
</tr>
<tr class="even">
<td><p><strong>Restart Appliance</strong></p></td>
<td><p>Restart the {product-title} appliance. You can either restart the appliance and clear the logs or just restart the appliance.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Shut Down Appliance</strong></p></td>
<td><p>Power down the appliance and exit all processes.</p></td>
</tr>
<tr class="even">
<td><p><strong>Summary Information</strong></p></td>
<td><p>Go back to the network summary screen for the {product-title} appliance.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Quit</strong></p></td>
<td><p>Leave the {product-title} appliance console.</p></td>
</tr>
</tbody>
</table>

# Configuring a Database for {product-title}

{product-title} supports the use of an internal or external database.
The following instructions are suitable for configuring an *internal*
database. For instructions on how to configure an external database
instead, see [Configuring an External
Database](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.1/single/installing-red-hat-cloudforms-on-red-hat-enterprise-linux-openstack-platform#configuring_an_external_database).

<div class="important">

Before installing an internal database, add a disk to the infrastructure
hosting your appliance. See the documentation specific to your
infrastructure for instructions for adding a disk. As a storage disk
usually cannot be added while a virtual machine is running, Red Hat
recommends adding the disk before starting the appliance.
{product-title} only supports installing of an internal VMDB on blank
disks; installation will fail if the disks are not blank.

</div>

1.  Start the appliance and open a terminal console.

2.  Enter the `appliance_console` command. The {product-title} appliance
    summary screen displays.

3.  Press **Enter** to manually configure settings.

4.  Select **Configure Database** from the menu.

5.  You are prompted to create or fetch an encryption key.
    
      - If this is the first {product-title} appliance, choose **Create
        key**.
    
      - If this is not the first {product-title} appliance, choose
        **Fetch key from remote machine** to fetch the key from the
        first appliance. For worker and multi-region setups, use this
        option to copy key from another appliance.
        
        <div class="note">
        
        All {product-title\_short} appliances in a multi-region
        deployment must use the same key.
        
        </div>

6.  Choose **Create Internal Database** for the database location.

7.  Choose a disk for the database. This can be either a disk you
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

8.  Enter **Y** or **N** for **Should this appliance run as a standalone
    database server?**
    
      - Select **Y** to configure the appliance as a database-only
        appliance. As a result, the appliance is configured as a basic
        PostgreSQL server, without a user interface.
    
      - Select **N** to configure the appliance with the full
        administrative user interface.

9.  When prompted, enter a unique number to create a new region.
    
    <div class="important">
    
    Creating a new region destroys any existing data on the chosen
    database.
    
    </div>

10. Create and confirm a password for the database.

{product-title} then configures the internal database. This takes a few
minutes. After the database is created and initialized, you can log in
to {product-title\_short}.

# Configuring General {product-title} Settings

After configuring the general settings for the appliance and creating a
database for it, you can now launch {product-title}. To do this, use the
**Start EVM Server Processes** option from the appliance console
([Configuring General Appliance
Settings](#configuring_general_appliance_settings)). Once you launch
{product-title}, note the **Hostname** and **IP Address** displayed on
the appliance console screen.

Open the {product-title} web-based user interface by accessing either
**Hostname** and **IP Address** on a web browser. At the login screen,
use the following credentials:

  - Username: **admin**

  - Password: **smartvm**

<div class="note">

You can also change the password of the **admin** account from the login
screen. To do so, click the **Update Password** link.

</div>

You can access and configure most {product-title} settings through the
**Configuration** menu. You can access this menu through **Administrator
| EVM** \> **Configuration**.

The options under the ![Configuration](config-gear.png)
**Configuration** menu allow you to configure global options for your
{product-title} environment, view diagnostic information, and view
analytics on the servers in the environment. The menu displays the
{product-title} environment at the enterprise, zone, and server levels.

There are four main areas:

  - **Settings**
    
    This menu allows you to configure global settings for your
    {product-title} infrastructure. You can also create analysis
    profiles and schedules for these profiles.

  - **Access Control**
    
    This menu contains options for configuring users, groups, roles, and
    tenants.

  - **Diagnostics**
    
    This menu displays the status of your servers and their roles and
    provides access to logs.

  - **Database**
    
    specify the location of your Virtual Machine Database (VMDB) and its
    login credentials.

# Configuring {product-title\_short} Metrics for SmartState Analysis

You can also configure {product-title\_short} to perform a *SmartState
Analysis*. This type of analysis collects details such as accounts,
drivers, network information, hardware, and security patches on assets
managed by the OpenStack provider. Enabling SmartState Analysis involves
two steps:

1.  [Configuring {product-title\_short} Capacity and
    Utilization](#cf-caputils), and

2.  [Enabling SmartState Analysis](#cf-smartproxy)

These steps are required to allow {product-title\_short} to collect
metrics from OpenStack and use them to perform a SmartState analysis.
You can choose different servers to perform either function; the
following sections assume that you will.

## Configuring {product-title\_short} Capacity and Utilization

For metrics collection to work properly, you also need to configure
{product-title} to allow for all three **Capacity & Utilization** server
roles, which are available from the settings menu under
menu:Configuration\[Server \> Server Control\].

To enable these server roles:

1.  Click **Configuration**, then select the server to configure from
    menu:Settings\[Zone\] in the accordion menu on the left.

2.  Navigate to the **Server Roles** list in the menu:Server\[Server
    Control\] section. From there, set the required capacity and
    utilization roles to **ON**, namely:
    
    1.  **Capacity & Utilization Coordinator**
    
    2.  **Capacity & Utilization Data Collector**
    
    3.  **Capacity & Utilization Data Processor**

3.  Click **Save**.

Data collection is enabled immediately. However, the first collection
begins 5 minutes after the server is started, and every 10 minutes after
that. Therefore, the longest the collection takes after enabling the
Capacity & Utilization Collector role is 10 minutes. The first
collection from a particular provider may take a few minutes since
{product-title} is gathering data points going one month back in time.

For more information, see [Capacity and Utilization
Collection](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.1/deployment-planning-guide/#capacity_and_utilization_collection)
from the *Deployment Planning Guide*.

## Enabling SmartState Analysis

After enabling the required server roles, enable SmartState analysis.
See [Smart State Analysis
Support](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/support_matrix/#smart_state_analysis_support)
from the Support Matrix and [Running a SmartState
Analysis](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#running-a-smartstate-analysis)
in the *Managing Providers* guide for more information.

Enabling SmartState analysis is similar to [Configuring
{product-title\_short} Capacity and Utilization](#cf-caputils), in that
the procedure also involves enabling server roles on a specific server.
To do so:

1.  Click i\*Configuration\*.

2.  Select the server to configure from menu:Settings\[Zone\] in the
    left pane of the appliance.

3.  Navigate to the **Server Roles** list in the menu:Server\[Server
    Control\] section. From there, set the appropriate SmartState roles
    to **ON**. Namely:
    
    1.  **SmartProxy**
    
    2.  **SmartState Analysis**

4.  Click **Save**.
