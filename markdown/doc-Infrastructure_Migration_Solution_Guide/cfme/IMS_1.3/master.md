The Red Hat Infrastructure Migration Solution enables you to migrate
virtual machines from VMware 6.0, or later, to Red Hat Virtualization or
Red Hat OpenStack Platform, using Red Hat CloudForms.

  - Red Hat Virtualization 4.3  
    Red Hat Virtualization (RHV) provides a virtualization platform
    built on Red Hat Enterprise Linux. You can manage your virtual
    infrastructure, including hosts, virtual machines, networks,
    storage, and users, from a centralized graphical user interface or
    with a REST API. See
    [RHV](https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.3/)
    documentation for more information.

  - Red Hat OpenStack Platform 13 or later  
    Red Hat OpenStack Platform (RHOSP) provides a scalable,
    fault-tolerant, private or public cloud based on Red Hat Enterprise
    Linux. See
    [RHOSP](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform)
    documentation for more information.

  - Red Hat CloudForms 5.0  
    Red Hat CloudForms is the environment in which you perform the
    migration. CloudForms is a unified set of management tools for use
    across virtualized, private cloud, and public cloud platforms. See
    [CloudForms](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/5.0)
    documentation for more information.

# Migrating from VMware to Red Hat Virtualization

This guide describes how to plan your migration, to prepare the VMware
and Red Hat Virtualization environments, and to migrate your VMware
virtual machines.

## Understanding the migration

Unresolved directive in master.adoc -
include::modules/con\_Migration\_workflow.adoc\[leveloffset=+2\]

Unresolved directive in master.adoc -
include::modules/con\_Migration\_network\_requirements.adoc\[leveloffset=+2\]

## Planning the migration

This section provides guidelines for planning your migration.

Unresolved directive in master.adoc -
include::modules/ref\_Questions\_to\_ask\_before\_migration.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/ref\_Optimizing\_your\_migration.adoc\[leveloffset=+2\]

## Preparing the migration environment

You can prepare the VMware and Red Hat environments for migration.

Unresolved directive in master.adoc -
include::modules/ref\_Software\_compatibility.adoc\[leveloffset=+2\]

### Preparing the VMware environment

You can prepare the VMware network and virtual machines for migration.

If you are performing more than ten concurrent migrations from a single
VMware hypervisor, you must configure the hypervisor.

Unresolved directive in master.adoc -
include::modules/proc\_Preparing\_the\_vmware\_network.adoc\[leveloffset=+3\]

<div class="note">

