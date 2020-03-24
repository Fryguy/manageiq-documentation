Policies are used to manage your virtual environment. There are two
types of policies available: compliance and control. Compliance policies
are used to harden your virtual infrastructure, making sure that your
security requirements are adhered to. Control policies are used to check
for a specific condition and perform an action based on the outcome. For
example:

  - Prevent virtual machines from running without an administrator
    account.

  - Prevent virtual machines from starting if certain patches are not
    applied.

  - Configure the behavior of a production virtual machine to only start
    if it is running on a production host.

  - Force a SmartState Analysis when a host is added or removed from a
    cluster.

{product-title\_short} policies are associated with cloud instances
using virtual machine analysis profiles. These are the steps required to
create a custom virtual machine analysis profile, and assigning it to a
cloud instance for use with SmartState analysis, via a control policy.

<div class="note">

For more detailed information about {product-title\_short} policies, see
[Assigning a Custom Analysis Profile to a Virtual
Machine](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.7/single/assigning-a-custom-analysis-profile-to-a-virtual-machine/)
and [Policies and Profiles
Guide](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.7/single/policies-and-profiles-guide/).

</div>

The following subsections demonstrate how to create host compliance and
instance control policies.

# Creating a Host Compliance Policy

The following procedure describes how to create a compliance policy that
checks whether firewalls are enabled on infrastructure provider nodes.
Nodes with disabled firewalls are marked *non-compliant*.

1.  Navigate to menu:Control\[Explorer\].

2.  Expand the **Policies** accordion, and click **Compliance
    Policies**.

3.  Select **Host Compliance Policies**.

4.  Click ![image](../images/1847.png) (**Configuration**),
    ![image](../images/1862.png) (**Add a New Host/Node Compliance
    Policy**).

5.  Type in a **Description** for the policy.
    
    ![image](../images/1935.png)

6.  Uncheck **Active** if you do not want this policy processed even
    when assigned to a resource.

7.  Add **Host / Node.Firewall Rules : Active CONTAINS "true"** to the
    *scope* of the policy . To do so:
    
    1.  In drop-down below the **Scope** section, choose **Field**. When
        you do, a new drop-down will appear below it; from there, select
        **Host/Node.Firewall.Rules: Active**.
    
    2.  A new drop-down will appear; from there, select **true**.
    
    3.  Click ![image](../images/1863.png) (**Commit expression element
        changes**) to add the scope.

8.  In the **Notes** area, add a detailed explanation of the policy.

9.  Click **Add**. The policy will be added and listed under **Host
    Compliance Policies** in the **Policies** accordion.

Next, create a *policy profile* and assign this new compliance policy to
it:

1.  Navigate to menu:Control\[Explorer\].

2.  Click on the **Policy Profiles** accordion, then click
    ![image](../images/1847.png) (**Configuration**), then
    ![image](../images/1862.png) (**Add a New Policy Profile**).

3.  In the **Basic Information** area, type in a unique description for
    the policy profile.
    
    ![image](../images/1931.png)

4.  From **Available Policies** in the **Policy Selection** area select
    all the policies you need to apply to this policy profile. Use the
    `Ctrl` key to select multiple policies.
    
    ![image](../images/1930.png)

5.  Click ![image](../images/1876.png) to add the **Policies**.
    
    ![image](../images/1929.png)

6.  Add to the **Notes** area if required.

7.  Click **Add**.

At this point, you can now add the new policy profile to the
infrastructure provider hosts:

1.  Navigate to menu:Compute\[Infrastructure \> Providers\], verify the
    provider you need to assign the policy profiles to.

2.  Click ![image](../images/1941.png) (**Policy**), and then click
    ![image](../images/1851.png)(**Manage Policies**).

3.  From the **Select Policy Profiles** area, you can click on the
    triangle next to a desired policy profile to expand it and see its
    member policies.

4.  Check the policy profiles you require to apply to the provider. It
    turns blue to show its assignment state has changed.

5.  Click **Save**.

# Creating a Virtual Machine Control Policy

The process of creating a *control policy* is similar to that of a
compliance policy. A control policy is driven by events after certain
conditions are met. The following control policy will start a SmartState
analysis on an instance every 24 hours:

1.  Navigate to menu:Control\[Explorer\].

2.  Expand the **Policies** accordion, and click **Control Policies**.

3.  Select **Vm Control Policies**.

4.  Click ![image](../images/1847.png) (**Configuration**), then
    ![image](../images/1862.png) (**Add a New VM and Instance Control
    Policy**).

5.  Enter a **Description**. This will be the name given to your VM
    control policy.

6.  Uncheck **Active** if you do not want this policy processed even
    when assigned to a resource.

7.  Add **VM and Instance : Last Analysis Time IS "Yesterday"** to the
    scope of the policy. To do so:
    
    1.  In drop-down below the **Scope** section, choose **Field**. When
        you do, a new drop-down will appear below it; from there, select
        **VM and Instance : Last Analysis Time**.
    
    2.  A new drop-down will appear; from there, select **true**.
    
    3.  Click ![image](../images/1863.png) (**Commit expression element
        changes**) to add the scope.

8.  Click **Add**. The policy is added and listed under **Vm Control
    Policies** in the **Policies** accordion.

You can now associate events, conditions, and actions to this control
policy. To do so:

1.  Navigate to menu:Control\[Explorer\].

2.  Click the **Policies** accordion, and select the control policy you
    just created.

3.  Click ![image](../images/1847.png) (**Configuration**),
    ![image](../images/1851.png) (**Edit this Policy’s Condition
    assignments**).

4.  In the **VM Operation** section, select **VM Power On**.

5.  Click **Save**. The **VM Power On** event should appear under your
    policy.

You can now associate an action to the **VM Power On** event. To do so:

1.  Select the **VM Power On** event.

2.  Click ![image](../images/1847.png) (**Configuration**), then
    ![image](../images/1851.png) (**Edit Actions for this Policy
    Event**).

3.  In the **Order of Actions if ALL Conditions are True** section,
    select **Generate Log Message** and **Initiate SmartState Analysis
    for VM**.

4.  Click **Save**.

Next, create a policy profile and assign this new control policy to it:

1.  Navigate to menu:Control\[Explorer\].

2.  Click on the **Policy Profiles** accordion, then click
    ![image](../images/1847.png) (**Configuration**), then
    ![image](../images/1862.png) (**Add a New Policy Profile**).

3.  Enter `Most Recent SmartState` in the **Description** field.

4.  In the **Policy Selection** area, choose the control policy you
    created earlier. This should have **VM and Instance Control** in its
    name. Add this policy to the **Profile Policies** box.

5.  Click **Add**.

At this point, you should now be able to add the policy profile to the
cloud providers.

1.  Navigate to menu:Compute\[Cloud \> Providers\].

2.  Select the overcloud you added in [???](#add-openstack-oc).

3.  Click ![image](../images/1941.png) (**Policy**), then
    ![image](../images/1851.png) (**Manage Policies**).

4.  Under **Select Policy Profiles**, select **Most Recent SmartState**.

5.  Click **Save**.
