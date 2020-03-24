Copy the SSH public keys of the VMware hypervisors to the conversion
hosts.

You can collect the VMware keys either when you configure the VMware
hypervisors for SSH transformation or by using `ssh-keyscan`.

# Copying keys collected during VMware hypervisor configuration

# Copying keys collected with `ssh-keyscan`

You must run `ssh-keyscan` for **each VMware hypervisor**. Otherwise
your conversion hosts will not have all the VMware hypervisor keys and
the migration will fail.

Perform the following procedure on each conversion host:
