You can create and assign different analysis profiles for specific
virtual machine configurations using the ManageIQ user interface. This
document describes the steps required to create a custom virtual machine
analysis profile, and assigning it to a virtual machine for use with
SmartState analysis, via a control policy.

1.  Creating a Virtual Machine Analysis Profile

2.  Creating an Action to Assign the Virtual Machine Analysis Profile to
    Analysis Task

3.  Creating a Virtual Machine Control Policy

4.  Creating a Policy Profile and Assigning the Virtual Machine Control
    Policy

5.  Assigning the Policy Profile to a Virtual Machine

# Creating a Virtual Machine Analysis Profile

1.  Log into the appliance as the **admin** user.

2.  Click **Configuration**.

3.  Expand the **Settings** accordion, then click **Analysis Profiles**.

4.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1862.png) (**Add VM Analysis Profile**).

5.  In **Basic Information**, enter **Name** and **Description** for the
    analysis profile.

6.  In the **Category** tab, select the categories you want to collect
    information for under **Category Selection**. The **Category** tab
    is available for virtual machine profiles only.

7.  In the **File** tab, click **\<New Entry\>** and specify the file to
    be scanned and if you want to collect contents for, then click
    **Save**. Repeat the step for adding multiple file name entries.

8.  In the **Registry** tab, enter the **Registry Key** and **Registry
    Value**, then click **Save**. To determine whether a registry key
    exists without providing a value, enter `*` in **Registry Value**.
    The **Registry** tab is available for virtual machine profiles only.

9.  In the **Event Log** tab, specify the event log entries to collect.
    Enter a **Filter Message** to look for specific text in a message.
    Enter a **Level** (*info*, *warn* or *error*, for example) to
    specify the event level. Enter the **Source** for the event log
    entry and **\# (Number) of Days** to specify how far back to check.

10. Click **Add**.

# Creating an Action to Assign the Virtual Machine Analysis Profile to the Analysis Task

Actions are performed after the condition is evaluated. You can
associate actions with specific events when you create a policy.
ManageIQ provides a set of default actions, but you can also create
custom actions using the ManageIQ user interface.

Use this procedure to create a custom action by adding the **Assign
Profile to Analysis Task** action type to the virtual machine analysis
profile (created in [Creating a Virtual Machine Analysis
Profile](#vm-analysis-profile)).

![image](images/create-custom-action.png)

1.  Navigate to <span class="menuchoice">Control \> Explorer</span>.

2.  Expand the **Actions** accordion and click ![image](images/1847.png)
    (**Configuration**), then ![image](images/1862.png) (**Add a new
    Action**).

3.  Enter a **Description** for the new action. This will be the name
    given to your new action.

4.  Select **Assign Profile to Analysis Task** from the **Action Type**
    list.

5.  Select the newly-created virtual machine analysis profile from the
    **Analysis Profiles** list.

6.  Click **Add**.

<div class="note">

You can only associate this action with an analysis start event.

</div>

The action is created and added to the **Available Actions** list.
Associate this action with the **VM Analysis Start** event when you
create a virtual machine control policy in the next procedure.

# Creating a Virtual Machine Control Policy

You can create a control policy by combining an event, a condition, and
an action. The procedure below describes how to create a virtual machine
control policy to assign the newly-created action to the **VM Analysis
Start** event. Optionally, you can use a scope expression that is tested
immediately when the policy is triggered by an event. If the item is out
of scope, then the policy will not continue on to the conditions, and
the assigned action will not run.

1.  Navigate to <span class="menuchoice">Control \> Explorer</span>.

2.  Expand the **Policies** accordion, and click **Control Policies**.

3.  Select **Vm Control Policies**.

4.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1862.png) (**Add a New VM and Instance Control
    Policy**).

5.  Enter a **Description**. This will be the name given to your VM
    control policy.

6.  Clear the **Active** box if you do not want this policy processed
    even when assigned to a resource.

7.  Optional: Enter a **Scope** (you can also create a scope as part of
    a condition, or not use one at all). If the virtual machine is not
    included in the scope, the assigned action will not run.
    
    You can use the drop-down list to create an expression for the
    **Scope**. Based on what you choose, different options appear. Click
    ![image](images/1863.png) (**Commit expression element changes**) to
    add the scope.

8.  Enter **Notes** if required.

9.  Click **Add**. The policy is added and listed under **Vm Control
    Policies** in the **Policies** accordion.

10. Select the newly-added VM control policy. You can now associate
    events, conditions, and actions with the policy.

11. Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1851.png) (**Edit this Policy’s Event
    assignments**).

