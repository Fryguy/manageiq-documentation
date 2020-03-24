# Clusters

Clusters provide high availability and load balancing for a group of
hosts. The **Clusters** page under <span class="menuchoice">Compute \>
Infrastructure</span> displays the clusters discovered in your
enterprise environment.

<div class="note">

Any filter applied will be in effect here.

</div>

![2202](images/2202.png)

Use the **Clusters Taskbar** to manage the analysis and tagging of your
clusters. These buttons manage multiple clusters at one time. To manage
one cluster, click on that cluster in the main area of the screen.

## Performing SmartState Analysis on Clusters

Analyze a cluster to gather historical data to compare with previous
points in time.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Clusters</span>.

2.  Check the clusters to analyze.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1942](images/1942.png) (**Perform SmartState Analysis**).

4.  Click **OK**.

The SmartState Analysis begins and returns the current data.

## Comparing Clusters

ManageIQ provides features to compare properties of clusters.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Clusters</span>.

2.  Check the clusters to compare.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2148](images/2148.png) (**Compare Selected items**). The
    comparison displays in a default expanded view and lists a limited
    set of properties.
    
    ![2203](images/2203.png)

4.  To delete a cluster from the comparison, click
    ![1861](images/1861.png)(**Remove this Cluster from the
    Comparison**).

5.  To go to a compressed view, click ![2024](images/2024.png)
    (**Compressed View**). To return to an expanded view, click
    ![2023](images/2023.png) (**Expanded View**).

6.  To change the base cluster that all other clusters compare to, click
    its label at the top of its column.

7.  To go to the cluster summary screen, click its virtual thumbnail or
    icon.

8.  There are three buttons in the taskbar to limit the type of views:
    
      - Click ![2178](images/2178.png) (**All attributes**) to see all
        attributes.
    
      - Click ![2204](images/2204.png) (**Attributes with different
        values**) to see only the attributes that are different across
        clusters.
    
      - Click ![2148](images/2148.png) (**Attributes with the same
        values**) to see only the attributes that are the same across
        clusters.

9.  To limit the mode of the view, there are two taskbar buttons.
    
      - Click ![2022](images/2022.png) (**Details Mode**) to see all
        details for an attribute.
    
      - Click ![2025](images/2025.png) (**Exists Mode**) to only see if
        an attribute exists compared to the base or not. This only
        applies to attributes that can have a Boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

This creates a comparison between clusters. Export this data or create a
report from your comparison for analysis using external tools.

### Creating a Cluster Comparison Report

Create a quick report of to compare clusters in CSV, TXT, or PDF
formats.

1.  Create the comparison to analyze.

2.  Click ![2107](images/2107.png) (**Download**).

3.  Click the output button for the type of report.
    
      - Click ![2133](images/2133.png) (**Download comparison report in
        TXT format**) for a text file.
    
      - Click ![2133](images/2133.png) (**Download comparison report in
        CSV format**) for a comma-separated file.
    
      - Click ![2134](images/2134.png) (**Download comparison report in
        PDF format**) for a PDF file.

## Viewing a Cluster

You can click on a specific cluster to view its details. The screen
provides you with a cluster taskbar, a cluster accordion, and a cluster
summary.

**Cluster Management Screen.**

![2206](images/2206.png)

1.  **Cluster Taskbar**: Choose between **Configuration**, **Policy**
    and **Monitoring** options for the selected cluster

2.  **Cluster Summary**: See cluster summary such as **Relationships**,
    **Totals for Hosts**, **Totals for VMs**

3.  **Cluster Summary Views**: Choose between graphical or text view of
    the cluster summary

4.  **Cluster Summary PDF**: Generates cluster summary in PDF format

5.  **Cluster Accordion**: See details about **Properties**,
    **Relationships**, **Storage Relationships** for the selected
    cluster

## Tagging Clusters

Use tags to categorize clusters.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Clusters</span>.

2.  Check the Clusters to tag.

3.  Click ![1941](images/1941.png) (**Policy**), and then
    ![1851](images/1851.png) (**Edit Tags**).
    
    ![2205](images/2205.png)

4.  Select a customer tag from the first dropdown, and then a value for
    the tag.

5.  Select more tags or click **Save** to save your changes.

## Viewing Capacity and Utilization Charts for a Cluster

View capacity and utilization for a cluster.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Clusters</span>.

2.  Click the cluster to view Capacity and Utilization data.

3.  Click ![1994](images/1994.png) (**Monitoring**), and then
    ![1994](images/1994.png) (**Utilization**) or from the accordion
    menu, click <span class="menuchoice">Properties \> Capacity &
    Utilization</span>.
    
    ![2208](images/2208.png)

4.  From **Interval**, select to view hourly or daily data points and
    the dates to view data. Use **Group by** to group the lines by
    SmartTags. Use **Time Profiles** to select a time range for the
    data.

![2209](images/2209.png)

The **Capacity & Utilization** charts display

<div class="note">

Daily charts only include full days of data. If a day does not include
all the 24 data points for a day, the data does not show for that day.

</div>

For information about data optimization including utilization trend
reports, see [Data Optimization](#data-optimization).

## Viewing Cluster Timeline

Use the cluster timeline to see a graphical depiction of operational and
configuration events over time.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Clusters</span>.

2.  Click the cluster to view the timeline.

3.  Click ![1994](images/1994.png) (**Monitoring**), and then
    ![1994](images/1994.png) (**Timelines**) or from the accordion menu,
    click <span class="menuchoice">Properties \> Timelines</span>.

4.  From **Options**, customize the period of time to display, and the
    types of events to see.
    
    ![2210](images/2210.png)
    
      - Use the **Interval** dropdown to select hourly or daily data
        points.
    
      - Use **Date** to type the date for the timeline to display.
    
      - If you select to view a daily timeline, use **Show** to set how
        many days back to go. The maximum history is 31 days.
    
      - The three **Event Group** dropdowns allow the selection of
        different groups of events to display. Each has its own color.
    
      - From the **Level** dropdown, select a **Summary** event if
        needed, or a **Detail** list of events. For example, the detail
        level of a *Power On* event might include the power on request,
        the starting event, and the actual **Power On** event. If you
        select **Summary**, the timeline only displays the Power On
        event.

5.  To see more detail on an item in the timeline, click on it. A
    balloon appears with a clickable link to the resource.

## Detecting Drift on Clusters

Over time, a cluster’s configuration might change. Drift is the
comparison of a cluster to itself at different points in time. The
cluster requires analysis at least twice to collect information.
Detecting drift provides users with the following benefits:

  - See the difference between the last known state of a cluster and its
    current state

  - Review the configuration changes that happen to a particular cluster
    between multiple points in time.

  - Capture the configuration drifts for a single cluster across a time
    period.

Detect drift on clusters:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Clusters</span>.

2.  Click on the cluster to view drift.

3.  Click **Relationships** in the cluster accordion.

4.  Click **Drift History**.

5.  Check the analyses to compare.

6.  Click ![1946](images/1946.png) (**Drift Analysis**) at the top of
    the screen. The results are displayed.

7.  Check the **Comparison** sections on the left to view in your
    comparison.

8.  Click the plus sign next to the section name to expand it.
    
      - An item displayed on red text shows a change from the base
        analysis. An item displayed in black text shows no change from
        the base analysis.
    
      - A ![2177](images/2177.png) (**Changed from previous**) shows
        there has been a change since the last analysis.
    
      - A ![2150](images/2150.png) (**Same as previous**) means there
        has been no change since the last analysis.
    
      - Click ![1861](images/1861.png) (**Remove from drift**) at the
        bottom of a column to remove a specific analysis. The drift is
        then recalculated and the new results display.

9.  Click ![2023](images/2023.png) (**Expanded View**) to see the
    expanded view. Click ![2024](images/2024.png) (**Compressed
    View**)\] to compress the information.

10. Click the minus sign next to the section name to collapse it.

11. To limit the type of views, there are three buttons in the taskbar.
    
      - Click ![2178](images/2178.png) (**All attributes**) to see all
        attributes of the sections selected.
    
      - Click ![2204](images/2204.png) (**Attributes with different
        values**) to see only the attributes different across drifts.
    
      - Click ![2148](images/2148.png) (**Attributes with the same
        values**) to see only the attributes the same across drifts.

The drift displays for your cluster. Download the data or create a
report from the drift for analysis using external tools.

## Creating a Drift Report for Clusters

Use the drift report feature to export information about your cluster’s
drift.

1.  Create a drift of a cluster.

2.  Click ![2107](images/2107.png) (**Download**).

3.  Click the output button for the type of report you want.
    
      - Click ![2133](images/2133.png) (**Download drift report in TXT
        format**) for a text file.
    
      - Click ![2133](images/2133.png) (**Download drift report in CSV
        format**) for a comma-separated file.
    
      - Click ![2134](images/2134.png) (**Download drift report in PDF
        format**) for a PDF file.

## Removing Clusters

If a cluster has been decommissioned or requires troubleshooting, it
might require removal from the VMDB.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Clusters</span>.

2.  Check the clusters to remove.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1861](images/1861.png) (**Remove Clusters from the VMDB**).

4.  Click **OK**.

The clusters are deleted. Any virtual machines or hosts associated with
these clusters remain, but are no longer associated with them.

# Hosts

The **Hosts** page under <span class="menuchoice">Compute \>
Infrastructure</span> displays the hosts discovered in your enterprise
environment.

<div class="note">

Any applied filters will be in effect here.

</div>

![2212](images/2212.png)

After adding or sorting your hosts, click on one to examine it more
closely and see its virtual machines, SmartProxy settings, and
properties.

![2222](images/2222.png)

1.  Top left quadrant: Number of virtual machines on this host

2.  Bottom left quadrant: Virtual machine software

3.  Top right quadrant: Power state of host

4.  Bottom right quadrant: Authentication status

| Icon                     | Description                                                                    |
| ------------------------ | ------------------------------------------------------------------------------ |
| ![2190](images/2190.png) | Validated: Valid authentication credentials have been added.                   |
| ![2191](images/2191.png) | Invalid: Authentication credentials are invalid                                |
| ![2192](images/2192.png) | Unknown: Authentication status is unknown or no credentials have been entered. |

## Filtering Hosts

The Host Filter accordion is provided to easily navigate through the
hosts. Use the ones provided or create your own. In addition, you can
set a default filter.

### Setting a Default Host Filter

Set the default filter for viewing your hosts.

1.  From the **Filters** accordion on the left, click on the filter to
    use.

2.  Click **Set Default** at the top of the filters list.

The default filter is set and marked by a green star next to its name.

### Creating a Host Filter

Create a filter for viewing your hosts.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click ![2125](images/2125.png) (**Advanced Search**) to open the
    expression editor.

3.  Use the expression editor to choose the appropriate options for your
    criteria.

4.  Click **Save**.

5.  Type in a name for the search expression in **Save this search as**.
    
    <div class="note">
    
    This title depends on the type of resource you are searching.
    
    </div>

6.  Click **Save**.

The filter is saved and displays in the **My Filters** area of the
**Filter** accordion.

## Performing SmartState Analysis on Hosts

Perform a SmartState analysis on a host to collect additional
information about it, such as patches, CPU, and memory.

<div class="note">

  - SmartState analysis on hosts is processed by the **Provider
    Operations** role. It is enabled by default.

  - For ESX or ESXi hypervisors, consider the following: ESX hosts
    utilize a service console for host management and can be accessed
    using SSH. ESXi hosts lack a service console and therefore SSH
    cannot be used to obtain information sets for patches, services,
    Linux packages, user groups, SSH Config, and FS Files.

  - `root` or administrator credentials are required to get patch
    information.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Check the hosts to analyze.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1942](images/1942.png)(**Perform SmartState Analysis**).

4.  Click **OK**.

## Comparing Hosts

ManageIQ allows you to compare hosts and check operating systems, host
software and version information, and hardware.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Check the hosts to compare.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2148](images/2148.png) (**Compare selected Hosts**). The
    comparison displays in a default expanded view, which lists a
    limited set of properties.

4.  To remove a host from the comparison, click ![1861](images/1861.png)
    (**Remove this Host from the comparison**) at the bottom of the
    column.

5.  To go to a compressed view, click ![2024](images/2024.png)
    (**Compressed View**). To return to an expanded view, click
    ![2023](images/2023.png) (**Expanded View**).

6.  To limit the mode of the view, there are two buttons in the taskbar.
    
      - Click ![2022](images/2022.png) (**Details Mode**) to see all
        details for an attribute.
    
      - Click ![2025](images/2025.png) (**Exists Mode**) to limit the
        view to if an attribute exists compared to the base or not. This
        only applies to attributes that can have a Boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

7.  To change the base host that compare to the other hosts, click its
    label at the top of its column.

8.  To go to the summary screen for a host, click its virtual thumbnail
    or icon.

### Host Comparison Sections

| Section         | Description                                                                                                                     |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Host Properties | Use this section to see basic information of the host, such as hostname, product, build number, hardware, and network adapters. |
| Security        | Use this to see users and groups for the host, and firewall rules.                                                              |
| Configuration   | Use this to see the operating system, applications, services, patches, vSwitches, vLANS, and advanced settings.                 |
| My Company Tags | Use this to see all tags.                                                                                                       |

### Using the Host Comparison Sections

The following procedure describes how to use the host comparison
sections.

1.  On the left of a comparison screen, select the categories of
    properties to display.

2.  Click the plus sign next to the sections name to expand it.

3.  The following descriptions pertain to the **Expanded View**
    ![2023](images/2023.png). Either the value of a property or an icon
    representing the property displays depending on the properties type.
    
      - A property displayed in the same color as the base means that
        the compared host matches the base for that property.
    
      - A property displayed in a different color from the base means
        that the compared host does not match the base for that
        property.

4.  If you are in the **Compressed View** ![2024](images/2024.png), the
    values of the properties do not display. All items are described by
    the icons shown below.
    
      - A ![2150](images/2150.png) (**checkmark**) means the compared
        host matches the base for that property. Hover over it and the
        value of the property displays.
    
      - A ![2151](images/2151.png) (**x**) means the compared host does
        not match the base for that property. Hover over it and the
        value of the property displays.

5.  Click the plus sign next to the section name to collapse it.

This comparison is viewable in multiple ways. Export the data or create
a report from your comparison for analysis using external tools.

### Creating a Host Comparison Report

Create a quick report to compare clusters in CSV, TXT, or PDF formats.

1.  Create the comparison to analyze.

2.  Click ![2107](images/2107.png) (**Download**).

3.  Click the output button for the type of report.
    
      - Click ![2133](images/2133.png) (**Download comparison report in
        TXT format**) for a text file.
    
      - Click ![2133](images/2133.png) (**Download comparison report in
        CSV format**) for a comma-separated file.
    
      - Click ![2134](images/2134.png) (**Download comparison report in
        PDF format**) for a PDF file.

## Refreshing Multiple Hosts

Manually refresh a host for its properties and related infrastructure
components.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Check the hosts to refresh.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2003](images/2003.png) (**Refresh Relationships and Power
    States**).

4.  Click **OK**.

When a host is refreshed and a new virtual machine is discovered on that
host, ManageIQ checks to see if the virtual machine is already
registered with another host. If this is the case, the host that the
virtual machine is associated with switches to the new host. If the
SmartProxy is monitoring a provider, this happens automatically. If not,
the next refresh of the host addresses this.

## Discovering Multiple Hosts

If not using a provider, use ManageIQ’s Discovery to find hosts in your
environment within a range of IP addresses.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1942](images/1942.png) (**Discover items**).

3.  Check the types of hosts to discover: `ESX` or `IPMI`.

4.  Type in a range of **IP Addresses**.
    
    ![2213](images/2213.png)

5.  Click **Start**.

ManageIQ searches for the supported hosts. When available, the new hosts
display. They are named by hostname and IP address. To make them
identifiable, edit the basic information for each host.

## Adding a Single Host

To analyze a host for more detailed information, add it to the VMDB
first. If the host has not been found during **Host Discovery** or
**Provider Refresh**, and the host’s IP address is known, use the **Add
a New Host** button.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1862](images/1862.png) (**Add a New item**).

3.  Type the **Name**, **Host Name**, and **IP Address** of the host to
    add. **Name** is how the device is labeled in the console. Select
    the type of operating system from the **Host Platform** dropdown. If
    the Host has been found during **Discovery** or **Refresh** and the
    host’s operating system has been identified, the **Host Platform**
    selector remains disabled. If adding an IPMI server for
    provisioning, add in the IP address of that host.
    
    <div class="important">
    
    The **Host Name** must use a unique fully qualified domain name.
    
    </div>
    
    ![2214](images/2214.png)

4.  In the **Credentials** box, the **Default** tab provides fields to
    type a user name with elevated security credentials and the user’s
    password. If using domain credentials, the format for **User ID** is
    in the format of `[domainname]\[username]`. On ESX hosts, if the
    `SSH` login is disabled for the **Default** user, type in a user
    with remote login access on the **Remote Login** tab.
    
    ![2215](images/2215.png)

5.  Click **Validate** to check the credentials.

6.  Click **Save**.

## Editing Hosts

If multiple hosts have the same settings or credentials, edit them at
the same time.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click ![1847](images/1847.png) (**Configuration**).

3.  Check the Hosts to edit.

4.  Click ![1851](images/1851.png) (**Edit Selected items**).

5.  Use **Credentials** to provide login credentials required for this
    host.
    
    ![2216](images/2216.png)
    
      - On the **Default** tab, type a user name with elevated security
        credentials and the users password. If you are using domain
        credentials, the format for User ID must be in the format of
        `[domainname]\[username]`.
    
      - On `ESX` hosts, if `SSH` login is disabled for the **Default**
        user, type in a user with remote login access on the **Remote
        Login** tab. If this is not supplied, *Default* credentials will
        be used.
    
      - Use **Web Services** to supply credentials for any web service
        calls made directly to the host system. If this is not supplied,
        **Default** credentials are used.
        
        <div class="note">
        
        Login credentials are required for performing SmartState
        Analysis on the host’s virtual machines and templates.
        
        </div>
        
        For each type of credential used, the following information is
        required:
    
      - Use **User ID** to specify a login ID.
    
      - Use **Password** to specify the password for the User ID.
    
      - Use **Verify Password** to confirm the password.

6.  Test the credentials by using the *Select Host to validate against*
    drop down and click **Validate**.

7.  Click **Save**.

## Viewing a Host

You can click on a specific host to review it. The screen shows a host
virtual thumbnail, a host taskbar, a host accordion, and a host summary.

**Host Management Screen.**

![2218](images/2218.png)

1.  **Host Taskbar**: Use the host taskbar to take actions on the
    selected host

2.  **Host Summary**: Use the host summary to see the properties of a
    host, drill down to a host’s information, and view its installed
    virtual machines

3.  **Host Summary Views**: Choose between graphical or text view of the
    provider summary

4.  **Host PDF**: Generates host summary in PDF format

5.  **Host Accordion**: See details about **Properties**,
    **Relationships**, **Security** and **Configuration** for the
    selected host

## Tagging Multiple Hosts

To categorize hosts together, apply tags to multiple hosts at the same
time.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Check the hosts to tag.

3.  Click ![1941](images/1941.png) (**Policy**), and then
    ![1851](images/1851.png) (**Edit Tags**).

4.  Select a customer tag from the first dropdown, and then a value for
    the tag.
    
    ![2217](images/2217.png)

5.  Select more tags or click **Save** to save your changes.

## Removing Hosts

If a host is decommissioned or requires troubleshooting, it might
require removal from the VMDB.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Check the hosts to remove.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1861](images/1861.png) (**Remove items from the VMDB**).

4.  Click **OK**.

The hosts are removed. The virtual machines remain in the VMDB, but are
no longer associated with their respective hosts.

## Scaling Down Compute Hosts

Through ManageIQ, you can perform a *Compute scale down* on a Red Hat
OpenStack infrastructure provider. This process involves decreasing its
Compute nodes used by an OpenStack infrastructure provider. Doing so
involves putting a Compute node into *maintenance mode* and removing it
from the provider afterwards. Once a node is in maintenance mode, it can
be repurposed (for examle, re-provision it as a Controller node),
repaired, or decommissioned altogether.

