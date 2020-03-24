Before attempting a large migration, you should perform several test
migrations with different maximum numbers of concurrent migrations for
your conversion hosts or providers. This will enable you to assess the
capabilities of your environment’s infrastructure.

1.  Click **Compute** → **Migration** → **Migration Plans**.

2.  Click **Create Migration Plan**. The **Create Migration Plan**
    wizard is displayed.
    
    ![Create Migration Plan screen](Create_Migration_Plan_screen.png)

3.  In the **General** screen, add the details of the migration plan:
    
    1.  Select an infrastructure mapping from the drop-down list.
    
    2.  Enter the migration plan **Name** and (optional)
        **Description**.
    
    3.  Select a virtual machine discovery method:
        
          - **Choose from a list of VMs discovered in the selected
            infrastructure mapping**
            
            If the virtual machines cannot be discovered, check that the
            source datastores and networks in the infrastructure mapping
            are correct.
        
          - **Import a CSV file with a list of VMs to be migrated**.
            
            A CSV file is required for previously migrated source
            virtual machines and recommended for large migrations.
    
    4.  Click **Next**.

4.  In the **VMs** screen, select the virtual machines for migration:
    
      - If you selected **Choose from a list of VMs discovered in the
        selected infrastructure mapping**, select the virtual machines
        for migration.
        
        You can search for virtual machines by **VM Name**, **Data
        Center**, **Cluster**, and **Folder**.
    
      - If you selected **Import a CSV file with a list of VMs to be
        migrated**:
        
        1.  Click **Import**.
        
        2.  Browse to the CSV file and click **Open**.
            
            If the virtual machines cannot be added to the migration
            plan, check the CSV file format and fields for errors.
            
            <div class="note">
            
            If the **Create Migration Plan** wizard freezes, refresh the
            web page, check the CSV file for errors (for example,
            virtual machines with duplicate `Name` fields and no other
            fields to distinguish them), and create a new migration
            plan.
            
            </div>
        
        3.  Click **Next**.

5.  In the **Advanced Options** screen, select the playbook service
    options:
    
    1.  Select a premigration and/or postmigration playbook service from
        the dropdown lists.
    
    2.  Select the virtual machines on which to run the playbook
        services.
    
    3.  Click **Next**.

6.  In the **Schedule** screen, select a schedule option and click
    **Create**:
    
      - **Save migration plan to run later**
        
        The migration plan is saved in **Migration Plans Not Started**
        and will not run unless you
        [schedule](#Scheduling_a_saved_migration_plan_{context}) it or
        click **Migrate** to run the scheduled migration plan
        immediately.
    
      - **Start migration immediately**
        
        The migration plan may take some time to complete. Progress bars
        indicate the amount of transferred data, the number of migrated
        virtual machines, and the elapsed time. You can [view a
        migration plan’s
        progress](#Viewing_migration_plan_progress_{context}) or [cancel
        a migration plan in
        progress](#Canceling_a_migration_plan_{context}).

7.  In the **Results** screen, click **Close**.
    
    When the migration plan has finished, click **Migration Plans
    Complete** to view the status of the migration plan. The completed
    migration plan shows the status of the migrated virtual machines.

In the migration plans list, you can click the **More Actions** icon
(![7](More_actions_icon.png)) to archive, edit, or delete a migration
plan.

If a migration fails because of external circumstances (for example,
power outage), you can [retry the migration
plan](#Retrying_a_failed_migration_plan_{context}).

# Scheduling a saved migration plan

To schedule a saved migration plan to run in the future:

1.  Click **Migration Plans Not Started**.

2.  Click the **Schedule** button of a migration plan.

3.  In the **Schedule Migration Plan** window, select a date and time
    and click **Schedule**.
    
    The plan’s status is **Migration Scheduled** with the date and time.

# Viewing a migration plan in progress

To view the progress of a migration plan:

1.  Click **Migration Plans in Progress**.

2.  Click a migration plan name to view its details, including the
    status of the migrating virtual machines.
    
    <div class="note">
    
    The counter in **Compute** → **Migration** → **Migration Plans** may
    be a few seconds ahead of the counter in the migration plan details
    view.
    
    The **Migration Plans** counter displays the total time for running
    the migration plan. The migration plan details counter displays the
    time for migrating the virtual machines.
    
    </div>

# Canceling a migration plan in progress

To cancel a migration plan in progress:

1.  Click **Migration Plans in Progress**.

2.  Select a migration plan and click **Cancel Migration**.

3.  Click **Cancel Migrations** to confirm the cancellation.
    
    The canceled migration appears in **Migration Plans Complete** with
    a red `x` indicating that the plan did not complete successfully.

# Retrying a failed migration plan

To retry a migration plan that failed because of external circumstances
(for example, power outage):

1.  Delete all objects created by the failed migration plan:

2.  Click **Compute** → **Migration** → **Migration Plans**.

3.  Click **Migration Plans Complete**.

4.  Click the **Retry** button beside the failed migration plan.