12. Under **VM Operation**, set **VM Analysis Start** to **Yes**.

13. Click **Save**.

14. Click the **VM Analysis Start** event to configure actions.

15. Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1851.png) (**Edit Actions for this Policy Event**).

16. In **Order of Actions if ALL Conditions are True**, select the
    action created in [Creating an Action to Assign the Virtual Machine
    Analysis Profile to the Analysis
    Task](#assign-profile-analysis-task-action) from the **Available
    Actions** list. This action will take place if the resources meet
    the conditions of the policy.
    
    ![image](images/edit-event.png)
    
    <div class="note">
    
    Each selected action can be executed synchronously or
    asynchronously; a synchronous action will not start until the
    previous synchronous action is completed, while an asynchronous
    action allows the next action to start whether or not the first
    action has completed. Also, at least one ManageIQ server in the
    ManageIQ zone must have the notifier server role enabled for the
    trap to be sent.
    
    </div>

17. Click (![image](images/1876.png)) which will move the action to
    **Selected Actions**. The selected action is set to (S) Synchronous
    by default. From **Selected Actions**, select the action, then:
    
      - Click **A** (Set selected Actions to Asynchronous) to make it
        asynchronous.
    
      - Click **S** (Set selected Actions to Synchronous) to make it
        synchronous. If creating a synchronous action, use the up and
        down arrows to identify in what order you want the actions to
        run.

18. Click **Save**.

# Creating a Policy Profile and Assigning the Virtual Machine Control Policy

Add a new policy profile and assign the virtual machine control policy
(created in [Creating a Virtual Machine Control
Policy](#create-vm-control-policy)) to it.

1.  Navigate to <span class="menuchoice">Control \> Explorer</span>.

2.  Expand the **Policy Profiles** accordion, click
    ![image](images/1847.png) (**Configuration**), then
    ![image](images/1862.png) (**Add a New Policy Profile**).

3.  In the **Basic Information** area, enter a **Description** for the
    policy profile.

4.  Under **Policy Selection**, select the virtual machine control
    policy created in [Creating a Virtual Machine Control
    Policy](#create-vm-control-policy) from the **Available Policies**
    list.

5.  Click (![image](images/1876.png)) to move the selected virtual
    machine control policy into this profile.

6.  Click **Add**.

# Assigning the Policy Profile to a Virtual Machine

Assign the policy profile you created in [Creating a Policy Profile and
Assigning the Virtual Machine Control
Policy](#create-policy-profile-assign-vm-control-policy) to a virtual
machine, and initiate SmartState analysis.

<div class="note">

Policy profiles can be specified at multiple levels. If you assign a
policy profile to a provider (Amazon EC2 or OpenStack for example), the
profile will apply to all hosts or virtual machines for that provider.

</div>

1.  Navigate to <span class="menuchoice">Compute \> Clouds \>
    Instances</span> or <span class="menuchoice">Compute \>
    Infrastructure \> Virtual Machines</span>. Select the virtual
    machine or instance.

2.  Click ![image](images/1941.png) (**Policy**), then
    ![image](images/1851.png) (**Manage Policies**).

3.  Under **Select Policy Profiles**, select the policy profile created
    in [Creating a Policy Profile and Assigning the Virtual Machine
    Control Policy](#create-policy-profile-assign-vm-control-policy). It
    will turn blue to show the selection. Click the triangle next to the
    policy profile to see its member policies.

4.  Click **Save**.

5.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/smartstate-icon.png) (**Perform SmartState
    Analysis**). A pop-up window appears to confirm the action.

6.  Click **OK**. SmartState analysis is initiated for the selected
    virtual machine or instance from the ManageIQ database.

SmartState analysis will now report back findings specified by the
custom virtual machine analysis profile.
