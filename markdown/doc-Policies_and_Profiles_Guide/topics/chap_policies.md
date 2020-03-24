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

# Control Policies

A control policy is a combination of an event, a condition, and an
action. This combination provides management capabilities in your
virtual environment.

  - An event is a trigger to check a condition.

  - A condition is a test triggered by an event.

  - An action is an execution that occurs if a condition is met.

Unresolved directive in chap\_policies.adoc -
include::To\_create\_a\_Control\_Policy.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::Editing\_Basic\_Info\_Scope\_and\_Notes\_for\_a\_Policy.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::Copying\_a\_Policy.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::Deleting\_a\_Policy.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::Creating\_a\_new\_Policy\_Condition.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::Editing\_Policy\_Condition\_Assignments.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::Editing\_Policy\_Event\_Assignments.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::To\_assign\_an\_Action\_to\_an\_Event.adoc\[\]

# Compliance Policies

Compliance policies are specifically designed to secure your environment
by checking conditions that you create. These conditions can include the
same conditions that you would use in a control policy, and most of the
procedures are the same. However, a compliance policy automatically
assigns the mark as a compliant action when the entity type (virtual
machine or host, for example) to which the policy applies passes all of
the conditions. If any of the conditions are not met, then the virtual
machine or host is marked as non-compliant. The compliance status is
shown in the summary screen for the entity type and on the compare and
drift screens.

Unresolved directive in chap\_policies.adoc -
include::To\_create\_a\_compliance\_Policy.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::To\_create\_a\_Condition\_to\_check\_file\_contents\_of\_a\_host.adoc\[\]

## Checking for Compliance

After you have created your compliance policies and assigned them to a
policy profile, you can check compliance in two ways. You can either
schedule the compliance check or perform the check directly from the
summary screen.

The compliance check runs all compliance policies that are assigned to
the host or virtual machine. If the item fails any of the checks, it is
marked as non-compliant in the item’s summary screen.

<div class="note">

To schedule, you must have `EvmRole-administrator` access to the
{product-title} server.

</div>

Unresolved directive in chap\_policies.adoc -
include::To\_schedule\_a\_Compliance\_check.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::To\_check\_a\_Virtual\_Machine\_for\_Compliance\_from\_the\_Summary\_Screen.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::To\_check\_a\_Host\_for\_Compliance\_from\_the\_Summary\_Screen.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::To\_check\_a\_Replicator\_for\_Compliance\_from\_the\_Summary\_Screen.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::To\_check\_a\_Pod\_for\_Compliance\_from\_the\_Summary\_Screen.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::To\_check\_a\_Container\_Node\_for\_Compliance\_from\_the\_Summary\_Screen.adoc\[\]

Unresolved directive in chap\_policies.adoc -
include::To\_check\_a\_Container\_Image\_for\_Compliance\_from\_the\_Summary\_Screen.adoc\[\]
