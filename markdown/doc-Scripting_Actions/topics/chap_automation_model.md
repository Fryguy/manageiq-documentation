# Understanding the Automate Model

Automate enables real-time, bi-directional process integration. This
provides users with a method to implement adaptive automation for
management events and administrative or operational activities.

Unresolved directive in chap\_automation\_model.adoc -
include::Automate\_Model2.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Creating\_a\_Domain.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Editing\_a\_Domain.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Deleting\_a\_Domain.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Importing\_a\_Domain.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Changing\_Priority\_Order\_of\_Domains.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Creating\_a\_Namespace.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::To\_create\_a\_class1.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::To\_create\_a\_schema\_for\_a\_class1.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::To\_edit\_a\_field\_in\_a\_schema1.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Editing\_Schema\_Sequence.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::To\_add\_an\_instance\_to\_a\_class1.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Copying\_a\_Class\_or\_Instance.adoc\[\]

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
a task. {product-title} allows for Ruby methods or backing a method
using an Ansible playbook. You can create your own methods or use
relationships to link to pre-existing ones.

{product-title} ships with a core set of Ruby gems used by the
{product-title} Rails Application. The Ruby gems in this set are subject
to change. If you are calling gems using Automate that are no longer in
this release, you can install them by using the `gem install` command.

While gems can be imported into automation methods using `require`, it
is recommended that the authors of the automation methods clearly
document the use of gems either in the core set or a custom set. It is
the responsibility of the author of such custom automation to own the
life cycle of any gem being referenced in those methods.

The Release Notes list Ruby gems that have been added, updated, or
removed in the latest version of {product-title}.

Unresolved directive in chap\_automation\_model.adoc -
include::To\_create\_a\_method1.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Creating\_a\_Dynamic\_Content\_Dialog.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Ansible\_method.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::Expression\_method\_overview.adoc\[\]

## Simulation

After your model is designed, use the simulate page to test it. It
allows you to see the results in tree and XML view.

Unresolved directive in chap\_automation\_model.adoc -
include::To\_simulate\_an\_Automate\_Model1.adoc\[\]

## Importing, Exporting, and Resetting the Datastore

The **Automate Model** can be exported and imported as a YAML file.
{product-title} allows you to back up your model by export. Red Hat may
provide you with new or updated classes, and provides an import function
for either a class or the entire model. Finally, you can reset the
datastore to its default. Always be sure to export the current datastore
before importing or resetting.

<div class="note">

The datastores you are exporting or importing between must use the same
{product-title\_short} version.

</div>

Unresolved directive in chap\_automation\_model.adoc -
include::To\_export\_all\_Classes\_classes1.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::To\_import\_Datastore\_classes1.adoc\[\]

Unresolved directive in chap\_automation\_model.adoc -
include::To\_reset\_the\_Datastore\_to\_the\_default1.adoc\[\]
