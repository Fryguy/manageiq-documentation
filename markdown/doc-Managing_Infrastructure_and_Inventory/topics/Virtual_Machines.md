The heterogeneous virtual machine container and guest support combined
with the ability to analyze information inside the virtual machine -
such as disk space, patch level or installed applications - provides
in-depth information across the virtual environment. This rich set of
information enables {product-title} users to improve problem resolution
times and effectively manage virtual machines.

The **Virtual Machines** pages display all virtual machines that were
discovered by your server. Note that if you have applied a filter to a
user, it will be in effect here. The **Virtual Machines** taskbar is a
menu driven set of buttons that provide access to functions related to
virtual machines.

![2124](2124.png)

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

![2137](2137.png)

1.  Top left quadrant: Operating system of the Virtual Machine

2.  Bottom left quadrant: Virtual Machine Hosts software

3.  Top right quadrant: Power state of Virtual Machine or Status icon

4.  Bottom right quadrant: Number of Snapshots for this Virtual Machine

| Icon              | Description                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![2138](2138.png) | Template: Virtual Template                                                                                                                                                                                                                                                                                                                                                                                                                |
| ![2139](2139.png) | Retired: When a virtual machine or instance is no longer required, it can be retired. Once a virtual machine or instance reaches its retirement date and time, it is immediately shut down and not allowed to restart. If an attempt to restart is made, {product-title} will shut down the virtual machine or instance.                                                                                                                  |
| ![2140](2140.png) | Archived: An archived virtual machine has no host or datastore associated with it. Archiving is done to move virtual machines to a low cost storage, either on demand or during retirement, if requested, to avoid incurring extra cost on a virtualized infrastructure due to virtual machine sprawl.                                                                                                                                    |
| ![2141](2141.png) | Orphaned: An orphaned virtual machine has no host but has a datastore associated with it. Orphaned virtual machines are those that have been removed from their providers but still exist on the storage. An orphaned virtual machine is unable to identify the associated host. A virtual machine also shows as orphaned if it exists on a different host than the host expected by the provider’s server.                               |
| ![2142](2142.png) | Disconnected: A disconnected virtual machine is one that has lost connection to either the provider’s storage, host, or both. A disconnect is usually a result of network issues on the provider side. For instance, if during virtual machine provisioning the storage is not set up or deleted, the virtual machine will still exist on the provider, but will not run on the host as it has lost connection to its provider’s storage. |
| ![2143](2143.png) | On: Virtual Machine is powered on.                                                                                                                                                                                                                                                                                                                                                                                                        |
| ![2144](2144.png) | Off: Virtual Machine is powered off.                                                                                                                                                                                                                                                                                                                                                                                                      |
| ![2145](2145.png) | Suspended: Virtual Machine has been suspended.                                                                                                                                                                                                                                                                                                                                                                                            |

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

# Filtering Virtual Machines and Templates

The **Virtual Machine Filter** accordion is provided so that you can
easily navigate through groups of virtual machines. You can use the ones
provided or create your own through **Advanced Filtering** capabilities.

1.  Navigate to menu:Compute\[Infrastructure \> Virtual Machines\].

2.  Go to the **VMs** or **Templates** accordion.

3.  Click on the desired filter from the left pane.

Unresolved directive in Virtual\_Machines.adoc -
include::To\_create\_a\_Virtual\_Machine\_or\_Template\_Filter.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_load\_a\_report\_filter\_or\_search\_expression.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Changing\_Views.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Sorting\_Virtual\_Machines\_and\_Templates.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Creating\_a\_Virtual\_Machine\_or\_Template\_Report.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Searching\_by\_Virtual\_Machine\_or\_Template\_Name.adoc\[\]

# Analyzing Virtual Machines and Templates

Analyze a virtual machine to collect metadata such as user accounts,
applications, software patches, and other internal information. If
{product-title} is not set up for automatic analysis, perform a manual
analysis of a virtual machine. To perform a SmartState analysis,
{product-title} requires a running SmartProxy with visibility to the
virtual machine’s storage location. If the virtual machine is associated
with a host or provider, ensure the virtual machine is registered with
that system to be properly analyzed; the server requires this
information since a snapshot might be created.

<div class="note">

SmartState Analysis of a virtual machine requires access to its host. To
perform a successful analysis, edit the virtual machine’s host and enter
the host’s authentication credentials.

</div>

1.  Navigate to menu:Compute\[Infrastructure \> Virtual Machines\].

2.  Click the accordion for the items to analyze.

3.  Check the **Virtual Machines** and **Templates** to analyze.

4.  Click ![1847](1847.png) (**Configuration**), then ![1942](1942.png)
    (**Perform SmartState Analysis**).

