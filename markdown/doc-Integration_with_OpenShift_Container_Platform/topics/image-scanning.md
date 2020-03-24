# Configuring Image Scanning

{product-title} manages vulnerability scanning of container images. When
an OpenShift provider is added, OpenShift images from the internal
registry are discovered. To enable image scanning, perform the following
configuration steps:

1.  Navigate to menu:Compute\[Containers \> Providers\].

2.  Select the checkboxes of the OpenShift providers on which to enable
    scanning.

3.  From the **Policy** pull-down menu, click **Manage Policies**.

4.  Select the **OpenSCAP profile** checkbox.

5.  Click **Save**.

This action will trigger a SmartState analysis, or scan, of all images
referenced by the OpenShift provider. The initial scan may take several
hours to complete, depending on the number and size of images. The scan
occurs in the OpenShift provider, which {product-title\_short} receives
and records in the database. OpenShift limits the number of scanning
pods; only three images can be scanned simultaneously.

# Scheduling A Recurring Scan

Software vulnerability databases are updated frequently. To apply these
updates, a rescan is required. To schedule a recurring scan of container
images:

![schedule openscap scan](schedule_openscap_scan.png)

1.  Click ![config gear](config-gear.png) (**Configuration**).

2.  From menu:Settings\[Zones\] in the left pane of the appliance,
    select **Schedules**.

3.  From the drop-down menu, click menu:Configuration\[Add a new
    Schedule\].

4.  Type an arbitrary **Name**.

5.  Type an arbitrary **Description**.

6.  Ensure the **Active** checkbox is selected.

7.  In **Action**, select **Container Image Analysis**.

8.  In **Filter**, select **All Container Images for Containers
    Provider**, **OpenShift**.

9.  In **Run**, set the schedule as desired.

10. Set the **Time Zone**, **Starting Date**, and **Starting Time**.

11. Click **Add**.

# Working with Images

## Viewing Results

Image scanning results are displayed in each image summary page.

1.  Select menu:Compute\[Containers \> Container Images\].

2.  Click the desired image.

For an OpenSCAP HTML report, locate the **Configuration** section and
select **OpenSCAP HTML**.

![container configuration](container_configuration.png)

For compliance and scanning history information, locate the
**Compliance** section and note the **Status** field or select
**Available** from the **History** field.

![container scan history](container_scan_history.png)

## Manual Scanning

SmartState analysis scanning may be initiated manually for images. From
an image summary page, select menu:Configuration\[Perform SmartState
Analysis\]. Refreshing the image page will reflect the latest scan
results and compliance history.

## Evaluating Compliance

If the image scan policy has been updated since the last scan,
compliance conditions may be re-evaluated. From an image summary page,
select menu:Policy\[Check Compliance of Last Known Configuration\].
Refreshing the image page will reflect the latest compliance history.

## Generating a Report on Images

You can output the results of an OpenSCAP scan of images to a report for
an overview of the security risk level of images. The **Images by Failed
OpenSCAP Rule Results** is included with {product-title\_short} and
shows whether the image has passed or failed OpenSCAP policy criteria,
and the security risk.

<div class="note">

You can also create a copy of this report and edit it to contain
additional information, such as the project name where the image is
used, to produce more useful results. See [Editing a
Report](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/monitoring_alerts_and_reporting/#editing-a-report)
and See [Reportable Fields in
{product-title}](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/monitoring_alerts_and_reporting/#appe_reportable_fields)
in *Monitoring, Alerts, and Reporting* for instructions on customizing
reports.

</div>

To create a report showing image compliance:

1.  Navigate to menu:Overview\[Reports\].

2.  Click the menu:Reports\[All Reports\] accordion.

3.  Navigate to menu:Configuration Management\[Containers \> Images by
    Failed OpenSCAP Rule Results\] for a report showing which images
    have failed the OpenSCAP compliance.

4.  Click ![play arrow](play_arrow.png) **Queue**.

5.  The report generation is placed in the queue and its status shows in
    the reports page.
    
    ![failedimagescan](failedimagescan.png)

6.  Click ![reload](reload.png) **(Refresh this page)** to update the
    status.

7.  Navigate to the **Saved Reports** accordion, and click the report
    when it is completed.

8.  Click on the report download buttons for the type of export you
    want. The report is automatically named with the type of report and
    date.
    
      - Click ![textImage](textImage.png) **(Download this report in
        text format)** to download as text.
    
      - Click ![textImage](textImage.png) **(Download this report in CSV
        format)** to download as a comma-separated file.
    
      - Click ![2134](2134.png) **(Download this report in PDF format)**
        to download as PDF.

# OpenSCAP Policy Profile

{product-title} is pre-configured with a default scanning policy
profile. This includes conditions to scan and identify compliance, as
well as annotate compliance failure. SmartState analysis is performed
when new images are added to OpenShift.

## Customizing the Scanning Policy Profile

The built-in OpenSCAP policy profile cannot be edited. You can, however,
assign *edited* copies of its policies to a new policy profile. This
will allow you to create a customized version of the built-in OpenSCAP
policy profile.

To do so, you will first have to copy the policy you want to customize:

1.  Navigate to menu:Control\[Explorer\].

2.  Click the **Policies** accordion, and select **Container Image
    Compliance Policies**, then click **OpenSCAP**.

3.  Click ![image](../images/1847.png)(**Configuration**), and an option
    to copy the policy should appear; for example,
    ![image](../images/1859.png) (**Copy this Container Image Policy**).

4.  Click **OK** to confirm.

The new policy is created with a prefix of **Copy of** in its
description, and it can be viewed in the Policies accordion.

![image](../images/1860-cppolicy.png)

You can now edit the copied policy. After editing copied policies, you
can add them to a new policy profile. For instructions on how to edit
policies, create a new policy profile, and add policies to it, see the
[Policies and
Profiles](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/policies_and_profiles_guide)
guide. Once you have a customized policy profile, you can assign it to a
containers provider.

# Controlling OpenShift Pod Execution

Through the default policy profile, non-compliant images receive the
control policy action **Mark as Non-Compliant**. This action annotates
the **image** object (not to be confused with the **imagestream**
object) with *images.openshift.io/deny-execution=true*. This annotation
may be used to prevent nodes from running non-compliant images.

# Reference

More information about OpenSCAP, see visit the [OpenSCAP web
site](https://www.open-scap.org/).
