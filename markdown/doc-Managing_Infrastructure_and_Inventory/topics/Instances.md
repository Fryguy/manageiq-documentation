**Images** are the static templates containing the software
configuration from which you provision a running **Instance** - a
virtual machine, with which you can interact - on your cloud provider.

The **Instance** and **Images** containers, combined with the ability to
analyze information inside each instance or image, provides in-depth
information across the cloud environment. This rich set of information
enables {product-title} users to improve problem resolution times and
effectively manage instances and images in their cloud environment.

The **Instances** and **Images** pages display all instances and images
the server discovered from your cloud providers. The taskbar on each
page is a menu driven set of buttons that provide access to functions
related to instances and images.

![image features](image_features.png)

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

![3393](3393.png)

1.  Top left quadrant: Operating system of the Instance

2.  Bottom left quadrant: Instance Cloud Provider

3.  Top right quadrant: Power state of Instance or Status icon

4.  Bottom right quadrant: Number of Snapshots for this Instance

| Icon              | Description                                                                              |
| ----------------- | ---------------------------------------------------------------------------------------- |
| ![2138](2138.png) | Template: Cloud Image                                                                    |
| ![2139](2139.png) | Retired: Instance has been retired                                                       |
| ![2140](2140.png) | Archived: Instance has no provider or availability zone associated with it.              |
| ![2141](2141.png) | Orphaned: Instance has no availability zone but does have a provider associated with it. |
| ![2142](2142.png) | Disconnected: Instance is disconnected.                                                  |
| ![2143](2143.png) | On: Instance is powered on.                                                              |
| ![2144](2144.png) | Off: Instance is powered off.                                                            |
| ![2145](2145.png) | Suspended: Instance has been suspended.                                                  |

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

# Filtering Instances and Images

The **Instance Filter** accordion is provided so that you can easily
navigate through groups of instances. You can use the ones provided or
create your own through **Advanced Filtering** capabilities.

Unresolved directive in Instances.adoc -
include::Using\_an\_Instance\_or\_Image\_Filter.adoc\[\]

Unresolved directive in Instances.adoc -
include::Creating\_an\_Instance\_or\_Image\_Filter.adoc\[\]

Unresolved directive in Instances.adoc -
include::Loading\_a\_Report\_Filter\_or\_Search\_Expression.adoc\[\]

Unresolved directive in Instances.adoc -
include::Changing\_Views\_for\_Instances\_and\_Images.adoc\[\]

Unresolved directive in Instances.adoc -
include::Sorting\_Instances\_and\_Images.adoc\[\]

Unresolved directive in Instances.adoc -
include::Creating\_an\_Instance\_or\_Image\_Report.adoc\[\]

Unresolved directive in Instances.adoc -
include::Searching\_for\_Instances\_or\_Images.adoc\[\]

Unresolved directive in Instances.adoc -
include::Analyzing\_Instances\_and\_Images.adoc\[\]

# Comparing Instances and Images

You can compare multiple instances in {product-title} server. This
allows you to see how different instances are from their original image.
This helps detect missing patches, unmanaged user accounts, or
unauthorized services.

Use the comparison feature to:

  - Compare multiple instances from different hosts

  - Compare multiple instances side-by-side

  - Quickly see similarities and differences among multiple instances
    and a base

  - Narrow the comparison display to categories of properties

  - Print or export in the comparison results to a PDF or CSV file

Compare instances and images:

1.  Navigate to menu:Compute\[Clouds \> Instances\].

2.  Click the accordion for the items to analyze.

3.  Click the checkboxes for the items to compare.

4.  Click ![1847](1847.png) (**Configuration**), and then
    ![2148](2148.png) (**Compare Selected items**). The comparison
    displays in a compressed view with a limited set of properties
    listed.

5.  To delete an item from the comparison, click
    ![1861](1861.png)(**Remove this VM from the comparison**) at the
    bottom of the items column.

