If you are performing more than 10 concurrent migrations from a VMware
hypervisor using VDDK transformation, the migration will fail because
the hypervisor’s NFC service memory buffer is limited to 10 parallel
connections. See [VMware Virtual Disk Programming Guide NFC session
connection
limits](https://code.vmware.com/docs/1674/virtual-disk-programming-guide/doc/vddkDataStruct.5.5.html#1025227)
and [Virt-v2v. VDDK: ESXi NFC service memory
limits](http://libguestfs.org/virt-v2v.1.html#vddk:-esxi-nfc-service-memory-limits)
for details.

You can increase the hypervisor’s NFC service memory to enable
additional connections for migrations.

1.  Log in to a VMware hypervisor as root.

2.  Change the value of `maxMemory` to `1000000000` in
    `/etc/vmware/hostd/config.xml`:
    
    ``` xml
    ...
          <nfcsvc>
             <path>libnfcsvc.so</path>
             <enabled>true</enabled>
             <maxMemory>1000000000</maxMemory>
             <maxStreamMemory>10485760</maxStreamMemory>
          </nfcsvc>
    ...
    ```

3.  Restart `hostd`:
    
        # /etc/init.d/hostd restart
    
    You do not need to reboot the VMware hypervisor.
