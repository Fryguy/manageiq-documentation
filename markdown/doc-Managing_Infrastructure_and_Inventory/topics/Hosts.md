The **Hosts** page under menu:Compute\[Infrastructure\] displays the
hosts discovered in your enterprise environment.

<div class="note">

Any applied filters will be in effect here.

</div>

![2212](2212.png)

After adding or sorting your hosts, click on one to examine it more
closely and see its virtual machines, SmartProxy settings, and
properties.

![2222](2222.png)

1.  Top left quadrant: Number of virtual machines on this host

2.  Bottom left quadrant: Virtual machine software

3.  Top right quadrant: Power state of host

4.  Bottom right quadrant: Authentication status

| Icon              | Description                                                                    |
| ----------------- | ------------------------------------------------------------------------------ |
| ![2190](2190.png) | Validated: Valid authentication credentials have been added.                   |
| ![2191](2191.png) | Invalid: Authentication credentials are invalid                                |
| ![2192](2192.png) | Unknown: Authentication status is unknown or no credentials have been entered. |

# Filtering Hosts

The Host Filter accordion is provided to easily navigate through the
hosts. Use the ones provided or create your own. In addition, you can
set a default filter.

Unresolved directive in Hosts.adoc -
include::To\_set\_a\_default\_Host\_Filter.adoc\[\]

Unresolved directive in Hosts.adoc -
include::To\_create\_a\_Host\_Filter.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Performing\_SmartState\_Analysis\_on\_Hosts.adoc\[\]

# Comparing Hosts

{product-title} allows you to compare hosts and check operating systems,
host software and version information, and hardware.

1.  Navigate to menu:Compute\[Infrastructure \> Hosts\].

2.  Check the hosts to compare.

3.  Click ![1847](1847.png) (**Configuration**), and then
    ![2148](2148.png) (**Compare selected Hosts**). The comparison
    displays in a default expanded view, which lists a limited set of
    properties.

4.  To remove a host from the comparison, click ![1861](1861.png)
    (**Remove this Host from the comparison**) at the bottom of the
    column.

5.  To go to a compressed view, click ![2024](2024.png) (**Compressed
    View**). To return to an expanded view, click ![2023](2023.png)
    (**Expanded View**).

6.  To limit the mode of the view, there are two buttons in the taskbar.
    
      - Click ![2022](2022.png) (**Details Mode**) to see all details
        for an attribute.
    
      - Click ![2025](2025.png) (**Exists Mode**) to limit the view to
        if an attribute exists compared to the base or not. This only
        applies to attributes that can have a Boolean property. For
        example, a user account exists or does not exist, or a piece of
        hardware that does or does not exist.

7.  To change the base host that compare to the other hosts, click its
    label at the top of its column.

8.  To go to the summary screen for a host, click its virtual thumbnail
    or icon.

Unresolved directive in Hosts.adoc -
include::Host\_Comparison\_Sections.adoc\[\]

Unresolved directive in Hosts.adoc -
include::To\_use\_Host\_Comparison\_Sections.adoc\[\]

Unresolved directive in Hosts.adoc -
include::To\_create\_a\_comparison\_report2.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Refreshing\_Multiple\_Hosts.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Discovering\_Multiple\_Hosts.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Adding\_a\_single\_Host.adoc\[\]

Unresolved directive in Hosts.adoc - include::Editing\_Hosts.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Reviewing\_a\_Host.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Tagging\_Multiple\_Hosts.adoc\[\]

Unresolved directive in Hosts.adoc - include::Removing\_Hosts.adoc\[\]

# Scaling Down Compute Hosts

Unresolved directive in Hosts.adoc -
include::Scaling\_Down\_Compute.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Refreshing\_Relationships\_and\_Power\_States\_for\_a\_Host.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Viewing\_Capacity\_and\_Utilization\_Charts\_for\_a\_Host.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Viewing\_the\_Host\_Timeline.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Host\_Virtual\_Summary.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Viewing\_Host\_Device\_Information.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Viewing\_Host\_Network\_Information.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Viewing\_Storage\_Adapters.adoc\[\]

Unresolved directive in Hosts.adoc -
include::Detecting\_Drift\_on\_Hosts.adoc\[\]

Unresolved directive in Hosts.adoc -
include::To\_create\_a\_drift\_report2.adoc\[\]