Before scaling down, evacuate or migrate any instances hosted on the
node you are removing. For instructions on either procedure, see
[Migrating a Live Instance](#_to_live_migrate_an_instance) or
[Evacuating an Instance](#_to_evacuate_an_instance).

After migrating or evacuating instances from the node, set the node to
maintenance mode. To do so:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click the OpenStack compute node to be removed from the provider.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Toggle Maintenance Mode**).
    
    <div class="note">
    
    This option can only be used with OpenStack providers with at least
    two Compute nodes.
    
    </div>

Repeat this procedure for every node you want to remove from the cloud
provider.

After setting a Compute node to maintenance mode, you can scale down its
provider:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click the provider to be scaled down.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Scale Down**).

4.  From the **Scale Infrastructure Provider Down** section, check the
    nodes to be removed from the provider. You can only do this for
    nodes where **Maintenance** is set to **true**.

5.  Click **Scale Down**.

## Refreshing Relationships and Power States for a Host

Refresh the relationships and power states of the items associated with
your hosts from the Host Taskbar.

<div class="note">

`root` or administrator credentials are required to get patch
information.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click on the host to refresh.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2003](images/2003.png) (**Refresh Relationships and Power
    States**) on the Host Taskbar.

ManageIQ determines the state (running, stopped, or paused) of all
virtual machines registered to the host.

## Viewing Capacity and Utilization Charts for a Host

View Capacity & Utilization data for hosts that are part of a cluster.

<div class="note">

Your ManageIQ server requires network visibility to the provider
assigned the **Server Role** of **Capacity & Utilization Collector** to
enable this feature.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click the Host to view capacity data.

3.  Click ![1994](images/1994.png) (**Monitoring**), and then
    ![1994](images/1994.png) (**Utilization**) or from the Host
    accordion, click <span class="menuchoice">Properties \> Capacity &
    Utilization</span>.

4.  From **Interval**, select to view hourly or daily data points and
    the dates to view data. Use **Group by** to group the lines by
    SmartTags. Use **Time Profiles** to select a time range for the
    data.
    
    ![2220](images/2220.png)

![2221](images/2221.png)

The charts are displayed for CPU, memory, disk, network, and running
virtual machines.

<div class="note">

Daily charts only include full days of data. If a day does not include
all the 24 data points for a day, the data does not show for that day.

</div>

For information about data optimization including utilization trend
reports, see [Data Optimization](#data-optimization).

## Viewing the Host Timeline

View the timeline of events for the virtual machines registered to a
host.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click the host to view the timeline.

3.  Click ![1994](images/1994.png) (**Monitoring**), and then
    ![1995](images/1995.png) (**Timelines**) or from the host accordion,
    click <span class="menuchoice">Properties \> Timelines</span>.

4.  From **Options**, customize the period of time to display and the
    types of events to see.
    
      - Use **Show** to select types of events to show on the timeline.
    
      - Use the **Interval** dropdown to select hourly or daily data
        points.
    
      - Use **Date** to type the date the timeline displays.
    
      - If you select to view a daily timeline, use **Show** to set how
        many days back to go. The maximum history is 31 days. If
        selecting **Hourly**, select the interval to see.
    
      - From the **Level** dropdown, select either a **Summary** event
        or a **Detail** list of events. For example, the detail level of
        a **Power On** event might include the power on request, the
        starting event, and the actual **Power On** event. If you select
        **Summary**, only the Power On event appears in the timeline.
    
      - The three **Event Group** dropdowns allow selection of different
        groups of events to display. Each group has its own color.

5.  To see more detail on an item in the timeline, click on it. A
    balloon appears with a clickable link to the resource.

## Host Virtual Summary

Clicking on a specific host shows the Host’s Virtual Thumbnail and an
`operating system-sensitive` screen of host information, called the Host
Summary. Where applicable, click on a subcategory of the Host Summary to
see more detail on that section.

A **Refresh** provides some basic information on the Host. To get more
detail, enter credentials for the host and perform a SmartState
Analysis.

The Summary divides into the following categories.

  - **Properties** include information such as base operating system,
    hostname, IP addresses, devices attached to the system, and storage
    adapters. Some categories can be clicked on for additional detail.
    For example, click **Network** to view the network adapters
    connected to the host.
    
    ![2227](images/2227.png)

  - **Relationships** include information on the provider, cluster,
    datastores, resource pools, and installed virtual machines.
    
    ![2228](images/2228.png)

  - **Security** shows the number of users, groups, patches installed,
    and firewall rules on the host. Click on any of these items to see
    further details.
    
    <div class="note">
    
    Run a SmartState Analysis on the host to retrieve this information.
    
    </div>

  - **Storage Relationships** shows the relationship the host has to
    LUNs, volumes, and file shares. The **Storage Inventory Role** must
    be enabled in the zone for these items to be populated.

  - **Configuration** shows the number of packages and services
    installed. Click on any of these items to see more details.
    
    <div class="note">
    
    Run a SmartState Analysis on the host to retrieve this information.
    
    </div>
    
    ![2230](images/2230.png)

  - **Smart Management** shows all tags assigned to this host.

  - **Authentication Status** shows all the types of credentials entered
    for this host and the whether those credentials are valid.

## Viewing Host Device Information

Access information on the hardware devices including processor, CPU type
and speed, and memory for each host.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click the host to view the network information.

3.  From the host accordion, click <span class="menuchoice">Properties
    \> Devices</span>.

## Viewing Host Network Information

Access information on networking including switches, network interfaces,
and local area networks for each host.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click the host to view the network information.

3.  From the host accordion, click <span class="menuchoice">Properties
    \> Network</span>.

![2231](images/2231.png)

## Viewing Storage Adapters

Access information on the storage adapters including storage type for
each host.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click the host to view the network information.

3.  From the host accordion, click <span class="menuchoice">Properties
    \> Storage Adapters</span>.

![2232](images/2232.png)

## Detecting Drift on Hosts

Over time, the configuration of a host might change. Drift is the
comparison of a host to itself at different points in time. The host
requires analysis at least twice to collect information. Detecting drift
provides you the following benefits:

  - See the difference between the last known state of a host and its
    current state.

  - Review the configuration changes that happen to a particular host
    between multiple points in time.

  - Capture the configuration drifts for a single host across a time
    period.

Detect drift on hosts:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Hosts</span>.

2.  Click on the host to view drift.

3.  Click **Relationships** in the host accordion.

4.  Click **Drift History**.

5.  Check the analyses to compare.

6.  Click ![1946](images/1946.png) (**Drift**) at the top of the screen.
    The results display.

7.  Check the **Comparison** sections on the left to view in your
    comparison.

8.  Click **Apply**.

9.  Click the plus sign next to the sections name to expand it.
    
      - An item displayed on red text shows a change from the base
        analysis. An item displayed in black text shows no change from
        the base analysis.
    
      - A ![2177](images/2177.png) (**Changed from previous**) shows a
        change since the last analysis.
    
      - A ![2150](images/2150.png) (**Same as previous**) means no
        change since the last analysis.
    
      - Click ![1861](images/1861.png) (**Remove from drift**) at the
        bottom of a column to remove a specific analysis. The drift
        recalculates and the new results display.

10. Click ![2023](images/2023.png) (**Expanded View**) to see the
    expanded view. Click ![2024](images/2024.png) (**Compressed View**)
    to compress the information.

11. Click the minus sign next to the sections name to collapse it.

12. To limit the type of views, you have three buttons in the taskbar:
    
      - Click ![2178](images/2178.png) (**All attributes**) to see all
        attributes of the sections you selected.
    
      - Click ![2204](images/2204.png) (**Attributes with different
        values**) to see only the attributes that are different across
        the drifts.
    
      - Click ![2148](images/2148.png) (**Attributes with the same
        values**) to see only the attributes that are the same across
        drifts.

The drift comparison displays. Download the data or create a report from
your drift for analysis using external tools.

## Creating a Drift Report for Hosts

Use the drift report feature to export information about your host’s
drift.

1.  Create the comparison to analyze.

2.  Click ![2107](images/2107.png) (**Download**).

3.  Click the output button for the type of report you want.
    
      - Click ![2133](images/2133.png) (**Download drift report in TXT
        format**) for a text file.
    
      - Click ![2133](images/2133.png) (**Download drift report in CSV
        format**) for a comma-separated file.
    
      - Click ![2134](images/2134.png) (**Download drift report in PDF
        format**) for a PDF file.

# Virtual Machines

The heterogeneous virtual machine container and guest support combined
with the ability to analyze information inside the virtual machine -
such as disk space, patch level or installed applications - provides
in-depth information across the virtual environment. This rich set of
information enables ManageIQ users to improve problem resolution times
and effectively manage virtual machines.

The **Virtual Machines** pages display all virtual machines that were
discovered by your server. Note that if you have applied a filter to a
user, it will be in effect here. The **Virtual Machines** taskbar is a
menu driven set of buttons that provide access to functions related to
virtual machines.

![2124](images/2124.png)

1.  History button

2.  Refresh screen button

3.  Taskbar

4.  Name search bar/Advanced Search button

5.  View buttons

6.  Download buttons

7.  Navigation bar

8.  Sort dropdown

9.  Main area in Grid View

10. Provider/Filter Navigation

The console uses **Virtual Thumbnails** to describe virtual machines and
templates. Each thumbnail contains four quadrants by default. This
allows you to glance at a virtual machine for a quick view of its
contents.

![2137](images/2137.png)

1.  Top left quadrant: Operating system of the Virtual Machine

2.  Bottom left quadrant: Virtual Machine Hosts software

3.  Top right quadrant: Power state of Virtual Machine or Status icon

4.  Bottom right quadrant: Number of Snapshots for this Virtual Machine

| Icon                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![2138](images/2138.png) | Template: Virtual Template                                                                                                                                                                                                                                                                                                                                                                                                                |
| ![2139](images/2139.png) | Retired: When a virtual machine or instance is no longer required, it can be retired. Once a virtual machine or instance reaches its retirement date and time, it is immediately shut down and not allowed to restart. If an attempt to restart is made, ManageIQ will shut down the virtual machine or instance.                                                                                                                         |
| ![2140](images/2140.png) | Archived: An archived virtual machine has no host or datastore associated with it. Archiving is done to move virtual machines to a low cost storage, either on demand or during retirement, if requested, to avoid incurring extra cost on a virtualized infrastructure due to virtual machine sprawl.                                                                                                                                    |
| ![2141](images/2141.png) | Orphaned: An orphaned virtual machine has no host but has a datastore associated with it. Orphaned virtual machines are those that have been removed from their providers but still exist on the storage. An orphaned virtual machine is unable to identify the associated host. A virtual machine also shows as orphaned if it exists on a different host than the host expected by the provider’s server.                               |
| ![2142](images/2142.png) | Disconnected: A disconnected virtual machine is one that has lost connection to either the provider’s storage, host, or both. A disconnect is usually a result of network issues on the provider side. For instance, if during virtual machine provisioning the storage is not set up or deleted, the virtual machine will still exist on the provider, but will not run on the host as it has lost connection to its provider’s storage. |
| ![2143](images/2143.png) | On: Virtual Machine is powered on.                                                                                                                                                                                                                                                                                                                                                                                                        |
| ![2144](images/2144.png) | Off: Virtual Machine is powered off.                                                                                                                                                                                                                                                                                                                                                                                                      |
| ![2145](images/2145.png) | Suspended: Virtual Machine has been suspended.                                                                                                                                                                                                                                                                                                                                                                                            |

The **Virtual Machines** page has three accordions organizing your
virtual machines and templates in different ways. All of these
accordions share a set of common controls:

  - Use **VMs and Templates** to view your virtual machines and
    templates organized by Provider. In addition, you can see archived
    and orphaned items here.

  - Use **VMs** to view, apply filters, and collect information about
    all of your virtual machines.

  - Use **Templates** to view, apply filters, and collect information
    about all of your templates.

Through the console, you are able to view your virtual machines in
multiple ways. For your virtual machines, you can:

  - Filter virtual machines

  - Change views

  - Sort

  - Create a report

  - Search by MyTags

  - Search by collected data

## Filtering Virtual Machines and Templates

The **Virtual Machine Filter** accordion is provided so that you can
easily navigate through groups of virtual machines. You can use the ones
provided or create your own through **Advanced Filtering** capabilities.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Go to the **VMs** or **Templates** accordion.

3.  Click on the desired filter from the left pane.

### Creating a Virtual Machine or Template Filter

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Go to the **VMs** or **Templates** accordion.

3.  Click **All VMs** or **All Templates**, then click
    ![2125](images/2125.png) (**Advanced Search**) to open the
    expression editor.

4.  Use the expression editor to choose the appropriate options for your
    criteria. Based on what you choose, different options will show.
    
      - For all of the types of searches, you have the options of
        creating an alias and requested user input. Select **Use Alias**
        to create a user friendly name for the search. If you are
        requested user input for the search, this text will show in the
        dialog box where the input is requested.
    
      - Click **Field** to create criteria based on field values.
        
        ![2126](images/2126.png)
    
      - Click **Count of** to create criteria based on the count of
        something, such as the number of snapshots for a virtual
        machine, or the number of virtual machines on a host.
        
        ![2127](images/2127.png)
    
      - Click **Tag** to create criteria based on tags assigned to your
        virtual infrastructure, such as for power states or production
        tagging.
        
        ![2128](images/2128.png)
    
      - Click **Registry** to create criteria based on registry values,
        such as the DCOM status of a Windows system. Note this criteria
        applies only to Windows operating systems.
        
        ![2129](images/2129.png)
    
      - Click **Find** to seek a particular value, and then check a
        property.
        
        ![2130](images/2130.png)

5.  Click ![1863](images/1863.png) (**Commit Expression Element
    Changes**) to add the expression.

6.  Click **Save**.

7.  Type in a name for the search expression in **Save this VM** search
    as. (Note that this title depends on the type of resource you are
    searching.) To set the filter to show globally, check **Global
    search**.

8.  Click **Save**.

The filter is saved and will show in the **My Filters** area of the
**Filter** accordion. If you checked **Global search**, the filter will
show under **Global Filters**.

### Loading a Report Filter or Search Expression

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to search either **VMs** or
    **Templates**.

3.  Click ![2125](images/2125.png) (**Advanced Search**) to open the
    expression editor.

4.  Click **Load**.

5.  Select either a saved virtual machine search or a virtual machine
    report filter.
    
    <div class="note">
    
    The set of items to select will depend on the type of resource you
    are searching.
    
    </div>
    
    ![2131](images/2131.png)

6.  Click **Load** to load the search expression.

7.  If you want to edit the expression, click on it and make any edits
    for the current expression.
    
      - Click ![1863](images/1863.png) (**Commit expression element
        changes**) to add the changes.
    
      - Click ![1899](images/1899.png) (**Undo the previous change**) to
        remove the change you just made.
    
      - Click ![1900](images/1900.png) (**Redo the previous change**) to
        put the change that you just made back.
    
      - Click ![1901](images/1901.png) (**AND with a new expression
        element**) to create a logical AND with a new expression
        element.
    
      - Click ![1902](images/1902.png) (**OR with a new expression
        element**) to create a logical OR with a new expression element.
    
      - Click ![1903](images/1903.png) (**Wrap this expression element
        with a NOT**) to create a logical NOT on an expression element
        or to exclude all the items that match the expression.
    
      - Click ![1904](images/1904.png) (**Remove this expression
        element**) to take out the current expression element.

8.  Click **Load**.

9.  Click **Apply**.

## Changing Views for Virtual Machines and Templates

While you can set the default view for different pages from the settings
menu, then <span class="menuchoice">Configuration \> My Settings \>
Default Views</span>, the current view can also be controlled from the
Virtual Machines pages.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to view.

3.  Click the appropriate button for the desired view.
    
      - Click ![2020](images/2020.png) for **Grid View**.
    
      - Click ![2021](images/2021.png) for **Tile View**.
    
      - Click ![2022](images/2022.png) for **List View**.

## Sorting Virtual Machines and Templates

Virtual machines and templates can be sorted by Name, Cluster, Host,
Datastore, Compliance, Last Analysis Time, Total Snapshots, or Region.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to sort.

3.  To sort virtual machines or templates when in grid or tile view:
    
      - From the **Sort by** dropdown, click the attribute to sort.

4.  To sort virtual machines or templates when in list view:
    
      - Select the **List View**.
    
      - Click on the **Column Name** to sort. For example, click on
        **Cluster** to sort by the name of the cluster.

## Creating a Virtual Machine or Template Report

For a listing of virtual machines and templates, you can create a quick
report in CSV, TXT, or PDF formats.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items for report creation.

3.  Click ![2107](images/2107.png) (**Download**).
    
      - Click ![2133](images/2133.png) for a **TXT** file.
    
      - Click ![2133](images/2133.png) for a **CSV** file.
    
      - Click ![2134](images/2134.png) for a **PDF** file.

## Searching for Virtual Machines or Templates

To the right of the taskbar on the *Virtual Machines* page, you can
enter names or parts of names for searching. You can search in the
following ways:

  - Type characters that are included in the name. For example, if you
    type `sp1`, all Virtual Machines whose names include `sp1` appear,
    such as `Windows2003sp1` and `Sp1clone`.

  - Use `*` at the end of a term to search for names that begin with
    specific characters. For example, type `v*` to find all virtual
    machines whose names begin with the letter `v`.

  - Use `\*` at the beginning of a term to search for names that end
    with specific characters. For example, type `*sp2` to find all
    virtual machines whose names end with `sp2`.

  - Erase all characters from the search box to go back to viewing all
    virtual machines.

Search for virtual machines or templates:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to search.
    
    ![2136](images/2136.png)

3.  In the **Name Filter** bar in the upper right corner of the window,
    type your criteria.

4.  Click ![2135](images/2135.png)(**Search by Name within results**) or
    press **Enter**.

5.  Type in other criteria to filter on what is currently displayed.

6.  Click ![2135](images/2135.png) (**Search by Name within results**)
    or press **Enter**.

## Analyzing Virtual Machines and Templates

Analyze a virtual machine to collect metadata such as user accounts,
applications, software patches, and other internal information. If
ManageIQ is not set up for automatic analysis, perform a manual analysis
of a virtual machine. To perform a SmartState analysis, ManageIQ
requires a running SmartProxy with visibility to the virtual machine’s
storage location. If the virtual machine is associated with a host or
provider, ensure the virtual machine is registered with that system to
be properly analyzed; the server requires this information since a
snapshot might be created.

<div class="note">

SmartState Analysis of a virtual machine requires access to its host. To
perform a successful analysis, edit the virtual machine’s host and enter
the host’s authentication credentials.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to analyze.

3.  Check the **Virtual Machines** and **Templates** to analyze.

4.  Click ![1847](images/1847.png) (**Configuration**), then
    ![1942](images/1942.png) (**Perform SmartState Analysis**).

5.  Click **OK**.

### Red Hat Enterprise Virtualization Prerequisites

#### SmartState Analysis on Red Hat Enterprise Virtualization Manager 3.1 and Above - Storage Support Notes

Note the following requirements when performing SmartState Analysis on
Red Hat Enterprise Virtualization Manager 3.1 and above.

  - NFS
    
      - The ManageIQ appliance requires a mount to the NFS datastore.

  - iSCSI / FCP
    
      - For Red Hat Enterprise Virtualization 3.1 and 3.2, clusters must
        use full Red Hat Enterprise Linux hosts and not Red Hat
        Enterprise Virtualization Hypervisor hosts. You can use either
        type of host in Red Hat Enterprise Virtualization 3.3 and above.
    
      - Each ManageIQ appliance performing SmartState Analysis requires
        sharable, non-bootable DirectLUN access to each attached
        iSCSI/FCP storage domain. In order to perform smart analysis,
        the appliance must mount the data storage as a DirectLUN disk.
    
      - A ManageIQ appliance **must** reside in each datacenter with the
        iSCSI / FCP storage type.

  - Other Notes
    
      - The **Edit Management Engine Relationship** option enables the
        VM SmartState Analysis job to determine the datacenter where a
        ManageIQ appliance is running and thus to identify what storage
        it has access to in a Red Hat Enterprise Virtualization
        environment.
        
          - After setting up a ManageIQ appliance and performing a
            refresh of the provider, find the ManageIQ appliance in the
            **Virtual Machine** accordion list and view its summary
            screen.
        
          - Click <span class="menuchoice">Configuration \> Edit
            Management Engine Relationship</span>.
        
          - Select the server that relates to this instance of the
            ManageIQ appliance.

<div class="important">

If you attach a DirectLUN disk after configuring the ManageIQ database,
access the appliance in a terminal and run `pvscan` to detect the
DirectLUN disk. Alternatively, in ManageIQ 5.2.1 and above, you can
restart the appliance to detect the disk automatically.

</div>

#### SmartState Analysis on Red Hat Enterprise Virtualization Manager 3.0 - Storage Support Notes

There are two additional steps required to perform a SmartState Analysis
on Red Hat Enterprise Virtualization Manager 3.0 using `iSCSI` or `FCP`
storage. NFS storage does not have these requirements.

1.  Enable `DirectLUN` support for the host and ManageIQ appliance that
    performs the analysis.
    
      - Enable `DirectLUN` on host.
    
      - Enable `DirectLUN` on the ManageIQ appliance. To do this, edit
        the desired Red Hat Enterprise Virtualization storage and get
        the `LUNID` value. Then, on the ManageIQ appliance virtual
        machine in the Red Hat Enterprise Virtualization user interface,
        right-click and select <span class="menuchoice">Edit \> Custom
        Properties</span> and enter the following in the **Custom
        Properties** edit box:
        
            directlun=<LUN ID>:readonly
        
        If you have multiple storage domains, separate them by a comma,
        similar to:
        
            directlun=<LUN ID 1>:readonly,<LUN ID 2>:readonly,<LUN ID N>:readonly
        
        <div class="note">
        
        The ManageIQ appliance must reside in the same data center as
        the storage you are trying to connect. If you have multiple data
        centers with `iSCSI` or `FCP` storage, you need a ManageIQ
        appliance in each data center to support virtual machine
        scanning.
        
        </div>

2.  **Set Server Relationship** - This is required to allow the virtual
    machine SmartState analysis job to determine which data center a
    ManageIQ appliance is running and therefore identify what storage it
    has access to in a Red Hat Enterprise Virtualization environment.
    
    1.  After setting up a ManageIQ appliance and performing a refresh
        of the Provider, find the ManageIQ appliance in the **Virtual
        Machine** accordion list and view its summary screen.
    
    2.  Click ![1847](images/1847.png) (**Configuration**), and then
        ![2146](images/2146.png)(**Edit Server Relationship**).
    
    3.  Select the server that relates to this instance of the ManageIQ
        appliance.

### VMware vSphere Prerequisites

#### Installing VMware VDDK on ManageIQ

Unresolved directive in
doc-Managing\_Infrastructure\_and\_Inventory/miq/topics/Virtual\_Machines.adoc
- include::/common/installing-vmware-vddk.adoc\[\]

## Comparing Virtual Machines and Templates

The ManageIQ Server allows you to compare multiple virtual machines.
This allows you to see how different virtual machines are from their
original template. This helps detect missing patches, unmanaged user
accounts, or unauthorized services.

Use the comparison feature to:

  - Compare multiple virtual machines from different hosts.

  - Compare multiple virtual machines side-by-side.

  - Quickly see similarities and differences among multiple virtual
    machines and a base.

  - Narrow the comparison display to categories of properties.

  - Print or export in the comparison results to a PDF or CSV file.

Compare virtual machines and templates:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to analyze.

3.  Check the items to compare.

4.  Click ![1847](images/1847.png) (Configuration), and then
    ![2148](images/2148.png) (Compare Selected items). The comparison
    displays in a compressed view with a limited set of properties
    listed.
    
    ![2149](images/2149.png)

5.  To delete an item from the comparison, click
    ![1861](images/1861.png)(Remove this item from Inventory) at the
    bottom of the items column. This option is only available when
    comparing more than two virtual machines.

6.  To view many items on one screen, go to a compressed view by
    clicking ![2024](images/2024.png) (Compressed View). To return to an
    expanded view, click ![2023](images/2023.png) (Expanded View).

7.  To limit the mode of the view, there are two buttons in the task
    bar.
    
      - Click ![2022](images/2022.png) (Details Mode) to see all details
        for an attribute.
    
      - Click ![2025](images/2025.png) (Exists Mode) to limit the view
        to if an attribute exists compared to the base or not. This only
        applies to attributes that can have a boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

8.  To change the base virtual machine that all the others are compared
    to, click its label at the top of its column.

9.  To go to the summary screen for a virtual machine, click its Virtual
    Thumbnail or icon.

### Virtual Machine and Templates Comparison Sections

The following table describes the different sections for comparison
information.

| Section         | Description                                                                                                                                                                                                                                     |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Properties      | Use this section to see basic information on the file location of the virtual machine, its name, and the virtual machine monitor vendor. Hardware, disk, CD/DVD drives, floppy drive, network adapter, and volume information is also included. |
| Security        | Use this to see users and groups for the virtual machine, including those which may be unauthorized compared to a template.                                                                                                                     |
| Configuration   | Use this to see Guest Applications, Win32 services, Linux Init Processes, Kernel Drivers, File System Drivers, and Patches.                                                                                                                     |
| My Company Tags | Use this to see all tags.                                                                                                                                                                                                                       |

### Using the Virtual Machine Comparison Sections

Use the comparison sections to view various comparison data and display
the data in different ways.

1.  On the left of a comparison screen, select what categories of
    properties to display.

2.  Click **Apply**.

3.  Click the plus sign next to the sections name to expand it.

4.  The following descriptions pertain to the **Expanded View**
    ![2023](images/2023.png). Whether you see the value of a property or
    an icon representing the property depends on the properties type.
    
      - A property displayed in the same color as the base means that
        the compared virtual machine matches the base for that property.
    
      - A property displayed in a different color from the base means
        that the compared virtual machine does not match the base for
        that property.

5.  If you are in the **Compressed View** ![2024](images/2024.png), the
    values of the properties will not be displayed. The icons shown
    below will describe all items.
    
      - A ![2150](images/2150.png) (**checkmark**) means that the
        compared virtual machine matches the base for that property. If
        you hover over it, the value of the property will display.
    
      - A ![2151](images/2151.png) (**x**) means that the compared
        virtual machine does not match the base for that property. If
        you hover over it, the value of the property will display.

6.  Click the minus sign next to the sections name to collapse it.

Your comparison can be viewed in multiple ways. Export the data or
create a report from your comparison for analysis using external tools.

### Creating a Virtual Machine Comparison Report

Output the data from a comparison report in TXT, CSV or PDF formats.

1.  Create the comparison for the report.

2.  Click the output button for the chosen report type.
    
      - Click ![2133](images/2133.png) (**Download comparison report in
        TXT format**) for a text file.
    
      - Click ![2133](images/2133.png) (**Download comparison report in
        CSV format**) for a CSV file.
    
      - Click ![2134](images/2134.png) (**Download comparison report in
        PDF format**) for a PDF file.

## Controlling the Power State of Red Hat Virtualization Virtual Machines

Follow this procedure to control the power states of Red Hat
Virtualization VMs through the ManageIQ console.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click on a VM to change the power state.

3.  Click **Power Operations**, then click the button for the desired
    power operation. Available operations will depend on the current
    power state of the VM.
    
      - Click ![2002](images/2002.png) (**Shutdown Guest**) to shutdown
        the guest OS on the VM.
    
      - Click ![restartguest](images/restartguest.png) (**Restart
        Guest**) to restart the guest OS on the VM.
    
      - Click ![1999](images/1999.png) (**Power On**) to power on the
        VM.
    
      - Click ![2000](images/2000.png) (**Power Off**) to power off the
        VM.
    
      - Click ![2004](images/2004.png) (**Suspend**) to suspend the VM.
    
      - Click ![2003](images/2003.png) (**Reset**) to reset the VM.

4.  Click **OK**.

## Refreshing Virtual Machines and Templates

Refresh your virtual machines to get the latest data the provider or
host can access. This includes information such as the power state,
container, and hardware devices attached to the virtual machine.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to analyze.

3.  Check the items to refresh.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2003](images/2003.png) (**Refresh Relationships and Power
    States**) on the **Virtual Machine Taskbar**.

