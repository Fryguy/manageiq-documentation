The Automate model provides flexibility to not only change parts of the
provisioning process, but also to allow you to automate other
operational tasks. Below are some scenarios where the Automate model can
help accomplish these tasks.

  - Intelligent Workload Management - An enterprise had a requirement
    that when a virtual machine has reached a High CPU Percent Ready for
    a specified period of time, a vMotion should occur to a more
    suitable host. For this reason, VMware’s Distributed Resource
    Scheduler (DRS) was not practical, as the CPU Ready metric could not
    trigger DRS. The solution was to leverage ManageIQ Control and
    ManageIQ Automate to drive the management of this workflow.

  - Power on only during business hours - An organization which gave a
    group of self-service users ManageIQ access had a requirement to
    only allow certain virtual machines to be powered during business
    hours. This was solved with ManageIQ Automate.

  - Auto-Tagging virtual machines based on file contents - An IT
    organization needed a way to consume information from a text file on
    a virtual machine and dynamically populate vCenter. The data used to
    auto-tag virtual machines is also used to align unmanaged virtual
    machines to the business.

# Updates to Rails and Ruby

Changes within Ruby and Rails versions can create issues for custom code
and automation in ManageIQ environments.

Before proceeding with major upgrades that include changes to versions
of Ruby and Rails, review the below resources.

## Updates and Changes in Rails

See [Rails Releases](https://weblog.rubyonrails.org/releases/) for
information on each release of Rails. To compare versions of Rails, see
[Comparing changes in Rails](https://github.com/rails/rails/compare).

## Updates and Changes in Ruby

See [Ruby Releases](https://www.ruby-lang.org/en/downloads/releases/)
for information on each release of Ruby by version number. To compare
versions of Ruby, see [Comparing changes in
Ruby](https://github.com/ruby/ruby/compare).

# Understanding the Automate Model

Automate enables real-time, bi-directional process integration. This
provides users with a method to implement adaptive automation for
management events and administrative or operational activities.

## Automate Model

The Automate model is arranged to provide an object oriented hierarchy
to control automation functions. The model uses the following
organizational units arranged in a hierarchy:

  - **Datastore** - The main organization unit that stores the entire
    model.

  - **Domains** - Domains act as collection of automation functions.
    Functions are executed depending on the order of Domain priority,
    which means a function in a Domain with a higher priority overrides
    the same functions specified in a lower-priority Domain. This allows
    ManageIQ to specify a core Domain (ManageIQ) but allow users to
    override automate functions with custom Domains. Each Domain
    contains a set of Namespaces.

  - **Namespaces** - Containers that organize and categorize functions
    of the model. Namespaces can contain child Namespaces as well as
    Classes.

  - **Classes** - Templates for a specific function of the model. Each
    Class uses a Schema to apply to Instances to populate with default
    values. Each class also can contain a set of methods.

  - **Instances** - An instance is a version of a class populated with
    initial configuration data. An instance can include a collection of
    any number of attributes, calls to methods, and relationships.

  - **Methods** - Methods are functions within the model. Methods use
    Ruby code to execute various operations needed for a Class.

ManageIQ contains a set of preconfigured Domains for users:

  - **ManageIQ** - The core domain for ManageIQ Automate operations.
    This domain is locked with the following Namespaces:
    
      - **Cloud** - General cloud instance lifecycle from provisioning,
        retirement, methods, email.
    
      - **Control** - Control contains email alerts for policy controls.
    
      - **Infrastructure** - General infrastructure VM lifecycle from
        provisioning, retirement, methods, email.
    
      - **Service** - Service lifecycle from provisioning, retirement,
        methods, email.
    
      - **System** - System contains classes that can provide the start
        points for all ManageIQ Automate activities.

  - **RedHat** - Domain containing advanced operations, specifically
    interactions with supported cloud and infrastructure providers. This
    domain is locked with the following Namespaces:
    
      - **Cloud** - Red Hat-supported cloud instance lifecycle from
        provisioning, retirement, methods, email.
    
      - **Infrastructure** - Red Hat-supported cloud instance lifecycle
        from provisioning, retirement, methods, email.
    
      - **Integration** - Used to interface with systems outside of
        ManageIQ. Use this namespace to integrate with additional
        systems.

You can copy classes and instances from locked Domains into your own
custom domains.

<div class="note">

Changing the existing classes or instances shipped with the product is
not recommended because this may hinder the operation of ManageIQ. You
can link to these methods using relationships.

</div>

To reset the Automate model to default settings, navigate to
<span class="menuchoice">Automate \> Import/Export</span> and click the
**Reset** option.

## Creating a Domain

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>. The default view is the Datastore.

2.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1862.png) (**Add a New Domain**).

3.  Type in a unique **Name** and **Description**. Choose if the Domain
    is **Enabled**.

4.  Click **Add**.

The new domain is created.

## Editing a Domain

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>. The default view is the Datastore.

2.  Select the Domain you want to edit.

3.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1851.png) (**Edit Selected Domain**).

4.  Make the required edits.

5.  Click **Save**.

You have edited the selected domain.

## Deleting a Domain

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>. The default view is the Datastore.

2.  Select the **Domain** that you want to delete.

3.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1861.png) (**Remove This Domain**).

4.  A window to confirm the removal of Domain appears.

5.  Click **OK**.

The selected Domain is deleted.

## Importing a Domain from a Git Repository

ManageIQ can import an Automate domain from a Git repository by
specifying a repository and branch, along with user details. Currently,
you can only add git domains via the **Import/Export** area of the user
interface.

![Import Datastore](images/import-datastore.png)

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Import/Export</span>.

2.  In **Import Datastore via git**, enter the **Git URL**. Select the
    branch or tag to use.

3.  Optionally, enter a **Username** and **Password**.

4.  Select **Verify Peer Certificate** if desired.

5.  Click **Submit**.

The new domain is imported via Git repository. Note that the domain is
validated on import.

## Changing Priority Order of Domains

Functions are executed depending on the order of Domain priority. Use
this procedure to change the priority order of domains.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>. The default view is the Datastore.

2.  Select the Domains you want to change the priority order for.

3.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1851.png) (**Edit Priority Order of Domains**).

4.  The list of Domains selected shows up. Note that you cannot change
    the priority of locked Domains and therefore locked Domains do not
    show up on the list.

5.  Select one or more consecutive groups to move up or down to change
    their priority as required.

6.  Click **Save**.

## Creating a Namespace

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>. The default view is the Datastore.

2.  Navigate through the various Domains and Namespaces until you reach
    the desired location for your new Namespace.

3.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1862.png) (**Add a New Namespace**).

4.  Type in a unique **Name** and **Description**.

5.  Click **Add**.

The new Namespace is created.

## Creating a Class

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>, navigate to the namespace you want to add a class
    to.

2.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1862.png) (**Add a new Class**).

3.  Type in a unique **Name** and **Description**.

4.  If you want to use the schema from a class that has already been
    created, select it from the **Inherits From** dropdown. If the class
    that the new class inherits from changes, the new class will also
    change.

5.  Click **Add**.

The new class is created and you can create a schema, add instances and
methods.

<div class="note">

For each class, create a schema if you did not choose to inherit from an
existing class. The schema can include attributes, methods, assertions,
and relationships.

</div>

## Creating a Schema for a Class

This procedure shows you how to create a schema.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>, and click the class you want to define a schema
    for.

2.  Click on the **Schema** tab.

3.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1851.png) (**Edit selected Schema**).

4.  Click ![image](images/2366.png) (**Click to add a new field**) to
    create a new field.

5.  Type in a **Name** for the new field.

6.  From **Type**, select **Assertion**, **Attribute**, **Method**,
    **Relationship**, or **State**.

7.  If applicable, select a **Data Type** and set a **Default Value**.

8.  Type in a user friendly **Display Name** and **Description**.