6.  To view many items on one screen, go to a compressed view by
    clicking ![2024](2024.png) (**Compressed View**). To return to an
    expanded view, click ![2023](2023.png) (**Expanded View**).

7.  To limit the mode of the view, there are two buttons in the task
    bar.
    
      - Click ![2022](2022.png) (**Details Mode**) to see all details
        for an attribute.
    
      - Click ![2025](2025.png) (**Exists Mode**) to limit the view to
        if an attribute exists compared to the base or not. This only
        applies to attributes that can have a boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

8.  To change the base instance that all the others are compared to,
    click its label at the top of its column.

9.  To go to the summary screen for an instance, click its **Virtual
    Thumbnail** or icon.

Unresolved directive in Instances.adoc -
include::Creating\_an\_Instance\_Comparison\_Report.adoc\[\]

Unresolved directive in Instances.adoc -
include::Refreshing\_Instances\_and\_Images.adoc\[\]

Unresolved directive in Instances.adoc -
include::Extracting\_Running\_Processes\_from\_Instances\_and\_Images.adoc\[\]

Unresolved directive in Instances.adoc -
include::Setting\_Ownership\_for\_Instances\_and\_Images.adoc\[\]

Unresolved directive in Instances.adoc -
include::Removing\_Instances\_and\_Images\_from\_the\_VMDB.adoc\[\]

Unresolved directive in Instances.adoc -
include::Tagging\_Instances\_and\_Images.adoc\[\]

Unresolved directive in Instances.adoc -
include::Reviewing\_an\_Instance\_or\_Image.adoc\[\]

Unresolved directive in Instances.adoc -
include::Viewing\_Running\_Processes\_after\_Collection.adoc\[\]

Unresolved directive in Instances.adoc -
include::Managing\_Security\_Groups.adoc\[\]

Unresolved directive in Instances.adoc -
include::Editing\_Instance\_or\_Image\_Properties.adoc\[\]

Unresolved directive in Instances.adoc -
include::Controlling\_the\_Power\_State\_of\_an\_Instance.adoc\[\]

Unresolved directive in Instances.adoc -
include::Right\_Sizing\_an\_Instance.adoc\[\]

# Resizing an Instance

Unresolved directive in Instances.adoc -
include::Resizing\_an\_Instance\_Change\_Flavor.adoc\[\]

# Migrating a Live Instance

Unresolved directive in Instances.adoc -
include::Instance\_Live\_Migration.adoc\[\]

# Evacuating an Instance

Unresolved directive in Instances.adoc -
include::Instance\_Evacuation.adoc\[\]

Unresolved directive in Instances.adoc -
include::Viewing\_Capacity\_and\_Utilization\_Charts\_for\_an\_Instance.adoc\[\]

Unresolved directive in Instances.adoc -
include::Viewing\_the\_Instance\_or\_Image\_Timeline.adoc\[\]

Unresolved directive in Instances.adoc -
include::Instance\_or\_Image\_Summary.adoc\[\]

Unresolved directive in Instances.adoc -
include::Viewing\_a\_User\_Information\_for\_an\_Instance\_or\_Image.adoc\[\]

Unresolved directive in Instances.adoc -
include::Viewing\_a\_Group\_Information\_for\_an\_Instance\_or\_Image.adoc\[\]

Unresolved directive in Instances.adoc -
include::Viewing\_Genealogy\_of\_an\_Instance\_or\_Image.adoc\[\]

Unresolved directive in Instances.adoc -
include::Detecting\_Drift\_on\_Instances\_or\_Images.adoc\[\]

Unresolved directive in Instances.adoc -
include::Creating\_a\_Drift\_Report\_for\_an\_Instance\_or\_Image.adoc\[\]

Unresolved directive in Instances.adoc -
include::Viewing\_Analysis\_History\_for\_an\_Instance\_or\_Image.adoc\[\]

Unresolved directive in Instances.adoc -
include::Viewing\_Event\_Logs\_for\_an\_Instance\_or\_Image.adoc\[\]
