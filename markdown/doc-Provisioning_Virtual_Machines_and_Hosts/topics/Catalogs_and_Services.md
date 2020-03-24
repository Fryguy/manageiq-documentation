# Catalogs and Services

Through the use of catalogs, {product-title} provides support for
multi-tier service provisioning to deploy layered workloads across
hybrid environments. You can create customized dialogs that will give
consumers of the services the ability to input just a few parameters and
provision the entire service. The following table lists the terminology
associated with catalogs that you will use within the CloudForms user
interface for service provisioning.

| Type                 | Information                                                                                                                                                                                             |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Catalog Bundle       | A group of templates.                                                                                                                                                                                   |
| Catalog Item         | A single template.                                                                                                                                                                                      |
| Template             | A template is a copy of a preconfigured virtual machine, designed to capture the installed software and software configurations, as well as the hardware configuration of the original virtual machine. |
| Dialog Tabs          | Part of a service dialog.                                                                                                                                                                               |
| Element              | An item on a tab in a dialog. It can be a button, check box, drop down list, radio button, tag control, text area box, or a text box.                                                                   |
| Provisioning Dialogs | Dialogs created for host provisioning, virtual machine migration, or virtual machine provisioning. The dialog name must be added to the appropriate provision instance to be processed.                 |
| Service Catalog      | A catalog item or catalog bundle that is available for provisioning.                                                                                                                                    |
| Service Dialogs      | Made up of fully customizable tabs, items, and values for use with service provisioning.                                                                                                                |

Terminology

## Generic Objects

Generic Objects are object-like entities, defined at runtime, that have
unique names and user-defined attributes and relationships. Residing in
the Automate Engine datastore, generic objects are designed to manage
objects other than those related to private infrastructure, and public
or private cloud providers.

Using automate requests, services and catalog items, generic objects can
be directly accessed or passed, during any step, as a parameter to a
service state machine. As a result, generic objects can be used to
quickly add the capability to provision and collect data on resources
not supported by {product-title}.

### Viewing Generic Objects Classes

View a list of generic objects and click through to see detailed summary
information for each object.

1.  Navigate to menu:Automate\[Generic Objects\].

2.  Click on a generic object class in the table to view its summary
    information.

### Creating Generic Objects Classes

Model a new resource by creating a generic object class and adding it to
your {product-title} inventory. Each generic object class can have
attributes, associations, and methods. Once created, generic object
classes are visible to users of the Self Service user interface at the
resource level.

Create a generic object class using the following steps:

1.  Navigate to menu:Automation\[Automate \> Generic Objects\].

2.  Click ![Configuration](1847.png) (**Configuration**), then click
    ![Add a New Generic Object Class](1862.png) (**Add a New Generic
    Object Class**).

3.  Provide a **Name** and **Description** for the new object class.

4.  In the **Attributes** field, enter a **Name** and choose a **Type**
    from the drop-down list. Click the ![Add](1848.png) button to add
    attributes.

5.  Enter a **Name** and select a **Class** for the object class’s
    **Associations**. Click the ![Add](1848.png) button to create
    additional associations.

6.  Provide a **Name** for the **Methods**. Click the ![Add](1848.png)
    button to add methods.

7.  Click **Add**.

### Editing Generic Object Classes

Edit existing generic object classes using the following steps:

1.  Navigate to menu:Automation\[Automate \> Generic Objects\].

2.  Click on a generic object class in the list view.

3.  Click ![Configuration](1847.png) (**Configuration**), then click
    ![Edit this Generic Object Class](1851.png) (**Edit this Generic
    Object Class**).

4.  Make required changes to the generic object class fields.

5.  Click **Save**.

### Removing Generic Objects Classes

Remove generic object classes from your inventory using the following
steps:

1.  Navigate to menu:Automation\[Automate \> Generic Objects\].

2.  Check the generic objects classes from the table to remove.

3.  Click ![Configuration](1847.png) (**Configuration**), then click
    ![Remove selected Generic Object Classes from Inventory](2098.png)
    (**Remove selected Generic Object Classes from Inventory**).

4.  Click **OK** to confirm.

### Exporting Generic Objects

Export generic objects from {product-title} to create a shared library.

Exporting a generic object requires the object has been created in
{product-title\_short}.

Procedure

1.  ssh to the {product-title\_short} appliance as `root`.

2.  Navigate to `/var/www/miq/vmdb`:
    
        # cd /var/www/miq/vmdb

3.  Create a temporary directory to store the generic object
    definitions:
    
        # mkdir tmp/generic_object_definitions

4.  Export the generic object definitions using the following `bin/rake`
    command:
    
        # bin/rake evm:export:generic_object_definitions -- --directory tmp/generic_object_definitions

Locate the exported yaml file containing the generic object properties
in the temporary folder.

### Importing Generic Objects

Import generic objects to {product-title\_short} from a shared library.

Procedure

1.  ssh to the {product-title\_short} appliance as `root`.

2.  Navigate to `/var/www/miq/vmdb`:
    
        # cd /var/www/miq/vmdb

3.  Create a temporary directory to store the generic object
    definitions:
    
        # mkdir tmp/generic_object_definitions

4.  Copy the yaml file containing the generic object definitions to the
    temporary folder:
    
        # cp generic_objects.yaml tmp/generic_object_definitions

5.  Import the generic object definitions to the {product-title\_short}
    appliance using the following `bin/rake` command:
    
        # bin/rake evm:import:generic_object_definitions -- --source tmp/generic_object_definitions

Confirm the generic objects have imported successfully by [Viewing
Generic Objects Classes](#view-generic-objects) in the
{product-title\_short} user interface.

## Service Dialogs

When provisioning a service, input will be needed from the requester.
Service dialogs are used to take input from the user. This input is
connected to a method in the Automate model that defines how the user’s
input is translated into the provision request. Before creating a
service dialog, be sure to plan what items you need the user to input.

### Adding a Service Dialog

<div class="important">

  - When creating a service dialog for use with Ansible playbook catalog
    items, variable elements must use the prefix **param\_** when
    assigning the value. For example, a new variable labeled **key1**
    should have its value set as **param\_key1**.

  - Using Ansible playbooks to populate dynamic dialog fields is not
    recommended due to delay times caused by the overhead of interaction
    between systems.

  - If you add the playbook automate method to a service dialog, only
    users with admin privileges can run the dialog.

</div>

{product-title} includes a drag-and-drop service dialog editor to create
service dialogs. The editor, with its drag-and-drop feature, provides a
visual representation of the components that comprise a service dialog.
You can easily design your service dialog utilizing dialog tabs,
sections (previously referred to as boxes), and elements.

When users access a service, the majority of options available to them
are preset and cannot be altered. The requirements for the service
determine the options and fields that need to be present in the dialog
for user input. A service dialog exposes some of those options to the
user so that even if they are ordering a basic Red Hat Enterprise Linux
7 machine, for example, they can at least choose the amount of memory,
virtual CPUs, or other options available to the instance they order. In
cases where certain fields must be unique, such as the name of virtual
machines in Red Hat Virtualization, users must enter their own unique
name for the virtual machine they choose or the operation will fail, so
this field must be exposed.

A service dialog contains three components:

  - One or more **Tabs**.

  - Inside the tabs, one or more **Sections**. Note that in the previous
    method of creating service dialogs using the {product-title\_short}
    user interface, **Sections** were referred to as **Boxes**.

  - Inside the sections, one or more **Elements**. Elements are controls
    that accept input. Elements contain methods, like check boxes,
    drop-down lists or text fields, to fill in the options on the
    provisioning dialog.

<div class="important">

The names of the elements must correspond to the options used in the
provisioning dialog.

</div>

1.  Navigate to menu:Automation\[Automate \> Customization\].

2.  Click the **Service Dialogs** accordion.

3.  Click ![1847](1847.png)(**Configuration**), and then
    ![1862](1862.png)(**Add a new Dialog**).
    
    ![edit section1](edit-section1.png)

4.  Enter basic details under **General**:
    
    1.  Enter the **Dialog’s name** and **Dialog’s description**.

5.  Add a new tab to the dialog:
    
    1.  Click ![1862](1862.png)**Create Tab**. Then, click the
        ![pencil](1851.png)icon on the new tab to edit tab information.
    
    2.  Enter a **Label**.
    
    3.  Optional: Enter a description for the tab in **Description**.
    
    4.  Click **Save**.

6.  Add a new section to the tab:
    
    1.  Click ![1862](1862.png)**Add Section**. Then, click the
        ![pencil](1851.png)icon on the upper-right to edit section
        details.
    
    2.  Enter a **Label**.
    
    3.  Optional: Enter a description for the section in
        **Description**.
    
    4.  Click **Save**.

7.  Add elements to the section:
    
    1.  From the list of elements on the left, click an element you want
        to add, then drag-and-drop it inside the section. Then, click
        the ![pencil](1851.png)icon next to the element to edit its
        field details.
        
        | Element Types | Additional Info                                                                                                                                                                                                                                                                |
        | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
        | Text Area     | Provides text area for users to enter text. You can enter the default text in **Default Value**, or leave it as blank.                                                                                                                                                         |
        | Text Box      | Text box is similar to a text area with the added option to enable **Protected** so the text is shown as asterisks(\*), instead of plain text.                                                                                                                                 |
        | Check Box     | Enable **Default Value** if you want the box checked by default.                                                                                                                                                                                                               |
        | Drop Down     | Use drop down to create list entries either manually or using automate methods. Enable **Dynamic** to create lists using automate methods; use **Entry Point** to select an automate instance. Enable **Show Refresh Button** to allow users to refresh list options manually. |
        | Radio Button  | Similar to a drop down but displays options using radio buttons.                                                                                                                                                                                                               |
        | Datepicker    | Use this to enable users to pick a date by clicking the calendar icon.                                                                                                                                                                                                         |
        | Timepicker    | use this to enable users to pick a date and time.                                                                                                                                                                                                                              |
        | Tag Control   | Select a **Category** of tags you want assigned to virtual machines associated with the service dialog. Enable **Single Select** if only one tag can be selected.                                                                                                              |
        

    2.  Enter a **Label**, **Name**, and **Description** for the
        element.
        
        <div class="important">
        
        Element names must correspond to the options used in the
        provisioning dialog. **Name** must use only alphanumeric
        characters and underscores without spaces. It is also used to
        retrieve the value of this element in the method used with the
        dialog and must start with **dialog\_service\_type**.
        
        </div>
    
    3.  Optional: Add additional information in **Help** to assist the
        user to complete the fields in the service dialog. This field is
        useful for explaining unfamiliar terminology or providing
        configuration tips. This information is presented when you hover
        over the \[\!\] exclamation mark in the Service Dialog while
        ordering a Service Catalog later.
    
    4.  Set other options as required.
    
    5.  Click **Save**.

8.  Optional: Repeat the above step to add more elements to the existing
    section, or create and add elements to a new section as required.

9.  Optional: Repeat the step to add a new tab to the dialog, and
    subsequent steps to add sections and elements to it as required.

10. Click **Save** to create the dialog.

The service dialog is now created, and added to the **Service Dialogs**
accordion.

### Creating a Service Dialog from a Container Template

Complete the following procedure to create a Service Dialog from a
Container Template.

1.  Navigate to menu:Compute\[Containers \> Container Templates\] and
    select the template for provisioning.

2.  Click ![1847](1847.png)(**Configuration**), then
    ![1862](1862.png)(**Create Service Dialog from Container
    Template**).

3.  Enter a name for the dialog in **Service Dialog Name**.

4.  Click **Save**.

You can use this service dialog when creating a catalog item for
container template provisioning; see [Creating an OpenShift Template
Catalog Item](#create-container-template-catalog-item).

### Importing Service Dialogs

You can share service dialogs between appliances using the export and
import features.

1.  Navigate to menu:Automation\[Automate \> Customization\].

2.  In the **Import/Export** accordion, click **Service Dialog
    Import/Export**.

3.  In the **Import** area, click **Browse** to select an import file.

4.  Click **Upload**.

### Exporting Service Dialogs

You can share service dialogs between appliances using the export and
import features.

1.  Navigate to menu:Automation\[Automate \> Customization\].

2.  In the **Import/Export** accordion, click **Service Dialog
    Import/Export**.

3.  In the **Export** area, select the service dialogs that you want to
    export.

4.  Click **Export**.

## Methods

### Creating a Method to Associate with the Dialog

You will need to create a method that connects the values in the dialog
with the provisioning request. The method should be created in the
`DOMAIN/Service/Provisioning/StateMachines/ServiceProvision_Template`
class of the **Automate** model.

<div class="note">

**DOMAIN** must be a user-defined Domain and not the locked ManageIQ
Domain. If necessary, you can copy the class from the ManageIQ domain
into a custom domain.

</div>

A method is provided below that was created for the following scenario:

  - You want to provision a three-tiered service that contains catalog
    items of web, app and DB. Each of these virtual machines (or cloud
    instances) has been tagged under the **Service** category with the
    appropriate value. Then, added as a catalog item and combined into a
    catalog bundle.

  - The **Service Dialog** captures the selection of small, medium or
    large application in a dropdown called **service\_type**. When
    referring to a value captured in an element in a dialog, the name of
    the element should be prefixed with **dialog\_**. For example,
    **service\_type** becomes **dialog\_service\_type** when used in the
    method.

  - The method will set the memory sizes for each of the catalog items
    based on the **service\_type** selection.

<!-- end list -->

    #            Automate Method
    #
    $evm.log("info", "Automate Method ConfigureChildDialog Started")
    #
    #            Method Code Goes here
    #
    $evm.log("info", "===========================================")
    $evm.log("info", "Listing ROOT Attributes:")
    $evm.root.attributes.sort.each { |k, v| $evm.log("info", "\t#{k}: #{v}")}
    $evm.log("info", "===========================================")
    
    stp_task = $evm.root["service_template_provision_task"]
    $evm.log("info", "===========================================")
    $evm.log("info", "Listing task Attributes:")
    stp_task.attributes.sort.each { |k, v| $evm.log("info", "\t#{k}: #{v}")}
    $evm.log("info", "===========================================")
    
    #############################################################
    #### This is how the method would look for dialog variables
    #############################################################
    dialog_service_type = $evm.root['dialog_service_type']
    $evm.log("info","User selected Dialog option = [#{dialog_service_type}]")
    
    stp_miq_request_task = stp_task.miq_request_task
    #$evm.log("info","(parent) miq_request_task:  = [#{stp_miq_request_task}]")
    
    #############################################################
    #### This is how you get the catalog items for the catalog bundle
    #############################################################
    
    stp_miq_request_tasks = stp_task.miq_request_tasks
    #$evm.log("info","(children) miq_request_tasks count:  = [#{stp_miq_request_tasks.count}]")
    
    #############################################################
    #### By going through the children, you can set the dialog variable for each of the children (we based our values on the childrens service tags)
    #############################################################
    
    stp_miq_request_tasks.each do |t|
    
      $evm.log("info"," Setting dialog for: #{t.description}")
      service = t.source
      service_resource = t.service_resource
      #$evm.log("info"," Child service resource name: #{service_resource.resource_name}")
      #$evm.log("info"," Child service resource description: #{service_resource.resource_description}")
    
      service_tag_array = service.tags(:app_tier)
      service_tag = service_tag_array.first.to_s
    
      memory_size = nil
    
    #############################################################
    #### The dialog_service_type is the attribute set on the service dialog
    #### We use the service_tag to decide what child gets what dialog
    #############################################################
    
      case dialog_service_type
      when "Small"
        case service_tag
        when "app"
          memory_size = 1024
        when "web"
          memory_size = 1024
        when "db"
          memory_size = 4096
        else
          $evm.log("info","Unknown Dialog type")
        end
      when "Large"
        case service_tag
        when "app"
          memory_size = 4096
        when "web"
          memory_size = 4096
        when "db"
          memory_size = 8192
        else
          $evm.log("info","Unknown Dialog type")
        end
      else
        $evm.log("info","Unknown Dialog type - setting Dialog options here")
      end
    
    #############################################################
    #### set_dialog_option sets the dialog for the child
    #############################################################
    
      t.set_dialog_option('memory',memory_size) unless memory_size.nil?
      $evm.log("info","Set dialog for selection: [#{dialog_service_type}]  Service_Tier: [#{service_tag}] Memory size: [#{memory_size}]")
    
    end
    #
    #
    #
    $evm.log("info", "Automate Method ConfigureChildDialog Ended")
    exit MIQ_OK

### Creating a Method in the Service Class

Service methods have been split based on purpose.

1.  Navigate to menu:Automation\[Automate \> Explorer\].

2.  Service Class is located at menu:DOMAIN\[Service \> Provisioning \>
    StateMachines \> Methods\] and menu:Domain\[Service \> Retirement \>
    StateMachines \> Methods\].
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>

3.  Click the **Methods** tab.

4.  Click ![1847](1847.png)(**Configuration**), then
    ![1862](1862.png)(**Add a New Method**).

5.  Enter a **Name** and **Display Name**.

6.  In the **Data** field, enter the method contents.

7.  Click **Validate** and wait for your data entry to be successfully
    validated.

8.  Click **Add**. ![6297](6297.png)

### Creating an Instance in the Service Class

1.  Navigate to menu:Automation\[Automate \> Explorer\].

2.  Service Class is located at menu:DOMAIN\[Service \> Provisioning \>
    StateMachines \> Methods\] and menu:Domain\[Service \> Retirement \>
    StateMachines \> Methods\].
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>

3.  Click the **Instances** tab.

4.  Click ![1847](1847.png)(**Configuration**), then
    ![1862](1862.png)(**Add a new Instance**).

5.  Enter a **Name** and **Display Name**.

6.  In the **Fields** area, enter the method’s name in **Value**.

7.  Click **Add**.

The instance is created so that it can be called from the
**ServiceProvision** class.

![6298](6298.png)

<div class="note">

After the method has been created, it must be mapped to an instance in
the `DOMAIN/Service/Service/Provisioning/StateMachines` class. The name
of the instance must be specified as the **Entry Point**. This method
must be called before the provision job begins.

</div>

### Associating a Method with an Automate Instance

Service methods have been split based on purpose.

1.  Navigate to menu:Automation\[Automate \> Explorer\].

2.  From the accordion menu, click the required service method.

3.  Service Class is located at menu:DOMAIN\[Service \> Provisioning \>
    StateMachines \> Methods\] and menu:Domain\[Service \> Retirement \>
    StateMachines \> Methods\].
    
    <div class="note">
    
    **DOMAIN** must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>

4.  Either create a new instance or select the **clone\_to\_service**
    instance.

5.  Click ![1847](1847.png)(**Configuration**), then
    ![1851](1851.png)(**Edit Selected Instance**).

6.  In the **configurechilddialog** value, put the path to the method.

7.  Click **Save** or **Add** if you are adding this to a new instance.

## Catalogs

Catalogs are used to create groups of virtual machines or instances for
provisioning. For example, a complete package of a database server,
desktop with specialized software already on it, and a firewall. You
will need to complete the following steps to create and provision a
service catalog.

1.  Create **Catalog Items** for each virtual machine or instance that
    will be part of the service.

2.  Create a **Service** dialog. For example, create a dropdown with
    three options small, medium, and large.

3.  Create a method for the Service Dialog. This method defines what
    each of the options means to each of the individual virtual machines
    or cloud instances for the service. This method is called from a
    service provisioning instance in the Automate model.

4.  Create an instance in the
    `DOMAIN/Service/Provisioning/StateMachines/ServiceProvision_Template`
    class that calls the method.
    
    <div class="note">
    
    DOMAIN must be a user-defined Domain and not the locked ManageIQ
    Domain. If necessary, you can copy the class from the ManageIQ
    domain into a custom domain.
    
    </div>

5.  Associate method with Automate instance.

6.  Create a **Catalog Bundle**, adding each of the catalog items to it.
    Select the **Service Dialog** you created. Use the instance created
    in the
    `DOMAIN/Service/Provisioning/StateMachines/ServiceProvision_Template`
    class as the **Entry Point**. Check **Display in Catalog** box.

7.  Provision a service.

### Creating a Catalog Bundle

1.  Navigate to menu:Services\[Catalogs\].

2.  Click the **Catalog Items** accordion.

3.  Click ![1847](1847.png)(**Configuration**), and then
    ![1862](1862.png)(**Add a New Catalog Bundle**).

4.  Enter a name and description for the bundle. Select **Display in
    Catalog**.

5.  Select the required **Catalog**.

6.  Select the required **Dialog**.

7.  Select chargeback currency.

8.  Enter **Price / Month**.

9.  Select the provisioning and retirement entry points.

10. Select **Additional Tenants**.

11. Click on the **Resources** tab, then select the catalog item you
    want to add to the bundle from the **Add a Resource** dropdown.

12. Click **Add**.

A catalog bundle is created and visible in the **Service Catalog**
accordion.

<div class="note">

You should also create and specify an Entry Point in the
`DOMAIN/Service/Provisioning/StateMachines/Methods/CatalogBundle` class
for each catalog item that is part of a bundle. If you do not, then the
pre and post provision processing will occur for each item in the bundle
in addition to processing for the **Catalog Bundle**. To set the entry
point, go into each **Catalog Item** and check **Display in Catalog**.
Then, you will see the **Entry Point** field.

</div>

### Copying a Catalog Bundle

1.  Navigate to menu:Services\[Catalogs\].

2.  Click the **Catalog Items** accordion.

3.  Select the catalog bundle you want to copy from **All Catalog
    Items**.

4.  Click ![1847](1847.png)(**Configuration**), and then
    ![Edit\_Sign](1851.png)(**Copy Selected Item**).

5.  Enter a name for the copy of catalog bundle you are creating. Note
    that this name must not already be in use.

6.  Click **Add**.

A copy of the catalog bundle is saved. You can now select this new copy
of the catalog bundle and edit as required by navigating to
![1847](1847.png)(**Configuration**), then clicking
![Edit\_Sign](1851.png)(**Edit this Item**).

### Creating a Catalog Item

Create a catalog item for each virtual machine or cloud instance that
will be part of the service.

1.  Navigate to menu:Services\[Catalogs\].

2.  Click the **Catalog Items** accordion.

3.  Click ![1847](1847.png)(**Configuration**), and then
    ![1862](1862.png)(**Add a New Catalog Item**).

4.  Select the **Catalog Item Type** you are adding. This list only
    shows items related to providers available or options activated in
    the appliance (for example, **Ansible Playbook** is available as a
    **Catalog Item Type** option if the Embedded Ansible server role is
    enabled on the appliance).

5.  Enter a name and description for the bundle. Select **Display in
    Catalog**.

6.  Select a **Catalog**.

7.  Select a **Dialog**.
    
    <div class="note">
    
    You can only choose from the catalogs and dialogs you have already
    created. If you haven’t done so, leave the values blank and edit
    later.
    
    </div>

8.  Select a **Zone**.

9.  Select the chargeback currency.

10. Enter **Price / Month**.

11. Select the catalog item’s **Subtype**.

12. Select the provisioning and retirement entry points, that is the
    Automate instance to run upon provisioning and retirement.
    
    <div class="note">
    
    The entry point must be a State Machine since the **Provisioning
    Entry Point** list is filtered to only show State Machine class
    instances. No other entry points will be available from the
    **Provisioning Entry Point** field.
    
    </div>

13. Select **Additional Tenants**.

14. Click **Add**.

### Copying a Catalog Item

<div class="note">

When copying a catalog item for reuse, you must click **Display in
Catalog** in the copied catalog item for the item to appear in the
catalog.

</div>

1.  Navigate to menu:Services\[Catalogs\].

2.  Click the **Catalog Items** accordion.

3.  Select the catalog item you want to copy from **All Catalog Items**.

4.  Click ![1847](1847.png)(**Configuration**), and then
    ![Edit\_Sign](1851.png)(**Copy Selected Item**).

5.  Enter a name for the copy of catalog item you are creating. Note
    that this name must not already be in use.

6.  Click **Add**.

A copy of the catalog item is saved. You can now select this new copy of
the catalog item and edit as required by navigating to
![1847](1847.png)(**Configuration**), then clicking
![Edit\_Sign](1851.png)(**Edit this Item**).

### Creating a Generic Catalog Item

Create generic catalog items for services non-specific to virtualization
or cloud environments. This catalog item type can serve a wide array of
needs, from creating a vLAN across a network to accessing virtual
machine IP addresses and adding them to a load balancer pool.

1.  Navigate to menu:Services\[Catalogs\].

2.  Click the **Catalog Items** accordion.

3.  Click ![1847](1847.png)(**Configuration**), and then
    ![1862](1862.png)(**Add a New Catalog Item**).

4.  Select **Generic** from the Catalog Item Type list.

5.  In the **Basic Info** subtab:
    
    1.  Type a **Name/Description**.
    
    2.  Check **Display in Catalog** to display the item in the catalog.
        A **Dialog** will be required if you select **Display in
        Catalog**.
    
    3.  Choose a **Catalog** to which to add the new item.
    
    4.  Select a **Dialog** from the available options.
    
    5.  Choose a **Subtype** from the list menu.
    
    6.  Add **Entry Point(NS/Cls/Inst)** options.
        
        1.  **Provisioning Entry Point (Domain/NS/Cls/Inst)** requires
            you to select an Automate instance to run upon provisioning.
        
        2.  **Retirement Entry Point (Domain/NS/Cls/Inst)** requires you
            to select an Automate instance to run upon retirement.
            
            <div class="note">
            
            The entry point must be a State Machine since the
            **Provisioning Entry Point** list is filtered to only show
            State Machine class instances. No other entry points will be
            available from the **Provisioning Entry Point** field.
            
            </div>

6.  In the **Details** subtab, write a **Long Description** for the
    catalog item.

7.  Click **Add**.

### Creating an Ansible Playbook Service Catalog Item

Create a catalog item that uses an Ansible Playbook to back it.

<div class="note">

  - Before creating an Ansible service, at least one repository, one
    playbook, and one credential must exist in the {product-title}
    inventory. Check your inventory and add the appropriate resources
    before creating an Ansible service. For more information, see
    [Automation Management
    Providers](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.5/html-single/managing_providers/#automation_management_providers)
    in *Managing Providers*.

  - Debugging verbosity is available for Ansible playbook catalog items.
    Selecting a higher verbosity value provides more detailed output as
    the playbook executes. **0 (Normal)** is the default value. **1
    (Verbose)** will yield return data while a value of **3 (Debug)**
    provides connection attempt and task invocation details. Higher
    levels, such as **4 (Connection)** can be useful for debugging SSH
    connections. Use **5 (WinRM Debug)** when debugging WinRM
    connections.

  - Using Ansible playbooks to populate dynamic dialog fields is not
    recommended due to delay times caused by the overhead of interaction
    between systems.

  - Only users with administrator privileges can run a service dialog
    based on a playbook.

</div>

1.  Navigate to menu:Services\[Catalogs\].

2.  In the **Catalog Items** accordion, click on the **All Catalog
    Items**.

3.  Click ![1847](1847.png)(**Configuration**), then
    ![1862](1862.png)(**Add a New Catalog Item**).

4.  Select **Ansible Playbook** from the **Catalog Item Type** drop-down
    list.

5.  Type a **Name** and **Description** for the new service catalog
    item.

6.  Click **Display in Catalog**.

7.  Select the appropriate **Catalog** from the drop-down list.

8.  In the **Provisioning** tab, set parameters for your catalog item to
    use by configuring a Playbook to back your service item:
    
    1.  Choose a **Repository** from the drop-down list.
    
    2.  Select the **Ansible Playbook** to use.
    
    3.  Assign the appropriate **Machine Credentials** from the
        drop-down list.
    
    4.  Add **Cloud** or **Network Credentials** from the drop-down
        lists.
    
    5.  Choose the **Host** against which to run the service item.
    
    6.  Set the **Max TTL** in minutes. The Time To Live (TTL) field
        allows you to set the maximum execution time for the playbook to
        run.
    
    7.  Use the **Escalate Privilege** toggle switch to enable user
        privilege escalation if called for in credentials during the
        playbook run.
    
    8.  Choose a **Verbosity** value to set the debug level for playbook
        execution.
    
    9.  Add key value pairs for **Variables** and their corresponding
        **Default Values**.
    
    10. In the **Dialog** options, choose an existing dialog from the
        **Use Existing** drop-down list or select **Create New** to add
        a new dialog.

9.  In the **Retirement** tab, set parameters for your catalog item to
    use by selecting values for the following:
    
    1.  Choose a **Repository** from the drop-down list.
    
    2.  Select the **Ansible Playbook** to use.
    
    3.  Assign the appropriate **Machine Credentials** from the
        drop-down list.
    
    4.  Add **Cloud** or **Network Credentials** from the drop-down
        lists.
    
    5.  Choose the **Host** against which to run the service item.
    
    6.  Set the **Max TTL** in minutes. The Time To Live (TTL) field
        allows you to set the maximum execution time for the playbook to
        run.
    
    7.  Use the **Escalate Privilege** toggle switch to enable user
        privilege escalation if called for in credentials during the
        playbook run.
    
    8.  Choose a **Verbosity** value to set the debug level for playbook
        execution.
    
    9.  Add key value pairs for **Variables** and their corresponding
        **Default Values**.
    
    10. In the **Dialog** options, choose an existing dialog from the
        **Use Existing** drop-down list or select **Create New** to add
        a new dialog.

10. Click **Add**.

### Creating an Ansible Tower Service Catalog Item

Create a service catalog item from an Ansible Tower template you can use
to execute an Ansible Tower playbook in {product-title}.

<div class="important">

You must first create the job or workflow template in Ansible Tower. The
job or workflow templates are automatically discovered by
{product-title} when refreshing your Ansible Tower provider’s inventory.

</div>

First, create a catalog:

1.  Navigate to menu:Services\[Catalogs\].

2.  Click ![Configuration](1847.png) (**Configuration**), then ![Add a
    New Catalog](1862.png) (**Add a New Catalog**)

3.  Enter a **Name** and **Description** for the catalog.

4.  Click **Add**.

Then, create an Ansible Tower service catalog item:

1.  Navigate to menu:Automation\[Ansible Tower \> Explorer\], then click
    on the **Templates** accordion menu.

2.  Click **Ansible Tower Templates** and select an Ansible Tower job or
    workflow template.

3.  Click ![Configuration](1847.png) (**Configuration**), then ![Create
    Service Dialog from Template](1862.png) (**Create Service Dialog
    from this Template**).

4.  Enter a **Service Dialog Name** (for example,
    *ansible\_tower\_job*)and click **Save**.

5.  Navigate to menu:Services\[Catalogs\]. Click **Catalog Items**.

6.  Click ![Configuration](1847.png) (**Configuration**), then ![Add a
    New Catalog Item](1862.png) (**Add a New Catalog Item**) to create a
    new catalog item with the following details, at minimum:
    
      - For **Catalog Item type**, select **Ansible Tower**.
    
      - Enter a **Name** for the service catalog item.
    
      - Select **Display in Catalog**.
    
      - In **Catalog**, select the catalog you created previously.
    
      - In **Dialog**, select the service dialog you created previously
        (in this example, *ansible\_tower\_job*). To ask the user to
        enter extra information when running the task, **Service
        Dialog** must be selected. A dialog is required if **Display in
        Catalog** is chosen.
    
      - In **Provider**, select your Ansible Tower provider. This brings
        up the **Ansible Tower Template** option and configures the
        **Provisioning Entry Point State Machine** automatically.
    
      - Add configuration information for **Reconfigure Entry Point**
        and **Retirement Entry Point** as applicable.
    
      - Select your desired **Ansible Tower Template** from the list.
        Generally, this is the Ansible Tower job or workflow template
        previously used to create the service dialog.

7.  Click **Add**. The catalog item you created will appear in the **All
    Service Catalog Items** list.

### Creating an Amazon Service Catalog Item

Use the following procedure to create an Amazon catalog item. Once
created, the catalog item and service dialog combine with all of the
options in the provisioning dialog. Users can then order Red Hat
Enterprise Linux instances from the **Service Catalog** in the
{product-title\_short} Service user interface.

1.  Navigate to menu:Services\[Catalogs\], then click on the **Catalog
    Items** accordion.

2.  Click ![1847](1847.png)(**Configuration**), then
    ![1862](1862.png)(**Add a New Catalog Item**).

3.  Select **Amazon** from the **Catalog Item Type** list.

4.  Enter the basic details in the **Basic Info** tab:
    
    1.  Enter a **Name** and **Description** for the new service catalog
        item.
    
    2.  Select **Display in Catalog**.
    
    3.  Select the appropriate catalog from the **Catalog** list.
    
    4.  Select the appropriate service dialog from the **Dialog** list.

5.  Click the **Request Info** tab to enter request details:
    
    1.  On the **Catalog** tab, select your Amazon AWS image name from
        the **Name** list, and the number of instances from the
        **Count** list. The **VM Name** will be overwritten during the
        provisioning process, but you can enter it as *changeme* for
        now.
    
    2.  On the **Properties** tab, select *T2 Micro* from the **Instance
        Type** list, and *Basic* or *Advanced* for **CloudWatch**. If
        you plan to access the instance, select a **Guest Access Key
        Pair**, too.
    
    3.  On the **Customize** tab, set the **Root Password** under
        **Credentials**, then select the *Basic root pass template* as a
        script for cloud-init under **Customize Template**.

6.  Click **Add**.

### Creating an Azure Service Catalog Item

Use the following procedure to create an Azure catalog item.

1.  Navigate to menu:Services\[Catalogs\], then click on the **Catalog
    Items** accordion.

2.  Click ![1847](1847.png)(**Configuration**), then
    ![1862](1862.png)(**Add a New Catalog Item**).

3.  Select **Azure** from the **Catalog Item Type** list.

4.  Enter the basic details in the **Basic Info** tab:
    
    1.  Enter a **Name** and **Description** for the new service catalog
        item.
    
    2.  Select **Display in Catalog**.
    
    3.  Select the appropriate catalog from the **Catalog** list.
    
    4.  Select the appropriate service dialog from the **Dialog** list.

5.  Click the **Request Info** tab to enter request details:
    
    1.  On the **Catalog** tab, select your Azure image name from the
        **Name** list, and the number of instances from the **Count**
        list. The **VM Name** will be overwritten during the
        provisioning process, but you can enter it as *changeme* for
        now.
    
    2.  Select appropriate **Environment** settings that are known to
        work for your Azure environment.
    
    3.  On the **Customize** tab, set the **Username** and **Password**
        under **Credentials**, then select the appropriate script under
        **Customize Template**.

6.  Click **Add**.

### Creating an OpenShift Template Catalog Item

<div class="note">

Before adding a new catalog item for container template provisioning,
create a service dialog from a container template. See [Creating a
Service Dialog from a Container
Template](#creating-a-service-dialog-from-container-template) for
details.

</div>

Complete the following procedure to create an OpenShift Template catalog
item.

1.  Navigate to menu:Services\[Catalogs\], then click on the **Catalog
    Items** accordion.

2.  Click ![1847](1847.png)(**Configuration**), then
    ![1862](1862.png)(**Add a New Catalog Item**).

3.  Select **OpenShift Template** from the **Catalog Item Type** list.

4.  Enter a **Name** and **Description** for the new service catalog
    item. Select **Display in Catalog**.

5.  Select the appropriate catalog from the **Catalog** list.

6.  From the **Dialog list**, select the service dialog you have created
    from a container template.

7.  Select your provider from the **Provider** list.

8.  Set the **Provisioning Entry Point**.

9.  Click **Add**.

### Creating an Orchestration Catalog Item

Use the following procedure to create an Orchestration catalog item.

1.  Navigate to menu:Services\[Catalogs\] and select **Catalog Items**
    in the accordion menu.

2.  Click ![Configuration](1847.png) **Configuration**, then click
    ![Green\_Plus\_Sign](1848.png) **Add a New Catalog Item**. The
    **Adding a new Service Catalog Item** window is displayed.

3.  Select **Orchestration** from the **Catalog Item Type** list.

4.  Enter the basic details in the **Basic Info**:
    
    1.  Enter a **Name** and **Description** for the new service catalog
        item.
    
    2.  Select **Display in Catalog** box.
    
    3.  Select the appropriate catalog from the **Catalog** list.
    
    4.  Select the appropriate dialog from the **Dialog** list.
    
    5.  Select the **Orchestration Template** from the list.

5.  Click **Add**.

### Provisioning a Service

1.  Navigate to menu:Services\[Catalogs\].

2.  Click the **Service Catalogs** accordion, and select the service to
    provision.

3.  Click **Order**.

The parameters are passed to the children based on the method tied to
the choices made in the dialog.

## Orchestration Stacks

Cloud orchestration is a service that allows you to create, update, and
manage cloud resources and their software components as a single unit
and then deploy them in an automated, repeatable way through a template.
Templates use a human-readable syntax and can be defined in text files,
thereby allowing users to check them into version control. Templates
allow you to easily deploy and reconfigure infrastructure for
applications within your cloud. A user can author the stack templates,
or can upload them from other sources.

{product-title} supports adding Amazon CloudFormation, OpenStack Heat,
Microsoft Azure, VNF, and VMware vApp template type, and provides the
ability to:

  - Inventory stacks and elements of each type into the
    {product-title\_short} VMDB.

  - Model the relationships of instances to their stacks, inclusive of
    the user interface. For example, selecting an instance within a
    region that is within a stack, the user interface shows this on the
    standard instance view.

  - Model the stack and its elements in the user interface.

<div class="note">

When importing a template into {product-title\_short}, the selected
elements are converted according to their type. For example, lists
convert to list boxes, and single items convert to text boxes.

</div>

### Creating an Orchestration Template

Complete the following procedure to add an orchestration template.

1.  Navigate to menu:Services\[Catalogs\] and select **Orchestration
    Templates** in the accordion menu.

2.  Click ![Configuration](1847.png)**Configuration**, then click
    ![Green\_Plus\_Sign](1848.png)**Create a new Orchestration
    Template**.

3.  Enter a **Name** and **Description** for your template.

4.  Select the template type from the **Template Type** list. The
    default is Amazon CloudFormation.

5.  Select **Draft** to create a draft template.

6.  Add your template in the area below for the selected **Template
    Type**.

7.  Click **Add**.

### Editing Orchestration Templates

Complete the following procedure to edit orchestration templates.

1.  Navigate to menu:Services\[Catalogs\] and select **Orchestration
    Templates** in the accordion menu.

2.  Select the orchestration template you want to edit from the **All
    Orchestration Templates** list.

3.  Click ![Configuration](1847.png)**Configuration**, then click
    ![Edit\_Sign](1851.png)**Edit this Orchestration Template**.

4.  Edit the template as needed.
    
    <div class="note">
    
    You can only edit the name and description of a read-only template
    as there can be stacks associated with the template.
    
    </div>

5.  Click **Save**.

### Copying Orchestration Templates

Complete the following procedure to copy an orchestration template to
create a new template.

1.  Navigate to menu:Services\[Catalogs\] and select **Orchestration
    Templates** in the accordion menu.

2.  Click ![Configuration](1847.png)**Configuration**, then click
    ![Copy](1859.png) **Copy this Orchestration Template**.

3.  Change the **Description** and the actual content of the template as
    required. {product-title\_short} automatically prefixes *Copy of* to
    the old template **Name**.
    
    <div class="note">
    
    To create a copy of an orchestration template into a new template,
    the old and new template content must differ.
    
    </div>

4.  Click **Add**.

### Deleting Orchestration Templates

Complete the following procedure to delete orchestration templates.

1.  Navigate to menu:Services\[Catalogs\] and select **Orchestration
    Templates** in the accordion menu.

2.  Select the orchestration template you want to delete from the **All
    Orchestration Templates** list.

3.  Click ![Configuration](1848.png)**Configuration**, then click
    ![Delete](1861.png)**Remove this Orchestration Template from
    Inventory**.

4.  Click **OK**.

<div class="note">

Read-only templates cannot be deleted.

</div>