See [???](#Migration_network_requirements_rhv_1-3_vddk) for firewall
rules.

</div>

Unresolved directive in master.adoc -
include::modules/proc\_Preparing\_the\_vmware\_virtual\_machines.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_vmware\_hypervisor\_for\_more\_than\_10\_concurrent\_vddk\_migrations.adoc\[leveloffset=+3\]

### Preparing the Red Hat environment

You can install and configure Red Hat Virtualization (RHV) and
CloudForms for migration.

Unresolved directive in master.adoc -
include::modules/proc\_Installing\_configuring\_rhv.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Installing\_configuring\_cf.adoc\[leveloffset=+3\]

#### Deploying the Red Hat Virtualization conversion hosts

You can configure the Red Hat Virtualization conversion hosts to use the
VMware Virtual Disk Development Kit (VDDK) in the CloudForms user
interface. VDDK converts the VMware disks.

Unresolved directive in master.adoc -
include::modules/proc\_Downloading\_conversion\_host\_image.adoc\[leveloffset=+4\]
Unresolved directive in master.adoc -
include::modules/proc\_Creating\_rhv\_conversion\_host\_with\_uci.adoc\[leveloffset=+4\]
Unresolved directive in master.adoc -
include::modules/proc\_Downloading\_vddk.adoc\[leveloffset=+4\]
Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_conversion\_hosts\_cloudforms.adoc\[leveloffset=+4\]
Unresolved directive in master.adoc -
include::modules/proc\_Verifying\_conversion\_hosts\_in\_browser.adoc\[leveloffset=+4\]

## Migrating the virtual machines

You can create an infrastructure mapping and create and run a migration
plan in the CloudForms user interface.

Optionally, you can [change the maximum number of concurrent migrations
for conversion hosts or
providers](#Changing_the_maximum_number_of_concurrent_migrations_rhv_1-3_vddk)
to control the migration process.

### Migration prerequisites

Check your migration for the following conditions, which have
prerequisites:

  - If you are migrating previously migrated virtual machines, you must
    [add previously migrated machines to the migration plan with a CSV
    file](#Creating_a_csv_file_to_add_virtual_machines_to_the_migration_plan_rhv_1-3_vddk).
    A CSV file is also recommended for large migrations.

  - If you are using Ansible playbooks for premigration/postmigration
    tasks, you must [create an Ansible repository and add credentials
    and playbooks to
    CloudForms](#Adding_ansible_playbooks_to_cloudforms_rhv_1-3_vddk).

  - If you are migrating virtual machines running RHEL or other Linux
    operating system, you must [create a RHEL premigration
    playbook](#Creating_a_rhel_premigration_playbook_rhv_1-3_vddk) to
    preserve IP addresses. You will select this playbook when you create
    a migration plan.

Unresolved directive in master.adoc -
include::modules/proc\_Creating\_a\_csv\_file\_to\_add\_virtual\_machines\_to\_the\_migration\_plan.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Adding\_ansible\_playbooks\_to\_cloudforms.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Creating\_a\_rhel\_premigration\_playbook.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Creating\_an\_infrastructure\_mapping.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Creating\_a\_migration\_plan\_in\_cloudforms.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Changing\_the\_maximum\_number\_of\_concurrent\_migrations.adoc\[leveloffset=+2\]

## Troubleshooting

You can review the migration logs, check common issues and mistakes, and
known issues to troubleshoot a migration error.

Unresolved directive in master.adoc -
include::modules/ref\_Migration\_logs.adoc\[leveloffset=+2\]

### Common issues and mistakes

Unresolved directive in master.adoc -
include::modules/ref\_Infrastructure\_mapping\_errors.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/ref\_Migration\_plan\_errors.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/ref\_Ip\_address\_errors.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/ref\_Environment\_configuration\_errors.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/ref\_Known\_issues.adoc\[leveloffset=+2\]
:rhv\_1-3\_vddk\!:

# Configuring the Red Hat Virtualization environment for SSH transformation

You can configure your Red Hat Virtualization environment for SSH
transformation if you cannot use VDDK.

<div class="note">

The default transformation method, VDDK, is much faster than SSH.

</div>

This configuration involves adding the following steps to [Preparing the
migration
environment](#Preparing_the_migration_environment_rhv_1-3_vddk):

<table>
<caption>Additional configuration for SSH transformation</caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Section</th>
<th>Additional configuration for SSH transformation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>After <a href="#Preparing_the_vmware_environment_rhv_1-3_vddk">Preparing the VMware environment</a></p></td>
<td><p>Go to:</p>
<ul>
<li><p><a href="#Configuring_the_vmware_hypervisors_for_ssh_transformation_rhv_1-3_ssh">???</a></p></li>
</ul>
<p>You can collect the SSH keys from the hypervisors at this time, if your security policies allow.</p>
<p>The private key of the SSH key pair that is generated in this step will be used in <a href="#Configuring_conversion_hosts_cloudforms_rhv_1-3_ssh">???</a>.</p></td>
</tr>
<tr class="even">
<td><p>After <a href="#Installing_configuring_rhv_rhv_1-3_vddk">???</a></p></td>
<td><p>If the conversion hosts are using SSSD with single sign-on, go to:</p>
<p>* <a href="#Reinstalling_ipa_client_rhv_1-3_ssh">???</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Create the RHV conversion hosts. Instead of <a href="#Configuring_conversion_hosts_cloudforms_rhv_1-3_vddk">???</a></p></td>
<td><p>Go to:</p>
<ul>
<li><p><a href="#Configuring_conversion_hosts_cloudforms_rhv_1-3_ssh">???</a></p></li>
<li><p><a href="#Copying_vmware_ssh_keys_to_conversion_hosts_rhv_1-3_ssh">???</a></p></li>
</ul></td>
</tr>
</tbody>
</table>

Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_the\_vmware\_hypervisors\_for\_ssh\_transformation.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Reinstalling\_ipa\_client.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_conversion\_hosts\_cloudforms.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Copying\_the\_vmware\_keys\_to\_the\_conversion\_hosts.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_secure\_remote\_login\_to\_the\_vmware\_hypervisors.adoc\[leveloffset=+2\]
:\!rhv\_1-3\_ssh:

# Migrating from VMware to Red Hat OpenStack Platform

This guide describes how to plan your migration, to prepare the VMware
and Red Hat OpenStack Platform environments, and to migrate your VMware
virtual machines.

## Understanding the migration

Unresolved directive in master.adoc -
include::modules/con\_Migration\_workflow.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/con\_Migration\_network\_requirements.adoc\[leveloffset=+2\]

## Planning the migration

This section provides guidelines for planning your migration.

Unresolved directive in master.adoc -
include::modules/ref\_Questions\_to\_ask\_before\_migration.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/ref\_Optimizing\_your\_migration.adoc\[leveloffset=+2\]

## Preparing the migration environment

You can prepare the VMware and Red Hat environments for migration.

Unresolved directive in master.adoc -
include::modules/ref\_Software\_compatibility.adoc\[leveloffset=+2\]

### Preparing the VMware environment

You can prepare the VMware network and virtual machines for migration.

If you are performing more than ten concurrent migrations from a single
VMware hypervisor, you must configure the hypervisor.

Unresolved directive in master.adoc -
include::modules/proc\_Preparing\_the\_vmware\_network.adoc\[leveloffset=+3\]

<div class="note">

See [???](#Migration_network_requirements_osp_1-3_vddk) for firewall
rules.

</div>

Unresolved directive in master.adoc -
include::modules/proc\_Preparing\_the\_vmware\_virtual\_machines.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_vmware\_hypervisor\_for\_more\_than\_10\_concurrent\_vddk\_migrations.adoc\[leveloffset=+3\]

### Preparing the Red Hat environment

You can install and configure Red Hat OpenStack Platform and CloudForms
for migration.

Unresolved directive in master.adoc -
include::modules/proc\_Installing\_osp.adoc\[leveloffset=+3\] Unresolved
directive in master.adoc -
include::modules/proc\_Installing\_configuring\_cf.adoc\[leveloffset=+3\]

#### Deploying the Red Hat OpenStack Platform conversion hosts

You can configure the Red Hat OpenStack Platform conversion hosts to use
the VMware Virtual Disk Development Kit (VDDK) in the CloudForms user
interface. VDDK converts the VMware disks.

Unresolved directive in master.adoc -
include::modules/proc\_Downloading\_conversion\_host\_image.adoc\[leveloffset=+4\]
Unresolved directive in master.adoc -
include::modules/proc\_Creating\_osp\_conversion\_hosts.adoc\[leveloffset=+4\]
Unresolved directive in master.adoc -
include::modules/proc\_Downloading\_vddk.adoc\[leveloffset=+4\]
Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_conversion\_hosts\_cloudforms.adoc\[leveloffset=+4\]
Unresolved directive in master.adoc -
include::modules/proc\_Verifying\_conversion\_hosts\_in\_browser.adoc\[leveloffset=+4\]

## Migrating the virtual machines

You can create an infrastructure mapping and create and run a migration
plan in the CloudForms user interface.

Optionally, you can [change the maximum number of concurrent migrations
for conversion hosts or
providers](#Changing_the_maximum_number_of_concurrent_migrations_osp_1-3_vddk)
to control the migration process.

### Migration prerequisites

Check your migration for the following conditions, which have
prerequisites:

  - If you are migrating previously migrated virtual machines, you must
    [add previously migrated machines to the migration plan with a CSV
    file](#Creating_a_csv_file_to_add_virtual_machines_to_the_migration_plan_osp_1-3_vddk).
    A CSV file is also recommended for large migrations.

  - If you are using Ansible playbooks for premigration/postmigration
    tasks, you must [create an Ansible repository and add credentials
    and playbooks to
    CloudForms](#Adding_ansible_playbooks_to_cloudforms_osp_1-3_vddk).

  - If you are migrating virtual machines running RHEL or other Linux
    operating system, you must [create a RHEL premigration
    playbook](#Creating_a_rhel_premigration_playbook_osp_1-3_vddk) to
    preserve IP addresses and select this playbook when you create a
    migration plan.

Unresolved directive in master.adoc -
include::modules/proc\_Creating\_a\_csv\_file\_to\_add\_virtual\_machines\_to\_the\_migration\_plan.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Adding\_ansible\_playbooks\_to\_cloudforms.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Creating\_a\_rhel\_premigration\_playbook.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/proc\_Creating\_an\_infrastructure\_mapping.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Creating\_a\_migration\_plan\_in\_cloudforms.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Changing\_the\_maximum\_number\_of\_concurrent\_migrations.adoc\[leveloffset=+2\]

## Troubleshooting

You can review the migration logs, check common issues and mistakes, and
known issues.

Unresolved directive in master.adoc -
include::modules/ref\_Migration\_logs.adoc\[leveloffset=+2\]

### Common issues and mistakes

Unresolved directive in master.adoc -
include::modules/ref\_Infrastructure\_mapping\_errors.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/ref\_Migration\_plan\_errors.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/ref\_Ip\_address\_errors.adoc\[leveloffset=+3\]
Unresolved directive in master.adoc -
include::modules/ref\_Environment\_configuration\_errors.adoc\[leveloffset=+3\]

Unresolved directive in master.adoc -
include::modules/ref\_Known\_issues.adoc\[leveloffset=+2\]

# Configuring the Red Hat OpenStack Platform environment for SSH transformation

You can configure your environment for SSH transformation if you cannot
use VDDK.

<div class="note">

The default transformation method, VDDK, is much faster than SSH.

</div>

This configuration involves adding the following steps to [Preparing the
migration
environment](#Preparing_the_migration_environment_osp_1-3_vddk):

<table>
<caption>Additional configuration for SSH transformation</caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Section</th>
<th>Additional configuration for SSH transformation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>After <a href="#Preparing_the_vmware_environment_osp_1-3_vddk">Preparing the VMware environment</a></p></td>
<td><p>Go to:</p>
<ul>
<li><p><a href="#Configuring_the_vmware_hypervisors_for_ssh_transformation_osp_1-3_ssh">???</a></p></li>
</ul>
<p>You can collect the SSH keys from the hypervisors at this time, if your security policies allow.</p>
<p>The private key of the SSH key pair that is generated in this step will be used in <a href="#Configuring_conversion_hosts_cloudforms_osp_1-3_ssh">???</a>.</p></td>
</tr>
<tr class="even">
<td><p>Create the conversion hosts. Instead of <a href="#Configuring_conversion_hosts_cloudforms_osp_1-3_vddk">???</a></p></td>
<td><p>Go to:</p>
<ul>
<li><p><a href="#Configuring_conversion_hosts_cloudforms_osp_1-3_ssh">???</a></p></li>
<li><p><a href="#Copying_vmware_ssh_keys_to_conversion_hosts_osp_1-3_ssh">???</a></p></li>
</ul></td>
</tr>
</tbody>
</table>

Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_the\_vmware\_hypervisors\_for\_ssh\_transformation.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Configuring\_conversion\_hosts\_cloudforms.adoc\[leveloffset=+2\]
Unresolved directive in master.adoc -
include::modules/proc\_Copying\_the\_vmware\_keys\_to\_the\_conversion\_hosts.adoc\[leveloffset=+2\]
:osp\_1-3\_ssh\!:
