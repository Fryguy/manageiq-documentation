Migration Analytics examines your VMware virtual machines and collects
data about their operating systems and workloads, using the [Red Hat
CloudForms](https://access.redhat.com/documentation/en-us/red_hat_cloudforms)
user interface.

Migration Analytics supports VMware version 6.0 (and later).

You then use the Migration Analytics service at
<https://cloud.redhat.com/beta> to analyze the data and create a report.
This report provides an estimate of the initial savings in migrating to
Red Hat, a detailed analysis of the VMware virtual machines, and
recommendations to help you plan your migration.

<div class="note">

Migration Analytics is available as a technology preview for Red Hat
CloudForms 5.0. For more information on the support scope for features
marked as technology previews, see [Technology Preview Features Support
Scope](https://access.redhat.com/support/offerings/techpreview/).

</div>

# Understanding Migration Analytics

You can scan your VMware virtual machines in CloudForms and create a
report with the [Migration Analytics
service](https://cloud.redhat.com/beta).

Unresolved directive in master.adoc -
include::modules/Migration-analytics-workflow.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/Migration-analytics-report.adoc\[leveloffset=+2\]

# Deploying Migration Analytics

You can deploy Migration Analytics by installing CloudForms on VMware,
adding the VMware provider, and configuring CloudForms.

Unresolved directive in master.adoc -
include::modules/Installing-cloudforms.adoc\[leveloffset=+2\] Unresolved
directive in master.adoc -
include::modules/Adding-provider-to-cloudforms.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/Assigning\_control\_policy\_to\_provider.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/Configuring-cloudforms.adoc\[leveloffset=+2\]

# Managing analysis profiles

A `default` analysis profile is used for scanning your VMware virtual
machines.

You can create a custom analysis profile by modifying the
`custom_profile.yaml` template in [???](#Custom-profile-yaml-example).

You can export existing analysis profiles for backup, troubleshooting,
or updates.

Unresolved directive in master.adoc -
include::modules/Creating-a-default-analysis-profile.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/Creating-a-custom-analysis-profile.adoc\[leveloffset=+2\]

<div class="note">

See [???](#Custom-profile-yaml-example) for the template.

</div>

Unresolved directive in master.adoc -
include::modules/Exporting-analysis-profiles.adoc\[leveloffset=+2\]

# Collecting data for Migration Analytics

You can scan your VMware virtual machines and download the results as an
inventory data file to your local machine.

Optionally, you can combine multiple inventory data files into a single
file in order to generate a single Migration Analytics report.

Unresolved directive in master.adoc -
include::modules/Scanning-vms-for-migration-analytics.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/Collecting-inventory-data.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/Combining-inventory-data-files.adoc\[leveloffset=+2\]

# Creating and filtering a Migration Analytics report

You can create a Migration Analytics report, filter the results, and
export the data.

Unresolved directive in master.adoc -
include::modules/Creating-migration-analytics-report.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/Filtering-migration-analytics-report.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/Exporting-migration-analytics-report.adoc\[leveloffset=+2\]

Unresolved directive in master.adoc -
include::modules/Custom\_profile\_yaml\_example.adoc\[leveloffset=+1\]
