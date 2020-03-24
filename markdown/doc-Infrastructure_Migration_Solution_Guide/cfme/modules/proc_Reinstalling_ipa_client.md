If you are using SSH transformation and configuring your Red Hat
Virtualization (RHV) conversion hosts for SSSD with single sign-on, you
must reinstall the `ipa-client` in the RHV Manager without the OpenSSH
client.

Otherwise, SSH fails for the vdsm user. See [BZ\#1544379:
ipa-client-install changes system-wide SSH
configuration](https://bugzilla.redhat.com/show_bug.cgi?id=1544379) for
more information.

This issue cannot be resolved by modifying the configuration file
because the file is restored during upgrades.

1.  Log in to the RHV Manager machine using SSH.

2.  Uninstall `ipa-client`:
    
        # ipa-client-install --uninstall

3.  Reinstall `ipa-client` without OpenSSH:
    
        # ipa-client-install --no-ssh
