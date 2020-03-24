{product-title} provides a large group of default reports organized into
categories. Each category has its own set of subfolders. These reports
have been constructed to help you view the most commonly requested and
significant data.

The categories of predefined reports available on {product-title} are:

  - **Configuration Management**: hardware, application, network,
    service, user account, operating system, and snapshot information
    for all of your items.

  - **Migration Readiness**: information related to items required to
    migrate a virtual machine.

  - **Operations**: free space on registered and unregistered virtual
    machines, power states for virtual machines, and SmartState analysis
    status.
    
    This category also provides reports relating to the operation of
    {product-title}, such as user IDs and snapshots taken by
    {product-title}.

  - **VM Sprawl**: usage information and disk waste.

  - **Relationships**: virtual machine, folder, and cluster
    relationships.

  - **Events**: operations and configuration management events.

  - **Performance by Asset Type**: performance of your virtual
    infrastructure.
    
    You must be capturing capacity and utilization data to get this
    information.

  - **Running Processes**: information on processes running on a virtual
    machine.
    
    You must have domain credentials entered for the zone to collect the
    information for these reports, and the virtual machine must have
    been analyzed at least once.

  - **Trending**: projections of datastore capacity, along with host CPU
    and memory use.

  - **Tenants**: quotas report aggregated by each tenant that shows
    quota name, total quota, in use, allocated, and available. The
    report currently lists all tenants and there is no nesting
    information available by parent and child tenants.

  - **Provisioning**: provisioning activity based on the approver,
    datastore, requester, and virtual machine.

For more detailed information on managing reports, see [Monitoring,
Alerts, and
Reporting](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.7/single/monitoring-alerts-and-reporting/).

# Generating a Single Report

1.  Navigate to menu:Overview\[Reports\]

2.  Click the **Reports** accordion and select the report you want to
    view.

3.  Click ![1847](1847.png) (**Queue**).

4.  The report generation is placed on the queue and its status shows in
    the reports page.
    
    ![2274](2274.png)

5.  Click ![2106](2106.png) **(Reload current display)** to update the
    status.

6.  When a report has finished generating, click on its row to view it.

# Scheduling a Report

You can view historical data by creating reports on a scheduled basis.
In addition, scheduled reports can be emailed directly to users:

1.  Navigate to menu:Overview\[Reports\]

2.  Click the **Reports** accordion and select the report you want to
    view.

3.  Click ![1847](1847.png) (**Configuration**), then **Add a new
    Schedule**.

4.  Fill in the **Basic Information** section.

5.  Configure the **Report Selection**.

6.  Configure the report’s schedule and frequency in the **Timer**
    section.

7.  Click **Save**.

# Viewing Reports

Once you have created a schedule for a report, you can view it at any
time after the first scheduled time has occurred.

1.  Navigate to menu:Overview\[Reports\].

2.  Click the **Saved Reports** accordion or the **Reports** accordion.

3.  Click on the instance of the report you want to view.
