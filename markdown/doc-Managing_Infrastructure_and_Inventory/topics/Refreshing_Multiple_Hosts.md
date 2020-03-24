Manually refresh a host for its properties and related infrastructure
components.

1.  Navigate to menu:Compute\[Infrastructure \> Hosts\].

2.  Check the hosts to refresh.

3.  Click ![1847](1847.png) (**Configuration**), and then
    ![2003](2003.png) (**Refresh Relationships and Power States**).

4.  Click **OK**.

When a host is refreshed and a new virtual machine is discovered on that
host, {product-title} checks to see if the virtual machine is already
registered with another host. If this is the case, the host that the
virtual machine is associated with switches to the new host. If the
SmartProxy is monitoring a provider, this happens automatically. If not,
the next refresh of the host addresses this.