5.  Click **OK**.

## Red Hat Enterprise Virtualization Prerequisites

Unresolved directive in Virtual\_Machines.adoc -
include::Storage\_Support\_Notes\_about\_Analyzing\_from\_RHEVM\_3.1.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Storage\_Support\_Notes\_about\_Analyzing\_from\_RHEVM\_3.0.adoc\[\]

## VMware vSphere Prerequisites

### Installing VMware VDDK on {product-title\_short}

Unresolved directive in Virtual\_Machines.adoc -
include::/common/installing-vmware-vddk.adoc\[\]

# Comparing Virtual Machines and Templates

The {product-title} Server allows you to compare multiple virtual
machines. This allows you to see how different virtual machines are from
their original template. This helps detect missing patches, unmanaged
user accounts, or unauthorized services.

Use the comparison feature to:

  - Compare multiple virtual machines from different hosts.

  - Compare multiple virtual machines side-by-side.

  - Quickly see similarities and differences among multiple virtual
    machines and a base.

  - Narrow the comparison display to categories of properties.

  - Print or export in the comparison results to a PDF or CSV file.

Compare virtual machines and templates:

1.  Navigate to menu:Compute\[Infrastructure \> Virtual Machines\].

2.  Click the accordion for the items to analyze.

3.  Check the items to compare.

4.  Click ![1847](1847.png) btn:\[(Configuration)\], and then
    ![2148](2148.png) btn:\[(Compare Selected items)\]. The comparison
    displays in a compressed view with a limited set of properties
    listed.
    
    ![2149](2149.png)

5.  To delete an item from the comparison, click
    ![1861](1861.png)btn:\[(Remove this item from Inventory)\] at the
    bottom of the items column. This option is only available when
    comparing more than two virtual machines.

6.  To view many items on one screen, go to a compressed view by
    clicking ![2024](2024.png) btn:\[(Compressed View)\]. To return to
    an expanded view, click ![2023](2023.png) btn:\[(Expanded View)\].

7.  To limit the mode of the view, there are two buttons in the task
    bar.
    
      - Click ![2022](2022.png) btn:\[(Details Mode)\] to see all
        details for an attribute.
    
      - Click ![2025](2025.png) btn:\[(Exists Mode)\] to limit the view
        to if an attribute exists compared to the base or not. This only
        applies to attributes that can have a boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

8.  To change the base virtual machine that all the others are compared
    to, click its label at the top of its column.

9.  To go to the summary screen for a virtual machine, click its
    btn:\[Virtual Thumbnail\] or icon.

Unresolved directive in Virtual\_Machines.adoc -
include::Virtual\_Machine\_and\_Templates\_Comparison\_Sections.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_use\_Comparison\_Sections.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_create\_a\_comparison\_report.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Controlling\_Power\_State\_of\_RHV\_VMs.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Refreshing\_Virtual\_Machines\_and\_Templates.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Extracting\_Running\_Processes.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_set\_ownership.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Removing\_Virtual\_Machines\_and\_Templates\_from\_the\_VMDB.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_tag\_Virtual\_Machines\_and\_Templates.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Viewing\_VMware\_Storage\_Profiles.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_running\_processes\_after\_collection.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_edit\_Virtual\_Machine\_or\_Template\_Properties.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Setting\_Ownership\_of\_a\_Virtual\_Machine\_or\_Template.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_right-size\_a\_Virtual\_Machine.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_capacity\_and\_utilization\_charts\_for\_a\_Virtual\_Machine.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_the\_timeline\_for\_a\_Virtual\_Machine\_or\_Template.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Virtual\_Machine\_or\_Template\_Summary.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Viewing\_the\_Operating\_System\_Properties.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Viewing\_Virtual\_Machine\_or\_Template\_Snapshot\_Information.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_a\_users\_group\_memberships.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_a\_groups\_members.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Viewing\_Genealogy\_of\_a\_Virtual\_Machine\_or\_Template.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_and\_compare\_genealogy.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_tag\_Virtual\_Machines\_or\_Templates\_with\_a\_common\_genealogy.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Viewing\_Drift\_on\_Virtual\_Machines\_or\_Templates.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_create\_a\_drift\_report.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_analysis\_history.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_disk\_information.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Reconfiguring\_VMs.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::To\_view\_event\_logs.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::VNC\_and\_SPICE\_consoles.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Snapshots.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::create-template-based-on-vm.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Retiring\_Virtual\_Machines.adoc\[\]

Unresolved directive in Virtual\_Machines.adoc -
include::Migrate\_VMs.adoc\[\]
