The *chargeback* feature allows you to calculate monetary virtual
machine charges based on owner or company tag. To use this feature you
must be collecting capacity and utilization data. For information on
server control settings and capacity & utilization collection settings,
see [???](#cf-caputils).

# Creating Chargeback Rates

{product-title} allows you to create your own set of computing and
storage costs to use for billing.

Chargeback rates can be configured at a single rate or in tiers, where
one rate is assigned to one usage range, and another rate is assigned to
a different usage range. You can also assign fixed and variable rates
per tier if desired.

1.  Navigate to menu:Overview\[Chargeback\].

2.  Click the **Rates** accordion and select **Compute** to create a CPU
    chargeback rate.

3.  Click ![1847](1847.png) **(Configuration)** and ![1862](1862.png)
    **(Add a new Chargeback Rate)**.

4.  Type in a **Description** for the chargeback rate.

5.  Select **Currency** and fill in the **Rate Details**.
    
    ![chargeback rate details](chargeback-rate-details.png)

6.  Click **Add**.

# Assigning Chargeback Rates

After assigning a chargeback rate, assign it to a cloud provider.

1.  Navigate to menu:Overview\[Chargeback\].

2.  Click the **Assignments** accordion, and click either **Compute** or
    **Storage**.

3.  In the **Basic Info** area, select **Selected Cloud/Infrastrcture
    Providers**.

4.  Select the chargeback rate you created in [Creating Chargeback
    Rates](#_to_create_chargeback_rates).

5.  Click **Save**.

# Creating a Chargeback Report

{product-title} allows you to create chargeback reports to monitor costs
you charged.

1.  Navigate to menu:Overview\[Reports\].

2.  Click the **Reports** accordion.

3.  Click ![1847](1847.png)**(Configuration)**, ![1862](1862.png) **(Add
    a new Report)**.

4.  On the **Columns** tab, fill out the **Basic Report Info** area.
    
      - Type a unique name in **Menu Name** for how you want the report
        described in the menu list.
    
      - Type the **Title** to display on the report.

5.  Add fields in the **Configure Report Columns** area.
    
      - From the **Base the report on** list, select **Chargebacks**.
    
      - Select the fields to include in the report from the **Available
        Fields** list, then click ![2289](2289.png) **(Move selected
        fields down)**. In addition to the fields, you can also select
        any tags that you have created and assigned.
    
      - Change the order of the fields in the report by clicking
        ![2290](2290.png) **(Move selected fields up)** or
        ![2289](2289.png) **(Move selected fields down)\]**.

6.  Click the **Formatting** tab to set the size of paper for a PDF and
    column header format.
    
      - From the **PDF Output** area, select the page size from the
        **Page Size** list.
    
      - From **Specify Column Headers and Formats**, type the text to
        display for each field. For each numeric field, you can also set
        the numeric format.

7.  Click the **Filter** tab to set filters for the data displayed in
    the report.
    
      - From **Chargeback Filters**, select how you want the costs to
        show, the tag category, the tag, and how you want the items
        grouped.
    
      - From **Chargeback Interval**, select the time interval. You must
        have a full interval worth of data in order to select an option
        other than **Partial** in the **Daily Ending With** list.

8.  Click the **Preview** tab, and then **Load** to see what the report
    will look like.

9.  When you are satisfied that you have the report that you want, click
    **Add** to create the new report.

The new report is created. To make the report accessible from the
**Report** menu, you must add it to a report menu.
