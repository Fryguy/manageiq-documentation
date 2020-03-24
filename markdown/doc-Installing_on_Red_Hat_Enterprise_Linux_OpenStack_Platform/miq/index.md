# Installing ManageIQ

Installing ManageIQ consists of the following steps:

1.  Downloading the appliance for your environment as a virtual machine
    image template.

2.  Setting up a virtual machine based on the appliance.

3.  Configuring the ManageIQ appliance.

After you have completed all the procedures in this guide, you will have
a working environment on which additional customizations and
configurations can be performed.

## Obtaining the appliance

1.  In a browser, navigate to
    [manageiq.org/download](manageiq.org/download).

2.  Select **OpenStack** from the **--Choose your platform--** list.

3.  Select **Stable** from the **--Choose a release--** list.

4.  Follow the instructions to download the appliance.

## Uploading the Appliance on OpenStack

Log in to your OpenStack dashboard to upload your ManageIQ appliance.

1.  Log in to the OpenStack dashboard.

2.  In the **Project** tab, navigate to <span class="menuchoice">Compute
    \> Images</span>.

3.  Click **Create Image**.

4.  In **Name**, enter a name for the image.

5.  From **Image Source** list, select **Image Location**. Note that
    currently only images available via an HTTP URL are supported.

6.  In **Image Location**, add an external (HTTP) URL to load the image
    from. For example, **<http://example.com/image.iso>**.

7.  From the **Format** list, select the image format. For example, `ISO
    - Optical Disk Image`.

8.  Specify the **Architecture**. For example, `i386` for a 32-bit
    architecture or `x86-64` for a 64-bit architecture.

9.  Leave the **Minimum Disk (GB)** and **Minimum RAM (MB)** fields
    empty.

10. Check the **Public** box to make the appliance available to all
    users.

11. Check the **Protected** box to protect the image from being
    accidentally deleted.

12. Click **Create Image**.

You have successfully uploaded the ManageIQ appliance.

The appliance image is placed in a queue to be uploaded. It may take
some time before the Status of the image changes from Queued to Active.

## Adding a Rule to a Security Group

Security groups specify what IP traffic is allowed to reach an instance
on its public IP address. Security group rules are processed before
network traffic reaches firewall rules defined within the guest itself.

<div class="note">

In the default configuration, the default security group accepts all
connections from the default source; all instances within the default
group can talk to each other on any port.

</div>

1.  From the OpenStack dashboard, navigate to
    <span class="menuchoice">Project \> Compute \> Access &
    Security</span>.

2.  Navigate to <span class="menuchoice">Security Groups \> Manage
    Rules</span> on the row for the default security group.
    ![7216](images/7216.png)

3.  Click **Add Rule**. ![4941](images/4941.png)

4.  Configure the rule.
    
    1.  Select <span class="menuchoice">Rule \> Custom TCP Rule</span>.
    
    2.  Select <span class="menuchoice">Direction \> Ingress</span>.
    
    3.  Select **Port** from the **Open Port** list.
    
    4.  Specify `443` in the **Port** field.
    
    5.  Select **CIDR** from the **Remote** list.
    
    6.  Specify `0.0.0.0/0` in the **CIDR** field.
    
    7.  Click **Add**.

## Creating a Custom Flavor

A flavor is a resource allocation profile that specifies, for example,
how many virtual CPUs and how much RAM can be allocated to an instance.
You can, for example, run ManageIQ on a Red Hat OpenStack m1.large
flavor, which specifies a virtual machine with 4 cores, 12 GB RAM, and
80 GB disk space. Creating a flavor to run ManageIQ is optional.

The following procedure demonstrates creating a flavor with the minimum
requirements (4 cores, 12 GB RAM, 44 GB disk space) for ManageIQ. For
more information about flavors, see the Red Hat OpenStack Platform
Administration User Guide.

1.  Log in to the OpenStack dashboard as admin.

2.  In the **Admin** tab, navigate to <span class="menuchoice">System \>
    Flavors</span>.

3.  Click **Create Flavor** to display the **Create Flavor** dialog.

4.  Configure the settings to define a flavor that meets ManageIQ system
    requirements.
    
    1.  Enter a name for the flavor.
    
    2.  Enter the following settings:
        
          - **VCPUs**: 4
        
          - **RAM MB**: 12288
        
          - **Root Disk GB**: 70
        
          - **Ephemeral Disk GB**: 0
        
          - **Swap Disk MB**: 0