The console returns a refreshed list of the data associated with the
selected virtual machines.

## Extracting Running Processes from Virtual Machines and Templates

ManageIQ can collect processes running on Windows virtual machines. To
do this, enter domain credentials for the zone where the virtual machine
is located.

For more information, see *General Configuration*. The virtual machine
must be running and must have an IP address in the VMDB, usually
obtained from a SmartState Analysis.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Check the Virtual Machines to collect the processes.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2152](images/2152.png)(**Extract Running Processes**) on the
    Taskbar.

4.  Click **OK**.

The server returns the running processes. View the summary of the
virtual machine to see the details.

## Setting Ownership for Virtual Machines and Templates

You can set the owner of a group of virtual machines and templates by
either individual user or group. This allows you an additional way to
filter and can be used to enforce quotas.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to change.

3.  Check the items to set ownership.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2155](images/2155.png) (**Set Ownership**) on the **Virtual
    Machine Taskbar**.

5.  From the **Select an Owner** dropdown, select a user, and from the
    **Select a Group** dropdown, select a group.
    
    ![2156](images/2156.png)

6.  Click **Save**.

## Removing Virtual Machines and Templates from the VMDB

If a virtual machine has been decommissioned or you need to perform some
troubleshooting, you might need to remove a specific virtual machine
from the VMDB. This does not however remove the virtual machine or
template from its Datastore or Provider.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to remove.

3.  Check the items to remove.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1861](images/1861.png) (**Remove from the VMDB**) button.

5.  Click **OK**.

## Tagging Virtual Machines and Templates

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to tag.

3.  Check the items to tag.

4.  Click ![1941](images/1941.png) (**Policy**), and then
    ![1851](images/1851.png) (**Edit Tags**).

5.  Select a customer tag from the first dropdown, and then a value for
    the tag.
    
    ![2159](images/2159.png)

## Viewing a VMware Virtual Machine’s Storage Profile

VMware storage profiles allow you to assign policies to datastores.
Storage profiles are used to tag virtual machines to ensure they operate
in compliance with settings in the datastore.

ManageIQ retrieves VMware virtual machine storage profile information in
the inventory, and associates the virtual machines and disks with them.

To view a virtual machine’s storage profile:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click a VMware virtual machine to open its summary page.

3.  The VMware **Storage Profile** is listed under **Properties**.

You can assign a storage profile when provisioning a VMware virtual
machine in ManageIQ, by using the virtual machine as a template to
clone. See [Provisioning Virtual
Machines](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.7/single/provisioning-virtual-machines-and-hosts/#provisioning-virtual-machines)
in *Provisioning Virtual Machines and Hosts* for instructions.

## Viewing Running Processes after Collection

1.  Click a virtual machine with collected processes.

2.  From the **Diagnostics** area, click **Running Processes**.

![2161](images/2161.png)

The most recent collection of running processes is displayed. Sort this
list by clicking on the column headers.

## Editing Virtual Machine or Template Properties

Edit the properties of a virtual machine or template to set parent and
child virtual machines. SmartState Analysis also can detect this.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to edit.

3.  Click the item to edit properties.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Edit selected item**) on the Taskbar.

5.  From the **Parent VM** dropdown, select the parent virtual machine.

6.  From **Child VM** selection, select virtual machines that are based
    on the current virtual machine from the list of **Available VMs**.

7.  Click **Save**.

## Setting Ownership of a Virtual Machine or Template

Set the owner of a virtual machine or template by either individual user
or group. This allows you an additional way to filter configuration
items.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the items to analyze.

3.  Click the item to set ownership.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2155](images/2155.png)(**Set Ownership**) on the taskbar.

5.  From the **Select an Owner** dropdown, select a user.
    
    ![2162](images/2162.png)

6.  From the **Select a Group** dropdown, select a group.

7.  Click **Save**.

## Right Sizing a Virtual Machine

ManageIQ uses collected statistics to recommend the best size for a
virtual machine. ManageIQ uses the information from the **Normal
Operating Range** to calculate the recommendations.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click a virtual machine for right-sizing.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2163](images/2163.png) (**Right-Size Recommendations**) button.

A new page appears with three levels of Memory and CPU recommendations,
Conservative, Moderate, and Aggressive, next to the Normal Operating
Range statistics.

## Viewing Capacity and Utilization Charts for a Virtual Machine

You can view capacity and utilization data for virtual machines that are
part of a cluster. Note that daily charts only include full days of
data. If all 24 data points for a day are not available, daily charts
are not displayed. For some capacity and utilization data, ManageIQ
calculates and shows trend lines in the charts which are created using
linear regression. The calculation uses the capacity and utilization
data collected by ManageIQ during the interval you specify.

<div class="note">

You must have a server with network visibility to your provider assigned
the server role of **Capacity & Utilization Collector** to use this
feature.

The virtual machine must be powered on to collect the data.

</div>

1.  From <span class="menuchoice">Compute \> Infrastructure \> Virtual
    Machines</span>, click the accordion that you want to view capacity
    data for.

2.  Click the item you want to view.

3.  Click ![1994](images/1994.png) (**Monitoring**), and then
    ![1994](images/1994.png) (**Utilization**).

4.  From **Interval**, select to view **Daily**, **Hourly**, or **Most
    Recent Hour** data points. When choosing **Daily**, you can also
    select the **Date**, and how far back you want to go from that date.
    When selecting **Hourly**, you can select the date for which you
    want to view hourly data. If you are using **Time Profiles**, you
    will be able to select that as an option, also.
    
    ![2246](images/2246.png)

5.  From **Compare to**, select **Parent Host** or **Parent Cluster**.
    The capacity and utilization charts for both items will show
    simultaneously.
    
    ![2247](images/2247.png)

<div class="note">

Daily charts only include full days of data. This means ManageIQ does
not show daily data for a day without a complete 24 data point range for
a day.

</div>

