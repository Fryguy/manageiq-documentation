Unresolved directive in index.adoc -
include::topics/installation.adoc\[\]

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

Unresolved directive in index.adoc -
include::topics/additional\_configuration.adoc\[\]

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
