In [???](#provisioning-an-openstack-instance-from-an-image), you
provisioned instance manually by entering values in provisioning dialogs
such as name, size, image, CPUs, etc. *Catalogs* are used to create
groups of instances for provisioning. {product-title\_short} enables
users to provision instances via a single **Order** button.

Creating a *service catalog* involves:

1.  Creating a **Service Dialog**. This is a UI interface element that
    allows users to interact with the service (for example, a drop-down
    list).

2.  Creating a **Catalog Item** for each instance that will be part of
    the service.

3.  Creating a *method* for the **Service Dialog**. This method defines
    what each option means to each individual cloud instances for the
    service. This method is called from a service provisioning instance
    in the **Automate** model.

<div class="note">

For more information about catalogs and services, see [Catalogs and
Services](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.7/single/provisioning-virtual-machines-and-hosts/#catalogs-services)
from the [Provisioning Virtual Machines and
Hosts](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/provisioning_virtual_machines_and_hosts/)
guide.

</div>

# Creating a Service Dialog

When provisioning a service, input will be needed from the requester.
**Service Dialogs** are used to take input from the user. This input is
connected to a method in the **Automate** model that defines how user
input is translated into the provision request. Before creating a
**Service Dialog**, be sure to plan what items you need the user to
input.

1.  Navigate to menu:Automation\[Automate \> Customization\].

2.  Click the **Service Dialogs** accordion.

3.  Click ![1847](1847.png)(**Configuration**), and then
    ![1862](1862.png)(**Add a new Dialog**).

4.  In **Dialog Information**, enter a **Label** and **Description**.
    Check the boxes for the buttons you want available at the bottom of
    the dialog form. The description will appear as hover text.
    
    As you enter the **Label** of the dialog, it should appear in the
    **Dialog** pane on the left.
    
    1.  Click ![1862](1862.png)(**Add**), then ![1862](1862.png)(**Add a
        New Tab to this Dialog**).
    
    2.  Enter a **Label** and **Description** for this tab.
        
        As you enter the **Label** of the tab, it should appear in the
        **Dialog** pane on the left under the dialog you are creating.
    
    3.  Click ![1862](1862.png)(**Add**), then ![1862](1862.png)(**Add a
        New Box to this Tab**).
    
    4.  Enter a **Label** and **Description** for this box.
        
        As you enter the **Label** of the box, it should appear in the
        **Dialog** pane on the left under the tab you are creating.

5.  Add an element to this box. Elements are controls that accept input.
    
    1.  Click ![1862](1862.png)(**Add**), then ![1862](1862.png)(**Add a
        New Element to this Box**).
    
    2.  Enter a **Label**, **Name**, and **Description** for this
        element.
        
        <div class="important">
        
        **Name** must use only alphanumeric characters and underscores
        without spaces. It is also used to retrieve the value of this
        element in the method used with the dialog and must start with
        **dialog\_service\_type**
        
        </div>
    
    3.  Select a **Type** for an element type. All **Type** options have
        a **Required** and **Default Value** field. Check **Required**
        or set **Required** to **true** if the element is required to
        proceed. You can also specify a default value. The rest of the
        options presented are based on which type of element you select.
        
        | Element Types          | Additional Info                                                                                                                                                                                                                                        |
        | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
        | Check Box              | Check **Default Value** if you want this check box checked by default.                                                                                                                                                                                 |
        | Date Control           | Use **Date Control** to create a field where users can select a date. If you want users to be able to select a date and time, use the **Date/Time Control** option.                                                                                    |
        | Date/Time Control      | Use **Date/Time Control** to create a field where users can select a date and time. Only one **Date Control** or **Date/Time Control** element can be present in a dialog.                                                                             |
        | Drop Down Dynamic List | Use **Drop Down Dynamic List** if you want the list options to be created using automate methods. Use **Entry Point (NS/Cls/Inst)** to select an automate instance. Check **Show Refresh Button** to allow users to refresh the list options manually. |
        | Radio Button           | This element type serves the same purpose as **Drop Down List** but displays options using radio buttons.                                                                                                                                              |
        | Tag Control            | Select a **Category** of tags you want assigned to the virtual machines associated with this service dialog. Check **Single Select** if only one tag can be selected.                                                                                  |
        | Text Area Box          | Provides text area for users to enter some text. You can also leave a message to users by typing in the **Default Value** field or leave it as blank.                                                                                                  |
        | Text Box               | This element type serves the same purpose as **Text Area Box** with the option to check **Protected** so the text is shown as asterisks (\*), instead of plain text.                                                                                   |
        

6.  Continue adding the dialog items you need. You can switch between
    dialogs, tabs, boxes, and elements by selecting their respective
    labels from the **Dialog** pane on the left.

7.  Click **Add**. Your dialog should appear in the **Service Dialogs**
    accordion.

# Creating a Catalog

A catalog is a way to organize or categorize catalog items and bundles.
Before you can associate a catalog item into a catalog, create an empty
catalog first:

1.  Navigate to menu:Services\[Catalogs\].

2.  Click the **Catalogs** accordion.

3.  Click ![1847](1847.png)(**Configuration**), and then
    ![1862](1862.png)(**Add a New Catalog**).

4.  Enter a **Name** and **Description**, leaving everything else blank.

5.  Click **Add**.

## Creating a Catalog Item

Unresolved directive in catalogs-services.adoc -
include::catalog-item-creation-openstack.adoc\[\]

## Ordering a Catalog Item

1.  Navigate to menu:Services\[Catalogs\].

2.  Click the **Service Catalogs** accordion, and select the service to
    provision.

3.  Click **Order**.