For information about data optimization including utilization trend
reports, see [Data Optimization](#data-optimization).

## Viewing the Virtual Machine or Template Timeline

View the timeline of events for a virtual machine or template if
registered to a Host.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the virtual machine to view the timeline.

3.  Click ![1994](images/1994.png) (**Monitoring**), and then
    ![1995](images/1995.png) (**Timelines**) on the taskbar.

4.  From **Options**, customize the period of time to display, and the
    types of events to view.
    
    ![2166](images/2166.png)
    
      - Use the **Interval** dropdown to select hourly or daily data
        points.
    
      - Use **Date** to type the date of the timeline to display.
    
      - If viewing a daily timeline, use **Show** to set how many days
        back to go. The maximum history is 31 days.
    
      - The three **Event Group** dropdowns allow selection of different
        event groups to display. Each has its own color.
    
      - From the **Level** dropdown, select either a **Summary** event
        or a **Detail** list of events. For example, the detail level of
        a **Power On** event might include the power on request, the
        starting event, and the actual **Power On** event. If you select
        **Summary**, you only see the **Power On** event in the
        timeline.

5.  To see more detail on an item in the timeline, click on it. A
    balloon appears with a clickable link to the resource.

## Virtual Machine or Template Summary

When you click on a specific virtual machine or template, you will see
the **Virtual Thumbnail**, and an operating system-specific screen of
the item, called the **Summary**. Where applicable, click on a
subcategory of the **Summary** to see more detail on that section.

<div class="note">

When you perform a SmartState Analysis on a virtual machine or template,
you get more detailed information in these categories.

</div>

  - **Properties** include information such as the base operating
    system, hostname, IP addresses, Virtual Machine vendor, CPU
    Affinity, devices attached to the system, and snapshots. This
    includes the ability to analyze multiple partitions, multiple disks,
    Linux logical volumes, extended partitions, and Windows drives. Some
    categories can be clicked on for additional detail. For example,
    click **Container** to view notes associated with a virtual machine.
    
    ![2167](images/2167.png)

  - **Lifecycle** shows the date of discovery and the last analysis. If
    a retirement date and time or owner has been set, these display as
    well.
    
    ![2168](images/2168.png)

  - **Relationships** include information on the parent host, genealogy
    such as parent and child virtual machines, and drift.
    
    ![2169](images/2169.png)

  - **Storage Relationships** shows relationships to Filers, LUNs,
    Volumes and File Shares.

  - **VMsafe** shows properties of the VMsafe agent if it is enabled.
    
    ![2170](images/2170.png)

  - **Normal Operating Ranges** shows the values for the normal
    operating range for this virtual machine. These statistics are used
    in calculating right sizing recommendations.
    
    ![2171](images/2171.png)

  - **Power Management** displays the current power state, last boot
    time, and last power state change. **State Changed On** is the date
    that the virtual machine last changed its power state. This is a
    container view of the power state, therefore a restart of the
    operating system does not cause the container power state to change
    and will not update this value.
    
    ![2172](images/2172.png)

  - **Security** includes information on users, groups, and security
    patches. Recall that the items shown on the **Summary** screen
    change based on the guest operating system.
    
    ![2173](images/2173.png)

  - **Configuration** includes information on applications, services,
    packages, and init processes. This section changes depending on the
    base operating system.
    
    ![2174](images/2174.png)

  - **Datastore Allocation Summary** shows how many and how much disk
    space has been allocated to this virtual machine as well as disk
    alignment and thin provisioning information.

  - **Datastore Actual Usage Summary** shows how much disk and memory
    the virtual machine is actually using.
    
    ![2175](images/2175.png)

  - **Diagnostics** provides a link to viewing running processes and the
    information from the latest collected event logs.

  - **Smart Management** shows all tags assigned to this virtual
    machine.

## Viewing the Operating System Properties

View details of the operating system from the **Virtual Machine
Summary** or the accordion. For Windows systems, see **Account
Policies** for the virtual machine.

1.  From <span class="menuchoice">Compute \> Infrastructure \> Virtual
    Machines</span>, click on the item to view its **Summary**.

2.  From the **Properties** section, click **Operating System**.

An expanded view of the operating systems properties and **Account
Policies** displays. This varies based on the operating system.

## Viewing Virtual Machine or Template Snapshot Information

View the list of snapshots to see a history of their creation and size.
ManageIQ provides the description, size, and creation time of the
snapshot as well as a view of the genealogy of the snapshots.

<div class="note">

Snapshot size is only available after the successful completion of a
**SmartState Analysis**.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the appropriate accordion containing the item you wish to view
    the snapshots of.

3.  Click on the item to view its **Summary**.

4.  From the **Summary**, click *Snapshots* in the **Properties** area.

5.  The list of snapshots show in a tree format and captures their
    genealogy.

## Viewing User Information for a Virtual Machine or Template

ManageIQ’s **SmartState Analysis** feature returns user information.
Drill into the user to get details on the user’s account, including
group memberships.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the item to view user information.

3.  Click on the item to view its **Summary**.

4.  From the **Security** section of the **Virtual Machine Summary**,
    click **Users**.

5.  Click the user to view details.

## Viewing Group Information for a Virtual Machine or Template

ManageIQ’s **SmartState Analysis** feature returns group information.
Explore a group to get a list of its users.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the item to view user information.

3.  Click on the item to view its **Summary**.

4.  From the **Security** section of the **Virtual Machine Summary**,
    click **Groups**.

5.  Click the group to view users.

## Viewing Genealogy of a Virtual Machine or Template

ManageIQ detects the lineage of a virtual machine. View a virtual
machine’s lineage and compare the virtual machines that are part of its
tree. This also allows tagging of virtual machines that share genealogy.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the item to view genealogy.

3.  Click on the item to view its **Summary**.

4.  From the **Relationships** area in the **Summary**, click
    **Genealogy**.

## Comparing Genealogy of a Virtual Machine or Template

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the item to view genealogy.

3.  Click on the item to view its **Summary**.

4.  From the **Relationships** area in the **Summary**, click
    **Genealogy**.

5.  Check the items to compare.

6.  Click ![2148](images/2148.png) (**Compare Selected VMs**).

## Tagging Virtual Machines or Templates with a Common Genealogy

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the item to view genealogy.

3.  Check the items to tag.

4.  Click ![1941](images/1941.png) (**Policy**), and then
    ![1851](images/1851.png) (**Edit Tags**).

5.  Select a customer tag from the first dropdown, and then a value for
    the tag.
    
    ![2176](images/2176.png)

## Detecting Drift on Virtual Machines or Templates

The configuration of a virtual machine might change over time. **Drift**
is the comparison of a virtual machine to itself at different points in
time. The virtual machine needs analysis at least twice to collect this
information. Detecting drift provides you the following benefits:

  - See the difference between the last known state of a machine and its
    current state.

  - Review the configuration changes that happen to a particular virtual
    machine between multiple points in time.

  - Review the host and datastore association changes that happen to a
    particular virtual machine between multiple points in time.

  - Review the classification changes that happen to a virtual machine
    between two time checks.

  - Capture the configuration drifts for a single virtual machine across
    a time period.

Detect drift on virtual machines or templates:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click on the item to view its **Summary**.

3.  From the **Relationships** area in the **Summary**, click **Drift
    History**.

4.  Check the analyses to compare.

5.  Click ![1946](images/1946.png) (**Select up to 10 timestamps for
    Drift Analysis**) at the top of the screen. The results display.

6.  Check the **Drift** sections on the left to view in your comparison.

7.  Click **Apply**.

8.  The following descriptions pertain to the **Expanded View**
    ![2023](images/2023.png). Whether you see the value of a property or
    an icon representing the property depends on the properties type.
    
      - A property displayed in the same color as the base means the
        compared analysis matches the base for that property.
    
      - A property displayed in a different color from the base means
        the compared analysis does not match the base for that property.

9.  If you are in the **Compressed View** ![2024](images/2024.png), the
    values of the properties are not displayed. All items are described
    by the icons shown below.
    
      - A ![2150](images/2150.png) (**checkmark**) means that the
        compared analysis matches the base for that property. If you
        hover over it, the value of the property will display.
    
      - A ![2177](images/2177.png) (**triangle**) means the compared
        analysis does not match the base for that property. If you hover
        over it, the value of the property displays. Click the minus
        sign next to the sections name to collapse it.

10. To limit the scope of the view, you have three buttons in the
    **Resource** button area.
    
      - Click ![2178](images/2178.png) (**All attributes**) to see all
        attributes of the sections you selected.
    
      - Click ![2204](images/2204.png) (**Attributes with different
        values**) to see only the attributes that are different across
        the drifts.
    
      - Click ![2148](images/2148.png) (**Attributes with the same
        values**) to see only the attributes that are the same across
        drifts.

11. To limit the mode of the view, there are two buttons in the
    **Resource** button area.
    
      - Click ![2022](images/2022.png) (**Details Mode**) to see all
        details for an attribute.
    
      - Click ![2025](images/2025.png) (**Exists Mode**) to only see if
        an attribute exists compared to the base or not. This only
        applies to attributes that can have a Boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

This creates a drift analysis. Download the data or create a report from
your drift for analysis using external tools.

## Creating a Drift Report for a Virtual Machine or Template

1.  Create the comparison to analyze.

2.  Click ![2107](images/2107.png) (**Download**).

3.  Click the output button for the type of report you want.
    
      - Click ![2133](images/2133.png) (**Download drift report in text
        format**) for a text file.
    
      - Click ![2133](images/2133.png) (**Download drift report in CSV
        format**) for a csv file.
    
      - Click ![2134](images/2134.png) (**Download drift report in PDF
        format**) for a PDF file.

## Viewing Analysis History for a Virtual Machine or Template

Each time a SmartState Analysis is performed on a virtual machine, a
record is created of the task. This information is accessed either from
the virtual machine accordion or the virtual machine summary. Use this
detail to find when the last analysis was completed and if it completed
successfully. If the analysis resulted in an error, the error is shown
here.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the item to view genealogy.

3.  Click on the item to view its **Summary**.

4.  From the **Relationships** area in the **Summary**, click **Analysis
    History**. A history of up to the last 10 analyses is displayed.
    
    ![2179](images/2179.png)

5.  Click on a specific analysis to see its details.

## Viewing Disk Information for a Virtual Machine or Template

Each time a SmartState Analysis is performed on a virtual machine or
template, information on the disks associated with the item is
collected. This includes free and used space information as well as the
type of disk and file system.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click on the item to view its **Summary**.

3.  From **Datastore Allocation Summary**, click **Disks**.

A list of the disks for the item with type, file system, size, and usage
information is displayed.

## Reconfiguring Virtual Machines

Memory, processors, disks, ISOs, and CD/DVD Drives can be reconfigured
on existing VMware and Red Hat Virtualization virtual machines using the
**Reconfigure this VM** button.

You can reconfigure multiple components on a virtual machine using one
request, or make each reconfiguration separately. Confirm your changes
using the **Submit** button.

<div class="important">

The following restrictions apply to adding and removing Red Hat
Virtualization virtual machine disks:

  - Supported by Red Hat Virtualization 4.0 and above.

  - Only a single bootable disk is supported.

  - The virtual machine requires at least one existing disk to allow
    adding additional disks. This is because the destination storage
    cannot be specified from the ManageIQ dialog, so the storage
    associated with the existing disk is reused.

</div>

### Adding a Disk to a Virtual Machine

A disk can be added to a VMware or Red Hat Virtualization virtual
machine with the following steps:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Click **Add Disk**.

5.  Specify the disk type, mode, size, and dependency options.

6.  Click **Submit**.

After the disk has been added, you can view the new disk by navigating
to <span class="menuchoice">Compute \> Infrastructure \> Virtual
Machines</span>. . Open the target virtual machine, then click
**Devices** to view the new disk.

### Removing a Virtual Machine Disk

A disk can be removed from a VMware or Red Hat Virtualization virtual
machine with the following steps:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Click **Delete** next to the disk to remove.

5.  Click **Submit**.

### Resizing a Virtual Machine Disk

<div class="note">

This functionality is available on VMware virtual machines only.

</div>

You can extend a VMware virtual machine’s disk with the following steps:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Click **Resize** next to the disk you want to resize to show
    resizing options.

5.  Specify the desired memory size and units (MB or GB). A disk can
    only be extended in size.

6.  Click **Confirm Resize** to select the values. Alternatively,
    selecting **Cancel Resize** shows the original values.

7.  Click **Submit**.

The disk resizing request is then processed for the virtual machine.

### Increasing or Decreasing a Virtual Machine’s Memory Size

You can increase or decrease a VMware or Red Hat Virtualization virtual
machine’s memory size with the following steps:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Select **Yes** next to **Memory** to show memory options.

5.  Specify the desired memory size and units (MB or GB).

6.  Click **Submit**.

The memory add request is then processed for the virtual machine.

### Reconfigure a Virtual Machine’s Processors

You can reconfigure a VMware or Red Hat Virtualization virtual machine’s
processors with the following steps:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Select **Yes** next to **Processors** to show processor options.
    
    ![Reconfigure processor](images/Reconfigure_processor.png)

5.  Specify the number of sockets and the number of cores per socket.
    The reconfiguration screen will calculate the **Total Processors**.

6.  Click **Submit**.

The virtual machine’s processors are then reconfigured.

### Adding or Removing Virtual Machine Network Adapters

<div class="note">

This functionality is available on VMware virtual machines only.

</div>

You can add or remove network adapters on a VMware virtual machine from
the **Reconfigure this VM** button.

#### Adding a Network Adapter to a VMware Virtual Machine

To add a network adapter to a virtual machine:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Click **Add Network** next to the disk you want to resize to show
    resizing options.

5.  Select the type of adapter from the list under **vLan**.

6.  Click **Confirm Add**.

7.  Click **Submit**.

A request to add the network adapter is then processed for the virtual
machine. You can view the details for the new network adapter by
navigating to the **Reconfigure this VM** area. When the network adapter
is added, a name and MAC address are assigned to the adapter.

#### Removing a Network Adapter from a VMware Virtual Machine

To remove a network adapter from a virtual machine:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Click **Delete** next to the network adapter you want to remove.

5.  Click **Submit**.

### Attach or Remove an ISO (VMware Virtual Machines Only)

You can attach an ISO to a VMware virtual machine using following steps:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Under **CD/DVD Drives**, click **Connect**.

5.  Select the **Host File** from the list to attach and click **Confirm
    Connect**.

6.  Click **Submit**.

The ISO is now attached to the VMware virtual machine.

You can remove an ISO on VMware virtual machine using following steps:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this VM**).

4.  Under **CD/DVD Drives**, locate the **Host File** and click
    **Disconnect**.

5.  Click **Confirm**.

6.  Click **Submit**.

The ISO is removed from the VMware virtual machine.

## Viewing Event Logs for a Virtual Machine or Template

Using an **Analysis Profile**, collect event log information from your
virtual machines.

See "Setting a Default Analysis Profile" in *General Configuration*.

<div class="note">

This feature is only available for Windows.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click the accordion for the item to view event logs.

3.  Click on the item to view its **Summary**.

4.  From **Diagnostics** click **Event Logs**.

The collected event log entries are displayed. Sort this list by
clicking on the column headers.

## Remote Consoles

A console is a graphical window that allows you to view the start up
screen, shut down screen, and desktop of a virtual machine, and to
interact with that virtual machine in a similar way to a physical
machine.

ManageIQ offers the following support for HTML5-based VNC, SPICE, and
WebMKS consoles:

  - VNC and SPICE consoles for Red Hat Virtualization Manager with
    websocket proxy.

  - VMware’s WebMKS HTML5-based console type.

  - VNC consoles for OpenStack using OpenStack-supplied websocket proxy.