9.  Check **Sub** to enable the substitution syntax of `${}`. Uncheck it
    if you want to use that syntax as a regular string.

10. Fill in **Collect** and **Message** as required. **Collect** is used
    to roll up values from resolved relationships. For example, a
    relationship can resolve to a large object tree. Use **collect** to
    specify how to pull out data from those child objects into the
    current object. If you give **collect** a name value, it will store
    the method result in an attribute of the current object with that
    name.

11. **On Entry**, **On Exit**, **On Error**, **Max Retries**, and **Max
    Time** are fields used mostly for state machines. Leave blank if not
    applicable.

12. Click ![image](images/1863.png) (**Add this entry**) to confirm the
    fields values.

13. For each new field, repeat steps 4 through 10.

14. When you have created all of the fields, click **Save**.

The class schema is created, and you can now add instances to it.

<div class="note">

You may need to edit a class schema to reorder, add, edit, or remove a
field. Classes define the order in which fields are processed and you
may need to process some items before others.

</div>

## Editing a Field in a Schema

This procedure describes how to edit schema fields.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>.

2.  Click the class you want to define a schema for.

3.  Click the **Schema** tab.

4.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1851.png) (**Edit selected Schema**).

5.  Make required changes to any of the definitions for the field.

6.  To remove a field, click ![image](images/2367.png) (**Click to
    delete this field from the schema**).

7.  Click **Save** when you are finished editing the schema.

Once the schema is created, you can add instances and methods to the
class.

## Editing Schema Sequence

This procedure shows you how to change schema sequence.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>.

2.  Click the class you want to change the schema sequence for.

3.  Click the **Schema** tab.

4.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1851.png) (**Edit Sequence**).

5.  In the **Class Schema Sequencing** area, click the field you want to
    change the sequence for.
    
      - To move a field up in the order of resolving an instance, click
        ![image](images/2290.png) (**Move selected field up**).
    
      - To move a field down in the order of resolving an instance,
        click ![image](images/2289.png) (**Move selected field down**).

6.  Click **Save** when you are finished editing the sequence.

## Adding an Instance to a Class

This procedure shows you how to create an instance.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>.

2.  Click the class you want to define a schema for.

3.  Click the **Instances** tab.

4.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1862.png) (**Add a new Instance**).

5.  In the **Main Info** area, type in a **Name**, **Display Name** and
    **Description**.

6.  In the **Fields** area, type in an appropriate value for each field,
    leave the field blank if no value is required, or use the default
    value.

7.  Click **Add**.

## Copying a Class or Instance

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>. The default view is the Datastore.

2.  Navigate through the various Domains and Namespaces until you reach
    the desired class or instance to copy.

3.  Click ![image](images/1847.png) (**Configuration**), then either
    (**Copy this Class**) or (**Copy this Instance**) depending on the
    object chosen.

4.  Choose the target Domain in the **To Domain** drop-down menu.

5.  The object retains the same path as the **From Domain** and
    overrides the class in **From Domain** if the **To Domain** has a
    high priority. You can also untick the **Copy to same path** option
    to specify a new Namespace.

6.  Click **Add**.

## Relationships

Relationships are used to connect to other instances in the **Automation
Datastore**. Relationships are formed using URI syntax. The following
can also be passed through a relationship:

  - Use `#` to set the message to send to the item in the relationship.

  - To pass an input to the method use `?` followed by the item to pass.

  - If you want to use a substitution, the syntax is `$\{}` with the
    substitution located between the brackets.

| Example                                                                                 | Explanation                                                                                                                                                                                    |
| --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/Cloud/VM/Provisioning/Naming/Default#create`                                          | This relationships uses the Default instance of the Naming class, which provides a means for other classes to name virtual machines. The relationship sends the `create` message to the class. |
| `/Cloud/VM/Provisioning/StateMachines/VMProvision_VM/AcquireMACAddress#$\{#ae_message}` | This relationships substitutes the message to send to the AcquireMACAddress instance of the VMProvision\_VM class with the value in `ae_message`.                                              |
| `/Cloud/VM/Retirement/Email/vm_retirement_emails?event=vm_retired`                      | Invokes the vm\_retirement\_emails instance of the Email class. Also sends the value `vm_retired` in the `event` attribute, which is used in the vm\_retirement\_emails method.                |
| `/Service/Lifecycle/Retirement?service_id=$\{process#service_id}`                       | Invokes the Retirement instance of the Lifecycle class and send a replacement value in `process#service_id` to the `service_id` attribute.                                                     |

## Methods

Methods are pieces of code associated with a class or object to perform
a task. ManageIQ allows for Ruby methods or backing a method using an
Ansible playbook. You can create your own methods or use relationships
to link to pre-existing ones.

ManageIQ ships with a core set of Ruby gems used by the ManageIQ Rails
Application. The Ruby gems in this set are subject to change. If you are
calling gems using Automate that are no longer in this release, you can
install them by using the `gem install` command.

While gems can be imported into automation methods using `require`, it
is recommended that the authors of the automation methods clearly
document the use of gems either in the core set or a custom set. It is
the responsibility of the author of such custom automation to own the
life cycle of any gem being referenced in those methods.

The Release Notes list Ruby gems that have been added, updated, or
removed in the latest version of ManageIQ.

### Creating a Method

This procedure shows you how to create a method.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>, navigate to the class where you want to create a
    method.

2.  Click the **Methods** tab.

3.  Click ![image](images/1847.png) (**Configuration**),
    ![image](images/1862.png) (**Add a New Method**).

4.  In the **Main Info** area, type in a **Name** and **Display Name**.

5.  For **Location**, select **inline**. Once selected, you will be
    presented with a **Data** area in which to write or copy the script.

6.  Click **Validate** to check the syntax.

7.  Click **Add**.

### Creating a Dynamic Content Dialog

The procedure describes the steps to create a dynamic content dialog.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>.

2.  From the accordion menu, click <span class="menuchoice">DOMAIN \>
    Cloud \> VM \> Operations \> Methods</span>.
    
    <div class="note">
    
    DOMAIN must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>
    
    This example uses the **Cloud** Namespace but can also use the
    **Infrastructure** namespace.

3.  Click ![image](images/1847.png) (**Configuration**), then
    ![image](images/1862.png) (**Add a new Instance**).

4.  In the **Main Info** area, enter **Name** = *`dynamic_list`*,
    replacing *`dynamic_list`* with an appropriate name for the method.

5.  Enter a **Display Name** and **Description**.

6.  In the **Fields** area, enter **Value** = *`dynamic_list`*. Leave
    the other fields blank or use the default values.

7.  Click **Add**.

8.  Navigate to **Methods** tab.

9.  In the **Main Info** area, enter **Name** = *`dynamic_list`* and
    populate the **Data** section with the example automate method
    below.

10. Click **Add**.

11. Set the automate entry point for the dialog control; use the new
    instance created in step four. You can create a new domain and copy
    the method to that domain.
    
        #  Automate Method
        
        dialog_field = $evm.object
        
        # sort_by: value / description / none
        dialog_field["sort_by"] = "value"
        
        # sort_order: ascending / descending
        #dialog_field["sort_order"] = "ascending"
        
        # data_type: string / integer
        dialog_field["data_type"] = "integer"
        
        # required: true / false
        # dialog_field["required"] = "true"
        
        dialog_field["values"] = {1 => "one", 2 => "two", 10 => "ten", 50 => "fifty"}
        dialog_field["default_value"] = 2

### Creating a Playbook Automate Method

ManageIQ can choose an Ansible playbook from a repository and execute it
as a method. Each playbook method can take additional input parameters
specified by the user.