5.  Click **Create Flavor**.

A new flavor specific to ManageIQ is created.

## Launching the Instance

1.  From the OpenStack dashboard, navigate to
    <span class="menuchoice">Project \> Compute \> Instances</span>.

2.  Click **Launch Instance**.

3.  Enter a name for the instance.

4.  Select the custom flavor for your instance. The flavor selection
    determines the computing resources available to your instance. The
    resources used by the flavor are displayed in the **Flavor Details**
    pane.

5.  Enter **1** in the **Instance Count** field.

6.  Select a boot option from the **Instance Boot Source** list:
    
      - **Boot from image** - displays a new field for **Image Name**.
        Select the image from the drop-down list.
    
      - **Boot from snapshot** - displays a new field for **Instance
        Snapshot**. Select the snapshot from the drop-down list.
    
      - **Boot from volume** - displays a new field for **Volume**.
        Select the volume from the drop-down list.
    
      - **Boot from image (creates a new volume)** - boot from an image
        and create a volume by choosing **Device Size** and **Device
        Name** for your volume. Some volumes can be persistent. To
        ensure the volume is deleted when the instance is deleted,
        select **Delete on Terminate**.
    
      - **Boot from volume snapshot (creates a new volume)** - boot from
        volume snapshot and create a new volume by choosing **Volume
        Snapshot** from the drop-down list and adding a **Device Name**
        for your volume. Some volumes can be persistent. To ensure the
        volume is deleted when the instance is deleted, select **Delete
        on Terminate**.

7.  Click **Networking** and select a network for the instance by
    clicking the **+** (plus) button for the network from **Available
    Networks**.

8.  Click **Launch**.

## Adding a Floating IP Address

When you create an instance, Red Hat OpenStack Platform automatically
assigns it a fixed IP address in the network to which the instance
belongs. This IP address is permanently associated with the instance
until the instance is terminated.

In addition to the fixed address, you can also assign a floating IP
address to an instance. Unlike fixed IP addresses, you can modify
floating IP addresses associations at any time, regardless of the state
of the instances involved.

1.  At the command-line on your RHEL OpenStack Platform host, create a
    pool of floating IP addresses using the `nova-manage floating
    create` command. Replace **IP\_BLOCK** with the desired block of IP
    addresses expressed in CIDR notation.
    
        $ nova-manage floating create IP_BLOCK

2.  In the **Project** tab, navigate to <span class="menuchoice">Compute
    \> Access & Security</span>.

3.  Click <span class="menuchoice">Floating IPs \> Allocate IP To
    Project</span>. The **Allocate Floating IP** window is displayed.
    ![7218](images/7218.png)

4.  Click **Allocate IP** to allocate a floating IP from the pool. The
    allocated IP address appears in the **Floating IPs** table.

5.  Select the newly allocated IP address from the **Floating IPs**
    table. Click **Associate** to assign the IP address to a specific
    instance. ![7217](images/7217.png)

6.  Select an instance with which to associate the floating IP Address.

7.  Click **Associate** to associate the IP address with the selected
    instance.

<div class="note">

To disassociate a floating IP address from an instance when it is no
longer required, click **Release Floating IPs**.

</div>

# Configuring ManageIQ

After installing ManageIQ and running it for the first time, you must
perform some basic configuration. To configure ManageIQ, you must at a
minimum:

1.  Add a disk to the infrastructure hosting your appliance.

2.  Configure the database.

Configure the ManageIQ appliance using the internal appliance console.

## Accessing the Appliance Console

1.  Start the appliance and open a terminal console.

2.  After starting the appliance, log in with a user name of `root` and
    the default password of `smartvm`. This displays the Bash prompt for
    the `root` user.

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

2.  After starting the appliance, log in with a user name of `root` and
    the default password of `smartvm`. This displays the Bash prompt for
    the `root` user.

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

2.  After starting the appliance, log in with a user name of `root` and
    the default password of `smartvm`. This displays the Bash prompt for
    the `root` user.

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

2.  After starting the appliance, log in with a user name of `root` and
    the default password of `smartvm`. This displays the Bash prompt for
    the `root` user.

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