<div class="note">

  - VMware no longer supports the MKS console type. Also, VMRC is no
    longer a browser plugin but a native desktop application. As a
    result, the VMware MKS and the VMRC plugin options have been
    disabled in ManageIQ.

  - Currently, attempting to connect to the VMware WebMKS console for a
    virtual machine fails when the server security type is set to `2`
    for that virtual machine.

  - Due to VMware licensing restrictions, Red Hat cannot ship the WebMKS
    SDK in ManageIQ. For information on how to configure WebMKS support
    in ManageIQ, see [Configuring WebMKS Support in
    ManageIQ](#configuring-the-webmks-support).

</div>

All of the above make use of the websocket protocol supported by all
recent versions of browsers, and can use SSL to encrypt the websocket
connection.

  - OpenStack  
    ManageIQ only makes an API call to get the URL for the console and
    open that console in a web browser; see [Directly Connect to a VNC
    Console](https://access.redhat.com/documentation/en/red-hat-openstack-platform/8/single/instances-and-images-guide/#connect_to_an_instance)
    in the Red Hat OpenStack Platform *Instances and Images Guide* for
    more details.

  - Red Hat Enterprise Virtualization Manager and VMware  
    By default, the websocket connection runs over HTTPS or HTTP based
    on how the application was accessed. Under an appliance, you will
    most likely use HTTPS, and, therefore, the websocket connection will
    be wss:// (websocket with SSL).
    
    When configuring Red Hat Virtualization Manager for virtual machine
    console access, set the display type for each virtual machine to
    `noVNC` or `SPICE HTML5`. For more information on configuring
    console options, see [Configuring Console
    Options](https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.2/html-single/virtual_machine_management_guide/index#sect-Configuring_Console_Options)
    in the Red Hat Virtualization *Virtual Machine Management Guide*.

### Configuring Console Access to VMware ESXi Hosts At A Network Layer

When configuring access to the VNC or HTML5 console, make sure that at a
network layer:

  - All VNC ports (5900-6000) are opened from the machine on which you
    access the ManageIQ Console to the ManageIQ.

  - All VNC ports (5900-6000) are opened from the ManageIQ to each
    VMware ESXi host running virtual machines that you want to access.

  - The firewall on VMware ESXi hosts is enabled and that the VMware
    ESXi host firewall ports are opened.

  - The VNC service (`gdbserver`) is running and that the `gdbserver`
    service has an association with ports 5900-6000 usually defined with
    a `/etc/vmware/firewall/service.xml` firewall rules configuration.
    
    The `gdbserver` ruleset must be enabled on each ESXi host running
    virtual machines that will be accessed through the HTML5 console or
    VNC console on the ManageIQ. The ruleset can be configured on the
    host itself, or using the VMware vCenter web user interface.

The following procedures apply to VMware vCenter 5.0 and later.

#### Using SSH to Configure VMware ESXi Hosts to Enable Console Access

Configure the `gdbserver` ruleset on the host using SSH.

1.  Access the host:
    
        # ssh host@example.com

2.  Set the `gdbserver` parameter:
    
        # esxcli network firewall ruleset set --ruleset-id gdbserver --enabled true

3.  Confirm that the ruleset is active:
    
        # esxcli network firewall ruleset list

#### Using the VMware vCenter Web Interface to Configure ESXi Hosts to Enable Console Access

Configure the `gdbserver` ruleset on the host using the VMware vCenter
web user interface.

1.  Select the ESXi host in the VMware vCenter web interface.

2.  Click the **Manage** tab.

3.  Click the **Settings** sub tab.

4.  Click <span class="menuchoice">System \> Security Profile</span>
    from the list on the left.

5.  Click **Edit**.

6.  Select the `gdbserver` ruleset, and then click **OK**.

#### Configuring the VMware ESXi Host Firewall Ports for Console Access

Follow these steps to configure the VMware ESXi host firewall ports for
HTML5 or VNC console access to guest virtual machine consoles. The
firewall ports must be enabled on each VMware ESXi host running virtual
machines that will be accessed through the HTML5 or VNC console on the
ManageIQ.

1.  Log in to your vSphere Client and select
    <span class="menuchoice">Home \> Inventory \> Hosts and
    Clusters</span>.

2.  In the **Hosts/Clusters** tree view, select the VMware ESXi host you
    want to configure for HTML5 or VNC console access.

3.  Select the **Configuration** tab and open the **Software** box.

4.  Select **Security Profile**.

5.  Navigate to the **Firewall Properties** dialog window by selecting
    the **Properties** link from the **Firewall** section.

6.  In the **Firewall Properties**, scroll down to **GDB Server** and
    select it.

7.  Click **OK**.

### Configuring WebMKS Support in ManageIQ

Complete the following steps to enable WebMKS support in ManageIQ.

1.  Log in to the ManageIQ user interface appliance console as the root
    user.

2.  On the ManageIQ user interface appliances, create a folder titled
    `webmks` in the `/var/www/miq/vmdb/public/` directory.
    
        /var/www/miq/vmdb/public/webmks

3.  Download and extract the contents of [VMware WebMKS
    SDK](https://www.vmware.com/support/developer/html-console/) into
    the `webmks` folder.

4.  Log in to the ManageIQ user interface as an administrative user. If
    you are already logged in, refresh the settings page in the ManageIQ
    user interface for the changes to take effect.

5.  Click ![config gear](images/config-gear.png) (**Configuration**).

6.  Click on the **Settings** accordion, then click **Zones**.

7.  Click the zone where the ManageIQ server is located.

8.  Click on the server.

9.  Under **VMware Console Support**, select **VMware WebMKS** from the
    **Use** list.

10. Click **Save**.

### Opening a Console for a Virtual Machine

Open a web-based VNC or SPICE console for a virtual machine.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click on the virtual machine that you want to access.

3.  Click ![screen](images/screen.png) (**Access**) and select **VM
    Console** or **Web Console**.

The virtual machine console opens in a new tab in your browser.

## Managing Virtual Machine Snapshots

A snapshot is a view of a virtual machine’s operating system and
applications on any or all available disks at a given point in time.
Take a snapshot of a virtual machine before you make a change to it that
may have unintended consequences. You can use a snapshot to return a
virtual machine to a previous state.

View virtual machines by infrastructure providers by navigating to
<span class="menuchoice">Compute \> Infrastructure \> Providers</span>.

### Creating a Virtual Machine Snapshot

To create a snapshot of a virtual machine:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine, and open it to view its details.

3.  Under **Properties**, click **Snapshots** to show information about
    the virtual machine’s snapshots.

4.  Click ![plus green](images/plus_green.png)(**Create a new snapshot
    for this VM**).

5.  Enter snapshot details in **Description**.

6.  (Optional) Select **Snapshot VM memory** for the snapshot to
    preserve the virtual machine’s current runtime state. This option
    will appear only if the VM **Power State** is
    ![2143](images/2143.png)(**On**).

7.  Click **Create**.

### Deleting a Virtual Machine Snapshot

To delete a virtual machine snapshot:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the target virtual machine, and open it to view its details.

3.  Under **Properties**, click **Snapshots** to show information about
    the virtual machine’s snapshots.

4.  Select the snapshot to delete under **Available Snapshots**.

5.  Click ![1861](images/1861.png) and select **Delete Selected
    Snapshot**.

6.  Click **OK**.

### Reverting a Virtual Machine to a Snapshot

A virtual machine can be reverted to a previous state using a snapshot.

<div class="important">

The virtual machine state must be powered `off` for the **Revert to
selected snapshot** option to be available.

</div>

To revert a virtual machine to a snapshot:

1.  Power the virtual machine off.

2.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

3.  Select the target virtual machine, and open it to view its details.

4.  Under **Properties**, click **Snapshots** to show information about
    the virtual machine’s snapshots.

5.  Select the snapshot to revert to under **Available Snapshots**.

6.  Click ![revert icon](images/revert_icon.png)(**Revert to selected
    snapshot**).

7.  Click **OK**.

## Creating a Template Based on a Virtual Machine

A template is a copy of a virtual machine (VM) that you can use to
simplify the subsequent, repeated creation of similar VMs. Templates
capture the configuration of software, configuration of hardware, and
the software installed on the VM on which the template is based.

<div class="note">

Virtual machines must meet the following criteria to publish as
templates:

  - The VM must not be blank, archived or orphaned.

  - The VM must be associated with a oVirt Engine provider.

  - oVirt Engine provider 4.0 or higher, with `use_ovirt_engine_sdk` set
    to `true` in `/var/www/miq/vmdb/config/settings.yml` on your
    ManageIQ appliance.

  - The VM power state is `OFF`.

  - Sealing a template is not supported for Windows OS VMs.

</div>

To create a template based on an existing VM:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Providers</span>.

2.  Click on a oVirt Engine provider.

3.  Select a VM.

4.  Click ![Lifecycle](images/2007.png) (**Lifecycle**), then click
    ![Publish selected VM to a Template](images/import.png) (**Publish
    selected VM to a Template**).

5.  Under the **Request** tab, provide **Request Information** and
    identify a **Manager**:
    
    1.  Enter an **E-Mail** address.
    
    2.  Provide a **First** and **Last** name in the individual fields.
    
    3.  Enter a **Manager** name.

6.  Assign tags to the new template in the **Purpose** tab.
    
    1.  Click on a tag category and check applicable tags.

7.  Use fields in the **Catalog** tab to identify the source VM and
    provide details for the template:
    
    1.  Select the source VM from the **Name** field.
    
    2.  (Optional) Check **Seal Template**.
        
        <div class="note">
        
        Sealing, which uses the `virt-sysprep` command, removes
        system-specific details from a virtual machine before creating a
        template based on that VM. This prevents the original VM’s
        details from appearing in subsequent VMs that are created using
        the same template. It also ensures the functionality of other
        features, such as predictable vNIC order.
        
        </div>
    
    3.  The **Number of VMs** indicates the output will be a single
        template.
    
    4.  Provide a **Name** and **Description** for the created template.

8.  Under the **Environment** tab, specify information for the storage
    domain in which to create the template’s disks.
    
    1.  Check **Choose Automatically** to allow ManageIQ to determine
        the destination cluster and datastore.
        
        Or, manually enter cluster and datastore information using the
        following steps:
    
    2.  Select the cluster with which to associate the template from the
        **Cluster** list. By default, this is identical to the cluster
        of the source VM.
    
    3.  Choose a **Datastore** for the destination to create the
        template’s disks.

9.  Provide provisioning and retirement information for VMs based on the
    template in the **Schedule** tab.
    
    1.  Select **Schedule** or **Immediately on Approval** for
        **Schedule Info** to determine when to provision the VM.
    
    2.  Set the **Time to Retirement** under **Lifespan** using the
        drop-down menu.

10. Click **Submit**.

## Retiring Virtual Machines

Specify a retirement date and time for virtual machines or instances
using ManageIQ.

To set retirement date and time:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Select the virtual machines or instances for retirement.

3.  Click ![Lifecycle](images/2007.png) (**Lifecycle**), then select
    **Set Retirement Date**.

4.  Under **Enter Retirement Date as**, select **Specific Date and
    Time**.

5.  Select a date using the calendar control, then click ![Select
    Time](images/2010.png) (**Select Time**).

6.  Specify the hour and minute for retirement.

7.  Select a **Retirement Warning** from the list.

8.  Click **Save**.

## Migrating Virtual Machines

ManageIQ supports migrating virtual machines between datacenters,
clusters, resource pools, folders and hosts. Create and submit a request
with detailed environment information to which to migrate the VM.

To create a request to migrate a virtual machine:

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Virtual Machines</span>.

2.  Click **VMs & Templates** on the accordion menu.

3.  Select the VM to migrate.

4.  Click ![1847](images/1847.png) (Configuration), and then
    ![2007](images/2007.png) (Lifecycle).

5.  Click ![migration icon](images/migration_icon.png) (Migrate selected
    items). The Migrate Virtual Machine form will appear.

6.  Under the **Request** tab:
    
    1.  Provide an **E-mail** address, **First Name** and **Last Name**.
    
    2.  Include any **Notes** and a Manager’s **Name**.

7.  Under the **Environment** tab:
    
    1.  Select a **Datacenter** to migrate the VM to.
    
    2.  Select a **Cluster** from the list.
    
    3.  Choose a **Resource Pool**.
    
    4.  Select a **Folder** to migrate the VM to.
    
    5.  Under **Host** choose a **Filter** and click on a **Name** from
        the list that appears.
    
    6.  **Filter** the **Datastore** and click a **Name** from the
        results.

8.  Under the **Schedule** tab:
    
    1.  Select **Schedule Info** for migrating the virtual machine.
        Provide a **Provision on** date if selecting **Schedule**.

9.  Click **Submit**.

# Resource Pools

Resource pools are used to allocate CPU and memory across a group of
virtual machines.

## Removing a Resource Pool

If a resource pool is decommissioned or requires troubleshooting, it
might require removal from the VMDB.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Resource Pools</span>.

2.  Click on the resource pool to remove.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1861](images/1861.png) (**Remove from the VMDB**).

4.  Click **OK**.

The resource pool is removed. The virtual machines remain in the VMDB,
but are no longer associated with this resource pool.

## Tagging a Resource Pool

Use tags to categorize a resource pool.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Resource Pools</span>.

2.  Click the resource pool to tag.

3.  Click ![1941](images/1941.png) (**Policy**), and then
    ![1851](images/1851.png) (**Edit Tags**).

4.  Select a customer tag from the first dropdown, and then a value for
    the tag.
    
    ![2233](images/2233.png)

## Viewing the Resource Pool Summary

Use the Resource Pool Summary to see the number of discovered virtual
machines, the parent host, and the parent cluster. It is the default
view when you click on one resource pool.

## Resource Pools Accordion

Use the **Resource Pools** accordion to access the properties and
objects associated with the resource pool.

  - Click **Properties** to view the Resource Pools summary screen.

  - Click **Relationships** to see the clusters, virtual machines, and
    hosts related to this resource pool.

# Datastores

A storage location is considered a device where digital information
resides and is connected to a resource. ManageIQ detects, analyzes, and
collects capacity and utilization data for both VMFS and NFS datastores.
Datastores connected to a provider are automatically created on
discovery. On creation of a repository, a datastore is automatically
created.

![datastores](images/datastores.png)

After detecting datastores, you might want to examine them more closely
to see virtual machines, hosts, and available space.

![2237](images/2237.png)

1.  File system type

2.  Number of hosts

3.  Number of virtual machines

4.  Available space

## Performing SmartState Analysis on Datastores

Analyze a datastore to collect information on the types of files on a
datastore, and to see the number of managed/registered,
managed/unregistered, and unmanaged virtual machines. To perform a
SmartState analysis, the datastore is accessible from a running host and
valid security credentials are supplied for that host.

<div class="note">

  - SmartState analysis on datastores is processed by the **Provider
    Operations** role. It is enabled by default.

  - Be aware that executing a SmartState analysis on a datastore from
    the console takes a while to return data on the content. If capacity
    and utilization roles are enabled, ManageIQ performs the analysis
    automatically on a scheduled basis approximately every 24 hours.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Datastores</span>.

2.  Select the datastores to analyze.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Perform SmartState Analysis](images/1942.png) (**Perform
    SmartState Analysis**).

4.  Click **OK**.

## Viewing a Datastore

You can click on a specific datastore to view its details. The screen
provides you with a datastore taskbar, virtual thumbnail, accordion, and
summary.

**Datastore Management Screen.**

![view datastore new](images/view-datastore-new.png)

1.  **Datastore Taskbar**: Choose between **Configuration**, **Policy**
    and **Monitoring** options for the selected datastore.

2.  **Datastore Summary**: See summary such as datastore properties,
    storage, VM information.

3.  **Datastore PDF**: Generates datastore summary in PDF format.

4.  **Datastore Accordion**: See details about **Properties**,
    **Relationships**, **Storage Relationships** and **Content** for the
    chosen datastore.

<div class="note">

To view **Content** section details, run a SmartState Analysis on the
datastore. For information on how to perform SmartState Analysis, see
[Performing SmartState Analysis on
Datastores](#smartstate_analysis_datastore).

</div>

## Tagging a Datastore

Use tags to categorize a datastore.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Datastores</span>.

2.  Click the datastore to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/1851.png) (**Edit Tags**).

4.  Select a customer tag from the first list, and then a value for the
    tag from the second list.
    
    ![2238](images/2238.png)

5.  Select more tags as required.

6.  Click **Save**.

## Viewing Capacity and Utilization Charts for a Datastore

You can view capacity and utilization data for a datastore.

<div class="note">

ManageIQ requires network visibility to your provider assigned the
server role of *Capacity & Utilization Collector* to enable this
feature.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Datastores</span>, then click the Datastore for which to view
    Capacity and Utilization data.

2.  Click ![Monitoring](images/1994.png) (**Monitoring**), and then
    ![Utilization](images/1994.png) (**Utilization**).

3.  From **Interval**, select to view hourly or daily data points and
    the dates to view data.

4.  Use **Show VM Types** to include only managed/registered,
    managed/unregistered, or unmanaged virtual machines.
    
      - **Managed/Registered VM** - A virtual machine connected to a
        host and exists in the VMDB. Also, a template connected to a
        management system and exists in the VMDB.
        
        <div class="note">
        
        Templates cannot be connected to a host.
        
        </div>
    
      - **Managed/Unregistered VM** - A virtual machine or template that
        resides on a repository that is no longer connected to a
        management system or host, but exists in the VMDB. A virtual
        machine previously considered registered might become
        unregistered if the virtual machine is removed from management
        system inventory.
    
      - **Not Managed** - Files discovered on a datastore that do not
        have a virtual machine associated with them in the VMDB. These
        files might be registered to a management system that ManageIQ
        does not have configuration information. Possible causes might
        be the management system has not been discovered or the
        management system has been discovered but no security
        credentials are provided.

5.  Use **Time Profiles** to select a time range for the data.

<div class="note">

Daily charts only include full days of data. If a day does not include
all the 24 data points for a day, the data does not show for that day.

</div>

For information about data optimization including utilization trend
reports, see [Data Optimization](#data-optimization).

## Removing a Datastore

If a datastore no longer contains any files associated with the virtual
environment, remove it from the VMDB. This button is enabled only if a
datastore is completely empty.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Datastores</span>.

2.  Click on the Datastore to remove.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Remove Datastore](images/2098.png) (**Remove Datastore from
    Inventory**).

4.  Click **OK**.

# Data Optimization

ManageIQ optimization functions allow you to view utilization trends in
your environment. In addition, you can predict where you have capacity
for additional virtual machines, see [Planning Where to Put a New
Virtual
Machine](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/deployment_planning_guide/#planning-where-to-put-a-new-virtual-machine)
in the *Deployment Planning Guide*.

<div class="note">

  - To access the utilization report features, you will first need to
    enable data collection in ManageIQ; see the following sections in
    the *Deployment Planning Guide*:
    
      - [Assigning the Capacity and Utilization Server
        Roles](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html/deployment_planning_guide/Capacity_Planning#assigning_the_capacity_and_utilization_server_roles)
    
      - [Capacity and Utilization Data
        Collected](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html/deployment_planning_guide/capacity_planning#data_collected)

</div>

## Utilization Trends

ManageIQ allows you to view the resource utilization of your clusters,
providers, and datastores. You can choose from summary, details, or
report view.

### Viewing a Utilization Trend Summary

This procedure shows you how to view a utilization trend summary.

1.  Navigate to <span class="menuchoice">Overview \> Utilization</span>.

2.  Click **Summary** if it is not already selected.

3.  Expand the tree on the left side, until you can see the desired
    providers, clusters, or datastores.

4.  Click on the item.

5.  Use the **Options** section in the **Summary** tab to change the
    characteristics of the data.
    
      - Use **Trends** to select how far back you want to calculate the
        trend.
    
      - Use **Selected Day** for the date you want to see percent
        utilization for in the chart on the **Summary** tab.
    
      - Use **Classification** to only see trends for a specific applied
        tag.
    
      - Use **Time Profile** to select an existing time profile. If the
        logged on user does not have any time profiles available, this
        option will not show.
    
      - Select a **Time Zone**.

### Viewing Detail Lines of a Utilization Trend

This procedure shows you how to view detail lines of a utilization
trend.

1.  Navigate to <span class="menuchoice">Overview \> Utilization</span>.

2.  Expand the tree on the left side, until you can see the desired
    providers, clusters, or datastores.

3.  Click on the item.

4.  Click **Details** if it is not already selected.

5.  From the **Options** area, select how far back you want to view the
    trends for and any classifications you want to use.

### Viewing a Report of a Utilization Trend

To find out more about resource utilization, view utilization trend
reports.

1.  Navigate to <span class="menuchoice">Overview \> Utilization</span>.

2.  Expand the tree on the left side, until you can see the desired
    providers, clusters, or datastores.

3.  Click on the item.

4.  Click **Report** if it is not already selected.

5.  From the **Options** area, select how far back you want to view the
    trends for and any classifications you want to use.

# PXE Servers

PXE servers are used by ManageIQ to bootstrap virtual machines for the
purpose of provisioning. They include images for different operating
systems that can be customized using customization templates and are
used in conjunction with IPMI Servers.

# Availability Zones

An availability zone is a provider-specific method of grouping cloud
instances and services. ManageIQ uses Amazon EC2 regions and OpenStack
Nova zones as availability zones.

## Viewing an Availability Zone

You can click on an availability zone to view its details. The screen
provides you with an availability zone accordion and an availability
zone summary page.

  - You can choose between graphical or text view of the datastore
    summary.

  - Use the availability zone accordion to view the **Properties** of
    the zone and its **Relationships** to other cloud resources.

  - Use the availability zone summary to see details on
    **Relationships** (**Cloud Provider**, **Instances**) and **Smart
    Management** (**Company Tags**).

## Viewing Availability Zone Relationships

Use the availability zone accordion’s **Relationship** section to see
items related to an availability zone.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Availability Zones</span>.

2.  Click the availability zone to view the configuration.

3.  From the availability zone accordion, click **Relationships**.

4.  Click the type of resource relationship to view as a list.

# Cloud Tenants

A tenant is an OpenStack term for an organizational unit or project.
ManageIQ creates cloud tenants to match existing OpenStack tenants for
managing resources and controlling visibility of objects.

<div class="note">

OpenStack tenant mapping must be enabled for cloud tenants to be
created. See [Tenant Mapping](#tenant-mapping) for details.

</div>

OpenStack uses tenants for the following reasons:

  - Assigning users to a project

  - Defining quotas for a project

  - Applying access and security rules for a project

  - Managing resources and instances for a project

This helps administrators and users organize their OpenStack environment
and define limits for different groups of people. For example, one
project might require higher quotas and another project might require
restricted access to certain ports. OpenStack allows you to define these
limits and apply them to a project.

ManageIQ can abstract information from tenants including quotas and
relationships to other OpenStack objects.

To see multiple tenants in ManageIQ, the user authenticating to your
OpenStack environment from ManageIQ must be configured to have
visibility into these tenants.

<div class="note">

This section describes OpenStack cloud tenant usage. For information
about tenants created in ManageIQ for access and resource control, see
[Access
Control](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/general_configuration/#access-control)
in *General Configuration*.

</div>

## Tenant Mapping

When adding an OpenStack cloud or infrastructure provider, enable
*tenant mapping* in ManageIQ to map any existing tenants from that
provider.

This means ManageIQ will create new cloud tenants to match each existing
OpenStack tenant; each new cloud tenant and its corresponding OpenStack
tenant will have identical resource assignments (including user and role
synchronization) with the exception of quotas. Tenant quotas are not
synchronized between ManageIQ and OpenStack, and are available for
reporting purposes only. You can manage quotas in ManageIQ but this will
not affect the quotas created in OpenStack.

During a provider refresh, ManageIQ will also check for any changes to
the tenant list in OpenStack. ManageIQ will create new cloud tenants to
match any new tenants, and delete any cloud tenants whose corresponding
OpenStack tenants no longer exist. ManageIQ will also replicate any
changes to OpenStack tenants to their corresponding cloud tenants.

If you leave tenant mapping disabled, ManageIQ will not create cloud
tenants or tenant object hierarchy from OpenStack.

## Viewing Cloud Tenant Relationships

From <span class="menuchoice">Compute \> Clouds \> Tenants</span>, click
on a specific cloud tenant to view its details.

The screen provides you with a cloud tenant accordion and a cloud tenant
summary.

  - Use cloud tenant summary views to change how you are looking at the
    **Summary**.

  - Use the cloud tenant accordion to view the **Properties** of the
    tenant and its **Relationships**.

  - Use the cloud tenant summary to see details on **Relationships**
    (**Cloud Provider**, **Security Groups**, **Instances**, and
    **Images**), **Quotas** (including all OpenStack **Compute**,
    **Network**, and **Volume** quotas) and **Smart Management**
    (**Company Tags**).

# Volumes

A volume is a block storage device that you can attach to or detach from
an instance to manage the storage available to that instance. Volumes
are managed through storage managers, which are added automatically to
ManageIQ when the corresponding provider is added.

## Amazon Elastic Block Store Manager Volumes

This section outlines the actions that you can perform on Amazon Elastic
Block Store manager volumes.

### Creating Volumes

You can create and attach volumes to your storage manager.

To create a volume:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![1862](images/1862.png) (**Add a new Cloud Volume**).

3.  Select the Amazon Elastic Block Store manager from the **Storage
    Manager** list.

4.  Select an availability zone from the **Availability Zone** list.

5.  Enter a **Volume Name**.

6.  Select the type of the volume from the **Cloud Volume Type** list.
    
    <div class="note">
    
    See [Amazon EBS Volume
    Types](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html)
    for more information on volume types.
    
    </div>

7.  Enter the size of the volume in gigabytes (GB).

8.  Select whether the volume should be encrypted using the
    **Encryption** toggle.

9.  Click **Add**.

The volume appears in the list of volumes after it has been provisioned.

### Creating a Snapshot of a Volume

You can create a snapshot of a volume to preserve the state of the
volume at a specific point in time. The snapshot can be used to create a
duplicate of the volume.

To create a snapshot of a volume:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click the volume to snapshot to open the volume’s summary page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Create a Snapshot of this Cloud
    Volume](images/volume-icon.png) (**Create a Snapshot of this Cloud
    Volume**).

4.  Enter a name for the snapshot in **Snapshot Name**.

5.  Click **Save**.

Click **Cloud Volume Snapshots** on the summary page of a volume to view
the snapshots for that volume.

### Attaching a Volume to an Instance

To attach a volume to an instance:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to attach.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Attach selected Cloud Volume to an
    Instance](images/volume-icon.png) (**Attach selected Cloud Volume to
    an Instance**) to open the **Attach Cloud Volume** screen.

4.  Select an instance from the list.

5.  Optionally, enter a **Device Mountpoint**.

6.  Click **Attach**.

### Detaching a Volume from an Instance

To detach a volume from an instance:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to detach.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Detach selected Cloud Volume from an
    Instance](images/volume-icon.png) (**Detach selected Cloud Volume
    from an Instance**) to open the **Detach Cloud Volume** screen.

4.  Select an instance from the list.

5.  Click **Detach**.

### Editing a Volume

You can edit several properties of existing volumes.

To edit a volume:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to edit to open its summary page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Edit this Cloud Volume](images/volume-icon.png) (**Edit this
    Cloud Volume**).

4.  Enter a new **Volume Name**.

5.  Select a new volume type from the **Cloud Volume Type** list.
    
    <div class="note">
    
    See [Amazon EBS Volume
    Types](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html)
    for more information on each of the volume types.
    
    </div>

6.  Enter a new size in gigabytes.

7.  Click **Save**.

### Deleting a Volume

To delete a volume from a storage manager:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to delete.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![1861](images/1861.png) (**Delete selected Cloud Volumes**).

## OpenStack Block Storage Manager Volumes

This section outlines the actions that you can perform on OpenStack
Block Storage manager volumes.

### Creating Volumes

You can create and attach volumes to your storage manager.

To create a volume:

<div class="important">

After creating a volume, only the volume name can be edited.

</div>

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![1862](images/1862.png) (**Add a new Cloud Volume**).

3.  Select the OpenStack Block Storage manager from the **Storage
    Manager** list.

4.  Enter a **Volume Name**.

5.  Enter the size of the volume in gigabytes (GB).

6.  Under **Placement**, select the cloud tenant to attach it to.

7.  Click **Add**.

The volume appears in the list of volumes after it has been provisioned.

### Creating a Backup of a Volume

You can create a backup of a volume to protect against data loss, and
restore it in the future.

<div class="important">

For OpenStack Block Storage managers, the `openstack-cinder-backup`
service must be enabled on the OpenStack Block Storage manager to create
a volume backup.

</div>

To create a backup of a volume:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click the volume you want to back up to open the volume’s summary
    page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Create a Backup of this Cloud
    Volume](images/volume-icon.png) (**Create a Backup of this Cloud
    Volume**).

4.  Enter a name for the backup in **Backup Name**.

5.  (Optional) Select **Incremental?** to take an incremental backup of
    the volume instead of a full backup.
    
    <div class="note">
    
    You can take an incremental backup of a volume if you have at least
    one existing full backup of the volume. An incremental volume saves
    resources by capturing only changes made to the volume since its
    last backup. See [Create an Incremental Volume
    Backup](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/storage_guide/ch-cinder#section-create-volume-backup-incremental)
    in the *Storage Guide* for more information.
    
    </div>

6.  (Optional) Select **Force?** to allow backup of a volume attached to
    an instance.
    
    <div class="note">
    
    Selecting the **Force** option will back up the volume whether its
    status is *available* or *in-use*. Backing up an *in-use* volume
    ensures data is crash-consistent.
    
    </div>

7.  Click **Save**.

View a volume’s backups by clicking **Cloud Volume Backups** on the
volume’s summary page.

<div class="note">

See [Back Up and Restore a
Volume](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html/storage_guide/ch-cinder#section-volumes-advanced-backup)
in the *Storage Guide* for more information about backups.

</div>

### Restoring a Volume from a Backup

In case of data loss, you can restore a volume from a backup with the
following steps:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click the volume whose backup you want to restore. This will open
    the volume’s summary page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Restore from a Backup of this Cloud
    Volume](images/volume-icon.png) (**Restore from a Backup of this
    Cloud Volume**).

4.  Select the volume to restore from in the **Cloud Volume Backup**
    list.

5.  Click **Save**.

### Restoring a Cloud Volume from a Backup

In case of data loss, you can restore from a cloud volume backup with
the following steps:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volume Backups</span>.

2.  Select a **Cloud Volume Backup** to restore.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Restore backup to Cloud Volume](images/volume-icon.png)
    (**Restore backup to Cloud Volume**).

4.  Select the **Volume** to restore from the backup.

5.  Click **Save**.

### Deleting a Cloud Volume Backup

Delete unnecessary cloud volume backups through the following steps:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volume Backups</span>.

2.  Select the **Cloud Volume Backups** to delete.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Delete selected Backups](images/1861.png) (**Delete selected
    Backups**).

4.  Click **OK** to confirm your choice.

### Creating a Snapshot of a Volume

You can create a snapshot of a volume to preserve the state of the
volume at a specific point in time. The snapshot can be used to create a
duplicate of the volume.

To create a snapshot of a volume:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Click the volume to snapshot to open the volume’s summary page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Create a Snapshot of this Cloud
    Volume](images/volume-icon.png) (**Create a Snapshot of this Cloud
    Volume**).

