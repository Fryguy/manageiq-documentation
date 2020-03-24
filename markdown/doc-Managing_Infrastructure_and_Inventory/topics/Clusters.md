Clusters provide high availability and load balancing for a group of
hosts. The **Clusters** page under menu:Compute\[Infrastructure\]
displays the clusters discovered in your enterprise environment.

<div class="note">

Any filter applied will be in effect here.

</div>

![2202](2202.png)

Use the **Clusters Taskbar** to manage the analysis and tagging of your
clusters. These buttons manage multiple clusters at one time. To manage
one cluster, click on that cluster in the main area of the screen.

Unresolved directive in Clusters.adoc -
include::Performing\_SmartState\_Analysis\_on\_Clusters.adoc\[\]

# Comparing Clusters

{product-title} provides features to compare properties of clusters.

1.  Navigate to menu:Compute\[Infrastructure \> Clusters\].

2.  Check the clusters to compare.

3.  Click ![1847](1847.png) (**Configuration**), and then
    ![2148](2148.png) (**Compare Selected items**). The comparison
    displays in a default expanded view and lists a limited set of
    properties.
    
    ![2203](2203.png)

4.  To delete a cluster from the comparison, click
    ![1861](1861.png)(**Remove this Cluster from the Comparison**).

5.  To go to a compressed view, click ![2024](2024.png) (**Compressed
    View**). To return to an expanded view, click ![2023](2023.png)
    (**Expanded View**).

6.  To change the base cluster that all other clusters compare to, click
    its label at the top of its column.

7.  To go to the cluster summary screen, click its virtual thumbnail or
    icon.

8.  There are three buttons in the taskbar to limit the type of views:
    
      - Click ![2178](2178.png) (**All attributes**) to see all
        attributes.
    
      - Click ![2204](2204.png) (**Attributes with different values**)
        to see only the attributes that are different across clusters.
    
      - Click ![2148](2148.png) (**Attributes with the same values**) to
        see only the attributes that are the same across clusters.

9.  To limit the mode of the view, there are two taskbar buttons.
    
      - Click ![2022](2022.png) (**Details Mode**) to see all details
        for an attribute.
    
      - Click ![2025](2025.png) (**Exists Mode**) to only see if an
        attribute exists compared to the base or not. This only applies
        to attributes that can have a Boolean property. For example, a
        user account exists or does not exist, or a piece of hardware
        that does or does not exist.

This creates a comparison between clusters. Export this data or create a
report from your comparison for analysis using external tools.

Unresolved directive in Clusters.adoc -
include::To\_create\_a\_comparison\_report1.adoc\[\]

Unresolved directive in Clusters.adoc -
include::Reviewing\_a\_Cluster.adoc\[\]

Unresolved directive in Clusters.adoc -
include::Tagging\_Clusters.adoc\[\]

Unresolved directive in Clusters.adoc -
include::Viewing\_Capacity\_and\_Utilization\_Charts\_for\_a\_Cluster.adoc\[\]

Unresolved directive in Clusters.adoc -
include::Viewing\_Cluster\_Timeline.adoc\[\]

Unresolved directive in Clusters.adoc -
include::Detecting\_Drift\_on\_Clusters.adoc\[\]

Unresolved directive in Clusters.adoc -
include::To\_create\_a\_drift\_report1.adoc\[\]

Unresolved directive in Clusters.adoc -
include::Removing\_Clusters.adoc\[\]