<div class="important">

  - You must first sync your playbook repositories before using them to
    create a method. See [Adding a Playbook
    Repository](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html/managing_providers/automation_management_providers#adding-a-playbook-repository)
    in *Managing Providers* for information on initial playbook
    repository set-up.

  - Using Ansible playbooks to populate dynamic dialog fields is not
    recommended due to delay times caused by the overhead of interaction
    between systems.

  - Only users with administrator privileges can run a service dialog
    based on a playbook automate method.

</div>

To create a playbook automate method:

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>, then click on a domain under **Datastore**.

2.  Under a namespace, select the class for which you want to create a
    new method.

3.  Click the **Methods** tab.

4.  Click ![image](images/1847.png) (**Configuration**) then,
    ![image](images/1862.png) (**Add a New Method**).

5.  In the **Main Info** area, select **Playbook** from the **Type**
    dropdown menu.

6.  Provide a **Name** and **Display Name**.

7.  Select a playbook **Repository** from the list.
    
    1.  Choose a **Playbook** to use.
    
    2.  Select the **Machine Credential** the playbook will use when it
        runs.
    
    3.  Select the **Vault Credential** to use.
    
    4.  From the **Cloud Type** list, select a cloud provider.
    
    5.  Choose the **Cloud Credential** that corresponds to the selected
        cloud type.

8.  Specify the **Hosts** on which the playbook will run. Choose
    **Localhost** or provide unique values in the **Specify host
    values** field.

9.  Set the **Max TTL** in minutes. The Time To Live (TTL) field allows
    you to set the maximum execution time for the playbook to run.

10. Select when to receive **Logging Output** from the options in the
    drop-down menu.

11. Use the **Escalate Privilege** toggle switch to enable user
    privilege escalation if credentials are called for during the
    playbook run.

12. Choose a **Verbosity** value to set the debug level for playbook
    execution.

13. Add required **Input Parameters** using the fields and values
    available. Click the ![add parameter](images/add_parameter.png) to
    add additional input parameters.
    
    <div class="note">
    
    Input parameters become extra vars, with substitution enabled. This
    overcomes the lack of a dialog which would normally allow for the
    input of additional information. For more information on extra vars,
    see the Ansible documentation.
    
    </div>

14. Click **Add** when finished.

Once created, the domain including your playbook method can be exported
to appliances in your testing or production environments or imported in
appliances in multiple regions.

<div class="important">

To import a domain with a playbook method, you must have an existing
Ansible playbook on the destination environment with the same name or
the import will fail.

</div>

See [Exporting All Datastore Classes](#exporting-all-datastore-classes)
for information.

#### Passing variables between successive playbook methods

Automate designers can pass variables between successive Ansible
playbook methods in a state machine using ManageIQ.

To pass variables between Ansible playbook methods, use the `set_stats`
module in your playbooks.

**Example.**

    ---
    # This playbook prints a simple debug message
    - name: Echo Hello, Fred and Wilma
      hosts: localhost
    
      tasks:
      - name: "playbook1 - testing input vars"
        set_stats:
          data:
            pb_var1a: "{{ input1a }}"
            pb_var1b: "{{ input1b }}"
    
      - debug: msg="Hello, {{ input1a }} and {{ input1b }}"

For more information on the `set_stats` module, see the
[Ansible](https://docs.ansible.com) documentation.

## Expression Methods

ManageIQ additionally provides support for Expression Methods, that
allow you to use advance search filters as Automate Methods,
substituting the user input from Automate Objects. Expression methods
have several distinct advantages, including: running directly in the
worker appliance; removing the overhead of forking a DRb process to run
the Automate Methods; no Ruby code required; and prebuilt for Dynamic
Dialogs.

### Input Parameters

Expression methods allow for substitution of user input through input
parameters,

| Input Parameter | Explanation                                                                                                                                                                                                                                  |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **arg**         | The argument used in the expression. Each argument should employ the prefix **arg**. Example: **arg1**: the first argument in the expression; **arg2**: the second argument in the expression; **argn**: the nth argument in the expression. |

#### Optional Input Parameters

<div class="note">

If attributes and distinct are not specified we try to store the result
in a variable called values with a hash consisting of id and name. This
makes it compatible with our existing dynamic dialog result set.

</div>

| Optional Input Parameter | Explanation                                                                                                                                               |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **attributes**           | A comma delimited list of attributes to select from the resultant objects. This should me marked as an Array Type in the Input Parameters field.          |
| **distinct**             | A comma delimited list of attributes which are distinct in the resultant objects.This should me marked as an Array Type in the Input Parameters field.    |
| **result\_obj**          | The object where the result data should be stored. (default: current object)                                                                              |
| **result\_attr**         | The name of the attribute which stores the result. (default: values)                                                                                      |
| **result\_type**         | The result type hash or array (default: dialog\_hash which matches to our dynamic dialog hash. Valid values are *hash*, *dialog\_hash*, *array*, *simple* |
| **on\_empty**            | The method behavior when the search returns an empty list.                                                                                                |
| **error**                | Abort. (default: error)                                                                                                                                   |
| **default**              | The default value in case the result is empty and you select warn.                                                                                        |

### Creating an Expression Method

Expression methods allow you to use advance search filters as automate
methods, substituting user input at runtime, and making them ideal for
dynamic dialogs.

To create an expression method:

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Explorer</span>, then click on a domain under **Datastore**.

2.  Under a namespace, select the class for which you want to create a
    new method.

3.  Click the **Methods** tab.

4.  Click ![image](images/1847.png) (**Configuration**) then,
    ![image](images/1862.png) (**Add a New Method**).

5.  In the **Main Info** area, select **expression** from the drop-down
    menu.

6.  Provide a **Name** and **Display Name**.

7.  Select an **Expression Object** from the drop-down menu.

8.  In the **Expression** editor, create the expression by setting the
    controls and values used at runtime:
    
    1.  Using the drop-down menu, select the value to use. Based on your
        selection, choose or input additional values from the drop-down
        menus or text fields that appear.
    
    2.  In the **Contains** field, input a value or click **User will
        input the value**.
    
    3.  Click ![image](images/1863.png) to complete the expression.

9.  Add **Input Parameters** for each of the user input fields required.
    
    1.  Click ![image](images/2366.png) to add a new parameter.
    
    2.  Provide a **Name**, **Default Value** and select a **Data Type**
        for each parameter.
    
    3.  Click ![image](images/1863.png) to add the parameter.
        
        <div class="note">
        
        If **User will input the value** is checked, arguments for each
        input parameter names using the prefix “arg”.
        
        For example, if there are 3 fields then the input parameter
        names should be arg1, arg2, and arg3. If there are two runtime
        parameters arg1 and arg2 must be defined in the input
        parameters. In the default value for these fields values can be
        substituted from other objects in the Automate Workspace.
        
        </div>

10. Click **Add**.

## Simulation

After your model is designed, use the simulate page to test it. It
allows you to see the results in tree and XML view.

### Simulating an Automate Model

This procedure shows you how to simulate an automate model.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Simulation</span>.

2.  In **Object Details**, select a type of object from
    `/System/Process/` that will initiate the model. The **Message**
    should be `create`. Type in the name of the **Request** where you
    are starting from.
    
    ![image](images/2368.png)

3.  Select the **Type** of item you want to run the simulation on. Then,
    select a specific one to use as the example.
    
    ![image](images/2369.png)

4.  Check **Execute Methods** if you want to perform the model and not
    just simulate it.
    
    ![image](images/2370.png)

5.  Type in the **Attribute/Value Pairs** fields if applicable.

6.  Click **Submit**.

Click on the **Tree View** or **XML View** tabs to see results.

## Importing, Exporting, and Resetting the Datastore

The **Automate Model** can be exported and imported as a YAML file.
ManageIQ allows you to back up your model by export. Red Hat may provide
you with new or updated classes, and provides an import function for
either a class or the entire model. Finally, you can reset the datastore
to its default. Always be sure to export the current datastore before
importing or resetting.

<div class="note">

The datastores you are exporting or importing between must use the same
ManageIQ version.

</div>

### Exporting All Datastore Classes

This procedure shows you how export datastore classes as a YAML file.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Import/Export</span>.

2.  Click ![image](images/2371.png) (**Export all Datastore classes and
    instances to a file**).

3.  Follow your browser’s prompts to save the file.

The datastore is zipped and exported as a `YAML` file.

### Importing Datastore Classes

This procedure shows you how to import datastore classes.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Import/Export</span>.

2.  Export the datastore so that you have a backup.

3.  Click **Choose file** to navigate to the location of the *\*.zip*
    file to import.

4.  Click **Upload**.

5.  After the file has uploaded, specify the following using the
    dropdown menus:
    
      - The domain to import into
    
      - The domain to import from
    
      - All namespaces you wish to import

6.  Click **Commit** to finish importing the selected domain.

The datastore is imported from the uploaded `YAML` files.

### Resetting Datastores to the Default

This procedure shows you how reset the datastores to the default.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Import/Export</span>.

2.  Export the datastore so that you have a backup.

3.  Click ![Reset](images/reset.png) (**Reset all components in the
    following domains: RedHat, ManageIQ**).

4.  Click **OK**.

# Invoking Automate

## Automate Examples

This chapter describes the ways to invoke an Automate workflow.
Automation can be initiated through an alert, an event, a ManageIQ
application, or a custom button. The same automation process can be
re-used across more than one of these. For example, using automation to
remove orphaned virtual machines and instances could be initiated by:

  - An administrator request from the ManageIQ console (from a custom
    button)

  - An alert indicating the datastore has less than 20% free-space

  - A virtual machine or instance unregistered event is detected

All invocations of an automate model must enter through the
`/System/Process` namespace.

## Invoking Automate using a Custom Button

Invoke an Automate model by mapping an Ansible playbook or instance from
the `/System/Process/Request` class to a custom button. Before creating
the button, you need to have an Ansible playbook service catalog item or
an instance in the `/System/Process/Request` class to map to it and a
button group to assign it to.

Create buttons for a cluster, host, datastore, provider, virtual
machines or cloud instances. When the button is clicked, the model or
playbook will be invoked for the selected item. For each of these, you
can have up to 15 buttons.

## Creating a Custom Button Group

This procedure shows you how to create a custom button group.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  Click the **Buttons** accordion.

3.  From the **Object Types** tree, select the type of object you want
    to create the button group for.

4.  Click ![image](images/1847.png)(**Configuration**),
    ![image](images/1862.png) (**Add a new Button Group**).

5.  Type in a **Button Group Text** and **Button Group Hover Text**, and
    select the **Button Group Image** you want to use.

6.  If custom buttons have already been created, assign them to the
    button group. If not, see [Creating a Custom
    Button](#create-a-custom-button) to create custom buttons.

7.  Click **Add**.

The button group will show in the object type you added the button to.

## Creating a Custom Button

This procedure shows you how to create a custom button.

<div class="note">

Custom buttons can be migrated to other ManageIQ appliances. See
[Migrating Custom Buttons](#export-import-custom-button) for guidance on
migrating custom buttons to a new ManageIQ appliance.

</div>

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  Click the **Buttons** accordion.

3.  From the **Object Types** tree, select the type of object you want
    to create the button for.

4.  Click **Unassigned Buttons**.

5.  Click ![image](images/1847.png)(**Configuration**), then
    ![image](images/1862.png) (**Add a new Button**).
    
    <div class="note">
    
    If ![image](images/1862.png) (**Add a new Button**) is not
    available, that means you have not created a button group for that
    object. To continue, create a button group first. See [Creating a
    Custom Button Group](#create-custom-button-group)
    
    </div>

6.  Under the **Options** tab:
    
    1.  Select the **Button** type from the list.
    
    2.  Enter button **Text** and **Hover Text**, and select the
        **Icon** and **Icon Color** to use.
    
    3.  Select a **Dialog** if applicable.
    
    4.  Check **Open URL** to open a browser window for the custom URL
        returned when the button is executed.
    
    5.  Choose a **Display For** option for the button.
    
    6.  Select a **Submit** parameter to choose how to submit objects to
        automate. Selecting *Submit All* will pass all objects at once
        when the button is executed, while choosing *One by one* will
        run execute the button action each time per object.

7.  Under the **Advanced** tab:
    
    1.  Set button **Enablement**. Click **Define Expression** to access
        the expression editor tool. Enter **Disabled Button Text** to
        display when the custom button is disabled.
    
    2.  Use **Visibility** to determine button appearance based on a
        custom expression. Click **Define Expression** to access the
        expression editor tool.
        
        <div class="note">
        
        For more about setting visibility and enablement for a custom
        button, see [Setting Enablement and Visibility for Custom
        Buttons](#filtering-actions-custom-buttons).
        
        </div>
    
    3.  In **Object Details**, select **Request** from the
        `/System/Process/` dropdown. By default, the message is
        `create`. Do not change it.
    
    4.  Enter a **Request** name for the `/System/Process/Request`
        instance.
    
    5.  Enter the **Attribute/Value Pairs** fields if applicable.
    
    6.  Set **Role Access**. Selecting *\<By Role\>* will display
        available roles. Check applicable roles.

8.  Click **Add** when you have confirmed that the button accomplishes
    the task you want.

The button will show in the object type you added the button to.

## Creating an Ansible Playbook Button

ManageIQ includes an option to create an Ansible Playbook custom button.
This feature allows users to select a playbook to run as well as an
inventory target to run it against. An Ansible playbook type button can
be defined for any object type available.

<div class="note">

An Ansible Playbook catalog item must exist in order to create an
Ansible Playbook custom button. For more information, see [Creating an
Ansible Playbook Service Catalog
Item](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.5/html/provisioning_virtual_machines_and_hosts/catalogs-services#create-playbook-service-catalog-item)
in the Provisioning Virtual Machines and Hosts guide.

</div>

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  Click the **Buttons** accordion.

3.  From the **Object Types** tree, select the type of object you want
    to create the button for.

4.  Click **Unassigned Buttons**.

5.  Click ![image](images/1847.png)(**Configuration**), then
    ![image](images/1862.png) (**Add a new Button**).
    
    <div class="note">
    
    If ![image](images/1862.png) (**Add a new Button**) is not
    available, that means you have not created a button group for that
    object. To continue, create a button group first. See [Creating a
    Custom Button Group](#create-custom-button-group).
    
    </div>

6.  Select **Ansible Playbook** from the **Button Type** drop-down menu.

7.  From the **Playbook Catalog Item** choose a playbook-backed catalog
    item to run.

8.  Choose a host from the **Inventory** against which to run the
    playbook. If **Specific Hosts** is selected, input the IP address or
    DNS names for each host in the text field, separating each with a
    comma.
    
    <div class="note">
    
    ManageIQ supports two configurations for host value input:
    
      - To allow user-provided host values, set the custom button to
        **Specific Hosts** and leave the associated text field blank.
    
      - To use admin-specified host values, remove the **Hosts** field
        when creating the dialog the service uses. In this
        configuration, the field will not appear to users. See [Service
        Dialogs](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html/provisioning_virtual_machines_and_hosts/catalogs-services#service-dialogs)
        for information on generating a service dialog.
    
    </div>

9.  Type in a **Text** and **Hover Text**, and select the **Icon** you
    want to use.

10. Select an **Icon Color** from the color selection palette that pops
    up.

11. Check **Open URL** to open a browser window for the custom URL
    returned when the playbook is run.

12. Select display options for the Ansible Playbook button from the
    **Display for** drop-down menu. Choose for the button to display in
    the list view, for single entities, or both.

13. Choose how to submit objects to automate by selecting an option from
    the **Submit** drop-down menu. Selecting **Submit all** will pass
    all objects at once when the playbook is executed, while choosing
    **One by one** will run the the playbook each time per object.

14. Click **Add** when you have confirmed that the button accomplishes
    the task you want.

## Editing a Custom Button

This procedure shows you how to edit a custom button.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  From the **Object Types** dropdown, select the type of object you
    want to edit the button for.

3.  Click the button you want to edit.

4.  Click ![image](images/1847.png)(**Configuration**),
    ![image](images/1851.png) (**Edit this Button**).

5.  Modify as required.

6.  Click **Save**.

## Deleting a Custom Button

This procedure shows you how to delete a custom button.

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>, then select the **Buttons** accordion.

2.  From the **Object Type** tree in the accordion menu, select the type
    of object you want to remove the button from.

3.  Click ![image](images/1847.png) (**Configuration**). then click
    ![image](images/2098.png) (**Remove this button**).

4.  Click **OK** to confirm that you want to delete this button.

## Setting Enablement and Visibility for Custom Buttons

ManageIQ adds methods for evaluating an expression to determine whether
a custom button is visible and enabled. Each method has a target object,
for example, a virtual machine or host, and expressions can set a custom
button to visible, hidden, or disabled.

<div class="note">

Filtering works on single objects and is not applicable to lists.

</div>

To apply filtering actions to a custom button:

1.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

2.  Click the **Buttons** accordion. Select the custom button to use.

3.  Click ![image](images/1847.png)(**Configuration**), then
    ![image](images/1851.png) (**Edit this Button**).

4.  Click the **Advanced** tab.

5.  To set enablement filtering on a custom button:
    
    1.  Under **Enablement**, click on **Define Expression**.
    
    2.  Create a visibility expression using the expression editor
        tools.
    
    3.  Click ![Confirm](images/1863.png) (**Confirm**) when finished
        defining the expression.
    
    4.  Provide **Disabled Button Text** in the field.

6.  To set visibility filtering on a custom button:
    
    1.  Under **Visibility**, click on **Define Expression**.
    
    2.  Create a visibility expression using the expression editor
        tools.
    
    3.  Click ![Confirm](images/1863.png) (**Confirm**) when finished
        defining the expression.

7.  Click **Save**.

## Using a Custom Button

This procedure shows you how to use custom buttons to invoke a cluster,
host, datastore, provider, virtual machine or instance.

1.  Go to the page for the item that you created a button for.

2.  Click the custom button group from the taskbar, and then your custom
    button.

The automate model is invoked for the specified item.

## Initiating Automate from an Event

You can also use a ManageIQ Policy Event to initiate automation. You can
either use the provided Raise Automation Event action or create a custom
automation action. The first case will start in the `/System/Process`
class, but then go to the Event that initiated the Automate model in the
`/System/Process/Event Class`. If you create your own custom action, it
will start from the `/System/Process` class and then go to the
`/System/Process/Request Class` instead.

For example, suppose that you always want the same Automate model to
occur when a virtual machine is created. You would use the Raise
Automation Event Action. There are instances in the
`/System/Process/Event Class` for the following Events that you can
select as part of a Policy:

![image](images/2373.png)

## Creating a Policy for Automate

This procedure shows you how to create a policy for automate.

1.  Navigate to <span class="menuchoice">Control \> Explorer</span>.

2.  Click the **Policies** accordion, and select **Control Policies**.

3.  Select **Vm Control Policies**.

4.  Click ![image](images/1847.png)(**Configuration**), then
    ![image](images/1862.png) (**Add a New Control Vm Policy**).

5.  Type in a **Description**.

6.  Uncheck **Active** if you do not want this policy processed even
    when assigned to a resource.

7.  Click **Add**. You are brought to the page where you add conditions
    and events to your new policy.

8.  Click ![image](images/1847.png)(**Configuration**), then
    ![image](images/1851.png) (**Edit this Policy’s Event
    assignments**).
    
      - Check the events you want to use to send to an **Automate
        Model**.
    
      - Click **Save**.
    
      - From the **Events** area, click on the **Description of the
        Event** you want to assign an action to.
    
      - Click ![image](images/1851.png) (**Edit Actions for this Policy
        Event**).

9.  Select **Raise Automation Event**, and click
    ![image](images/1876.png) (**Move selected Actions into this
    Event**).

10. Click **Save**.

You can now assign this policy to a **Policy Profile**. Then, assign the
policy profile to the virtual machines. Every time this event happens on
the virtual machine the appropriate Automate Model will be initiated.

<div class="note">

If you want the policy to initiate an Automate Model from the
`/System/Process/Request` class, then you can create your own custom
action. Be sure to have an instance in the `/System/Process/Request`
class for it to map to.

</div>

## Creating a Custom Automate Action

This procedure shows you how to create a custom Automate action.

1.  Navigate to <span class="menuchoice">Control \> Explorer</span>
    accordion.

2.  Click the **Actions** accordion.

3.  Click ![image](images/1847.png)(**Configuration**), then
    ![image](images/1862.png) (**Add a new Action**).

4.  Type in a **Description** for the Action.

5.  Select **Invoke a Custom Automation** from **Action Type**.

6.  In **Custom Automation**,
    
      - For **Message**, type `create`.
    
      - For **Request**, type in the name of the instance of the
        `/System/Process/Request Class` in the second.

7.  Type in the **Attribute/Value Pairs** fields if applicable.

8.  Click **Add**.

The action is created and can be added to a policy.

# Objects

# Virtual Machine Properties

When using these items in a method, prefix them with `vm.`. For example:
`vm.storage_id.`

| Friendly Name or Description          | Raw Column Name                      |
| ------------------------------------- | ------------------------------------ |
| Allocated Disk Storage                | allocated\_disk\_storage             |
| Autostart                             | autostart                            |
| Blackbox Exists                       | blackbox\_exists                     |
| Blackbox Validated                    | blackbox\_validated                  |
| Boot Time                             | boot\_time                           |
| Busy                                  | busy                                 |
| Cluster                               | ems\_cluster\_name                   |
| Configuration XML                     | config\_xml                          |
| Connection State                      | connection\_state                    |
| CPU Affinity                          | cpu\_affinity                        |
| CPU Limit                             | cpu\_limit                           |
| CPU Reserve                           | cpu\_reserve                         |
| CPU Reserve Expand                    | cpu\_reserve\_expand                 |
| CPU Shares                            | cpu\_shares                          |
| CPU Shares Level                      | cpu\_shares\_level                   |
| Created on Time                       | ems\_created\_on                     |
| Currently Used Space                  | used\_storage\_by\_state             |
| Datastore Path                        | v\_datastore\_path                   |
| Date Created                          | created\_on                          |
| Date Updated                          | updated\_on                          |
| Description                           | description                          |
| Ems                                   | ems\_id                              |
| Evm Owner                             | evm\_owner\_id                       |
| Evm Owner Email                       | evm\_owner\_email                    |
| Evm Owner Name                        | evm\_owner\_name                     |
| ManageIQ Unique ID (Guid)             | guid                                 |
| Format                                | format                               |
| Host                                  | host\_id                             |
| Host Name                             | host\_name                           |
| Id                                    | id                                   |
| Is a Template                         | v\_is\_a\_template                   |
| Last Analysis Attempt On              | last\_scan\_attempt\_on              |
| Last Analysis Time                    | last\_scan\_on                       |
| Last Compliance Status                | last\_compliance\_status             |
| Last Compliance Timestamp             | last\_compliance\_timestamp          |
| Last Perf Capture On                  | last\_perf\_capture\_on              |
| Last Sync Time                        | last\_sync\_on                       |
| Location                              | location                             |
| Memory Limit                          | memory\_limit                        |
| Memory Reserve                        | memory\_reserve                      |
| Memory Reserve Expand                 | memory\_reserve\_expand              |
| Memory Shares                         | memory\_shares                       |
| Memory Shares Level                   | memory\_shares\_level                |
| Name                                  | name                                 |
| OS Name                               | os\_image\_name                      |
| Owner                                 | owner                                |
| Paravirtualization                    | paravirtualization                   |
| Parent Cluster                        | v\_owning\_cluster                   |
| Parent Datacenter                     | v\_owning\_datacenter                |
| Parent Folder (Hosts & Clusters)      | v\_owning\_folder                    |
| Parent Folder (VMs & Templates)       | v\_owning\_blue\_folder              |
| Parent Folder Path (Hosts & Clusters) | v\_owning\_folder\_path              |
| Parent Folder Path (VMs & Templates)  | v\_owning\_blue\_folder\_path        |
| Parent Host Platform                  | v\_host\_vmm\_product                |
| Parent Resource Pool                  | v\_owning\_resource\_pool            |
| Pct Free Disk                         | v\_pct\_free\_disk\_space            |
| Platform                              | platform                             |
| Power State                           | power\_state                         |
| Previous State                        | previous\_state                      |
| Registered                            | registered                           |
| Reserved                              | reserved                             |
| Retired                               | retired                              |
| Retirement                            | retirement                           |
| Retires On                            | retires\_on                          |
| Service                               | service\_id                          |
| Smart                                 | smart                                |
| Standby Action                        | standby\_action                      |
| State Changed On                      | state\_changed\_on                   |
| Storage                               | storage\_id                          |
| Storage Name                          | storage\_name                        |
| Template                              | template                             |
| Thin Provisioned                      | thin\_provisioned                    |
| Tools Status                          | tools\_status                        |
| Total Provisioned Space               | provisioned\_storage                 |
| Total Snapshots                       | v\_total\_snapshots                  |
| Total Used Disk Space                 | used\_disk\_storage                  |
| Uid Ems                               | uid\_ems                             |
| Uncommitted Space                     | uncommitted\_storage                 |
| Used Storage                          | used\_storage                        |
| V Pct Used Disk Space                 | v\_pct\_used\_disk\_space            |
| VDI Available                         | vdi\_available                       |
| VDI Connection DNS Name               | vdi\_connection\_dns\_name           |
| VDI Connection Logon Server           | vdi\_connection\_logon\_server       |
| VDI Connection Name                   | vdi\_connection\_name                |
| VDI Connection Remote IP Address      | vdi\_connection\_remote\_ip\_address |
| VDI Connection Session Name           | vdi\_connection\_session\_name       |
| VDI Connection Session Type           | vdi\_connection\_session\_type       |
| VDI Connection URL                    | vdi\_connection\_url                 |
| VDI Endpoint IP Address               | vdi\_endpoint\_ip\_address           |
| VDI Endpoint MAC Address              | vdi\_endpoint\_mac\_address          |
| VDI Endpoint Name                     | vdi\_endpoint\_name                  |
| VDI Endpoint Type                     | vdi\_endpoint\_type                  |
| VDI User Appdata                      | vdi\_user\_appdata                   |
| VDI User DNS Domain                   | vdi\_user\_dns\_domain               |
| VDI User Domain                       | vdi\_user\_domain                    |
| VDI User Home Drive                   | vdi\_user\_home\_drive               |
| VDI User Home Path                    | vdi\_user\_home\_path                |
| VDI User Home Share                   | vdi\_user\_home\_share               |
| VDI User Logon Time                   | vdi\_user\_logon\_time               |
| VDI User Name                         | vdi\_user\_name                      |
| Vendor                                | vendor                               |
| Version                               | version                              |
| VMsafe Agent Address                  | vmsafe\_agent\_address               |
| VMsafe Agent Port                     | vmsafe\_agent\_port                  |
| VMsafe Enable                         | vmsafe\_enable                       |
| VMsafe Fail Open                      | vmsafe\_fail\_open                   |
| VMsafe Immutable VM                   | vmsafe\_immutable\_vm                |
| VMsafe Timeout (ms)                   | vmsafe\_timeout\_ms                  |

Virtual Machine Properties

# Methods for use in Ruby Scripts

To use one of these in one of your own Ruby methods, use the syntax of
`vm.method`. For example, to reboot the guest operating system, use
`vm.rebootGuest`.

| Method                      | Description                                                                                                               |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| start                       | Start Virtual Machine container.                                                                                          |
| stop                        | Stop Virtual Machine container.                                                                                           |
| suspend                     | Suspend Virtual Machine container.                                                                                        |
| unregister                  | Unregister Virtual Machine.                                                                                               |
| collect\_running\_processes | Collect the running processes from a started Virtual Machine.                                                             |
| shutdownGuest               | Shutdown the guest operating system of the VM container. Requires VMware tools (or vendors tools) installed on the guest. |
| standbyGuest                | Put the guest operating system into standby. Requires VMware tools (or vendors tools) installed on the guest.             |
| rebootGuest                 | Reboot the guest operating system. Requires VMware tools (or vendors tools) installed on the guest.                       |

# Host Properties

When using these items in a method, prefix them with host, such as
`host.ems_id`.

| Friendly Name or Description                  | Raw Column Name                                        |
| --------------------------------------------- | ------------------------------------------------------ |
| All Enabled Ports                             | all\_enabled\_ports                                    |
| Annotation                                    | v\_annotation                                          |
| Authentication Status                         | Authentication\_status                                 |
| Connection State                              | connection\_state                                      |
| CPU usage MHz rate average over time period   | cpu\_usagemhz\_rate\_average\_avg\_over\_time\_period  |
| CPU usage MHz rate high over time period      | cpu\_usagemhz\_rate\_average\_high\_over\_time\_period |
| CPU usage MHz rate low over time period       | cpu\_usagemhz\_rate\_average\_low\_over\_time\_period  |
| Custom Attribute 1                            | custom\_1                                              |
| Custom Attribute 2                            | custom\_2                                              |
| Custom Attribute 3                            | custom\_3                                              |
| Custom Attribute 4                            | custom\_4                                              |
| Custom Attribute 5                            | custom\_5                                              |
| Custom Attribute 6                            | custom\_6                                              |
| Custom Attribute 7                            | custom\_7                                              |
| Custom Attribute 8                            | custom\_8                                              |
| Custom Attribute 9                            | custom\_9                                              |
| Date Created                                  | created\_on                                            |
| Derived memory usage average over time period | derived\_memory\_used\_avg\_over\_time\_period         |
| Derived memory usage high over time period    | derived\_memory\_used\_high\_over\_time\_period        |
| Derived memory usage low over time period     | derived\_memory\_used\_low\_over\_time\_period         |
| Ems                                           | ems\_id                                                |
| Enabled Inbound Ports                         | enabled\_inbound\_ports                                |
| Enabled Outbound Ports                        | enabled\_outbound\_ports                               |
| Enabled Run Level 0 Services                  | enabled\_run\_level\_0\_services                       |
| Enabled Run Level 1 Services                  | enabled\_run\_level\_1\_services                       |
| Enabled Run Level 2 Services                  | enabled\_run\_level\_2\_services                       |
| Enabled Run Level 3 Services                  | enabled\_run\_level\_3\_services                       |
| Enabled Run Level 4 Services                  | enabled\_run\_level\_4\_services                       |
| Enabled Run Level 5 Services                  | enabled\_run\_level\_5\_services                       |
| Enabled Run Level 6 Services                  | enabled\_run\_level\_6\_services                       |
| Enabled TCP Inbound Ports                     | enabled\_tcp\_inbound\_ports                           |
| Enabled TCP Outbound Ports                    | enabled\_tcp\_outbound\_ports                          |
| Enabled UDP Inbound Ports                     | enabled\_udp\_inbound\_ports                           |
| Enabled UDP Outbound Ports                    | enabled\_udp\_outbound\_ports                          |
| EVM Unique ID (Guid)                          | guid                                                   |
| Hostname                                      | hostname                                               |
| Id                                            | id                                                     |
| IP Address                                    | ipaddress                                              |
| Last Compliance Status                        | last\_compliance\_status                               |
| Last Compliance Timestamp                     | last\_compliance\_timestamp                            |
| Last Perf Capture On                          | last\_perf\_capture\_on                                |
| Last Analysis Time                            | last\_scan\_on                                         |
| Name                                          | name                                                   |
| OS Name                                       | os\_image\_name                                        |
| Platform                                      | platform                                               |
| Power State                                   | power\_state                                           |
| Region Description                            | region\_description                                    |
| Region Number                                 | region\_number                                         |
| Reserved                                      | reserved                                               |
| Service Names                                 | service\_names                                         |
| Settings                                      | settings                                               |
| Smart                                         | smart                                                  |
| SSH Root Access                               | ssh\_permit\_root\_login                               |
| Uid Ems                                       | uid\_ems                                               |
| Date Updated                                  | updated\_on                                            |
| User Assigned Os                              | user\_assigned\_os                                     |
| Parent Cluster                                | v\_owning\_cluster                                     |
| Parent Datacenter                             | v\_owning\_datacenter                                  |
| Parent Folder (Hosts & Clusters)              | v\_owning\_folder                                      |
| Total Datastores                              | v\_total\_storages                                     |
| Total VMs                                     | v\_total\_vms                                          |
| VMM Build Number                              | vmm\_buildnumber                                       |
| VMM Platform                                  | vmm\_product                                           |
| VMM Vendor                                    | vmm\_vendor                                            |
| VMM Version                                   | vmm\_version                                           |

# Provider Properties

When using these items in a method, prefix them with `ems`, such as
`ems.ems_id`.

| Friendly Name or Description                            | Raw Column Name                                         |
| ------------------------------------------------------- | ------------------------------------------------------- |
| Aggregate VM CPUs                                       | aggregate\_vm\_cpus                                     |
| Aggregate VM Memory                                     | aggregate\_vm\_memory                                   |
| CPU Ratio                                               | v\_cpu\_vr\_ratio                                       |
| CPU Usage MHZ Rate Average High Over Time Period        | cpu\_usagemhz\_rate\_average\_high\_over\_time\_period" |
| CPU Usage MHZ Rate Average Low Over Time Period         | cpu\_usagemhz\_rate\_average\_low\_over\_time\_period   |
| CPU Usage MHZ Rate Average Over Time Period             | cpu\_usagemhz\_rate\_average\_avg\_over\_time\_period   |
| Date Created                                            | created\_on                                             |
| Date Updated                                            | updated\_on                                             |
| Derived Memory Usage Rate Average High Over Time Period | derived\_memory\_used\_high\_over\_time\_period         |
| Derived Memory Usage Rate Average Low Time Period       | derived\_memory\_used\_low\_over\_time\_period          |
| Derived Memory Usage Rate Average Over Time Period      | derived\_memory\_used\_avg\_over\_time\_period          |
| Distributed Resource Scheduler Automation Level         | drs\_automation\_level                                  |
| Distributed Resource Scheduler Enabled                  | drs\_enabled                                            |
| Distributed Resource Scheduler Migration Threshold      | drs\_migration\_threshold                               |
| EMS ID                                                  | ems\_id                                                 |
| EVM Zone                                                | zone\_name                                              |
| High-Availability Admission Control                     | ha\_admit\_control                                      |
| High-Availability Enabled                               | ha\_enabled                                             |
| High-Availability Max Failures                          | ha\_max\_failures                                       |
| Id                                                      | id                                                      |
| Last Performance Data Captured                          | last\_perf\_capture\_on                                 |
| Last Smart State Analysis                               | last\_scan\_on                                          |
| Memory Ratio                                            | v\_ram\_vr\_ratio                                       |
| Name                                                    | name                                                    |
| Parent Datacenter                                       | v\_parent\_datacenter                                   |
| Qualified Description                                   | v\_qualified\_desc                                      |
| Region Description                                      | region\_description                                     |
| Region Number                                           | region\_number                                          |
| Reserved                                                | reserved                                                |
| Total CPU Speed                                         | aggregate\_cpu\_speed                                   |
| Total Hosts                                             | total\_hosts                                            |
| Total Memory                                            | aggregate\_memory                                       |
| Total Number of Logical CPUs                            | aggregate\_logical\_cpus                                |
| Total Number of Physical CPUs                           | aggregate\_physical\_cpus                               |
| Total Vms                                               | total\_vms                                              |
| Unique Identifier                                       | uid\_ems                                                |

# Storage Properties

When using these items in a method, prefix them with `storage`, such as
`storage.name`.

| Friendly Name or Description       | Raw Column Name                    |
| ---------------------------------- | ---------------------------------- |
| Date Created                       | created\_on                        |
| Date Updated                       | updated\_on                        |
| Disk Files Percent of Used         | v\_disk\_percent\_of\_used         |
| Free Space                         | free\_space                        |
| Free Space Percent of Total        | v\_free\_space\_percent\_of\_total |
| Id                                 | id                                 |
| Last Analysis Time                 | last\_scan\_on                     |
| Last Perf Capture On               | last\_perf\_capture\_on            |
| Location                           | location                           |
| Multiple Host Access               | multiplehostaccess                 |
| Name                               | name                               |
| Non-VM Files Percent of Used       | v\_debris\_percent\_of\_used       |
| Other VM Files Percent of Used     | v\_vm\_misc\_percent\_of\_used     |
| Provisioned Space Percent of Total | v\_provisioned\_percent\_of\_total |
| Reserved                           | reserved                           |
| Size of Non-VM Files               | v\_total\_debris\_size             |
| Size of Other VM Files             | v\_total\_vm\_misc\_size           |
| Size of VM Memory Files            | v\_total\_vm\_ram\_size            |
| Size of VM Snapshot Files          | v\_total\_snapshot\_size           |
| Snapshot Files Percent of Used     | v\_snapshot\_percent\_of\_used     |
| Store Type                         | store\_type                        |
| Total Hosts                        | v\_total\_hosts                    |
| Total Managed Registered Vms       | total\_managed\_registered\_vms    |
| Total Managed Unregistered Vms     | total\_managed\_unregistered\_vms  |
| Total Provisioned Space            | v\_total\_provisioned              |
| Total Space                        | total\_space                       |
| Total Unmanaged Vms                | total\_unmanaged\_vms              |
| Total VMs                          | v\_total\_vms                      |
| Uncommitted                        | uncommitted                        |
| Used Space                         | v\_used\_space                     |
| Used Space Percent of Total        | v\_used\_space\_percent\_of\_total |
| VM Memory Files Percent of Used    | v\_memory\_percent\_of\_used       |

Storage Properties

# FAQs and Flows

# Phase 1: Create Provision Request

![image](images/2375.png)

| Question                                                                        | Answer                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Where do I create a new provisioning profile based on a users LDAP group?       | Navigate to \[`VM / Provisioning / Profile`\] of either the **Cloud** or **Infrastructure** namespace in your domain.                                                                                                                                   |
| Where can I specify a pre-dialog to present to a Requester in their LDAP group? | Custom pre-dialogs can be defined in \[`VM / Provisioning /
Profile / <LDAP Group Name>`\] of either the **Cloud** or **Infrastructure** namespace in your domain.                                                                                      |
| I would like to customize our dialogs. Where are all the dialogs kept?          | All dialogs are located on each ManageIQ appliance in the `/var/www/miq/vmdb/db/fixtures` directory.                                                                                                                                                    |
| What happens if I do not specify any profiles for provisioning?                 | ManageIQ searches for a matching LDAP group in the \[`VM / Provisioning / Profile`\] class of either the **Cloud** or **Infrastructure** namespace in your domain. If an LDAP profile is NOT found then ManageIQ will use the `missing class instance`. |

# Phase 2: Request Approval

![image](images/2376.png)

| Question                                                                                  | Answer                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Where can I specify auto-approval values on a per virtual machine template basis?         | Tags can be assigned to templates in the form of \[**prov\_max\_vms**, **prov\_max\_cpus**, **prov\_max\_memory**, **prov\_max\_retirement\_days**\].                                        |
| Where can I modify the default Auto-Approval values?                                      | These values can be set in the \[`Service / Provisioning / StateMachines /
ServiceProvisionRequestApproval / Default`\] class instance in your domain.                                       |
| How can I customize the email that is sent when a request is approved?                    | The Request Approved email message can be modified in \[`VM / Provisioning / Email / MiqProvisionRequest_Approved`\] in either the **Cloud** or **Infrastructure** namespace of your domain. |
| How can I customize the email that is sent when a request is denied?                      | The Request Denied email message can be modified in \[`VM / Provisioning / Email / MiqProvisionRequest_Denied`\] in either the **Cloud** or **Infrastructure** namespace of your domain.     |
| How can I customize the email that is sent when a request is not Auto-approved?           | The Request Pending email message can be modified in \[`VM / Provisioning / Email / MiqProvisionRequest_Denied`\] in either the **Cloud** or **Infrastructure** namespace of your domain.    |
| If a Request Approval requires manual approval, how does an Approver approve the request? | Log into ManageIQ as an approver/admin and navigate to <span class="menuchoice">Virtual Machines \> Requests</span> and then click on the request.                                           |

# Phase 3: Quota Validation

| Question                                                                   | Answer                                                                                                                                                                                                                                                                              |
| -------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Where in ManageIQ can I set default quota thresholds for users and groups? | These values can be set in the \[`VM
Provisioning / StateMachines / ProvisionRequestQuotaVerification`\] class instance of either the **Cloud** or **Infrastructure** namespace in your domain.                                                                                     |
| Where in ManageIQ can I set individual and group quota thresholds?         | Tags can be assigned to groups or users by navigating to <span class="menuchoice">Configuration \> Access Control</span>. The following are valid tags that can be assigned to group or individual users: \[**quota\_max\_cpu**, **quota\_max\_memory**, **quota\_max\_storage**\]. |
| Where can I customize the way our virtual machines are named?              | Virtual machine naming conventions can be altered using the methods in the \[`VM /
Provisioning / Naming`\] class of either the **Cloud** or **Infrastructure** namespace in your domain.                                                                                           |
| How can I customize the email that is sent when a request is denied?       | The Request Denied email message can be modified in the \[`VM /
Provisioning / Email / MiqProvisionRequest_Denied`\] in either the **Cloud** or **Infrastructure** namespace of your domain.                                                                                        |

# Phase 4: Provisioning

![Target Type: Cloning a Template to a Virtual Machine](images/2377.png)

![Target Type: Clone to Template](images/2378.png)

| Question                                                                                | Answer                                                                                                                                                                                                          |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Where can I customize the email message that is sent upon provisioning completion?      | This can be customized using the \[`VM / Provisioning / Email
/ MiqProvision_Complete` \] in either the **Cloud** or **Infrastructure** namespace of your domain.                                               |
| Where can I change what is put into the virtual machines Annotation after provisioning? | These settings can be modified by leveraging the `*_PreProvision Ruby` methods in \[`VM / Provisioning / StateMachines /
Methods`\] in either the **Cloud** or **Infrastructure** namespace of your domain.     |
| Where do I set the default VC folder location for provisioning virtual machines?        | This can be modified by leveraging by leveraging the `*_PreProvision Ruby` methods in \[`VM / Provisioning / StateMachines /
Methods`\] in either the **Cloud** or **Infrastructure** namespace of your domain. |
| Where can I modify the virtual machine customization spec mapping?                      | This can be modified by leveraging by leveraging the `*_PreProvision
Ruby` methods in \[`VM / Provisioning / StateMachines / Methods`\] in either the **Cloud** or **Infrastructure** namespace of your domain. |
| Where can I modify the Clone\_to\_Template state\_machine?                              | Navigate to \[`VM / Provisioning / StateMachines / VMProvision_VM / template`\] in either the **Cloud** or **Infrastructure** namespace of your domain.                                                         |
| Where can I modify the Clone\_to\_VM state\_machine?                                    | Navigate to \[`VM /
Provisioning / StateMachines / VMProvision_VM / clone_to_vm`\] in either the **Cloud** or **Infrastructure** namespace of your domain.                                                      |

# Phase 5: Retirement

![image](images/2379.png)

| Question                                                                                            | Answer                                                                                                                                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Where can I customize the email message that is sent upon completion of virtual machine retirement? | This can be customized using the \[`VM /
Retirement / Email / vm_retirement_emails`\] in either the **Cloud** or **Infrastructure** namespace of your domain.                                                                                                                    |
| Where can I customize the email message that is sent during virtual machine retirement warnings?    | This can be customized using the \[`VM /
Retirement / Email / vm_retirement_emails`\] in either the **Cloud** or **Infrastructure** namespace of your domain.                                                                                                                    |
| If I want to customize what gets called during the retirement phase where should I look?            | This can be customized using the \[`VM / Retirement
/ StateMachines / VMRetirement`\] in either the **Cloud** or **Infrastructure** namespace of your domain.                                                                                                                    |
| How can I extend the virtual machine retirement date an additional number of days?                  | Create a custom button for virtual machines that launches \[`/System/Request/vm_retire_extend`\]. Then navigate to the \[`VM /
Retirement / Email / vm_retire_extend`\] Ruby method in the **Cloud** or **Infrastructure** namespaces and set the `vm_retire_extend_days` value. |

# Inline Method to Create a Provision Request

# Ruby method

``` ruby
# ManageIQ Automate Method
#
$evm.log("info", "ManageIQ Automate Method  Building VM Provisioning Request Started")
#
 
prov= $evm.root['miq_provision']

  # arg1 = version
  args = ['1.1']
  # arg2 = templateFields
  args << {'name' => 'App'}
  # arg3 = vmFields
  args << {'vm_name' => 'CRM_APP', 'request_type' => 'template'}
  # arg4 =  requester
  args << {'owner_email' => 'admin@asd.com', 'owner_last_name' => 'Admin', 'owner_first_name' => 'Admin', 'user_name' => 'admin'}
  # arg5 =  tags
  args << {'crm' => 'true'}
  # arg6 =  WS Values
  args << nil
  # arg7 = emsCustomAttributes
  args << nil
  # arg8 = miqCustomAttributes
  args << nil

$evm.log("info","Building provisioning request with the following arguments: <#{args.inspect}>")
result = $evm.execute('create_provision_request', *args)
```

# Migrating Custom Buttons

# Migrating Custom Buttons

This workflow demonstrates how to export custom buttons from one
ManageIQ appliance and import them in another ManageIQ appliance.

1.  Export custom buttons from the source ManageIQ appliance:
    
    1.  SSH into the ManageIQ appliance as `root`.
    
    2.  Create a temporary directory:
        
            # mkdir /tmp/custom_buttons
    
    3.  Navigate to the Virtual Management Database (VMDB) directory:
        
            # vmdb
    
    4.  Export custom buttons using the following `rake` command:
        
            # rake evm:export:custom_buttons -- --directory /tmp/custom_buttons
    
    5.  Confirm the `yaml` file was created by navigating to the new
        directory:
        
            # cd /tmp/custom_buttons

2.  Copy the directory to the target ManageIQ appliance:
    
        scp -r /tmp/custom_buttons/ hostname:/tmp/custom_buttons

3.  Import custom buttons on the target ManageIQ appliance:
    
    1.  SSH to the target ManageIQ appliance as `root`.
    
    2.  Navigate to the VMDB directory:
        
            # vmdb
    
    3.  Import custom buttons using the following `rake` command:
        
            # rake evm:import:custom_buttons -- --source /tmp/custom_buttons

To verify successful import of custom buttons:

1.  Log in to the target ManageIQ appliance.

2.  Navigate to <span class="menuchoice">Automation \> Automate \>
    Customization</span>.

3.  Click **Buttons** in the accordion menu.

Imported buttons will appear under the parent **Object Type**.