4.  Enter a name for the snapshot in **Snapshot Name**.

5.  Click **Save**.

Click **Cloud Volume Snapshots** on the summary page of a volume to view
the snapshots for that volume.

<div class="note">

See [Create, Use, or Delete Volume
Snapshots](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/storage_guide/#section-create-clone-delete-vol-snapshots)
in the *Storage Guide* for more information about snapshots.

</div>

### Attaching a Volume to an Instance

To attach a volume to an instance:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to attach.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Attach selected Cloud Volume to an
    Instance](images/volume-icon.png) (**Attach selected Cloud Volume to
    an Instance**) to open the **Attach Cloud Volume** screen.

4.  Select an instance from the list.

5.  Optionally, enter a **Device Mountpoint**.

6.  Click **Attach**.

### Detaching a Volume from an Instance

To detach a volume from an instance:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to detach.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Detach selected Cloud Volume from an
    Instance](images/volume-icon.png) (**Detach selected Cloud Volume
    from an Instance**) to open the **Detach Cloud Volume** screen.

4.  Select an instance from the list.

5.  Click **Detach**.

### Editing a Volume

Only the volume name can be edited on an existing volume.

To edit a volume’s name:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to edit to open its summary page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Edit this Cloud Volume](images/volume-icon.png) (**Edit this
    Cloud Volume**).

4.  Enter the new **Volume Name**.

5.  Click **Save**.

### Deleting a Volume

To delete a volume from a storage manager:

1.  Navigate to <span class="menuchoice">Storage \> Block Storage \>
    Volumes</span>.

2.  Select the volume to delete.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![1861](images/1861.png) (**Delete selected Cloud Volumes**).

# Flavors

Flavors indicate the resource profiles available for instances. Each
flavor contains a value set for CPUs, CPU cores and memory. Flavors
allow you to pre-configure resource settings, which you can then apply
during instance provisioning. You can also change the flavor of a
provisioned instance; see [Resizing an
Instance](#_to_resize_an_instance_via_flavor) for instructions.

ManageIQ provides the ability to view individual flavor information and
instances currently using the flavor.

## Creating a Flavor

You can create a new flavor for the provider.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Flavors</span>.

2.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1862](images/1862.png) (**Add a new Flavor**).

3.  Select the provider from the **Provider** list.

4.  Enter a **Name** for the flavor.

5.  Enter **RAM size in MB**.

6.  Enter **VCPUs**.

7.  Enter **Disk size in GB**.

8.  Enter **Swap size in MB**.

9.  Enter **RXTX factor**. This is an optional property allows servers
    with a different bandwidth to be created with the RXTX factor. The
    default value is 1. That is, the new bandwidth will be the same as
    that of the attached network.

10. Click **Public** to set `True` or `False`. The default is `True`. If
    you set it to false, select cloud tenants from the **Cloud Tenant**
    list.

11. Click **Add**.

## Viewing a Flavor

You can click on a specific flavor to view its details. The screen
provides you with a flavor accordion and a flavor summary.

  - Use flavor summary views to change how you are looking at the
    summary.

  - Use the flavor accordion to view the **Properties** of the flavor
    and its **Relationships**.

  - Use the flavor summary to see details on **Properties** (**CPUs**,
    **CPU Cores**, **Memory**), **Relationships** (**Cloud Provider**,
    **Instances**), and **Smart Management** (**Company Tags**).

## Viewing Flavor Relationships

Use the **Relationship** section in the flavor accordion to see items
related to the flavor.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Flavors</span>.

2.  Click a flavor to view the configuration.

3.  From the flavor accordion, click **Relationships**.

4.  Click the type of resource to see the flavor’s relationships.

## Deleting a Flavor

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Flavors</span>.

2.  Select the flavors you want to remove from the list.

3.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![Remove Flavor](images/2098.png) (**Remove selected Flavors**).

4.  Cick **OK** on the warning window to remove selected flavors
    permanently.

# Cloud Networks

ManageIQ enables configuration and administration for the
software-defined networking component of Red Hat OpenStack Platform. The
virtual network infrastructure enables connectivity between instances
and the physical external network.

This section describes common cloud network administration tasks, such
as adding and removing subnets and routers to suit your Red Hat
OpenStack Platform providers.

## Creating and Administering Cloud Networks

Create a network to provide instances a place to communicate internally
and receive IP addresses using Dynamic Host Configuration Protocol
(DHCP). A network can also be integrated with external networks in your
Red Hat OpenStack Platform deployment or elsewhere, such as the physical
network.

<div class="note">

  - Keystone API v3 is required to create cloud tenants on Red Hat
    OpenStack Platform cloud providers. For more information, see
    [OpenStack Identity
    (keystone)](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/11/html-single/architecture_guide/#comp-identity)
    in the Red Hat OpenStack Platform *Architecture Guide*.

  - For further details on cloud network objects and administration, see
    the [*Networking
    Guide*](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/12/html-single/networking_guide/#add_an_interface)
    in the Red Hat OpenStack Platform documentation..

</div>

### Adding a Cloud Network

Add a new cloud network following the steps in this procedure:

1.  Navigate to <span class="menuchoice">Networks \> Networks</span>.

2.  Click ![Configuration](images/1847.png)(**Configuration**) and click
    **Add a new Cloud Network**.

3.  In the **Network Providers** area, select a **Network Manager** from
    the drop-down menu.

4.  Under **Placement**, select a **Cloud Tenant**.

5.  In the **Network Provider Information** section, choose a **Provider
    Network Type**.
    
      - If **Local** is selected, provide a **Physical Network** name.
    
      - If **GRE** is selected, provide a **Physical Network** name and
        **Segmentation ID**.

6.  In the **Network Information** area:
    
    1.  Provide a descriptive **Network Name** based on the role the
        network will perform.
    
    2.  Enable an **External Router**
    
    3.  Set the **Administrative State** to control whether the network
        is immediately available.
    
    4.  Establish **Shared** status of the network.

7.  Click **Add**.

### Editing Cloud Network Details

To edit network information details of a cloud network:

1.  Navigate to <span class="menuchoice">Networks \> Networks</span>.

2.  Select a network from the list view.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Edit selected Cloud Network](images/1851.png) (**Edit selected
    Cloud Network**).

4.  Edit **Network Information** fields.

5.  Click **Save**.

### Deleting a Cloud Network

To delete a cloud network:

1.  Navigate to <span class="menuchoice">Networks \> Networks</span>.

2.  Select a cloud network from the list view.

3.  Click ![Configuration](images/1847.png)(**Configuration**), then
    click **Delete selected Cloud Networks**.

## Creating and Administering Subnets

ManageIQ enables creation and administration of subnets for your cloud
networks. Create subnets in pre-existing networks as means to grant
network connectivity to instances. Subnets are the means by which
instances are granted network connectivity. Each instance is assigned to
a subnet as part of the instance creation process.

Consider proper placement of instances to best accommodate their
connectivity requirements:

  - Tenant networks in OpenStack Networking can host multiple subnets.

  - Subnets are isolated from one another.

  - Host distinctly different systems on different subnets within the
    same network.

  - Instances on one subnet that wish to communicate with another subnet
    must have traffic directed by a router.

  - Place systems requiring a high volume of traffic amongst themselves
    in the same subnet, avoiding routing and subsequent latency and load
    issues.

### Adding a Subnet

Add a subnet to an existing cloud network following the procedure below.

1.  Navigate to <span class="menuchoice">Networks \> Subnets</span>.

2.  Click ![Configuration](images/1847.png)(**Configuration**), then
    click **Add a new Cloud Subnet**.

3.  Select a **Network Manager**.

4.  Under **Placement**, select a **Cloud Tenant**.

5.  Provide the following **Cloud Subnet** details:
    
    1.  A descriptive **Subnet Name**.
    
    2.  The **Gateway** IP address of the router interface for the
        default gateway.
    
    3.  **Enable DHCP** services for the subnet. DHCP allows automated
        distribution of IP settings to instances.
    
    4.  Select the **IP Version**. The IP address range in the Network
        Address field must match whichever version you select.
    
    5.  Input the **Subnet CIDR** address in CIDR format, which contains
        the IP address range and subnet mask in one value.
        
        <div class="note">
        
        Determine the address by calculating the number of bits masked
        in the subnet mask and append that value to the IP address
        range. For example, the subnet mask 255.255.255.0 has 24 masked
        bits. To use this mask with the IPv4 address range
        192.168.122.0, specify the address 192.168.122.0/24.
        
        </div>

### Editing a Cloud Subnet

To edit the details of a cloud subnet:

1.  Navigate to <span class="menuchoice">Networks \> Subnets</span>.

2.  Click on a subnet from the list view.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Edit this Cloud Subnet](images/1851.png) (**Edit this Cloud
    Subnet**).

4.  Edit **Cloud Subnet details** fields.

5.  Click **Save**.

## Configuring Network Routers

ManageIQ enables configuration for Red Hat OpenStack Platform provider
cloud network routing services using an SDN-based virtual router.

  - Routers are a requirement for your instances to communicate with
    external subnets, including those out in the physical network.

  - Routers and subnets connect using interfaces, with each subnet
    requiring its own interface to the router.

  - A router’s default gateway defines the next hop for any traffic
    received by the router.

  - A router’s network is typically configured to route traffic to the
    external physical network using a virtual bridge.

### Adding a Network Router

Add a network router to an existing cloud network by following the
procedure below.

1.  Navigate to <span class="menuchoice">Networks \> Network
    Routers</span>.

2.  Click ![Configuration](images/1847.png)(**Configuration**) and click
    **Add a new Router**.

3.  In the **Network Provider** area, select a **Network Manager**.

4.  Provide a **Router Name**.

5.  Under **External Gateway**:
    
    1.  If **Yes** is selected, provide the following:
        
        1.  Choose to **Enable Source NAT**. In Source Network Address
            Translation (SNAT), he NAT router modifies the IP address of
            the sender in IP packets. SNAT is commonly used to enable
            hosts with private addresses to communicate with servers on
            the public Internet.
        
        2.  Select a **Network**.
        
        3.  Select a **Subnet**.

6.  Select a **Cloud Tenant**.

7.  Click **Add**.

### Editing Network Router Details

To edit the details of a network router:

1.  Navigate to <span class="menuchoice">Networks \> Network
    Routers</span>.

2.  Select a network router from the list view.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Edit selected Router](images/1851.png) (**Edit selected Router**).

4.  Edit required fields.

5.  Click **Save**.

### Adding an Interface to a Network Router

Interfaces allow you to interconnect routers with subnets. As a result,
the router can direct any traffic that instances send to destinations
outside of their intermediate subnet.

To add an interface to a network router:

1.  Navigate to <span class="menuchoice">Networks \> Network
    Routers</span>.

2.  Select a network router from the list view.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Add Interface to this Router](images/1851.png) (**Add Interface to
    this Router**).

4.  Select a **Subnet** from the list.

5.  Click **Add**.

### Removing a Network Router Interface

You can remove an interface to a subnet if you no longer require the
router to direct its traffic.

To remove an interface:

1.  Navigate to <span class="menuchoice">Networks \> Network
    Routers</span>.

2.  Select a network router in the list view.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Remove Interface from this Router](images/1851.png) (**Remove
    Interface from this Router**).

4.  Confirm your choice.

### Deleting a Network Router

To delete a network router:

1.  Navigate to <span class="menuchoice">Networks \> Network
    Routers</span>.

2.  Select a network router from the list view.

3.  Click ![Configuration](images/1847.png)(**Configuration**), then
    click **Delete selected Routers**.

## Creating Floating IPs

Floating IP addresses allow you to direct ingress network traffic to
your cloud network instances. Define a pool of validly routable external
IP addresses, which can then be dynamically assigned to an instance. All
incoming traffic destined for that floating IP is routed to the instance
to which it has been assigned.

<div class="note">

Red Hat OpenStack Networking allocates floating IP addresses to all
projects (tenants) from the same IP ranges/CIDRs. As a result, every
subnet of floating IPs is consumable by any and all projects. Manage
this behavior using quotas for specific projects.

</div>

### Adding Floating IPs.

Floating IP addresses allow you to direct ingress network traffic to
your instances.

Add floating IP addresses to an existing cloud network by following the
procedure below.

1.  Navigate to <span class="menuchoice">Networks \> Floating
    IPs</span>.

2.  Click ![COnfiguration](images/1847.png)(**Configuration**) and click
    Add a new Floating IP.

3.  Select a **Network Manager**.

4.  Choose an **External Network**

5.  Under **Association Information** provide the following:
    
    1.  (Optional) An **Associated Port** for the floating IP.
    
    2.  (Optional) The **Floating IP Address**.

6.  Select a **Cloud Tenant**.

7.  Click **Add**.

### Managing Port Association of a Floating IP

To manage the port associations of a floating IP:

1.  Navigate to <span class="menuchoice">Networks \> Floating
    IPs</span>.

2.  Click on a floating IP from the list view.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Manage the port association of this Floating IP](images/1851.png)
    (**Manage the port association of this Floating IP**).

4.  To associate a port, add a new **Port id**

5.  To disassociate a port, delete the **Port id** field information.

6.  Click **Save**.

### Deleting a Floating IP

To delete a floating IP

1.  Navigate to <span class="menuchoice">Networks \> Floating
    IPs</span>.

2.  SClick on a floating IP from the list view to view its summary page.

3.  Click ![Configuration](images/1847.png)(**Configuration**), then
    click **Delete this Floating IP**.

## Security Groups

You can group instances using security groups to restrict port or IP
address accessibility. Security groups can be created and assigned to
instances using ManageIQ instance provisioning.

Cloud providers that currently support this function include: Amazon
EC2, OpenStack, and Red Hat Enterprise Virtualization.

### Editing Security Group Details

Editing security group information allows users to make changes to
existing security group details and firewall rules, in additional to
adding new firewall rules.

To edit details of a security group:

1.  Navigate to <span class="menuchoice">Networks \> Security
    Groups</span>.

2.  Click on a security group to view the summary page.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    ![Edit this Security Group](images/1851.png) (**Edit this Security
    Group**).

4.  Under **Security Group Information**, edit the **Security Group
    Name** and the **Security Group Description**.

5.  Edit existing **Firewall Rules** or add new firewall rules by
    clicking **Add a Firewall Rule**.

6.  Click **Save**.

### Viewing Security Groups

This procedure describes how to view security groups.

1.  Navigate to <span class="menuchoice">Networks \> Security
    Groups</span>.

2.  Click the desired security groups for viewing the details.
    
      - In **Properties**, you can view the basic information of the
        security group.
    
      - In **Relationships**, you can view the cloud provider and the
        instances associated with the security group.
    
      - In **Firewall Rules**, you can view a list of ports and IP
        ranges that are accessible.
        
        <div class="note">
        
        This box is not available if you have not set any rules for your
        security group.
        
        </div>

### Tagging Security Groups

Apply tags to security groups to categorize them.

1.  Navigate to <span class="menuchoice">Networks \> Security
    Groups</span>.

2.  Select the security group to tag.

3.  Click ![1941](images/1941.png) (**Policy**), and then
    ![1851](images/1851.png) (**Edit Tags**).

4.  Select a customer tag to assign from the dropdown menu.

5.  Select a value to assign.

6.  Click **Save**.

### Deleting a Security Group

To delete a security group:

1.  Navigate to <span class="menuchoice">Networks \> Security
    Groups</span>.

2.  Click on a security group in the list view to view its summary page.

3.  Click on ![Configuration](images/1847.png)(**Configuration**), then
    click **Delete this Security Group**.

# Instances and Images

**Images** are the static templates containing the software
configuration from which you provision a running **Instance** - a
virtual machine, with which you can interact - on your cloud provider.

The **Instance** and **Images** containers, combined with the ability to
analyze information inside each instance or image, provides in-depth
information across the cloud environment. This rich set of information
enables ManageIQ users to improve problem resolution times and
effectively manage instances and images in their cloud environment.

The **Instances** and **Images** pages display all instances and images
the server discovered from your cloud providers. The taskbar on each
page is a menu driven set of buttons that provide access to functions
related to instances and images.

![image features](images/image_features.png)

1.  History button

2.  Refresh screen button

3.  Taskbar

4.  Download buttons

5.  View buttons

6.  Name search bar/Advanced Search button

7.  Sort dropdown

8.  Navigation bar

9.  Main area in List View

10. Cloud/Filter Navigation

Console uses Virtual Thumbnails to describe instances and images. Each
thumbnail contains four quadrants by default. This allows you to glance
at an instance or image for a quick view of its contents.

![3393](images/3393.png)

1.  Top left quadrant: Operating system of the Instance

2.  Bottom left quadrant: Instance Cloud Provider

3.  Top right quadrant: Power state of Instance or Status icon

4.  Bottom right quadrant: Number of Snapshots for this Instance

| Icon                     | Description                                                                              |
| ------------------------ | ---------------------------------------------------------------------------------------- |
| ![2138](images/2138.png) | Template: Cloud Image                                                                    |
| ![2139](images/2139.png) | Retired: Instance has been retired                                                       |
| ![2140](images/2140.png) | Archived: Instance has no provider or availability zone associated with it.              |
| ![2141](images/2141.png) | Orphaned: Instance has no availability zone but does have a provider associated with it. |
| ![2142](images/2142.png) | Disconnected: Instance is disconnected.                                                  |
| ![2143](images/2143.png) | On: Instance is powered on.                                                              |
| ![2144](images/2144.png) | Off: Instance is powered off.                                                            |
| ![2145](images/2145.png) | Suspended: Instance has been suspended.                                                  |

The **Instances** page has four accordions organizing your instances and
images in different ways. All of these accordions share a set of common
controls:

  - Use **Instances by Provider** and **Images by Provider** to view
    your instances and images organized by provider. In addition, you
    can see archived and orphaned items here.

  - Use the **Instances** to view, apply filters, and collect
    information about all of your instances.

  - Use **Images** to view, apply filters, and collect information about
    all of your images.

Through the console, you can view your instances and images in multiple
ways:

  - Filter instances

  - Change views

  - Sort

  - Create a report

  - Search by Tags

  - Search by collected data

## Filtering Instances and Images

The **Instance Filter** accordion is provided so that you can easily
navigate through groups of instances. You can use the ones provided or
create your own through **Advanced Filtering** capabilities.

### Using an Instance or Image Filter

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click on the **Instances** or **Images** accordion.

3.  Click on the desired filter from the left pane.

### Creating an Instance or Image Filter

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Go to the **Instances** or **Images** accordion.

3.  Click **All Instances** or **All Images**, then click
    ![2125](images/2125.png) (**Advanced Search**) to open the
    expression editor.

4.  Use the expression editor to choose the appropriate options for your
    criteria. Based on what you choose, different options will show.
    
      - For all of the types of searches, you have the options of
        creating an alias and requested user input. Select **Use Alias**
        to create a user friendly name for the search. If you are
        requested user input for the search, this text will show in the
        dialog box where the input is requested.
    
      - Click **Field** to create criteria based on field values.
        
        ![2126](images/2126.png)
    
      - Click **Count of** to create criteria based on the count of
        something, such as the number of snapshots for an instance, or
        the number of instances on a host.
        
        ![2127](images/2127.png)
    
      - Click **Tag** to create criteria based on tags assigned to your
        virtual infrastructure, such as for power states or production
        tagging.
        
        ![2128](images/2128.png)
    
      - Click **Find** to seek a particular value, and then check a
        property.
        
        ![2130](images/2130.png)

5.  Click ![1863](images/1863.png) (**Commit Expression Element
    Changes**) to add the expression.

6.  Click **Save**.

7.  Type in a name for the search expression in **Save this Instance
    search as**. To set the filter to show globally, check **Global
    Search**.

8.  Click **Save**.

The filter is saved and shows in the **My Filters** area of the
**Filter** accordion. If you checked **Global Search**, the filter shows
there.

### Loading a Report Filter or Search Expression

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the items to search (either **Instances** or
    **Images**).

3.  Click ![2125](images/2125.png) (**Advanced Search**) to open the
    expression editor.

4.  Click **Load**.

5.  Select either a saved instance search or an instance report filter.
    
    <div class="note">
    
    The set of items to select will depend on the type of resource you
    are searching.
    
    </div>

6.  Click **Load** to load the search expression.

7.  If you want to edit the expression, click on it and make any edits
    for the current expression.
    
      - Click ![1863](images/1863.png) (**Commit expression element
        changes**) to add the changes.
    
      - Click ![1899](images/1899.png) (**Undo the previous change**) to
        remove the change you just made.
    
      - Click ![1900](images/1900.png) (**Redo the previous change**) to
        put the change that you just made back.
    
      - Click ![1901](images/1901.png) (**AND with a new expression
        element**) to create a logical `AND` with a new expression
        element.
    
      - Click ![1902](images/1902.png) (**OR with a new expression
        element**) to create a logical `OR` with a new expression
        element.
    
      - Click ![1903](images/1903.png) (**Wrap this expression element
        with a NOT**) to create a logical NOT on an expression element
        or to exclude all the items that match the expression.
    
      - Click ![1904](images/1904.png) (**Remove this expression
        element**) to take out the current expression element.

8.  Click **Load**.

9.  Click **Apply**.

## Changing Views for Instances and Images

While you can set the default view for different pages from the settings
menu, then <span class="menuchoice">Configuration \> My Settings \>
Default Views</span>, the current view can also be controlled from the
Instances pages.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the items to view.

3.  Click the appropriate button for the desired view.
    
      - Click ![2020](images/2020.png) for **Grid View**.
    
      - Click ![2021](images/2021.png) for **Tile View**.
    
      - Click ![2022](images/2022.png) for **List View**.

## Sorting Instances and Images

Virtual machines and images can be sorted by Name, Availability Zone,
Flavor, Cloud Provider, Compliant, Last Analysis Time, and Region.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the desired items to sort.

3.  To sort instances or images when in grid or tile view:
    
      - From the **Sort by dropdown**, click the attribute to sort.

4.  To sort instances or images when in list view:
    
      - Select the **List View**.
    
      - Click on the **Column Name** to sort. For example, click on
        **Availability Zone** to sort by the name of the availability
        zone.

## Creating an Instance or Image Report

For a listing of instances and images, you can create a quick report in
CSV, TXT, or PDF formats.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the desired items for report creation.

3.  Click ![2107](images/2107.png)(**Download**).
    
      - Click ![2133](images/2133.png) for a **TXT** file.
    
      - Click ![2133](images/2133.png) for a **CSV** file.
    
      - Click ![2134](images/2134.png) for a **PDF** file.

## Searching for Instances or Images

To the right of the taskbar on the **Instances** page, you can enter
names or parts of names for searching. You can search in the following
ways.

  - Type characters that are **included** in the name. For example, if
    you type `sp1`, all Instances whose names include `sp1` appear, such
    as `Windows2003` and `Sp1clone`.

  - Use `*` at the end of a term to search for names that begin with
    specific characters. For example, type `v*` to find all instances
    whose names begin with the letter `v`.

  - Use `*` at the beginning of a term to search for names that end with
    specific characters. For example, type `*\sp2` to find all instances
    whose names end with `sp2`.

  - Erase all characters from the search box to go back to viewing all
    instances.

Search for instances and images:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the desired items to search.
    
    ![2136](images/2136.png)

3.  In the **Name Filter** bar in the upper right corner of the window,
    type your criteria.

4.  Click ![2135](images/2135.png)(**Search by Name within results**) or
    press **Enter**.

5.  Type in other criteria to filter on what is currently displayed.

6.  Click ![2135](images/2135.png) (**Search by Name within results**)
    or press **Enter**.

## Analyzing Instances and Images with SmartState Analysis

Analyze an instance to collect metadata such as user accounts,
applications, software patches, and other internal information. If
ManageIQ is not set up for automatic analysis, perform a manual analysis
of an instance. To perform a SmartState Analysis, ManageIQ requires a
running SmartProxy with visibility to the instance’s storage location so
that a snapshot can be created.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the items to analyze.

3.  Check the instances and images to analyze.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1942](images/1942.png) (**Perform SmartState Analysis**) on the
    taskbar.

5.  Click **OK**.

<div class="note">

<div class="title">

Restrictions on Displaying Files Collected

</div>

  - File size bigger than 20k characters

  - File with missing name

  - Non MIME .conf file, with non ascii characters

  - Non MIME .conf file, without content

  - MIME .exe binary file

<!-- end list -->

  - MIME .txt non binary file

  - Non MIME .conf ascii file

</div>

<div class="important">

SmartState Analysis for instances runs as a process independent from
providers. For example, a successful SmartState Analysis of a host does
not mean SmartState Analysis for instances will be successful. Ensure to
enter credentials for the provider that contains the instance for the
SmartState Analysis to work.

</div>

## Comparing Instances and Images

You can compare multiple instances in ManageIQ server. This allows you
to see how different instances are from their original image. This helps
detect missing patches, unmanaged user accounts, or unauthorized
services.

Use the comparison feature to:

  - Compare multiple instances from different hosts

  - Compare multiple instances side-by-side

  - Quickly see similarities and differences among multiple instances
    and a base

  - Narrow the comparison display to categories of properties

  - Print or export in the comparison results to a PDF or CSV file

Compare instances and images:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the items to analyze.

3.  Click the checkboxes for the items to compare.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2148](images/2148.png) (**Compare Selected items**). The
    comparison displays in a compressed view with a limited set of
    properties listed.

5.  To delete an item from the comparison, click
    ![1861](images/1861.png)(**Remove this VM from the comparison**) at
    the bottom of the items column.

6.  To view many items on one screen, go to a compressed view by
    clicking ![2024](images/2024.png) (**Compressed View**). To return
    to an expanded view, click ![2023](images/2023.png) (**Expanded
    View**).

7.  To limit the mode of the view, there are two buttons in the task
    bar.
    
      - Click ![2022](images/2022.png) (**Details Mode**) to see all
        details for an attribute.
    
      - Click ![2025](images/2025.png) (**Exists Mode**) to limit the
        view to if an attribute exists compared to the base or not. This
        only applies to attributes that can have a boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

8.  To change the base instance that all the others are compared to,
    click its label at the top of its column.

9.  To go to the summary screen for an instance, click its **Virtual
    Thumbnail** or icon.

### Creating an Instance Comparison Report

Output a the data from a comparison report in TXT, CSV or PDF formats.

1.  Create the comparison for the report.

2.  Click ![2107](images/2107.png) (**Download**).
    
      - Click ![2133](images/2133.png) for a **TXT** file.
    
      - Click ![2133](images/2133.png) for a **CSV** file.
    
      - Click ![2134](images/2134.png) for a **PDF** file.

## Refreshing Instances and Images

Refresh your instances to get the latest data the provider can access.
This includes information such as the power state, container, and
hardware devices attached to the instance.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the desired items to analyze.

3.  Click the checkboxes for the items to refresh.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2003](images/2003.png)(**Refresh Relationships and Power States**)
    on the **Instance Taskbar**.

## Extracting Running Processes from Instances and Images

ManageIQ can collect processes running on Windows instances. To do this,
enter domain credentials for the zone where the instance is located. The
instance must be running and must have an IP address in the VMDB,
usually obtained from a SmartState Analysis.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the checkboxes for the instances to collect processes.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2152](images/2152.png)(**Extract Running Processes**) on the
    taskbar.

4.  Click **OK**.

## Setting Ownership for Instances and Images

You can set the owner of a group of instances and images by either
individual user or group. This allows you an additional way to filter
and can be used to enforce quotas.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the items to change.

3.  Click the checkboxes for the items to set ownership.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2155](images/2155.png) (**Set Ownership**) on the **Instance
    Taskbar**.

5.  From the **Select an Owner** dropdown, select a user.
    
    ![2156](images/2156.png)

6.  From the **Select a Group** dropdown, select a group

7.  Click **Save**.

## Removing Instances and Images from the VMDB

If an instance has been decommissioned or you need to perform some
troubleshooting, you might need to remove a specific instance from the
VMDB. This does not however remove the instance or image from its
provider.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the items to remove.

3.  Click the checkboxes for the items to remove.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1861](images/1861.png) (**Remove from the VMDB**) button.

5.  Click **OK**.

## Tagging Instances and Images

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the items to tag.

3.  Click the checkboxes for the items to tag.

4.  Click ![1941](images/1941.png) (**Policy**), and then
    ![1851](images/1851.png) (**Edit Tags**).

5.  Select a customer tag from the first dropdown, and then a value for
    the tag.
    
    ![2159](images/2159.png)

6.  Click **Save**.

## Reviewing an Instance or Image

After viewing your list of instances and images, click on a specific
item to review a **Summary** screen of it. The **Summary** screen
provides you with a **Virtual Thumbnail** and a **Taskbar**.

  - Use the **Taskbar** to perform actions on the selected item.

  - Use **Summary Views** to change the view type of the summary screen.

  - Use **Virtual Thumbnails** for a quick glance at the item.

  - Use the **Summary** screen to see a quick summary of the attributes
    of the item.

## Viewing Running Processes after Collection

1.  Click an instance with collected processes.

2.  From the **Diagnostics** area, click **Running Processes**.

The most recent collection of running processes is displayed. Sort this
list by clicking on the column headers.

## Managing Security Groups for Cloud Instances

Manage security groups associated with cloud provider instances using
ManageIQ.

To add a security group to an instance:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click on **Instances by Provider**, and select an instance.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Add a Security Group](images/cloud-security.png) (**Add a
    Security Group**).

4.  Select a **Security Group** from the drop-down menu to add to the
    instance.

5.  Click **Save**.

To remove a security group from an instance:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click on **Instances by Provider**, and select an instance.

3.  Click ![Configuration](images/1847.png) (**Configuration**), then
    click ![Remove a Security Group](images/cloud-security.png)
    (**Remove a Security Group**).

4.  Select a **Security Group** from the drop-down menu to remove from
    the instance.

5.  Click **Save**.

## Editing Instance or Image Properties

Edit the properties of an instance or image to set parent and child
instances. SmartState Analysis also can detect this.

1.  From <span class="menuchoice">Compute \> Clouds \> Instances</span>.

2.  Click the accordion for the items to edit.

3.  Click the item to edit properties.

4.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png)(**Edit this Instance or Edit this Image**)
    on the Taskbar.

5.  From the **Parent Instance** dropdown, select the parent instance.

6.  From **Child Instance** selection, select instances that are based
    on the current instance from the list of **Available Instances**.

7.  Click **Save**.

## Controlling the Power State of an Instance

Follow this procedure to control the power states of an instance through
the ManageIQ console.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the instance to change the power state.

3.  Click **Power Operations**, then click the button for the desired
    power operation.
    
      - Click ![1999](images/1999.png) (**Start**) to start the selected
        instances.
    
      - Click ![2000](images/2000.png) (**Terminate**) to terminate the
        selected instances.
    
      - Click ![2004](images/2004.png) (**Suspend**) to suspend the
        selected instances.
    
      - Click ![2001](images/2001.png) (**Reset**) to reset the selected
        instances.
    
      - Click ![2002](images/2002.png) (**Stop Guest**) to stop the
        guest operating system.
    
      - Click ![2003](images/2003.png) (**Restart Guest**) to restart
        the guest operating system.

4.  Click **OK**.

## Right Sizing an Instance

ManageIQ uses collected statistics to recommend the best size for an
instance. ManageIQ uses the information from the **Normal Operating
Range** to calculate the recommendations.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click an instance for right-sizing.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![2163](images/2163.png) (**Right-Size Recommendations**) button.

A new page appears with three levels of Memory and CPU recommendations,
Conservative, Moderate, and Aggressive, next to the Normal Operating
Range statistics.

## Resizing an Instance

ManageIQ allows you to resize an existing, active instance by changing
its flavor. This is only possible if your OpenStack deployment has:

  - At least two Compute nodes, or with resizing to the same host
    enabled

  - Enough capacity to support the needs of the new flavor

<div class="note">

Keep in mind that the instance will undergo a controlled shutdown when
you change its flavor.

For more information about the requirements and underlying OpenStack
process involved, see [Resize an
Instance](https://access.redhat.com/documentation/en/red-hat-openstack-platform/8/single/instances-and-images-guide/#section-resize-instance)
in the Red Hat OpenStack Platform *Instances and Images Guide*.

</div>

To resize an instance through ManageIQ:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the instance whose flavor you want to change.

3.  Click ![1847](images/1847.png) (**Configuration**), and then
    ![1851](images/1851.png) (**Reconfigure this Instance**).

4.  In the **Reconfigure Instance** section, select the new flavor you
    want from the **Choose Flavor** dropdown.

5.  Click **Submit**. Doing so will initiate the flavor change, and it
    might take several minutes before ManageIQ verifies whether the
    change was successful.

See [Flavors](#flavors) and [Manage
Flavors](https://access.redhat.com/documentation/en/red-hat-openstack-platform/8/single/instances-and-images-guide/#section-flavors)
in the Red Hat OpenStack Platform *Instances and Images Guide* for more
information.

## Migrating a Live Instance

*Live migration* involves moving a live instance between Compute nodes.
Live migration is useful for avoiding instance downtime during cloud
maintenance or load management. See [How to Migrate a Live
Instance](https://access.redhat.com/documentation/en/red-hat-openstack-platform/version-8/migrating-instances/#how_to_migrate_a_live_instance)
in the Red Hat OpenStack Platform *Migrating Instances* guide for
details on the underlying OpenStack process.

To migrate a live instance:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  On the right pane, click the instance to be migrated. Use the
    **Instances by Provider** accordion to filter instances by provider
    and/or availability zone.

3.  Click ![2007](images/2007.png)(**Lifecycle**), then
    ![2097](images/2097.png) (**Migrate selected Instance**).

4.  On the **Migrate Instance** section, select your preferred migration
    options:
    
      - **Auto-select Host?**: let the OpenStack provider automatically
        choose a destination Compute node. If you prefer to choose a
        specific node, uncheck this option and choose from the
        **Destination Host** dropdown.
    
      - **Block Migration**: check this option to perform a
        *block-based* migration. With this migration, the entire virtual
        machine image is moved from the source node to the destination
        node. If your OpenStack provider uses *shared storage*, leave
        this option unchecked. See
        [Prerequisites](https://access.redhat.com/documentation/en/red-hat-openstack-platform/version-8/migrating-instances/#prerequisites)
        in the Red Hat OpenStack Platform *Migrating Instances* guide
        for related information.
    
      - **Disk Over Commit**: check this option to prevent the OpenStack
        provider from verifying first whether the destination host has
        available disk space to host the instance.

5.  Click **Submit**.

Once the migration initiates, the instance list will reload with a
message indicating that the selected instance is being migrated. Upon
completion, the instance list will reload and the evacuated instance
will be displayed as ![2143](images/2143.png) (**On**).

## Evacuating an Instance

If a Compute node is shut down, you can *evacuate* instances hosted on
it. This is only useful if the instances use shared storage or block
storage volumes. See [Evacuate
Instances](https://access.redhat.com/documentation/en/red-hat-openstack-platform/8/single/instances-and-images-guide/#section-migration-evacuation)
in the Red Hat OpenStack Platform *Instances and Images Guide* for
details on the underlying OpenStack process.

To evacuate an instance:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  On the right pane, click the instance to be evacuated. Use the
    **Instances by Provider** accordion to filter instances by provider
    and/or availability zone.

3.  Click ![2007](images/2007.png)(**Lifecycle**), then
    ![2097](images/2097.png)(**Evacuate selected Instance**).

4.  On the **Evacuate Host** section, select your preferred evacuation
    options:
    
      - **Auto-select Host?**: let the OpenStack provider automatically
        choose a destination Compute node. If you prefer to choose a
        specific node, uncheck this option and choose from the
        **Destination Host** dropdown.
    
      - **On Shared Storage**: leave this checked to indicate that all
        instance files are on shared storage.

5.  Click **Submit**.

Once the evacuation initiates, the instance list will reload with a
message indicating that the selected instance is being evacuated. Upon
completion, the instance list will reload and the evacuated instance
will be displayed as ![2143](images/2143.png) (**On**).

## Viewing Capacity and Utilization Charts for an Instance

View capacity and utilization data for instances that are part of a
cluster.

<div class="note">

You must have a server with network visibility to your provider assigned
the server role of **Capacity & Utilization Collector** to use this
feature. For more information, see *General Configuration*.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion to view capacity data.

3.  Click the item to view.

4.  Click ![1994](images/1994.png) (**Monitoring**), and then
    ![1994](images/1994.png) (**Utilization**) on the taskbar.

5.  Select to view hourly, most recent hour, or daily data points for
    the dates to view data.
    
    ![2309](images/2309.png)

6.  Select a **Time Profile**.

![5063](images/5063.png)

<div class="note">

Daily charts only include full days of data. This means ManageIQ does
not show daily data for a day without a complete 24 data point range for
a day.

</div>

For information about data optimization including utilization trend
reports, see [Data Optimization](#data-optimization).

## Viewing the Instance or Image Timeline

View the timeline of events for an instance or image if registered to a
host.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the instance to view the timeline.

3.  Click ![1994](images/1994.png) (**Monitoring**), and then
    ![1995](images/1995.png) (**Timelines**) on the taskbar.

4.  From **Options**, customize the period of time to display, and the
    types of events to view.
    
    ![2166](images/2166.png)
    
      - Use the **Interval** dropdown to select hourly or daily data
        points.
    
      - Use **Date** to type the date of the timeline to display.
    
      - If viewing a daily timeline, use **Show** to set how many days
        back to go. The maximum history is 31 days.
    
      - The three **Event Group** dropdowns allow selection of different
        event groups to display. Each has its own color.
    
      - From the **Level** dropdown, select either a **Summary** event
        or a **Detail** list of events. For example, the detail level of
        a **Power On** event might include the power on request, the
        starting event, and the actual **Power On** event. If you select
        **Summary**, you only see the **Power On** event in the
        timeline.

5.  To see more detail on an item in the timeline, click on it. A
    balloon appears with a clickable link to the resource.

## Viewing the Instance or Image Summary

When you click on a specific instance or image, you will see the
**Virtual Thumbnail**, and an operating system-specific summary screen
of the item. Where applicable, click on a subcategory of the summary to
see more detail on that section.

The summary page contains the following categories:

  - **Properties** include information such as the base operating
    system, hostname, IP addresses, instance vendor, cloud resources,
    and snapshots. This includes the ability to analyze multiple
    partitions, multiple disks, Linux logical volumes, extended
    partitions, and Windows drives. Some categories can be clicked on
    for additional detail. For example, click **Container** to view
    notes associated with an instance.

  - **Lifecycle** shows the date of discovery and the last analysis. If
    a retirement date and time or owner has been set, these display as
    well.

  - **Relationships** include information on the instance’s cloud
    provider, genealogy such as parent and child instances, and drift.

  - **VMsafe** shows properties of the VMsafe agent if it is enabled.

  - **Compliance** shows the status of system compliance checks and
    history of past checks.

  - **Power Management** displays the current power state, last boot
    time, and last power state change. **State Changed On** is the date
    that the instance last changed its power state. This is a container
    view of the power state, therefore a restart of the operating system
    does not cause the container power state to change and does not
    update this value.

  - **Security** includes information on users and groups.

  - **Configuration** includes information on applications, services,
    packages, init processes, and files. This section changes depending
    on the base operating system.

  - **Diagnostics** provides a link to viewing running processes and the
    information from the latest collected event logs.

  - **Smart Management** shows all tags assigned to this instance.

Performing a SmartState Analysis on an instance or image provides more
detailed information in these categories.

## Viewing User Information for an Instance or Image

ManageIQ’s **SmartState Analysis** feature returns user information.
Explore the user to get details on the user’s account, including group
memberships.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click on the instance or image to open its summary page.

3.  From the **Security** section of the summary page, click **Users**.

4.  Click the user to view details.

## Viewing Group Information for an Instance or Image

ManageIQ’s **SmartState Analysis** feature returns group information.
Explore the group to get a list of its users.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the item to view user information.

3.  Click on the item to view its **Summary**.

4.  From the **Security** section of the **Instance Summary**, click
    **Groups**.

5.  Click the group to view users.

## Viewing Genealogy of an Instance or Image

ManageIQ detects the lineage of an instance. View an instance’s lineage
and compare the instances that are part of its tree. This also allows
tagging of instances that share genealogy.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the item to view genealogy.

3.  Click on the item to view its **Summary**.

4.  From the **Relationships** area in the **Summary**, click
    **Genealogy**.

## Detecting Drift on Instances or Images

The configuration of an instance might change over time. **Drift** is
the comparison of an instance to itself at different points in time. The
instance needs to be analyzed at least twice to collect this
information. Detecting drift provides you the following benefits:

  - See the difference between the last known state of a machine and its
    current state.

  - Review the configuration changes that happen to a particular
    instance between multiple points in time.

  - Review the association changes that happen to a particular instance
    between multiple points in time.

  - Review the classification changes that happen to an instance between
    two time checks.

  - Capture the configuration drifts for a single instance across a time
    period.

Detect drift on instances or images:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the item to view drift.

3.  Click on the item to view its **Summary**.

4.  From the **Relationships** area in the **Summary**, click **Drift
    History**.

5.  Click the checkboxes for the analyses to compare.

6.  Click ![1946](images/1946.png) (**Select up to 10 timestamps for
    Drift Analysis**)\] at the top of the screen. The results display.

7.  Check the **Drift** sections on the left to view in your comparison.

8.  Click **Apply**.

9.  The following descriptions pertain to the **Expanded View**
    ![2023](images/2023.png). Whether you see the value of a property or
    an icon representing the property depends on the properties type.
    
      - A property displayed in the same color as the base means the
        compared analysis matches the base for that property.
    
      - A property displayed in a different color from the base means
        the compared analysis does not match the base for that property.

10. If you are in the **Compressed View** ![2024](images/2024.png), the
    values of the properties are not displayed. All items are described
    by the icons shown below.
    
      - A ![2150](images/2150.png) (**checkmark**) means that the
        compared analysis matches the base for that property. If you
        hover over it, the value of the property will display.
    
      - A ![2177](images/2177.png) (**triangle**) means the compared
        analysis does not match the base for that property. If you hover
        over it, the value of the property displays. Click the minus
        sign next to the sections name to collapse it.

11. To limit the scope of the view, you have three buttons in the
    **Resource** button area.
    
      - Click ![2178](images/2178.png) (**All attributes**) to see all
        attributes of the sections you selected.
    
      - Click ![2204](images/2204.png) (**Attributes with different
        values**) to see only the attributes that are different across
        the drifts.
    
      - Click ![2148](images/2148.png) (**Attributes with the same
        values**) to see only the attributes that are the same across
        drifts.

12. To limit the mode of the view, there are two buttons in the
    **Resource** button area.
    
      - Click ![2022](images/2022.png) (**Details Mode**) to see all
        details for an attribute.
    
      - Click ![2025](images/2025.png) (**Exists Mode**) to only see if
        an attribute exists compared to the base or not. This only
        applies to attributes that can have a Boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

This creates a drift analysis. Download the data or create a report from
your drift for analysis using external tools.

## Creating a Drift Report for an Instance or Image

1.  Create the comparison to analyze.

2.  Click ![2107](images/2107.png) (**Download**).

3.  Click the output button for the type of report you want.
    
      - Click ![2133](images/2133.png) (**Download drift report in text
        format**) for a text file.
    
      - Click ![2133](images/2133.png) (**Download drift report in CSV
        format**) for a csv file.
    
      - Click ![2134](images/2134.png) (**Download drift report in PDF
        format**) for a PDF file.

## Viewing Analysis History for an Instance or Image

Each time a SmartState Analysis is performed on an instance, a record is
created of the task. This information is accessed either from the
instance accordion or the instance summary. Use this detail to find when
the last analysis was completed and if it completed successfully. If the
analysis resulted in an error, the error is shown here.

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the desired item to view analysis history.

3.  Click on the item to view its summary.

4.  From the **Relationships** area in the summary, click **Analysis
    History**. A history of up to the last 10 analyses is displayed.
    
    ![2179](images/2179.png)

5.  Click on a specific analysis to see its details.

## Viewing Event Logs for an Instance or Image

Using an **Analysis Profile**, collect event log information from your
instances.

See section "Setting a Default Analysis Profile" in *General
Configuration*.

<div class="note">

This feature is only available for Windows.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span>.

2.  Click the accordion for the item to view event logs.

3.  Click on the item to view its **Summary**.

4.  From **Diagnostics** click **Event Logs**.

The collected event log entries are displayed. Sort this list by
clicking on the column headers.

# Orchestration Stacks

Navigate to <span class="menuchoice">Compute \> Clouds \> Stacks</span>
to see a list of orchestration stacks along with information such as
*Name*, *Provider*, *Type*, *Status*, *Instances*, *Security Groups*,
and *Cloud Networks*. Click on a stack to see more information about it,
including properties, retirement date and time, and relationships with
the cloud provider and instances. You can click on instances to see
details of all instances the stack relates to.

## Tagging Orchestration Stacks

Apply tags to orchestration stacks to categorize them together at the
same time. . Navigate to <span class="menuchoice">Compute \> Clouds \>
Stacks</span>. . Select the orchestration stacks to tag. . Click
![Policy](images/1941.png) (**Policy**), and then ![Edit
Tags](images/2158.png) (**Edit Tags**). . **Select a customer tag to
assign** from the first list. . Select a value to assign from the second
list. . Click **Save**.

## Retiring Orchestration Stacks

You can either retire orchestration stacks on a set date and time, or
retire them immediately.

To set a retirement date:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Stacks</span>.

2.  Select the orchestration stacks to retire on a set date and time.

3.  Click ![2007](images/2007.png)(**Lifecycle**), and then ![Set
    Retirement Dates](images/retirement.png) (**Set Retirement Dates**).

4.  On the **Retire Orchestration Stacks** page, set **Retirement Date
    and Time**.

5.  Select **Retirement Warning** from the list. The default is *None*.

6.  Click **Save**.

<div class="note">

Saving a blank date will remove all retirement dates.

</div>

To retire selected stacks immediately:

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Stacks</span>.

2.  Select the orchestration stacks to retire now.

3.  Click ![2007](images/2007.png)(**Lifecycle**), and then ![Retire
    selected Stacks](images/retirement.png) (**Retire selected
    Orchestration Stacks**). A pop-up window appears to confirm the
    action.

4.  Click **OK**.

## Removing Orchestration Stacks

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Stacks</span>.

2.  Select the orchestration stacks to remove from the VMDB. A warning
    pop-up window appears to confirm the action.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Remove Orchestration Stacks](images/2098.png) (**Remove
    Stacks from the VMDB**).

4.  Click **OK**.

# Key Pairs

This tab lists key pairs and fingerprints for all cloud providers. Click
on a key pair to see a summary and its relationship with instances. On
this screen, click on instances to see details of all instances the key
pair relates to. You can use the key pairs added during provisioning
instances.

<div class="note">

Adding a new key pair is currently only supported for OpenStack.

</div>

## Adding a New Key Pair

1.  Navigate to <span class="menuchoice">Compute \> Clouds \> Key
    Pairs</span>.

2.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1862](images/1862.png) (**Add a new Key Pair**).

3.  In **Basic Information**, enter a **Name** and the **Public Key
    (optional)** generated using **ssh-keygen** command.

4.  Select your OpenStack provider from the **Provider** list.

5.  Click **Add**.

## Removing a Key Pair

1.  Navigate to <span class="menuchoice">Compute \> Clouds \> Key
    Pairs</span>.

2.  Select the key pair you want to remove from the key pairs list. Or,
    click on the key pair to see the instances it relates to.

3.  Click ![1847](images/1847.png) (**Configuration**), then click
    ![1861](images/1861.png) (**Remove selected Key Pairs from
    Inventory**). A warning appears to confirm the action.

4.  Click **OK**.

## Downloading Key Pairs

1.  Navigate to <span class="menuchoice">Compute \> Clouds \> Key
    Pairs</span>. You will see a list of existing key pairs.

2.  Click the ![Download](images/download-button.png) button, then
    select the option to download key pairs data in your preferred
    format:
    
    1.  Download as Text
    
    2.  Download as CSV
    
    3.  Print or export as PDF

# Object Stores

Navigate to <span class="menuchoice">Storage \> Object Stores</span> to
see a list of all cloud object stores along with information including
*Key*, *Size (bytes)*, *Object Count*, *Cloud Tenant*, and *Cloud
Provider*. Click on an object store to see its properties and
relationships with the cloud provider, tenant, and object store on the
summary page.

## Tagging Object Stores

Apply tags to object stores to categorize them together at the same
time.

1.  Navigate to <span class="menuchoice">Storage \> Object
    Stores</span>.

2.  Select the object stores to tag.

3.  Click ![Policy](images/1941.png) (**Policy**), and then ![Edit
    Tags](images/2158.png) (**Edit Tags**).

4.  **Select a customer tag to assign** from the first list.

5.  Select a value to assign from the second list.

6.  Click **Save**.

# VMware Networking Switches

After adding a VMware provider, ManageIQ automatically discovers all
vSphere distributed switches (vDS) on that provider and collects the
information in the ManageIQ inventory.

Navigate to <span class="menuchoice">Compute \> Infrastructure \>
Networking</span> to see a list of all VMware switches, along with
information including *Name*, *Ports*, and *UUID*. Switches and port
groups are listed by provider, then cluster on the sidebar.

Click on a switch to view its summary page, which displays relationships
with hosts, and any tags.

## Tagging VMware Networking Switches

Use tags to categorize vSphere distributed switches.

1.  Navigate to <span class="menuchoice">Compute \> Infrastructure \>
    Networking</span>.

2.  Select the switches to tag.

3.  Click ![1941](images/1941.png) (**Policy**), and then
    ![1851](images/1851.png) (**Edit Tags**).
    
    ![VDS tagging](images/VDS-tagging.png)

4.  Select a customer tag from the first dropdown, and then a value for
    the tag.

5.  Select more tags or click **Save** to apply the tags.

# Container Entities

This chapter provides information on managing resources on your
containers providers.

## The Containers Overview Page

The containers overview page shows information on all containers
providers and entities known to ManageIQ. The **Overview** page provides
links to other summary pages which contain further information on the
containers providers and entities. The **Overview** page also provides
metrics for **Aggregated Node Utilization**, **Network Utilization
Trend**, **New Image Usage Trend**, **Node Utilization**, and **Pod
Creation and Deletion Trends**.

![Containers Overview](images/containers-overview.png)

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Overview</span>.

2.  Click the desired containers entity, or provider, if applicable, for
    viewing the summary with further information.

<div class="note">

To reliably associate pods and images, ManageIQ requires information
from the `docker-pullable` field, added in OpenShift 3.3.1.2. This can
affect the results of the **Chargeback by Image** report for older
OpenShift providers, and potentially cause image inspection (done as
part of Smart State Analysis) to fail due to associating a container to
the wrong image. Consequently, ManageIQ may not report accurate
information about pods and images in OpenShift providers before version
3.3.1.2.

</div>

## Viewing a Container Entity Summary

Container entity (object) summaries are found at
<span class="menuchoice">Compute \> Containers \> *Entity*</span>, where
you can view information about container entities and their components.

  - Viewing a Containers Provider Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span> to view information on different aspects of a
    containers provider. The summary includes:
    
      - The status of the provider and its components.
    
      - The relationships between different entities of the containers
        provider. These relationships are summarized in the
        **Relationships** box on the right-hand side of the summary
        page.
        
        ![Entity Relationships](images/entity-relationships.png)
    
      - Additional information on aggregated capacity of all CPU cores
        of all nodes, and aggregated capacity of all memory of all
        nodes.

<!-- end list -->

  - Viewing a Container Nodes Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Container Nodes</span> to view information on different aspects of a
    container node. The summary includes:
    
      - The number of entities on a node.
    
      - A node’s capacity and utilization.
    
      - The version of the underlying operating system and software.

To view the timeline of events for a node from a container nodes summary
page, click ![Monitoring](images/1994.png) (**Monitoring**), and then
![Timelines](images/1995.png) (**Timelines**).

  - Viewing a Containers Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Containers</span> to view information on different aspects of a
    container. The summary includes:
    
      - The relationships of the container to a related node, pod, or
        image.
    
      - The node the container runs on.
    
      - The container ID.
    
      - Properties of the container image, such as name, tag, etc.

<!-- end list -->

  - Viewing a Container Images Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Container Images</span> to view information on different aspects of
    a container image. The summary includes:
    
      - The containers currently using the images.
    
      - The image registry the image is from.

<!-- end list -->

  - Viewing an Image Registries Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \> Image
    Registries</span> to view information on different aspects of an
    image registry. The summary includes:
    
      - Which images are from the registry.
    
      - The number of images that come from that registry.
    
      - Which containers use images from that registry.
    
      - The host and port of the registry.

<!-- end list -->

  - Viewing a Pods Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Pods</span> to view information on different aspects of a pod. The
    summary includes:
    
      - The containers that are part of the pod.
    
      - The services that reference the pod.
    
      - The node the pod runs on.
    
      - If the pod controlled by a replicator.
    
      - The IP address of the pod.

<!-- end list -->

  - Viewing a Replicators Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Replicators</span> to view information on different aspects of a
    replicator. The summary includes:
    
      - The number of requested pods.
    
      - The number of current pods.
    
      - The labels and selector for the replicator.

<!-- end list -->

  - Viewing a Container Services Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Container Services</span> to view information on different aspects
    of a container service. The summary includes:
    
      - The pods that the container service provide traffic to.
    
      - The port configurations for the container service.
    
      - The labels and selector for the container service.

<!-- end list -->

  - Viewing a Volumes Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Volumes</span> to view information on the persistent volumes of a
    container provider. The summary includes:
    
      - The pods the volume is connected to.
    
      - The volume’s connection parameters.
    
      - The volume’s storage capacity.
    
      - The volume’s iSCSI target details (if applicable).

<!-- end list -->

  - Viewing a Container Builds Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Container Builds</span> to view different aspects of a container
    build. The summary includes:
    
      - The build configuration the container build is based on.
    
      - Which build instances have been created.
    
      - Which phase in the build process the instance has completed.
    
      - Which pod a build instance reside in.

<!-- end list -->

  - Viewing a Container Templates Summary  
    Navigate to <span class="menuchoice">Compute \> Containers \>
    Container Templates</span> to view different aspects of a container
    template. The summary includes:
    
      - The project the template is associated with.
    
      - The objects the template contains.
    
      - The parameters that can be used with the template’s objects.
    
      - The template’s version number.

## Using the Topology Widget

The **Topology** widget is an interactive topology graph, showing the
status and relationships between the different entities of the
containers providers and projects to which ManageIQ has access.

  - The topology graph includes pods, containers, services, nodes,
    virtual machines, hosts, routes, and replicators within the overall
    containers provider environment.

  - Each entity in the graph displays a color indication of its status.

  - Hovering over any individual graph element will display a summary of
    details for the individual element.

  - Double-click the entities in the graph to navigate to their summary
    pages.

  - It is possible to drag elements to reposition the graph.

  - Click the legend at the top of the graph to show or hide entities.

  - Click **Display Names** on the right-hand side of the page to show
    or hide entity names.

### Viewing the Topology for Container Providers

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Providers</span>.

2.  Click the desired containers provider for viewing the provider
    summary.

3.  On the provider summary page, click **Topology** in the **Overview**
    box on the right side of the page.

### Viewing the Topology for Container Provider Projects

The project topology page displays the project as the center node,
surrounded by its related entities.

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Projects</span>.

2.  Click on a project.

3.  On the project summary page, click ![Topology View
    button](images/topologyviewbutton.png) (**Topology View**) on the
    top right side of the page.

### Limiting the Number of Containers Shown in the Topology View

1.  Navigate to the settings menu, then **My Settings**, and click on
    the **Visual** tab.

2.  Select the number of container items from the drop-down under
    **Topology Default Items in View**.

3.  Click **Save**.

## Analyzing Container Images with SmartState Analysis

Perform a SmartState Analysis of a container image to inspect the
packages included in an image.

1.  Navigate to <span class="menuchoice">Compute \> Containers \>
    Container Images</span>.

2.  Check the container image to analyze. You can check multiple images.

3.  Click ![Configuration](images/1847.png) (**Configuration**), and
    then ![Perform SmartState Analysis](images/1942.png) (**Perform
    SmartState Analysis**).

The container image is scanned. The process will copy over any required
files for the image. After reloading the image page, all new or updated
packages are listed.

To monitor the status of container image SmartState Analysis tasks,
navigate to the settings menu, then **Tasks**. The status of each task
is displayed including time started, time ended, what part of the task
is currently running, and any errors encountered.

<div class="note">

See [*Scanning Container Images in CloudForms with
OpenSCAP*](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/scanning_container_images_in_cloudforms_with_openscap/)
for details on scanning container images using OpenSCAP policies.

</div>

## Configuring Automatic Tagging for Container Entities

Container object labels in OpenShift can be used to automatically create
tags and tag categories in ManageIQ. This is done by mapping ManageIQ
tags to existing OpenShift or Kubernetes labels.

Labels from OpenShift can be mapped to ManageIQ tags for the following
container entities:

  - Projects

  - Nodes

  - Routes

  - Replicators

  - Container services

  - Pods

  - Container builds

<div class="note">

Tags automatically created from OpenShift labels are completely managed
by the ManageIQ system and cannot be manually assigned or unassigned.
Deleting a mapping rule from ManageIQ immediately deletes the resulting
tags.

</div>

You can view a container entity’s OpenShift labels on the entity’s
details page under **Labels**.

The following example shows how to configure tagging for a node, but the
same steps can be used for mapping labels to tags on other container
entities.

To configure automatic tagging on container entities using labels:

1.  Note the *key* of the OpenShift label you want to map to a ManageIQ
    tag. OpenShift labels consist of two parts: a *key* and a *value*.
    
    1.  Navigate to <span class="menuchoice">Compute \> Containers \>
        Nodes</span>.
    
    2.  Select a node to open its summary page.
    
    3.  Under **Labels**, note the label(s) to map to ManageIQ tag(s).
        Any OpenShift labels will list the *key* in the left column of
        the **Labels** table, and the *value* in the right column of the
        **Labels** table.
        
        This node has six labels (key/value pairs) that were created in
        OpenShift and collected in the ManageIQ inventory:
        
        ![OCPnode summary](images/OCPnode-summary.png)
        
        <div class="note">
        
        To create an OpenShift label, see [Developer CLI
        Operations](https://docs.openshift.com/container-platform/3.3/cli_reference/basic_cli_operations.html)
        in the OpenShift Container Platform *CLI Reference* guide. A new
        label added in OpenShift will only show up in ManageIQ after the
        next OpenShift provider refresh.
        
        </div>

2.  Navigate to **Configuration** and select the region.

3.  Click the **Map Tags** tab.

4.  Click **Add** to create a new mapping rule.
    
    1.  Select a container entity to tag from the **Entity** list, or
        select **\<All\>** to tag all entities.
    
    2.  Specify the *key* from the OpenShift label you noted earlier in
        the **Label** field.
    
    3.  Specify a ManageIQ tag category in **Category** to map the label
        to. If the tag category does not exist yet in ManageIQ, it will
        be created automatically.
        
        ![Add label mapping](images/Add_label_mapping.png)
    
    4.  Click **Add**. The mapping will show in the table on the **Map
        Tags** tab.

5.  Refresh the provider to complete the mapping:
    
    1.  Navigate to <span class="menuchoice">Compute \> Containers \>
        Providers</span>.
    
    2.  Select the provider to refresh.
    
    3.  Click ![1847](images/1847.png) (**Configuration**), and then
        ![2003](images/2003.png) (**Refresh Items and Relationships**).

The label will display on the entity’s summary page under **Smart
Management** under **Company Tags** as `<Category> : <value>`.

![OCP autotagged](images/OCP-autotagged.png)

Any container entity with the OpenShift `zone` label will be tagged
automatically as `category1` in ManageIQ. If the *value* for `zone` is
`south`, for example, the entity will be tagged as `category1 : south`.

You can use these tags to create reports. See [Monitoring, Alerts, and
Reporting](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.7/single/monitoring-alerts-and-reporting/)
for details on creating reports.
