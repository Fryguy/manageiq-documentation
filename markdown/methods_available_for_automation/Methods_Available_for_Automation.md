**Abstract.**

This guide provides advanced methods for {product-title}'s automation
functions. Methods can be used from within {product-title} to create
custom actions and workflows for the object’s managed by
{product-title}. Information and procedures in this book are relevant to
{product-title} administrators. This document is organized by the object
hierarchy in the Automate Model.

# Terminology

  - Account Role  
    A designation assigned to a user allowing or restricting a user to
    parts and functions of the {product-title} console.

  - Action  
    An execution that is performed after a condition is evaluated.

  - Alert  
    {product-title} alerts notify administrators and monitoring systems
    of critical configuration changes and threshold limits in the
    virtual environment. The notification can take the form of either an
    email or an SNMP trap.

  - Analysis Profile  
    A customized scan of hosts, virtual machines, or instances. You can
    collect information from categories, files, event logs, and registry
    entries.

  - Cloud  
    A pool of on-demand and highly available computing resources. The
    usage of these resources are scaled depending on the user
    requirements and metered for cost.

  - {product-title} Appliance  
    A virtual machine on which the virtual management database (VMDB)
    and {product-title} server reside.

  - {product-title} Console  
    A web-based interface into the {product-title} Appliance.

  - {product-title} Role  
    A designation assigned to a {product-title} server that defines what
    a {product-title} server can do.

  - {product-title} Server  
    The application that runs on the {product-title} Appliance and
    communicates with the SmartProxy and the VMDB.

  - Cluster  
    Hosts that are grouped together to provide high availability and
    load balancing.

  - Condition  
    A test of criteria triggered by an event.

  - Discovery  
    Process run by the {product-title} server which finds virtual
    machine and cloud providers.

  - Drift  
    The comparison of a virtual machine, instance, host, cluster to
    itself at different points in time.

  - Event  
    A trigger to check a condition.

  - Event Monitor  
    Software on the {product-title} Appliance which monitors external
    providers for events and sends them to the {product-title} server.

  - Host  
    A computer on which virtual machine monitor software is loaded.

  - Instance/Cloud Instance  
    A on-demand virtual machine based upon a predefined image and uses a
    scalable set of hardware resources such as CPU, memory, networking
    interfaces.

  - Managed/Registered VM  
    A virtual machine that is connected to a host and exists in the
    VMDB. Also, a template that is connected to a provider and exists in
    the VMDB. Note that templates cannot be connected to a host.

  - Managed/Unregistered VM  
    A virtual machine or template that resides on a repository or is no
    longer connected to a provider or host and exists in the VMDB. A
    virtual machine that was previously considered registered may become
    unregistered if the virtual machine was removed from provider
    inventory.

  - Provider  
    A computer on which software is loaded which manages multiple
    virtual machines that reside on multiple hosts.

  - Policy  
    A combination of an event, a condition, and an action used to manage
    a virtual machine.

  - Policy Profile  
    A set of policies.

  - Refresh  
    A process run by the {product-title} server which checks for
    relationships of the provider or host to other resources, such as
    storage locations, repositories, virtual machines, or instances. It
    also checks the power states of those resources.

  - Regions  
    Regions are used to create a central database for reporting and
    charting. Regions are used primarily to consolidate multiple VMDBs
    into one master VMDB for reporting.

  - Resource  
    A host, provider, instance, virtual machine, repository, or
    datastore.

  - Resource Pool  
    A group of virtual machines across which CPU and memory resources
    are allocated.

  - Repository  
    A place on a datastore resource which contains virtual machines.

  - SmartProxy  
    The SmartProxy is a software agent that acts on behalf of the
    {product-title} Appliance to perform actions on hosts, providers,
    storage and virtual machines. + The SmartProxy can be configured to
    reside on the {product-title} Appliance or on an ESX server version.
    The SmartProxy can be deployed from the {product-title} Appliance,
    and provides visibility to the VMFS storage. Each storage location
    must have a SmartProxy with visibility to it. The SmartProxy acts on
    behalf of the {product-title} Appliance. If the SmartProxy is not
    embedded in the {product-title} server, it communicates with the
    {product-title} Appliance over HTTPS on standard port 443.

  - SmartState Analysis  
    Process run by the SmartProxy which collects the details of a
    virtual machine or instance. Such details include accounts, drivers,
    network information, hardware, and security patches. This process is
    also run by the {product-title} server on hosts and clusters. The
    data is stored in the VMDB.

  - SmartTags  
    Descriptors that allow you to create a customized, searchable index
    for the resources in your clouds and infrastructure.

  - Storage Location  
    A device, such as a VMware datastore, where digital information
    resides that is connected to a resource.

  - Tags  
    Descriptive terms defined by a {product-title} user or the system
    used to categorize a resource.

  - Template  
    A template is a copy of a preconfigured virtual machine, designed to
    capture installed software and software configurations, as well as
    the hardware configuration, of the original virtual machine.

  - Unmanaged Virtual Machine  
    Files discovered on a datastore that do not have a virtual machine
    associated with them in the VMDB. These files may be registered to a
    provider that the {product-title} server does not have configuration
    information on. Possible causes may be that the provider has not
    been discovered or that the provider has been discovered, but no
    security credentials have been provided.

  - Virtual Machine  
    A software implementation of a system that functions similar to a
    physical machine. Virtual machines utilize the hardware
    infrastructure of a physical host, or a set of physical hosts, to
    provide a scalable and on-demand method of system provisioning.

  - Virtual Management Database (VMDB)  
    Database used by the {product-title} Appliance to store information
    about your resources, users, and anything else required to manage
    your virtual enterprise.

  - Virtual Thumbnail  
    An icon divided into smaller areas that summarize the properties of
    a resource.

  - Zones  
    {product-title} Infrastructure can be organized into zones to
    configure failover and to isolate traffic. Zones can be created
    based on your environment. Zones can be based on geographic
    location, network location, or function. When first started, new
    servers are put into the default zone.

# Methods Available for Use with {product-title}

Methods can be used from within {product-title} to create custom actions
and workflows for the objects managed for your {product-title}
Infrastructure. This document describes the methods available for use in
{product-title}. This document is organized by the object hierarchy in
the Automate Model.

## $evm.root

When an Automate method is launched, it has one global variable: `$evm`.
The `$evm` variable allows the method to communicate back to
{product-title}. The `$evm.root` is the root object in the workspace, it
provides access to the data currently loaded in the {product-title}
model. It use the object’s data to solve more complex problems by
integrating with {product-title} methods.

The following is an excerpt from the **InspectMe** method that can be
found in the **ManageIQ\\System\\Request** namespace. The dumpRoot
method accesses the `$evm.root` object, and sends all of its attributes
to the {product-title} Automate log for review. In the dumpServer
Method, the inspect method is run based on the value of the miq\_server
obtained from the `$evm.root` object.

``` ruby
   #########################
   #
   # Method: dumpRoot
   # Description: Dump Root information
   #
   ##########################
   def dumpRoot
     $evm.log("info", "#{@log_prefix} - Root:<$evm.root> Begin Attributes")
     $evm.root.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - Root:<$evm.root> Attributes - #{k}: #{v}")}
     $evm.log("info", "#{@log_prefix} - Root:<$evm.root> End Attributes")
     $evm.log("info", "")
   end

   #########################
   #
   # Method: dumpServer
   # Inputs: $evm.root['miq_server']
   # Description: Dump MIQ Server information
   #
   ##########################
   def dumpServer
     $evm.log("info","#{@log_prefix} - Server:<#{$evm.root['miq_server'].name}> Begin Attributes")
     $evm.root['miq_server'].attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - Server:<#{$evm.root['miq_server'].name}> Attributes - #{k}: #{v.inspect}")}
     $evm.log("info","#{@log_prefix} - Server:<#{$evm.root['miq_server'].name}> End Attributes")
     $evm.log("info", "")
   end
```

The result of dumpRoot is below. The value of miq\_server is what gets
passed into the dumpServer method.

    [----] I, [2012-10-23T13:53:54.517279 #5320:f329024]  INFO -- : <User-Defined Method> [InspectMe] - EVM Automate Method Started
    [----] I, [2012-10-23T13:53:54.523637 #5320:f329024]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> Begin Attributes
    [----] I, [2012-10-23T13:53:54.527552 #5320:ef8c538]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> Attributes - miq_server: #<MiqAeMethodService::MiqAeServiceMiqServer:0x0000001e76d900>
    [----] I, [2012-10-23T13:53:54.528801 #5320:ef8c538]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> Attributes - miq_server_id: 1
    [----] I, [2012-10-23T13:53:54.529961 #5320:ef8c538]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> Attributes - object_name: Request
    [----] I, [2012-10-23T13:53:54.531067 #5320:ef8c538]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> Attributes - request: inspectme
    [----] I, [2012-10-23T13:53:54.534054 #5320:ef8c538]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> Attributes - vm: DEV-JaneM
    [----] I, [2012-10-23T13:53:54.535156 #5320:ef8c538]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> Attributes - vm_id: 85
    [----] I, [2012-10-23T13:53:54.536238 #5320:ef8c538]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> Attributes - vmdb_object_type: vm
    [----] I, [2012-10-23T13:53:54.537159 #5320:f329024]  INFO -- : <User-Defined Method> [InspectMe] - Root:<$evm.root> End Attributes
    [----] I, [2012-10-23T13:53:54.537772 #5320:f329024]  INFO -- : <User-Defined Method>

## Method Hierarchy

The Automate Model inline methods have a hierarchy. The sublevels in the
hierarchy have access to the methods for itself and the levels above it.
For example, Red Hat Hosts have access to the Red Hat Host methods, Host
Methods, and Base Methods.

The following nested list displays the hierarchy. Certain methods in
this list have links to additional methods detailed in this book.
Methods without links do not have any additional methods.

  - Top Level: Base - [Base Methods](#base-methods)
    
      - Authentication (authentication)
        
          - Private Keys (auth\_private\_key)
            
              - Key Pair for Clouds (auth\_key\_pair\_cloud)
                
                  - Amazon (auth\_key\_pair\_amazon)
                
                  - OpenStack (auth\_key\_pair\_openstack)
    
      - Availability Zones (availability\_zone) - [Availability Zones
        (availability\_zone)](#availability_zone)
        
          - Amazon (availability\_zone\_amazon)
        
          - OpenStack (availability\_zone\_openstack)
    
      - Classification (classification) - [Classifications
        (classification)](#classification)
    
      - Cloud Networks (cloud\_network) - [Cloud Networks
        (cloud\_network)](#cloud_network)
    
      - Cloud Resource Quotas (cloud\_resource\_quota) - [Cloud Resource
        Quotas (cloud\_resource\_quota)](#cloud_resource_quota)
        
          - OpenStack (openstack\_resource\_quota)
    
      - Cloud Subnets (cloud\_subnet) - [Cloud Subnets
        (cloud\_subnet)](#cloud_subnet)
    
      - Cloud Tenants (cloud\_tenant) - [Cloud Tenants
        (cloud\_tenant)](#cloud_tenant)
    
      - Customization Templates (customization\_template) -
        [Customization Template
        (customization\_template)](#customization_template)
        
          - Cloud Init (customization\_template\_cloud\_init)
        
          - Kickstart (customization\_template\_kickstart)
        
          - Sysprep (customization\_template\_sysprep)
    
      - Cluster (ems\_cluster) - [Clusters (ems\_cluster)](#ems_cluster)
    
      - Event (ems\_event) - [Management System Events
        (ems\_event)](#ems_event)
    
      - Folder (ems\_folder) - [Management System Folders
        (ems\_folder)](#ems_folder)
    
      - Providers (ext\_management\_system) - [Providers
        (ext\_management\_system)](#ext_management_system)
        
          - Cloud (ems\_cloud)
            
              - Amazon (ems\_amazon)
            
              - Openstack (ems\_openstack)
        
          - Infrastructure (ems\_infra)
            
              - Microsoft System Center VMM (ems\_microsoft)
            
              - Red Hat Enterprise Virtualization (ems\_redhat)
            
              - VMware vCenter (ems\_vmware)
    
      - Filesystems (filesystem)
    
      - Firewall Rules (filewall\_rule) - [Firewall Rules
        (firewall\_rule)](#firewall_rule)
    
      - Flavors - [Flavors (flavor)](#flavor)
        
          - Amazon (flavor\_amazon)
        
          - OpenStack (flavor\_openstack)
    
      - Floating IPs (floating\_ip) - [Floating IPs
        (floating\_ip)](#floating_ip)
        
          - Amazon (floating\_ip\_amazon)
        
          - OpenStack (floating\_ip\_openstack)
    
      - Guest Applications (guest\_application) - [Guest Applications
        (guest\_application)](#guest_application)
    
      - Guest Devices (guest\_device) - [Guest Device
        (guest\_device)](#guest_device)
    
      - Hardware (hardware) - [Hardware (hardware)](#hardware)
    
      - Hosts (host) - [Hosts (host)](#host)
        
          - Red Hat Enterprise Virtualization (host\_redhat)
        
          - VMware (host\_vmware)
            
              - VMware ESX (host\_vmware\_esx) - [Hosts: Vmware ESX
                (host\_vmware\_esx)](#host_vmware_esx)
    
      - ISO Images (iso\_image)
    
      - Jobs (job)
    
      - LANs (lan) - [LAN (lan)](#lan)
    
      - Groups (miq\_group) - [Groups (miq\_group)](#miq_group)
    
      - Policies (miq\_policy)
    
      - Proxies (miq\_proxy) - [Proxies (miq\_proxy)](#miq_proxy)
    
      - Requests (miq\_request) - [Request (miq\_request)](#miq_request)
        
          - Automation (automation\_request) - [Automation Request
            (automation\_request)](#automation_request)
        
          - Host Provisioning (miq\_host\_provision\_request) - [Host
            Provision Request
            (miq\_host\_provision\_request)](#miq_host_provision_request)
        
          - VM Provisioning (miq\_provision\_request) - [VM Provision
            Request (miq\_provision\_request)](#miq_provision_request)
            
              - VM Templates (miq\_provision\_request\_template)
        
          - Service Reconfiguration (service\_reconfigure\_request)
        
          - Service Template Provisioning
            (service\_template\_provision\_request)
        
          - VM Migration (vm\_migrate\_request)
        
          - VM Reconfiguration (vm\_reconfigure\_request)
    
      - Request Task (miq\_request\_task) - [Request Task
        (miq\_request\_task)](#miq_request_task)
        
          - Automation (automation\_task) - [Automation Task
            (automation\_task)](#automation_task)
        
          - Host Provisioning (miq\_host\_provision) - [Host Provision
            Task (miq\_host\_provision)](#miq_host_provision)
        
          - VM Provisioning (miq\_provision) - [VM Provision Task
            (miq\_provision)](#miq_provision)
            
              - Cloud (miq\_provision\_cloud) - [VM Provisioning for
                Clouds Task
                (miq\_provision\_cloud)](#miq_provision_cloud)
                
                  - Amazon (miq\_provision\_amazon)
                
                  - OpenStack (miq\_provision\_openstack)
            
              - Red Hat Enterprise Virtualization
                (miq\_provision\_redhat)
                
                  - Via ISO (miq\_provision\_redhat\_via\_iso)
                
                  - Via PXE (miq\_provision\_redhat\_via\_pxe)
            
              - VMware (miq\_provision\_vmware)
                
                  - Via NetApp RCU
                    (miq\_provision\_vmware\_via\_net\_app\_rcu)
                
                  - Via PXE (miq\_provision\_vmware\_via\_pxe)
        
          - Service Reconfiguration (service\_reconfigure\_task) -
            [Service Reconfiguration Task
            (service\_reconfigure\_task)](#service_reconfigure_task)
        
          - Service Template Provisioning
            (service\_template\_provision\_task) - [Service Template
            Provision Task
            (service\_template\_provision\_task)](#service_template_provision_task)
        
          - VM Migratation (vm\_migrate\_task) - [VM Migrate Task
            (vm\_migrate\_task)](#vm_migrate_task)
        
          - VM Reconfiguration (vm\_reconfigure\_task)
    
      - Servers (miq\_server) - [Servers (miq\_server)](#miq_server)
    
      - Networks (network) - [Network (network)](#network)
    
      - Operating Systems (operating\_system)
    
      - PXE Images (pxe\_image) - [PXE Image (pxe\_image)](#pxe_image)
        
          - iPXE (pxe\_image\_ipxe)
        
          - PXELINUX (pxe\_image\_pxelinux)
    
      - PXE Servers (pxe\_server) - [PXE Server
        (pxe\_server)](#pxe_server)
    
      - Resource Pools (resource\_pool)
    
      - Security Groups (security\_group) - [Security Groups
        (security\_group)](#security_group)
        
          - Amazon (security\_group\_amazon)
        
          - OpenStack (security\_group\_openstack)
    
      - Services (service) - [Services (service)](#service)
    
      - Service Resources (service\_resource) - [Service Resource
        (service\_resource)](#service_resource)
    
      - Service Templates (service\_template) - [Service Template
        (service\_template)](#service_template)
    
      - Snapshots (snapshot) - [Snapshot (snapshot)](#snapshot)
    
      - Storages (storage) - [Datastores (storage)](#storage)
    
      - Switches (switch) - [Switch (switch)](#switch)
    
      - Users (user) - [User (user)](#user)
    
      - VMs or Templates (vm\_or\_template) - [Virtual Machines and
        Templates (vm\_or\_template)](#vm_or_template)
        
          - Templates (miq\_template)
            
              - Cloud (template\_cloud)
                
                  - Amazon (template\_amazon)
                
                  - OpenStack (template\_openstack)
            
              - Infrastructure (template\_infra)
                
                  - Microsoft (template\_microsoft)
                
                  - Red Hat Enterprise Virtualization (template\_redhat)
                
                  - VMware (template\_vmware)
        
          - VMs (vm) - [VMs (vm)](#vm)
            
              - Clouds (vm\_cloud) - [VMs for Clouds
                (vm\_cloud)](#vm_cloud)
                
                  - Amazon (vm\_amazon)
                
                  - OpenStack (vm\_openstack)
            
              - Infrastructure (vm\_infra)
                
                  - Microsoft (vm\_microsoft)
                
                  - Red Hat Enterprise Virtualization (vm\_redhat)
                
                  - Vmware (vm\_vmware)
    
      - Windows Images (windows\_images) - [Windows Image
        (windows\_image)](#windows_image)

## Base Methods

These methods may be used with all objects available in the Automate
Model.

| Method                                                                                          | Usage                                                                                                             |
| ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| inspect                                                                                         | Returns a string containing a list of attributes of the object. See the **InspectMe** method in **Samples** class |
| inspect\_all                                                                                    | Returns all information for an object                                                                             |
| virtual\_column\_names                                                                          | Returns the object’s virtual columns names                                                                        |
| virtual\_columns\_inspect                                                                       | Returns the object’s virtual columns and values                                                                   |
| reload                                                                                          | Returns to original object to prevent the internal object from being returned                                     |
| model\_suffix                                                                                   | Returns object’s suffix. For an object of type MiqAeServiceVmVmware, returns **"Vmware"**                         |
| tagged\_with?(category, name)                                                                   | Is the object tagged with the category and name specified?                                                        |
| tags(category = nil)-- this means that category is an optional parameter, with a default of nil | Returns the tags                                                                                                  |
| tag\_assign(tag)                                                                                | Assigns tag to the object, except for the `miq_provision` object, which uses `add_tag(category, tag_name)`        |
| tag\_unassign(tag)                                                                              | Unassigns tag to the object, except for the `miq_provision` object, which uses `clear_tag(category, tag_name)`    |

The **InspectMe** **Sample Method** uses many of the Methods shown in
this document. The method returns attributes of the {product-title}
Server and then returns attributes for the host, cluster, and virtual
machine from the provider of invocation. In many environments it is
linked to a button.

``` ruby
###################################
# EVM Automate Method: InspectMe
#
# Notes: Dump the objects in storage to the automation.log
###################################

begin
  @method = 'InspectMe'
  @log_prefix = "[#{@method}]"
  $evm.log("info", "#{@log_prefix} - EVM Automate Method Started")

  # Turn on verbose logging
  @debug = true

  # List the types of object we will try to detect
  obj_types = %w{ vm host storage ems_cluster ext_management_system }
  obj_type = $evm.root.attributes.detect { |k,v| obj_types.include?(k)}

  # uncomment below to dump root object attributes
  dumpRoot

  # uncomment below to dump miq_server object attributes
  dumpServer

  # If obj_type is NOT nil
  unless obj_type.nil?
    rootobj = obj_type.first
    obj = obj_type.second
    $evm.log("info", "#{@log_prefix} - Detected Object:<#{rootobj}>")
    $evm.log("info","")

    case rootobj
    when 'host' then dumpHost(obj)
    when 'vm' then dumpVM(obj)
    when 'ems_cluster' then dumpCluster(obj)
    when 'ext_management_system' then dumpEMS(obj)
    when 'storage' then dumpStorage(obj)
    end
  end

  #
  # Exit method
  #
  $evm.log("info", "#{@log_prefix} - EVM Automate Method Ended")
  exit MIQ_OK

  #
  # Set Ruby rescue behavior
  #
rescue => err
  $evm.log("error", "#{@log_prefix} - [#{err}]\n#{err.backtrace.join("\n")}")
  exit MIQ_ABORT
end
```

## Availability Zones (availability\_zone)

| Method                  | Use                                |
| ----------------------- | ---------------------------------- |
| ext\_management\_system | Returns object’s Management System |
| vms                     | Returns object’s VMs               |
| vms\_and\_templates     | Returns object’s VMs and templates |
| cloud\_subnets          | Returns object’s cloud subnets     |

## Classifications (classification)

| Method    | Use                            |
| --------- | ------------------------------ |
| parent    | Returns object’s parent object |
| namespace | Returns object’s namespace     |
| category  | Returns object’s category      |
| name      | Returns object’s name          |
| to\_tag   | Returns object’s tag mapping   |

## Cloud Networks (cloud\_network)

| Method                  | Use                                |
| ----------------------- | ---------------------------------- |
| ext\_management\_system | Returns object’s Management System |
| cloud\_tenant           | Returns object’s cloud tenant      |
| cloud\_subnets          | Returns object’s cloud subnets     |
| security\_groups        | Returns object’s security groups   |
| vms                     | Returns object’s VMs               |

## Cloud Resource Quotas (cloud\_resource\_quota)

| Method                  | Use                                |
| ----------------------- | ---------------------------------- |
| ext\_management\_system | Returns object’s Management System |
| cloud\_tenant           | Returns object’s cloud tenant      |

## Cloud Subnets (cloud\_subnet)

| Method             | Use                                |
| ------------------ | ---------------------------------- |
| cloud\_network     | Returns object’s cloud network     |
| availability\_zone | Returns object’s availability zone |
| vms                | Returns object’s VMs               |

## Cloud Tenants (cloud\_tenant)

| Method                  | Use                                    |
| ----------------------- | -------------------------------------- |
| ext\_management\_system | Returns object’s Management System     |
| security\_groups        | Returns object’s security groups       |
| cloud\_networks         | Returns object’s cloud network         |
| vms                     | Returns object’s VMs                   |
| vms\_and\_templates     | Returns object’s VMs and templates     |
| miq\_templates          | Returns object’s templates             |
| floating\_ips           | Returns object’s floating IP addresses |
| cloud\_resource\_quotas | Returns object’s quotas                |

## Customization Template (customization\_template)

| Method      | Use                                        |
| ----------- | ------------------------------------------ |
| Pxe\_images | Returns customization templates pxe images |

## Clusters (ems\_cluster)

| Method                  | Use                                                             |
| ----------------------- | --------------------------------------------------------------- |
| all\_resource\_pools    | Return all of the object’s Resource Pools                       |
| all\_vms                | Return all of the object’s Virtual Machines                     |
| default\_resource\_pool | Return the object’s default Resource Pool                       |
| ems\_events             | Returns an array of EmsEvent records associated with the object |
| ext\_management\_system | Return object’s Management System                               |
| hosts                   | Return object’s Hosts                                           |
| parent\_folder          | Return object’s Parent Folder                                   |
| register\_host(host)    | Register Host to this Cluster                                   |
| resource\_pools         | Return object’s Resource Pools                                  |
| storages                | Return object’s datastores                                      |
| vms                     | Return object’s Virtual Machines                                |

``` ruby
  #########################
  #
  # Method: dumpCluster
  # Inputs: $evm.root['ems_cluster']
  # Description: Dump Cluster information
  #
  ##########################
  def dumpCluster(cluster)
    $evm.log("info","#{@log_prefix} - Cluster:<#{cluster.name}> Begin Attributes")
    cluster.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - Cluster:<#{cluster.name}> Attributes - #{k}: #{v.inspect}")}
    $evm.log("info","#{@log_prefix} - Cluster:<#{cluster.name}> End Attributes")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Cluster:<#{cluster.name}> Begin Associations")
    cluster.associations.sort.each { |assc| $evm.log("info", "#{@log_prefix} - Cluster:<#{cluster.name}> Associations - #{assc}")}
    $evm.log("info","#{@log_prefix} - Cluster:<#{cluster.name}> End Associations")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Cluster:<#{cluster.name}> Begin Virtual Columns")
    cluster.virtual_column_names.sort.each { |vcn| $evm.log("info", "#{@log_prefix} - Cluster:<#{cluster.name}> Virtual Columns - #{vcn}: #{cluster.send(vcn)}")}
    $evm.log("info","#{@log_prefix} - Cluster:<#{cluster.name}> End Virtual Columns")
    $evm.log("info","")
  end
```

## Management System Events (ems\_event)

| Method                  | Use                                                                                             |
| ----------------------- | ----------------------------------------------------------------------------------------------- |
| ext\_management\_system | Returns object’s provider                                                                       |
| ems                     | Shortcut to ext\_management\_system                                                             |
| src\_vm                 | Source VM for the event                                                                         |
| vm                      | VM for the event                                                                                |
| src\_host               | Source Host for the event                                                                       |
| host                    | Host for the event                                                                              |
| dest\_vm                | Destination VM for the event                                                                    |
| service                 | Service for the event                                                                           |
| dest\_host              | Destination Host for the event                                                                  |
| refresh(\*targets)      | Refresh the target types specified (ems, vm, host, src\_vm, src\_host, dest\_vm, or dest\_host) |

## Management System Folders (ems\_folder)

| Method                  | Use                                    |
| ----------------------- | -------------------------------------- |
| hosts                   | Returns hosts that are in the folder   |
| vms                     | Returns VMs that are in folder         |
| register\_host(host)    | Registers specified host to the folder |
| folder\_path(\*options) | Returns folders path                   |

## Providers (ext\_management\_system)

| Method                              | Use                                                                        |
| ----------------------------------- | -------------------------------------------------------------------------- |
| authentication\_password\_encrypted | Returns credentials password encrypted                                     |
| authentication\_password            | Returns credentials password unencrypted                                   |
| authentication\_userid              | Returns credentials user id                                                |
| ems\_clusters                       | Returns object’s clusters                                                  |
| ems\_events                         | Returns an array of EmsEvent records associated with the object            |
| ems\_folders                        | Returns object’s folders                                                   |
| hosts                               | Returns object’s hosts                                                     |
| refresh                             | Refreshes relationships and power states for objects related to the object |
| resource\_pools                     | Returns object’s resource pools                                            |
| storages                            | Returns object’s storages                                                  |
| vms                                 | Returns object’s vms                                                       |
| to\_s                               | Converts object to string                                                  |

``` ruby
  #########################
  #
  # Method: dumpEMS
  # Inputs: $evm.root['ext_management_system']
  # Description: Dump EMS information
  #
  ##########################
  def dumpEMS(ems)
    $evm.log("info","#{@log_prefix} - EMS:<#{ems.name}> Begin Attributes")
    ems.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - EMS:<#{ems.name}> Attributes - #{k}: #{v.inspect}")}
    $evm.log("info","#{@log_prefix} - EMS:<#{ems.name}> End Attributes")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - EMS:<#{ems.name}> Begin Associations")
    ems.associations.sort.each { |assc| $evm.log("info", "#{@log_prefix} - EMS:<#{ems.name}> Associations - #{assc}")}
    $evm.log("info","#{@log_prefix} - EMS:<#{ems.name}> End Associations")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - EMS:<#{ems.name}> Begin EMS Folders")
    ems.ems_folders.each { |ef| ef.attributes.sort.each { |k,v| $evm.log("info", "#{@log_prefix} - EMS:<#{ems.name}> EMS Folder:<#{ef.name}> #{k}: #{v.inspect}")}}
    $evm.log("info","#{@log_prefix} - EMS:<#{ems.name}> End EMS Folders")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - EMS:<#{ems.name}> Begin Virtual Columns")
    ems.virtual_column_names.sort.each { |vcn| $evm.log("info", "#{@log_prefix} - EMS:<#{ems.name}> Virtual Columns - #{vcn}: #{ems.send(vcn)}")}
    $evm.log("info","#{@log_prefix} - EMS:<#{ems.name}> End Virtual Columns")
    $evm.log("info","")
  end
```

### Cloud Providers (ems\_cloud)

| Method                  | Use                                         |
| ----------------------- | ------------------------------------------- |
| availability\_zones     | Return the provider’s availability zones    |
| cloud\_networks         | Return the provider’s available networks    |
| cloud\_networks         | Return the provider’s available tenants     |
| flavors                 | Return the provider’s hardware flavors      |
| floating\_ips           | Return the provider’s floating IP addresses |
| key\_pairs              | Return the provider’s key pairs             |
| security\_groups        | Return the provider’s security groups       |
| cloud\_resource\_quotas | Return the provider’s resource quotas       |

## Firewall Rules (firewall\_rule)

| Method                  | Use                                   |
| ----------------------- | ------------------------------------- |
| resource                | Return object’s resource              |
| source\_security\_group | Return object’s source security group |

## Flavors (flavor)

| Method                  | Use                                |
| ----------------------- | ---------------------------------- |
| ext\_management\_system | Returns object’s Management System |
| vms                     | Returns object’s VMs               |

## Floating IPs (floating\_ip)

| Method                  | Use                                |
| ----------------------- | ---------------------------------- |
| ext\_management\_system | Returns object’s Management System |
| vm                      | Returns object’s VMs               |
| cloud\_tenant           | Returns object’s cloud tenant      |

## Guest Applications (guest\_application)

| Method | Use                   |
| ------ | --------------------- |
| vm     | Returns object’s VM   |
| host   | Returns object’s Host |

## Guest Device (guest\_device)

| Method   | Use                       |
| -------- | ------------------------- |
| hardware | Returns object’s hardware |
| switch   | Returns object’s switch   |
| lan      | Returns object’s LAN      |
| network  | Returns object’s network  |

## Hardware (hardware)

| Method            | Use                               |
| ----------------- | --------------------------------- |
| ipaddresses       | Returns object’s IP addresses     |
| guest\_devices    | Returns object’s guest devices    |
| storage\_adapters | Returns object’s storage adapters |
| nics              | Returns object’s nics             |
| ports             | Returns object’s ports            |
| vm                | Returns object’s Virtual Machine  |
| host              | Returns object’s Host             |
| mac\_addresses    | Returns object’s MAC addresses    |

## Hosts (host)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>authentication_password</p></td>
<td><p>Returns credential password</p></td>
</tr>
<tr class="even">
<td><p>authentication_userid</p></td>
<td><p>Returns credential user</p></td>
</tr>
<tr class="odd">
<td><p>datacenter</p></td>
<td><p>Returns datacenter</p></td>
</tr>
<tr class="even">
<td><p>directories</p></td>
<td><p>Returns list of directories for the object</p></td>
</tr>
<tr class="odd">
<td><p>domain</p></td>
<td><p>Returns the domain portion of the hostname</p></td>
</tr>
<tr class="even">
<td><p>ems_cluster</p></td>
<td><p>Returns cluster</p></td>
</tr>
<tr class="odd">
<td><p>ems_events</p></td>
<td><p>Returns an array of EmsEvent records associated with the object</p></td>
</tr>
<tr class="even">
<td><p>ems_folder</p></td>
<td><p>Returns hosts folder on Management System</p></td>
</tr>
<tr class="odd">
<td><p>event_log_threshold?(options)</p></td>
<td><p>Searches event log records to determine if an event has occurred x number of times within a defined time frame. Returns true if the number of matching records found are greater or equal to the specified freq_threshold, otherwise it returns false</p>
<p>Options values:</p>
<p><strong>:message_filter_type</strong> - Must be one of "STARTS WITH", "ENDS WITH", "INCLUDES", "REGULAR EXPRESSION"</p>
<p><strong>:message_filter_value</strong> - &lt;string value to search for&gt;</p>
<p><strong>:time_threshold</strong> - Options time interval to search. Example: 2.days (Search the past 2 days of event logs) Default 10.days</p>
<p><strong>:freq_threshold</strong> - Number of occurrences to check for. Default = 2</p>
<p><strong>:source</strong>, <strong>:event_id</strong>, <strong>:level</strong>, <strong>:name</strong> - Options filter values</p></td>
</tr>
<tr class="even">
<td><p>ext_management_system</p></td>
<td><p>Returns Management System</p></td>
</tr>
<tr class="odd">
<td><p>files</p></td>
<td><p>Returns list of files for the object</p></td>
</tr>
<tr class="even">
<td><p>guest_applications</p></td>
<td><p>Returns Guest Applications</p></td>
</tr>
<tr class="odd">
<td><p>hardware</p></td>
<td><p>Returns hardware</p></td>
</tr>
<tr class="even">
<td><p>lans</p></td>
<td><p>Returns LANs</p></td>
</tr>
<tr class="odd">
<td><p>operating_system</p></td>
<td><p>Returns Operating System</p></td>
</tr>
<tr class="even">
<td><p>storages</p></td>
<td><p>Returns datastores</p></td>
</tr>
<tr class="odd">
<td><p>switches</p></td>
<td><p>Returns network switches</p></td>
</tr>
<tr class="even">
<td><p>vms</p></td>
<td><p>Returns VMs.</p></td>
</tr>
<tr class="odd">
<td><p>credentials(type = :remote)</p></td>
<td><p>Returns credentials for a Host for the specified type as an array for username/pwd. (Default type is :remote if no type is specified.)</p>
<p>Supports 4 different types of credentials:</p>
<p><strong>:default</strong> = Default</p>
<p><strong>:remote</strong> = Remote Login (think SSH for ESX)</p>
<p><strong>:ws</strong> = Web Services</p>
<p><strong>:ipmi</strong> = IPMI</p>
<p><em>Example 1:</em></p>
<p><code>cred = host.credentials</code></p>
<p>cred ⇒ ["user", "pwd"]&lt;/literal&gt;</p>
<p><em>Example 2:</em></p>
<p><code>user_str, pwd_str = host.credentials(:ipmi)</code></p>
<p>user_str ⇒ "user"</p>
<p>pwd_str ⇒ "pwd"&lt;/literal&gt;</p></td>
</tr>
<tr class="even">
<td><p>ems_custom_keys</p></td>
<td><p>Returns Management Systems custom keys</p></td>
</tr>
<tr class="odd">
<td><p>ems_custom_get(key)</p></td>
<td><p>Gets Value for specified Management Systems custom key</p></td>
</tr>
<tr class="even">
<td><p>ems_custom_set(attribute, value)</p></td>
<td><p>Sets value for specified custom key of the Management System</p></td>
</tr>
<tr class="odd">
<td><p>custom_keys</p></td>
<td><p>Lists {product-title} Server custom keys</p></td>
</tr>
<tr class="even">
<td><p>custom_get(key)</p></td>
<td><p>Gets value for specified {product-title} Server custom key</p></td>
</tr>
<tr class="odd">
<td><p>custom_set(key, value)</p></td>
<td><p>Sets value for specified {product-title} Server custom key</p></td>
</tr>
<tr class="even">
<td><p>ssh_exec(script)</p></td>
<td><p>Runs the specified script on the host</p></td>
</tr>
<tr class="odd">
<td><p>get_realtime_metric(metric, range, function)</p></td>
<td><p>Returns specified realtime metric</p></td>
</tr>
<tr class="even">
<td><p>current_memory_usage</p></td>
<td><p>Returns current memory usage</p></td>
</tr>
<tr class="odd">
<td><p>current_cpu_usage</p></td>
<td><p>Returns current cpu usage</p></td>
</tr>
<tr class="even">
<td><p>current_memory_headroom</p></td>
<td><p>Returns current memory headroom</p></td>
</tr>
<tr class="odd">
<td><p>to_s</p></td>
<td><p>Converts object to string</p></td>
</tr>
<tr class="even">
<td><p>scan</p></td>
<td><p>Performs SmartState Analysis on the object</p></td>
</tr>
</tbody>
</table>

The following table lists the metric types available for the
`get_realtime_metric(metric, range, function)` method for hosts.

| Metric                               | Description                                            |
| ------------------------------------ | ------------------------------------------------------ |
| v\_derived\_storage\_used            | Capacity - Used space in bytes                         |
| v\_pct\_cpu\_ready\_delta\_summation | CPU - Percentage ready                                 |
| v\_pct\_cpu\_wait\_delta\_summation  | CPU - Percentage wait                                  |
| v\_pct\_cpu\_used\_delta\_summation  | CPU - Percentage used                                  |
| v\_derived\_host\_count              | State - Number of hosts (Hourly Count / Daily Average) |
| v\_derived\_cpu\_reserved\_pct       | CPU - Percentage available                             |
| v\_derived\_memory\_reserved\_pct    | Memory - Percentage available                          |

The following Ruby snippet demonstrates using the
`get_realtime_metric(metric, range, function)` method using the
`v_pct_cpu_ready_delta_summation` metric.

``` ruby
host = $evm.root['host']
cpu_rdy = host.get_realtime_metric(:v_pct_cpu_ready_delta_summation, [15.minutes.ago.utc,5.minutes.ago.utc], :avg)
```

``` ruby
  #########################
  #
  # Method: dumpHost
  # Inputs: $evm.root['host']
  # Description: Dump Host information
  #
  ##########################

  def dumpHost(host)
    host = $evm.object['host'] || $evm.root['host']
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> Begin Attributes")
    host.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - Host:<#{host.name}> Attributes - #{k}: #{v.inspect}")}
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> End Attributes")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> Begin Associations")
    host.associations.sort.each { |assc| $evm.log("info", "#{@log_prefix} - Host:<#{host.name}> Associations - #{assc}")}
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> End Associations")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> Begin Hardware")
    host.hardware.attributes.each { |k,v| $evm.log("info", "#{@log_prefix} - Host:<#{host.name}> Hardware - #{k}: #{v.inspect}")}
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> End Hardware")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> Begin Lans")
    host.lans.each { |lan| lan.attributes.sort.each { |k,v| $evm.log("info", "#{@log_prefix} - Host:<#{host.name}> Lan:<#{lan.name}> - #{k}: #{v.inspect}")}}
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> End Lans")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> Begin Switches")
    host.switches.each { |switch| switch.attributes.sort.each { |k,v| $evm.log("info", "#{@log_prefix} - Host:<#{host.name}> Swtiche:<#{switch.name}> - #{k}: #{v.inspect}")}}
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> End Switches")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> Begin Operating System")
    host.operating_system.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - Host:<#{host.name}> Operating System - #{k}: #{v.inspect}")}
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> End Operating System")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> Begin Guest Applications")
    host.guest_applications.each { |guest_app| guest_app.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - Host:<#{host.name}> Guest Application:<#{guest_app.name}> - #{k}: #{v.inspect}")}}
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> End Guest Applications")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> Begin Virtual Columns")
    host.virtual_column_names.sort.each { |vcn| $evm.log("info", "#{@log_prefix} - Host:<#{host.name}> Virtual Columns - #{vcn}: #{host.send(vcn).inspect}")}
    $evm.log("info","#{@log_prefix} - Host:<#{host.name}> End Virtual Columns")
    $evm.log("info", "")
  end
```

### Hosts: Vmware ESX (host\_vmware\_esx)

| Method                                                  | Use                                             |
| ------------------------------------------------------- | ----------------------------------------------- |
| disable\_vmotion(device = nil)                          | Disable vMotion                                 |
| enable\_vmotion(device = nil)                           | Enable vMotion                                  |
| enter\_maintenance\_mode(timeout = 0, evacuate = false) | Put Host in Maintenance Mode                    |
| exit\_maintenance\_mode(timeout = 0)                    | Leave Maintenance Mode                          |
| in\_maintenance\_mode?                                  | Check to see if the host is in Maintenance Mode |
| power\_down\_to\_standby(timeout = 0, evacuate = false) | Put Host in standby                             |
| power\_up\_from\_standby(timeout = 0)                   | Take Host out of standby                        |
| reboot(force = false)                                   | Reboot Host                                     |
| shutdown(force = false)                                 | Shutdown Host                                   |
| vmotion\_enabled?(device = nil)                         | Check to see if vMotion is enabled              |

## LAN (lan)

| Method         | Use                               |
| -------------- | --------------------------------- |
| switch         | Returns object’s switch           |
| guest\_devices | Returns object’s guest devices    |
| vms            | Returns object’s Virtual Machines |
| templates      | Returns object’s templates        |
| hosts          | Returns object’s Hosts            |

## Groups (miq\_group)

| Method                  | Use                                                         |
| ----------------------- | ----------------------------------------------------------- |
| users                   | Returns users in the current miq\_group                     |
| vms                     | Returns Virtual Machines that this group owns               |
| custom\_keys            | Returns all custom keys for the group                       |
| custom\_get(key)        | Returns the value of the specified custom key for the group |
| custom\_set(key, value) | Sets the value for the specified key                        |

``` ruby
  #########################
  #
  # Method: dumpGroup
  # Inputs: $evm.root['user'].miq_group
  # Description: Dump User's Group information
  #
  ##########################

  def dumpGroup
    user = $evm.root['user']
    unless user.nil?
      miq_group = user.miq_group
      unless miq_group.nil?
        $evm.log("info","#{@method} - Group:<#{miq_group.description}> Begin Attributes [miq_group.attributes]")
        miq_group.attributes.sort.each { |k, v| $evm.log("info", "#{@method} - Group:<#{miq_group.description}> Attributes - #{k}: #{v.inspect}")} unless $evm.root['user'].miq_group.nil?
        $evm.log("info","#{@method} - Group:<#{miq_group.description}> End Attributes [miq_group.attributes]")
        $evm.log("info", "")

        $evm.log("info","#{@method} - Group:<#{miq_group.description}> Begin Associations [miq_group.associations]")
        miq_group.associations.sort.each { |assc| $evm.log("info", "#{@method} - Group:<#{miq_group.description}> Associations - #{assc}")}
        $evm.log("info","#{@method} - Group:<#{miq_group.description}> End Associations [miq_group.associations]")
        $evm.log("info","")

        $evm.log("info","#{@method} - Group:<#{miq_group.description}> Begin Virtual Columns [miq_group.virtual_column_names]")
        miq_group.virtual_column_names.sort.each { |vcn| $evm.log("info", "#{@method} - Group:<#{miq_group.description}> Virtual Columns - #{vcn}: #{miq_group.send(vcn).inspect}")}
        $evm.log("info","#{@method} - Group:<#{miq_group.description}> End Virtual Columns [miq_group.virtual_column_names]")
        $evm.log("info","")
      end
    end
  end
```

## Request (miq\_request)

Request objects are submitted to {product-title} Server for processing.
After the request phase, the request becomes a task object. The table
below shows the relationship between a request object and a task object.

| Request Object                        | Task Object                        |
| ------------------------------------- | ---------------------------------- |
| automation\_request                   | automation\_task                   |
| miq\_host\_provision\_request         | miq\_host\_provision               |
| miq\_provision\_request               | miq\_provision                     |
| vm\_reconfigure\_request              | vm\_reconfigure\_task              |
| service\_template\_provision\_request | service\_template\_provision\_task |
| vm\_migrate\_request                  | vm\_migrate\_task                  |

If you set something on the request object, it will be inherited by the
task instance that does the work. This may be useful if you are
provisioning multiple virtual machines at a time and need to modify the
same setting for all. Otherwise, the item can be modified on the
individual task.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>add_tag(category, tag_name)</p></td>
<td><p>Add a tag to a provision instance by specifying the category and tag name</p>
<p><em>Example:</em></p>
<p><code>miq_provision.add_tag(:location, "CHI")</code></p></td>
</tr>
<tr class="even">
<td><p>approve(approver,reason for approval)</p></td>
<td><p>Approves the miq_request.</p>
<p><em>Example:</em></p>
<p><code>$evm.root["miq_request"].approve("admin", "Auto-Approved")</code></p></td>
</tr>
<tr class="odd">
<td><p>approvers</p></td>
<td><p>Returns request approvers.</p></td>
</tr>
<tr class="even">
<td><p>authorized?</p></td>
<td><p>Returns true if authorized, false if not.</p></td>
</tr>
<tr class="odd">
<td><p>clear_tag(category=nil, tag_name=nil)</p></td>
<td><p>Without any parameters, the clear_tag method clears all tags from the provision request. Providing a category clears all tags selected in that category. Clear a specific category/tag by providing it.</p>
<p><em>Example:</em></p>
<p><code>miq_provision.clear_tag(:location, "CHI")</code></p></td>
</tr>
<tr class="even">
<td><p>deny</p></td>
<td><p>Denies the miq_request</p>
<p><em>Example:</em></p>
<p><code># Deny the request</code></p>
<p>$evm.log('info',"Request denied because of Quota")</p>
<p>$evm.root["miq_request"].deny("admin", "Quota Exceeded")&lt;/literal&gt;</p></td>
</tr>
<tr class="odd">
<td><p>get_classification(category)</p></td>
<td><p>Works the same as get_tag(category) but the returned data is a hash with :name and :description</p>
<p><em>Example:</em></p>
<p><code>request.get_classification(:department)</code></p>
<p><em>Returns:</em></p>
<p><code>[{:name⇒"accounting", :description⇒"Accounting"}, {:name⇒"engineering", :description⇒"Engineering"}]</code></p></td>
</tr>
<tr class="even">
<td><p>get_classifications</p></td>
<td><p>Works the same as get_tag but the returned tag data is a hash with :name and :description</p>
<p><em>Example:</em></p>
<p><code>request.get_classifications</code></p>
<p><em>Returns:</em></p>
<p><code>{:cc⇒{:name⇒"001", :description⇒"Cost Center 001"}, :department⇒[{:name⇒"accounting", :description⇒"Accounting"}, {:name⇒"engineering", :description⇒"Engineering"}]}</code></p></td>
</tr>
<tr class="odd">
<td><p>get_option(key)</p></td>
<td><p>Returns a value from the options hash based on the name of the key name passed in. Internally many of the values are stored as an array of items. (For example, a target host would be stored as the index to the host object in the db and the display name.) Calling this method will return the first item if it is an array. For non-array values the item is returned unmodified.</p>
<p><em>Example:</em></p>
<p><code>miq_provision_request.get_option(:number_of_cpus)</code></p></td>
</tr>
<tr class="even">
<td><p>get_tag(category)</p></td>
<td><p>Returns the tags selected for the specified tag category.</p>
<p><em>Example:</em></p>
<p><code>request.get_tag(:department)</code></p>
<p><em>Returns:</em></p>
<p><code>["accounting", "engineering"]</code></p></td>
</tr>
<tr class="odd">
<td><p>get_tags</p></td>
<td><p>Get all selected tags stored in a hash by category. If more than one tag is selected in a category, the hash will contain an array of tag names. Otherwise it will contain the tag name as a string.</p>
<p><em>Example:</em></p>
<p><code>request.get_tags</code></p>
<p><em>Returns:</em></p>
<p><code>{:cc⇒"001", :department⇒["accounting", "engineering"]}</code></p></td>
</tr>
<tr class="even">
<td><p>miq_request</p></td>
<td><p>(Legacy support) Internal Note: The miq_request instance use to be a separate instance from the specific request instance (like miq_provision_request). When the classes were refactored into 1 this method was added to allow existing code and automate methods to continue to run unchanged.)</p></td>
</tr>
<tr class="odd">
<td><p>miq_request_tasks</p></td>
<td><p>Returns the requests tasks</p></td>
</tr>
<tr class="even">
<td><p>options</p></td>
<td><p>Returns a hash containing all the options set for the current provision object</p></td>
</tr>
<tr class="odd">
<td><p>pending</p></td>
<td><p>Puts the object in a pending state for approval</p>
<p><em>Example:</em></p>
<p><code># Raise automation event: request_pending</code></p>
<p>$evm.root["miq_request"].pending&lt;/literal&gt;</p></td>
</tr>
<tr class="even">
<td><p>reason</p></td>
<td><p>Returns reason for approval or denial of request</p></td>
</tr>
<tr class="odd">
<td><p>requester</p></td>
<td><p>Returns the requester</p></td>
</tr>
<tr class="even">
<td><p>resource</p></td>
<td><p>Returns the resource for the request</p></td>
</tr>
<tr class="odd">
<td><p>set_message(value)</p></td>
<td><p>Sets the message for the request</p></td>
</tr>
<tr class="even">
<td><p>set_option(key, value)</p></td>
<td><p>Sets the specified key/value pair for the object</p></td>
</tr>
</tbody>
</table>

### Automation Request (automation\_request)

| Method            | Use                             |
| ----------------- | ------------------------------- |
| automation\_tasks | Returns object’s automate tasks |

### Host Provision Request (miq\_host\_provision\_request)

| Method                | Use                                           |
| --------------------- | --------------------------------------------- |
| miq\_host\_provisions | Returns the miq\_host\_provisions objects     |
| ci\_type              | Returns the cloud infrastructure type: `host` |

### VM Provision Request (miq\_provision\_request)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>check_quota(quota_type, options={})</p></td>
<td><p>Returns the quota information for the specified type</p></td>
</tr>
<tr class="even">
<td><p>ci_type</p></td>
<td><p>Returns the cloud infrastructure type: 'vm'</p></td>
</tr>
<tr class="odd">
<td><p>eligible_clusters</p></td>
<td><p>Returns an array of available Cluster objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>eligible_customization_templates</p></td>
<td><p>Returns an array of available Customization Templates filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_folders</p></td>
<td><p>Returns an array of available Folder objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>eligible_hosts</p></td>
<td><p>Returns an array of available Host objects filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_iso_images</p></td>
<td><p>Returns an array of available ISO image objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>eligible_pxe_images</p></td>
<td><p>Returns an array of available PXE Image objects filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_pxe_servers</p></td>
<td><p>Returns an array of available PXE Server objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>eligible_resource_pools</p></td>
<td><p>Returns an array of available Resource Pool objects filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_resources(rsc_type)</p></td>
<td><p>Returns eligible resources given the type specified</p></td>
</tr>
<tr class="even">
<td><p>eligible_storages</p></td>
<td><p>Returns an array of available Storage (Datastore) objects filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_windows_images</p></td>
<td><p>Returns an array of available Windows Image objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>get_folder_paths</p></td>
<td><p>Returns a hash where the key is an index and the value is the fully-qualified path name of the folder.</p>
<p><em>Example:</em></p>
<p><code>{7 ⇒ Dev/Dept1/QA, 8 ⇒ Test/Dept2/QA}</code></p>
<p>This format is useful when a fully-qualified path is required to match the folder name. For example, if you had multiple QA folders under different departments in the sample above. To find the proper QA folder you need to evaluate the entire folder path.</p></td>
</tr>
<tr class="odd">
<td><p>get_retirement_days</p></td>
<td><p>Returns the number of dates until retirement</p></td>
</tr>
<tr class="even">
<td><p>miq_provision</p></td>
<td><p>Returns the task.</p></td>
</tr>
<tr class="odd">
<td><p>miq_request</p></td>
<td><p>Returns the miq_provision_requests miq_request object</p></td>
</tr>
<tr class="even">
<td><p>set_cluster(rsc)</p></td>
<td><p>Set the cluster to use based on object returned from eligible_clusters</p></td>
</tr>
<tr class="odd">
<td><p>set_customization_template(rsc)</p></td>
<td><p>Set the customization_template to use based on object returned from eligible_customization_templates</p></td>
</tr>
<tr class="even">
<td><p>set_folder(folder_path)</p></td>
<td><p>Set the folder to use based on object returned from eligible_folders. In addition, set_folder accepts the following folder types:</p>
<p><strong>Folder Paths</strong> - separated by forward slashes. Must include Data-center name. For example, 'Prod/Discovered virtual machine' where 'Prod' is the Data-center name and 'Discovered virtual machine' is the folder name.</p>
<p><strong>Object</strong> - object returned from the get_folder_paths method.</p></td>
</tr>
<tr class="odd">
<td><p>set_host(rsc)</p></td>
<td><p>Set the host to use based on object returned from eligible_hosts</p></td>
</tr>
<tr class="even">
<td><p>set_network_adapter(idx, nic_hash, value=nil)</p></td>
<td><p>Modifies the network card attached to the VM container</p>
<p><em>Available settings:</em></p>
<p><strong>:is_dvs</strong> true / false (Default: false)</p>
<p><strong>:network</strong> (Network Name)</p>
<p><strong>:mac_address</strong></p>
<p><strong>:devicetype</strong> (Default: VirtualPCNet32) Defined by VMware: <a href="http://www.vmware.com/support/developer/vc-sdk/visdk400pubs/ReferenceGuide/vim.vm.device.VirtualEthernetCard.html">http://www.vmware.com/support/developer/vc-sdk/visdk400pubs/ReferenceGuide/vim.vm.device.VirtualEthernetCard.html</a></p>
<p><strong>:connectable</strong> ⇒ {:allowguestcontrol ⇒ true / false} (Default: true)</p>
<p><strong>:connectable</strong> ⇒ {:startconnected ⇒ true / false} (Default: true)</p>
<p><strong>:connectable</strong> ⇒ {:connected ⇒ true / false} (Default: true)</p>
<p><em>Example:</em></p>
<p><code>prov.set_network_adapter(1, {:network ⇒ dvs_net1, :is_dvs ⇒ true} )</code></p></td>
</tr>
<tr class="odd">
<td><p>set_network_address_mode(mode)</p></td>
<td><p>Sets IP address type. Available modes are dhcp and static</p></td>
</tr>
<tr class="even">
<td><p>set_nic_settings(idx, nic_hash, value=nil)</p></td>
<td><p>Modifies the network interface settings at the operating system level</p>
<p><em>Available settings:</em></p>
<p><strong>:addr_mode</strong> "dhcp" / "static" (Default: Statis)</p>
<p><strong>:ip_addr</strong></p>
<p><strong>:subnet_mask</strong></p>
<p><strong>:gateway</strong></p>
<p><strong>:dns_domain</strong></p>
<p><strong>:dns_servers</strong> (Windows Only) Comma separated values</p>
<p><strong>:sysprep_netbios_mode</strong> (Windows Only) Defined by VMware: <a href="http://www.vmware.com/support/developer/vc-sdk/visdk400pubs/ReferenceGuide/vim.vm.customization.IPSettings.NetBIOSMode.html">http://www.vmware.com/support/developer/vc-sdk/visdk400pubs/ReferenceGuide/vim.vm.customization.IPSettings.NetBIOSMode.html</a></p>
<p><strong>:wins_servers</strong> Passed as a string specifying the Primary and Secondary WINS servers separated by a comma. <code>&lt;PrimaryWINS&gt;, &lt;SecondaryWINS&gt;</code></p>
<p><em>Example:</em></p>
<p><code>prov.set_nic_settings(1, {:ip_addr⇒10.226.133.55, :subnet_mask⇒'255.255.255.192', :gateway⇒'10.226.133.5', :addr_mode⇒["static", "Static"] } )</code></p></td>
</tr>
<tr class="odd">
<td><p>set_iso_image(rsc)</p></td>
<td><p>Set the iso_image to use based on object returned from eligible_iso_images</p></td>
</tr>
<tr class="even">
<td><p>set_pxe_image(rsc)</p></td>
<td><p>Set the pxe_image to use based on object returned from eligible_pxe_images</p></td>
</tr>
<tr class="odd">
<td><p>set_pxe_server(rsc)</p></td>
<td><p>Set the pxe_server to use based on object returned from eligible_pxe_servers</p></td>
</tr>
<tr class="even">
<td><p>set_resource_pool(rsc)</p></td>
<td><p>Set the resource_pool to use based on object returned from eligible_resource_pools</p></td>
</tr>
<tr class="odd">
<td><p>set_resource(rsc)</p></td>
<td><p>Sets the resource for the request. (Helper method, should not be called directly)</p></td>
</tr>
<tr class="even">
<td><p>set_retirement_days</p></td>
<td><p>Set the number of days until retirement</p></td>
</tr>
<tr class="odd">
<td><p>set_storage(rsc)</p></td>
<td><p>Set the Datastore (storage object) to use based on object returned from eligible_storages</p></td>
</tr>
<tr class="even">
<td><p>set_vm_notes(note)</p></td>
<td><p>Sets text for the VM notes (aka annotation) field</p></td>
</tr>
<tr class="odd">
<td><p>set_windows_image(rsc)</p></td>
<td><p>Set the windows_image to use based on object returned from eligible_windows_images</p></td>
</tr>
<tr class="even">
<td><p>source_type</p></td>
<td><p>Returns the provision source type. (values are 'vm' or 'template')</p></td>
</tr>
<tr class="odd">
<td><p>src_vm_id</p></td>
<td><p>Returns ID of the template being cloned</p></td>
</tr>
<tr class="even">
<td><p>target_type</p></td>
<td><p>Returns the provision target type. (values are 'vm' or 'template')</p></td>
</tr>
<tr class="odd">
<td><p>vm_template</p></td>
<td><p>Returns the requests template</p></td>
</tr>
</tbody>
</table>

## Request Task (miq\_request\_task)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>add_tag(category, tag_name)</p></td>
<td><p>Add a tag to a provision instance by specifying the category and tag name.</p>
<p><em>Example:</em></p>
<p><code>miq_provision.add_tag(:location, "CHI")</code></p></td>
</tr>
<tr class="even">
<td><p>clear_tag(category=nil, tag_name=nil)</p></td>
<td><p>Without any parameters, the clear_tag method will clear all tags from the provision request. Providing a category will clear all tags selected in that category. Clear a specific category/tag by providing it.</p>
<p><em>Example:</em></p>
<p><code>miq_provision.clear_tag(:location, "CHI")</code></p></td>
</tr>
<tr class="odd">
<td><p>destination</p></td>
<td><p>Returns the destination object. (The resultant object from running the task. In the case of provisioning, this would be the newly created VM.)</p></td>
</tr>
<tr class="even">
<td><p>execute</p></td>
<td><p>Executes or processes the request.</p></td>
</tr>
<tr class="odd">
<td><p>finished(msg)</p></td>
<td><p>Sets the task to finished with the supplied message.</p></td>
</tr>
<tr class="even">
<td><p>get_classification(category)</p></td>
<td><p>Works the same as get_tag(category) but the returned data is a hash with :name and :description.</p>
<p><em>Example:</em></p>
<p><code>request.get_classification(:department)</code></p>
<p><em>Returns:</em></p>
<p><code>[{:name⇒"accounting", :description⇒"Accounting"}, {:name⇒"engineering", :description⇒"Engineering"}]</code></p></td>
</tr>
<tr class="odd">
<td><p>get_classifications</p></td>
<td><p>Works the same as get_tag but the returned tag data is a hash with :name and :description.</p>
<p><em>Example:</em></p>
<p><code>request.get_classifications</code></p>
<p><em>Returns:</em></p>
<p><code>{:cc⇒{:name⇒"001", :description⇒"Cost Center 001"}, :department⇒[{:name⇒"accounting", :description⇒"Accounting"}, {:name⇒"engineering", :description⇒"Engineering"}]}</code></p></td>
</tr>
<tr class="even">
<td><p>get_option_last(key)</p></td>
<td><p>This method is the same as get_option, except that it returns the last array value.</p></td>
</tr>
<tr class="odd">
<td><p>get_option(key)</p></td>
<td><p>Returns a value from the options hash based on the name of the key name passed in. Internally many of the values are stored as an array of items. (For example, a target host would be stored as the index to the host object in the db and the display name.) Calling this method will return the first item if it is an array. For non-array values the item is returned unmodified.</p>
<p><em>Example:</em></p>
<p><code>miq_provision_request.get_option(:number_of_cpus)</code></p></td>
</tr>
<tr class="even">
<td><p>get_tag(category)</p></td>
<td><p>Returns the tags selected for the specified tag category.</p>
<p><em>Example:</em></p>
<p><code>request.get_tag(:department)</code></p>
<p><em>Returns:</em></p>
<p><code>["accounting", "engineering"]</code></p></td>
</tr>
<tr class="odd">
<td><p>get_tags</p></td>
<td><p>Get all selected tags stored in a hash by category. If more than one tag is selected in a category, the hash will contain an array of tag names. Otherwise it will contain the tag name as a string.</p>
<p><em>Example:</em></p>
<p><code>request.get_tag</code></p>
<p><em>Returns:</em></p>
<p><code>{:cc⇒"001", :department⇒["accounting", "engineering"]}</code></p></td>
</tr>
<tr class="even">
<td><p>message=(msg)</p></td>
<td><p>Sets the message for the request task.</p></td>
</tr>
<tr class="odd">
<td><p>miq_request</p></td>
<td><p>Returns the miq_request for the task.</p></td>
</tr>
<tr class="even">
<td><p>miq_request_task</p></td>
<td><p>Returns the parent miq_request task.</p></td>
</tr>
<tr class="odd">
<td><p>miq_request_tasks</p></td>
<td><p>Returns the children miq_request tasks.</p></td>
</tr>
<tr class="even">
<td><p>options</p></td>
<td><p>Returns a hash containing all the options set for the current object.</p></td>
</tr>
<tr class="odd">
<td><p>set_option(key, value)</p></td>
<td><p>Updates a key/value pair in the options hash for the provision object. Often the value is required to be an array.</p></td>
</tr>
<tr class="even">
<td><p>source</p></td>
<td><p>Returns the source object. (The source, or input, object that the task runs against. In the case of provisioning, this would be the VM or template selected to be provisioned.)</p></td>
</tr>
</tbody>
</table>

### Automation Task (automation\_task)

| Method              | Use                                           |
| ------------------- | --------------------------------------------- |
| automation\_request | Returns associated automation\_request object |
| status              | Returns status of the task                    |

### Host Provision Task (miq\_host\_provision)

| Method                        | Use                                       |
| ----------------------------- | ----------------------------------------- |
| host                          | Returns object’s host                     |
| miq\_host\_provision\_request | Returns the request that created the task |
| status                        | Returns status of host provision          |

### VM Provision Task (miq\_provision)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>check_quota(quota_type, options={})</p></td>
<td><p>Returns the quota information for the specified type</p></td>
</tr>
<tr class="even">
<td><p>eligible_clusters</p></td>
<td><p>Returns an array of available Cluster objects filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_customization_templates</p></td>
<td><p>Returns an array of available Customization Templates</p></td>
</tr>
<tr class="even">
<td><p>eligible_folders</p></td>
<td><p>Returns an array of available Folder objects filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_hosts</p></td>
<td><p>Returns an array of available Host objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>eligible_iso_images</p></td>
<td><p>Returns an array of available ISO Image objects filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_pxe_images</p></td>
<td><p>Returns an array of available PXE Image objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>eligible_pxe_servers</p></td>
<td><p>Returns an array of available PXE Servers filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>eligible_resource_pools</p></td>
<td><p>Returns an array of available Resource Pool objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>eligible_resources(rsc_type)</p></td>
<td><p>Returns the eligible resources for the resource type specified</p></td>
</tr>
<tr class="odd">
<td><p>eligible_storages</p></td>
<td><p>Returns an array of available Storage (Datastore) objects filtered by previously selected resources</p></td>
</tr>
<tr class="even">
<td><p>eligible_windows_images</p></td>
<td><p>Returns an array of available Windows Image objects filtered by previously selected resources</p></td>
</tr>
<tr class="odd">
<td><p>get_domain_details</p></td>
<td><p>Returns domain information</p></td>
</tr>
<tr class="even">
<td><p>get_domain_name</p></td>
<td><p>Returns domain name</p></td>
</tr>
<tr class="odd">
<td><p>get_folder_paths</p></td>
<td><p>Returns a hash where the key is an index and the value is the fully-qualified path name of the folder.</p>
<p><em>Example:</em></p>
<p><code>{7 ⇒ Dev/Dept1/QA, 8 ⇒ Test/Dept2/QA})</code>.</p>
<p>This format is useful when a fully-qualified path is required to match the folder name. For example, if you had multiple QA folders under different departments in the sample above. To find the proper QA folder you need to evaluate the entire folder path.</p></td>
</tr>
<tr class="even">
<td><p>get_network_details</p></td>
<td><p>Returns network information</p></td>
</tr>
<tr class="odd">
<td><p>get_network_scope</p></td>
<td><p>Returns network scope</p></td>
</tr>
<tr class="even">
<td><p>miq_provision_request</p></td>
<td><p>Returns the provision request object</p></td>
</tr>
<tr class="odd">
<td><p>set_cluster(rsc)</p></td>
<td><p>Set the cluster to use based on object returned from eligible_clusters</p></td>
</tr>
<tr class="even">
<td><p>set_customization_spec(name=nil, override=false)</p></td>
<td><p>Sets the name of the custom spec to use as defined by its name in Virtual Center</p></td>
</tr>
<tr class="odd">
<td><p>set_customization_template(rsc)</p></td>
<td><p>Set the customization_template to use based on object returned from eligible_customization_templates</p></td>
</tr>
<tr class="even">
<td><p>set_dvs(portgroup, switch = portgroup)</p></td>
<td><p>Set the name of the Distributed Virtual Switch (portgroup). An options &lt;switch&gt; name can also be passed</p>
<p><em>Example:</em></p>
<p><code>miq_provision.set_dvs('default')</code></p></td>
</tr>
<tr class="odd">
<td><p>set_folder(folder_path)</p></td>
<td><p>Set the folder to use based on object returned from eligible_folders. In addition, set_folder accepts the following folder types:</p>
<p><strong>Folder Paths</strong> - separated by forward slashes. Must include Data-center name.</p>
<p><em>Example:</em></p>
<p>'Prod/Discovered virtual machine' where 'Prod' is the Data-center name and 'Discovered virtual machine' is the folder name.</p>
<p><strong>Object</strong> - object returned from the get_folder_paths method</p></td>
</tr>
<tr class="even">
<td><p>set_host(rsc)</p></td>
<td><p>Set the host to use based on object returned from eligible_hosts</p></td>
</tr>
<tr class="odd">
<td><p>set_network_adapter(idx, nic_hash, value=nil)</p></td>
<td><p>Modifies the network card attached to the VM container</p>
<p><em>Available settings:</em></p>
<p><strong>:is_dvs</strong> true / false (Default: false)</p>
<p><strong>:network</strong> (Network Name)</p>
<p><strong>:mac_address</strong></p>
<p><strong>:devicetype</strong> (Default: VirtualPCNet32) Defined by VMware: <a href="http://www.vmware.com/support/developer/vc-sdk/visdk400pubs/ReferenceGuide/vim.vm.device.VirtualEthernetCard.html">http://www.vmware.com/support/developer/vc-sdk/visdk400pubs/ReferenceGuide/vim.vm.device.VirtualEthernetCard.html</a></p>
<p><strong>:connectable</strong> ⇒ {:allowguestcontrol ⇒ true / false} (Default: true)</p>
<p><strong>:connectable</strong> ⇒ {:startconnected ⇒ true / false} (Default: true)</p>
<p><strong>:connectable</strong> ⇒ {:connected ⇒ true / false} (Default: true)</p>
<p><em>Example:</em></p>
<p><code>prov.set_network_adapter(1, {:network ⇒ dvs_net1, :is_dvs ⇒ true} )</code></p></td>
</tr>
<tr class="even">
<td><p>set_network_address_mode(mode)</p></td>
<td><p>Available modes are dhcp and static</p></td>
</tr>
<tr class="odd">
<td><p>set_nic_settings(idx, nic_hash, value=nil)</p></td>
<td><p>Modifies the network interface settings at the operating system level</p>
<p><em>Available settings:</em></p>
<p><strong>:addr_mode</strong> "dhcp" / "static" (Default: Statis)</p>
<p><strong>:ip_addr</strong></p>
<p><strong>:subnet_mask</strong></p>
<p><strong>:gateway</strong></p>
<p><strong>:dns_domain</strong></p>
<p><strong>:dns_servers</strong> (Windows Only) Comma separated values</p>
<p><strong>:sysprep_netbios_mode</strong> (Windows Only) Defined by VMware: <a href="http://www.vmware.com/support/developer/vc-sdk/visdk400pubs/ReferenceGuide/vim.vm.customization.IPSettings.NetBIOSMode.html">http://www.vmware.com/support/developer/vc-sdk/visdk400pubs/ReferenceGuide/vim.vm.customization.IPSettings.NetBIOSMode.html</a></p>
<p><strong>:wins_servers</strong> Passed as a string specifying the Primary and Secondary WINS servers separated by a comma. "&lt;PrimaryWINS&gt;, &lt;SecondaryWINS&gt;"</p>
<p><em>Example:</em></p>
<p><code>prov.set_nic_settings(1, {:ip_addr⇒10.226.133.55, :subnet_mask⇒'255.255.255.192', :gateway⇒'10.226.133.5', :addr_mode⇒["static", "Static"] } )</code></p></td>
</tr>
<tr class="even">
<td><p>set_iso_image(rsc)</p></td>
<td><p>Set the iso_image to use based on object returned from eligible_iso_images</p></td>
</tr>
<tr class="odd">
<td><p>set_pxe_image(rsc)</p></td>
<td><p>Set the pxe_image to use based on object returned from eligible_pxe_images</p></td>
</tr>
<tr class="even">
<td><p>set_pxe_server(rsc)</p></td>
<td><p>Set the pxe_server to use based on object returned from eligible_pxe_servers</p></td>
</tr>
<tr class="odd">
<td><p>set_resource_pool(rsc)</p></td>
<td><p>Set the resource_pool to use based on object returned from eligible_resource_pools</p></td>
</tr>
<tr class="even">
<td><p>set_storage(rsc)</p></td>
<td><p>Set the Datastore (storage object) to use based on object returned from eligible_storages</p></td>
</tr>
<tr class="odd">
<td><p>set_vlan(vlan)</p></td>
<td><p>Sets the name of the VLan to use</p>
<p><em>Example:</em></p>
<p><code>miq_provision.set_vlan('default')</code></p></td>
</tr>
<tr class="even">
<td><p>set_vm_notes(note)</p></td>
<td><p>Sets text for the VM notes (aka annotation) field</p></td>
</tr>
<tr class="odd">
<td><p>set_vm_notes(notes)</p></td>
<td><p>Sets text for the VM notes (aka annotation) field</p></td>
</tr>
<tr class="even">
<td><p>set_windows_image(rsc)</p></td>
<td><p>Set the windows_image to use based on object returned from eligible_windows_images</p></td>
</tr>
<tr class="odd">
<td><p>source_type</p></td>
<td><p>Returns the provision source type. (values are 'vm' or 'template')</p></td>
</tr>
<tr class="even">
<td><p>status</p></td>
<td><p>Returns provision status</p></td>
</tr>
<tr class="odd">
<td><p>target_type</p></td>
<td><p>Returns the provision target type. (values are 'vm' or 'template')</p></td>
</tr>
<tr class="even">
<td><p>vdi_farm</p></td>
<td><p>Returns VDI Farm information</p></td>
</tr>
<tr class="odd">
<td><p>vm</p></td>
<td><p>The newly created vm</p></td>
</tr>
<tr class="even">
<td><p>vm_template</p></td>
<td><p>Returns the template selected to be provisioned</p></td>
</tr>
</tbody>
</table>

``` ruby
begin
  miq_provision = $evm.root["miq_provision"] || $evm.root['miq_provision']
  prov = $evm.root["miq_provision"]
  user = prov.miq_request.requester
  raise "User not specified" if user.nil?

  ###################################
  # Process Change Request Number and set VM Annotation
  ###################################
  intake = prov.get_option(:vm_description)
  intake = "Change Request#: #{intake}"
  prov.set_option(:vm_description,intake)

  ###################################
  # Set the customization spec based on the environment tag chosen in the dialog
  ###################################
  tags = prov.get_tags
  $evm.log("info","Tags: #{tags.inspect}")
  env = tags[:environment]
  $evm.log("info", "Mapping custom spec based on Category Environment <#{env}> chosen in the dialog")
  if env.eql? "dev"
    customization_spec = "Dev-Specification"
    miq_provision.set_customization_spec(customization_spec)
  end
  if env.eql? "stg"
    customization_spec = "Stg-Specification"
    miq_provision.set_customization_spec(customization_spec)
  end

  ###################################
  # Set the VM Notes as follows:
  ###################################
  vm_notes = "#{intake}"
  vm_notes +=  "\nOwner: #{miq_provision.get_option(:owner_first_name)} #{miq_provision.get_option(:owner_last_name)}"
  vm_notes += "\nEmail: #{miq_provision.get_option(:owner_email)}"
  vm_notes += "\nSource Template: #{miq_provision.vm_template.name}"
  miq_provision.set_vm_notes(vm_notes)

  ###################################
  # Drop the VM in the targeted folder
  # In VC a folder must exist that matches the LDAP Group
  # VM will be placed in the Folder
  ###################################
  if prov.get_option(:placement_folder_name).nil?
    ###################################
    # If you want to use a Default folder, set folder = below to the default
    ###################################
    #    folder = "22F DC/LAB FARM/GSE/Intel/Infrastructure/ManageIQ/SelfServiceVMs"
    folder = "DC1/Infrastructure/ManageIQ/SelfService"
    $evm.log("info", "Placing VM in VC folder: <#{folder}")
    $evm.log("info", "Set_folder called with [#{folder.inspect}]")

    miq_provision.set_folder(folder)
  end

  ####################################################
  # Set the IP Address based on the :mac_address entered in the dialog
  #
  ####################################################
  ipaddr = prov.get_option(:mac_address)

  if ! ipaddr.nil?
    # Set provisioning options to override options
    prov.set_option(:sysprep_spec_override, [true, 1])
    prov.set_option(:addr_mode, ["static", "Static"])
    prov.set_option(:ip_addr, ipaddr)
    # Reset :mac_address to nil
    prov.set_option(:mac_address, nil)
  end

  $evm.log("info", "Provision Options: #{prov.options.inspect}")

  exit MIQ_OK

rescue => err
  $evm.log("info", "Set_folder err [#{err}]\n#{err.backtrace.join("\n")}")
end
```

### VM Provisioning for Clouds Task (miq\_provision\_cloud)

| Method                    | Use                                    |
| ------------------------- | -------------------------------------- |
| availability\_zones       | Returns object’s availability zones    |
| instance\_types           | Returns object’s instance types        |
| security\_groups          | Returns object’s security groups       |
| floating\_ip\_addresses   | Returns object’s floating IP addresses |
| cloud\_networks           | Returns object’s cloud network         |
| cloud\_subnets            | Returns object’s cloud subnet          |
| guest\_access\_key\_pairs | Returns object’s guest key pair        |
| cloud\_tenants            | Returns object’s cloud tenant          |

### Service Template Provision Task (service\_template\_provision\_task)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>dialog_options</p></td>
<td><p>Returns object’s dialog options hash</p></td>
</tr>
<tr class="even">
<td><p>get_dialog_option(key)</p></td>
<td><p>Returns object’s dialog value for the specified key</p></td>
</tr>
<tr class="odd">
<td><p>service_resource</p></td>
<td><p>Returns the service resource for the task</p></td>
</tr>
<tr class="even">
<td><p>set_dialog_option(key, value)</p></td>
<td><p>Sets a dialog option</p>
<p><em>Example:</em></p>
<p><code>set_dialog_option('memory',memory_size)</code></p></td>
</tr>
<tr class="odd">
<td><p>status</p></td>
<td><p>Returns the tasks status</p></td>
</tr>
</tbody>
</table>

### Service Reconfiguration Task (service\_reconfigure\_task)

| Method                          | Use                                                 |
| ------------------------------- | --------------------------------------------------- |
| dialog\_options                 | Show all dialog options for object                  |
| get\_dialog\_option(key)        | Show a dialog option based stored in key            |
| set\_dialog\_option(key, value) | Set value as a dialog option in key                 |
| status                          | Returns status of the task                          |
| finished(msg)                   | Sets the task to finished with the supplied message |

### VM Migrate Task (vm\_migrate\_task)

| Method | Use                                  |
| ------ | ------------------------------------ |
| status | Returns status of the migration task |

## Proxies (miq\_proxy)

| Method                                 | Use                         |
| -------------------------------------- | --------------------------- |
| host                                   | Returns object’s hosts      |
| powershell(script, returns = 'string') | Submits a powershell script |

## Servers (miq\_server)

These methods are available to the {product-title} Server.

| Method         | Use                                           |
| -------------- | --------------------------------------------- |
| zone           | Returns {product-title} Servers Zone          |
| region\_number | Returns {product-title} Servers Region Number |
| region\_name   | Returns {product-title} Servers Region Name   |

``` ruby
  #########################
  #
  # Method: dumpServer
  # Inputs: $evm.root['miq_server']
  # Description: Dump MIQ Server information
  #
  ##########################
  def dumpServer
    $evm.log("info","#{@method} - Server:<#{$evm.root['miq_server'].name}> Begin Attributes")
    $evm.root['miq_server'].attributes.sort.each { |k, v| $evm.log("info", "#{@method} - Server:<#{$evm.root['miq_server'].name}> Attributes - #{k}: #{v.inspect}")}
    $evm.log("info","#{@method} - Server:<#{$evm.root['miq_server'].name}> End Attributes")
    $evm.log("info", "")
  end
```

## Network (network)

| Method        | Use                            |
| ------------- | ------------------------------ |
| hardware      | Returns object’s hardware      |
| guest\_device | Returns object’s guest devices |

## PXE Image (pxe\_image)

| Method                   | Use                                      |
| ------------------------ | ---------------------------------------- |
| customization\_templates | Returns object’s customization templates |
| pxe\_server              | Returns object’s pxe server              |

## PXE Server (pxe\_server)

| Method                            | Use                                            |
| --------------------------------- | ---------------------------------------------- |
| advertised\_images                | Returns object’s advertised images             |
| advertised\_pxe\_images           | Returns object’s advertised pxe images         |
| default\_pxe\_image\_for\_windows | Returns object’s default pxe image for windows |
| discovered\_images                | Returns object’s discovered images             |
| discovered\_pxe\_images           | Returns object’s discovered pxe images         |
| images                            | Returns object’s images                        |
| pxe\_images                       | Returns object’s pxe\_images                   |
| windows\_images                   | Returns object’s windows images                |

## Security Groups (security\_group)

| Method                  | Use                                |
| ----------------------- | ---------------------------------- |
| ext\_management\_system | Returns object’s Management System |
| cloud\_network          | Returns object’s cloud network     |
| cloud\_tenant           | Returns object’s cloud tenant      |
| firewall\_rules         | Returns object’s firewall rules    |
| vms                     | Returns object’s VMs               |

## Services (service)

| Method                          | Use                                                                         |
| ------------------------------- | --------------------------------------------------------------------------- |
| custom\_keys                    | Returns custom keys                                                         |
| customer\_get                   | Gets Value for specified custom key                                         |
| custom\_set(attribute, value)   | Sets value for specified custom key                                         |
| display=(display)               | Set display option                                                          |
| group=(group)                   | Sets group that owns the service                                            |
| name=(new\_name)                | Sets name of service                                                        |
| owner=(owner)                   | Sets owner of the service                                                   |
| retire\_now                     | Retire Service immediately                                                  |
| retirement\_warn=(seconds)      | Sets when to send retirement warning                                        |
| retires\_on=(date)              | Sets retirement date                                                        |
| shutdown\_guest                 | Shuts downs guest operating system of the Service                           |
| start                           | Start the Service                                                           |
| stop                            | Stop the Service                                                            |
| suspend                         | Suspend the Service                                                         |
| vms                             | Show all virtual machines associated with this service                      |
| direct\_vms                     | Show virtual machines directly associated with this service                 |
| indirect\_vms                   | Show virtual machines associated with lower level services in the hierarchy |
| root\_service                   | Show the top level service in the hierarchy for the target service          |
| all\_service\_children          | Show all lower level services to the target service in the hierarchy        |
| direct\_service\_children       | Show direct services associated with the target service                     |
| indirect\_service\_children     | Show services associated with lower level services of the target service    |
| parent\_service                 | Show the parent service for the target service                              |
| description=(new\_description)  | Sets the service description                                                |
| remove\_from\_vmdb              | Delete the service from the database                                        |
| dialog\_options                 | Returns all dialog options                                                  |
| get\_dialog\_option(key)        | Returns a specific dialog option specified by `key`                         |
| set\_dialog\_option(key, value) | Sets `value` of a dialog option specified by `key`                          |

## Service Resource (service\_resource)

| Method            | Use                                     |
| ----------------- | --------------------------------------- |
| service           | Returns the associated service          |
| service\_template | Returns the associated service template |
| resource          | Returns the resource for the request    |
| source            | Returns the source object               |

## Service Template (service\_template)

| Method        | Use                                 |
| ------------- | ----------------------------------- |
| group=(group) | Sets group for the service template |
| owner=(owner) | Sets owner for the service template |

## Snapshot (snapshot)

These methods can be used on Snapshots

| Method                 | Use                                           |
| ---------------------- | --------------------------------------------- |
| vm                     | Returns Snapshots VM                          |
| current?               | Checks to see if this is the current snapshot |
| get\_current\_snapshot | Returns the current snapshot id               |
| revert\_to             | Reverts to specified snapshot                 |
| remove                 | Removes specified snapshot                    |

## Datastores (storage)

| Method                   | Use                                            |
| ------------------------ | ---------------------------------------------- |
| ext\_management\_systems | Returns object’s Management System             |
| hosts                    | Returns object’s Hosts                         |
| vms                      | Returns object’s Virtual Machines              |
| unregistered\_vms        | Returns object’s unregistered Virtual Machines |
| to\_s                    | Converts object to string                      |
| scan                     | Performs SmartState Analysis on the object     |

``` ruby
  #########################
  #
  # Method: dumpStorage
  # Inputs: $evm.root['storage']
  # Description: Dump Storage information
  #
  ##########################

  def dumpStorage(storage)
    $evm.log("info","#{@log_prefix} - Storage:<#{storage.name}> Begin Attributes")
    storage.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - Storage:<#{storage.name}> Attributes - #{k}: #{v.inspect}")}
    $evm.log("info","#{@log_prefix} - Storage:<#{storage.name}> End Attributes")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Storage:<#{storage.name}> Begin Associations")
    storage.associations.sort.each { |assc| $evm.log("info", "#{@log_prefix} - Storage:<#{storage.name}> Associations - #{assc}")}
    $evm.log("info","#{@log_prefix} - Storage:<#{storage.name}> End Associations")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - Storage:<#{storage.name}> Begin Virtual Columns")
    storage.virtual_column_names.sort.each { |vcn| $evm.log("info", "#{@log_prefix} - Storage:<#{storage.name}> Virtual Columns - #{vcn}: #{storage.send(vcn)}")}
    $evm.log("info","#{@log_prefix} - Storage:<#{storage.name}> End Virtual Columns")
    $evm.log("info","")
  end
```

## Switch (switch)

These methods can be used on Switches.

| Method         | Use                            |
| -------------- | ------------------------------ |
| host           | Returns switch’s Host          |
| guest\_devices | Returns switch’s guest devices |
| lans           | Returns switch’s lans          |

## User (user)

These methods can be used on the currently logged on user.

| Method                       | Use                                               |
| ---------------------------- | ------------------------------------------------- |
| current\_group               | Returns user’s assigned internal group            |
| custom\_get(key)             | Returns the custom key value specified by "key"   |
| custom\_keys                 | Returns an array of custom keys                   |
| custom\_set(key,value)       | Sets custom value for "key" to "value"            |
| email                        | Returns user’s email address                      |
| get\_ladap\_attribute(name)  | Returns the value of the specified LDAP attribute |
| get\_ldap\_atttribute\_names | Returns user’s LDAP attribute names               |
| ldap\_group                  | Returns user’s assigned LDAP group                |
| miq\_requests                | Returns user’s requests                           |
| name                         | Returns user’s name                               |
| userid                       | Returns user’s userid                             |
| vms                          | Returns Virtual Machines that this user owns      |

``` ruby
  #########################
  #
  # Method: dumpUser
  # Inputs: $evm.root['user']
  # Description: Dump User information
  #
  ##########################

  def dumpUser
    user = $evm.root['user']
    unless user.nil?
      $evm.log("info","#{@method} - User:<#{user.name}> Begin Attributes [user.attributes]")
      user.attributes.sort.each { |k, v| $evm.log("info", "#{@method} - User:<#{user.name}> Attributes - #{k}: #{v.inspect}")}
      $evm.log("info","#{@method} - User:<#{user.name}> End Attributes [user.attributes]")
      $evm.log("info", "")

      $evm.log("info","#{@method} - User:<#{user.name}> Begin Associations [user.associations]")
      user.associations.sort.each { |assc| $evm.log("info", "#{@method} - User:<#{user.name}> Associations - #{assc}")}
      $evm.log("info","#{@method} - User:<#{user.name}> End Associations [user.associations]")
      $evm.log("info","")

      $evm.log("info","#{@method} - User:<#{user.name}> Begin Virtual Columns [user.virtual_column_names]")
      user.virtual_column_names.sort.each { |vcn| $evm.log("info", "#{@method} - User:<#{user.name}> Virtual Columns - #{vcn}: #{user.send(vcn).inspect}")}
      $evm.log("info","#{@method} - User:<#{user.name}> End Virtual Columns [user.virtual_column_names]")
      $evm.log("info","")
    end
  end
```

## Virtual Machines and Templates (vm\_or\_template)

The following methods can be used on a virtual machine or template
object.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>changed_vm_value?</p></td>
<td><p>Checks the 2 most recent drift state captures, and answers whether the specified value changed between them</p></td>
</tr>
<tr class="even">
<td><p>collect_running_processes</p></td>
<td><p>Collects the running processes of the object</p></td>
</tr>
<tr class="odd">
<td><p>create_snapshot(name, desc = nil)</p></td>
<td><p>Create a snapshot of the object</p></td>
</tr>
<tr class="even">
<td><p>custom_get(key)</p></td>
<td><p>Get the value of specified {product-title} Server key from the object</p></td>
</tr>
<tr class="odd">
<td><p>custom_keys</p></td>
<td><p>List all {product-title} Server custom keys for the object</p></td>
</tr>
<tr class="even">
<td><p>custom_set(key, value)</p></td>
<td><p>Set a custom {product-title} Server key value</p></td>
</tr>
<tr class="odd">
<td><p>datacenter</p></td>
<td><p>Returns object’s Datacenter</p></td>
</tr>
<tr class="even">
<td><p>direct_service</p></td>
<td><p>Show the direct service relationship of the virtual machine</p></td>
</tr>
<tr class="odd">
<td><p>directories</p></td>
<td><p>Returns number of directories on the object</p></td>
</tr>
<tr class="even">
<td><p>ems_blue_folder (this will be reworked to be more VMware-specific)</p></td>
<td><p>Returns object’s blue folder from VMware. These are the folders showing in VM and Templates view in VMware</p></td>
</tr>
<tr class="odd">
<td><p>ems_cluster</p></td>
<td><p>Returns object’s cluster</p></td>
</tr>
<tr class="even">
<td><p>ems_custom_get(key)</p></td>
<td><p>Gets specified key of custom Management System Attribute</p></td>
</tr>
<tr class="odd">
<td><p>ems_custom_keys</p></td>
<td><p>List the custom keys defined by the Management System for the object</p></td>
</tr>
<tr class="even">
<td><p>ems_custom_set(attribute, value)</p></td>
<td><p>Sets specified key and value of custom Management System Attribute</p></td>
</tr>
<tr class="odd">
<td><p>ems_folder</p></td>
<td><p>Returns object’s folder on Management System</p></td>
</tr>
<tr class="even">
<td><p>ems_ref_string</p></td>
<td><p>Returns unique identifier the Management System uses to identify this resource. For example, in VMware a VM would return a value like: <code>vm-26622</code></p></td>
</tr>
<tr class="odd">
<td><p>event_log_threshold? (options)</p></td>
<td><p>Searches event log records to determine if an event has occurred x number of times within a defined time frame. Returns true if the number of matching records found are greater or equal to the specified freq_threshold, otherwise it returns false</p>
<p><em>Options:</em></p>
<p><strong>:message_filter_type</strong> - Must be one of "STARTS WITH", "ENDS WITH", "INCLUDES", "REGULAR EXPRESSION"</p>
<p><strong>:message_filter_value</strong> - &lt;string value to search for&gt;</p>
<p><strong>:time_threshold</strong> - Options time interval to search. Example: 2.days (Search the past 2 days of event logs) Default 10.days</p>
<p><strong>:freq_threshold</strong> - Number of occurrences to check for. Default = 2</p>
<p><strong>:source</strong>, <strong>:event_id</strong>, <strong>:level</strong>, <strong>:name</strong> - Options filter values</p></td>
</tr>
<tr class="even">
<td><p>event_threshold?(options)</p></td>
<td><p>Checks if an event (or multiple events) have occurred X number of times in N seconds. The values below are used if no data is passed</p>
<p><em>Example:</em></p>
<p><code>event_threshold?(options = {:time_threshold ⇒ 30.minutes, :event_types ⇒ ["MigrateVM_Task_Complete"], :freq_threshold ⇒ 2})</code></p></td>
</tr>
<tr class="odd">
<td><p>ext_management_system</p></td>
<td><p>Returns object’s Management System</p></td>
</tr>
<tr class="even">
<td><p>files</p></td>
<td><p>Returns number of files on the object</p></td>
</tr>
<tr class="odd">
<td><p>get_realtime_metric(metric, range, function)</p></td>
<td><p>Returns specified realtime metric</p></td>
</tr>
<tr class="even">
<td><p>group=(group)</p></td>
<td><p>Sets object’s group</p></td>
</tr>
<tr class="odd">
<td><p>guest_applications</p></td>
<td><p>Returns object’s Guest Application list</p></td>
</tr>
<tr class="even">
<td><p>hardware</p></td>
<td><p>Returns object’s Hardware</p></td>
</tr>
<tr class="odd">
<td><p>host</p></td>
<td><p>Returns object’s Host</p></td>
</tr>
<tr class="even">
<td><p>migrate(host, pool = nil, priority = "defaultPriority", state = nil)</p></td>
<td><p>Migrates the object to another host. The only required parameter is host</p></td>
</tr>
<tr class="odd">
<td><p>miq_provision</p></td>
<td><p>If VM was created using {product-title} Server provisioning, this is the miq_provision task instance that created the VM</p></td>
</tr>
<tr class="even">
<td><p>operating_system</p></td>
<td><p>Returns object’s Operating System</p></td>
</tr>
<tr class="odd">
<td><p>owner</p></td>
<td><p>Return object’s owner</p></td>
</tr>
<tr class="even">
<td><p>owner=(owner)</p></td>
<td><p>Sets object’s owner</p></td>
</tr>
<tr class="odd">
<td><p>performances_maintains_value_for_duration?</p></td>
<td><p>Based on options given, checks to see if a performance threshold is maintained for a time period</p>
<p><em>Example:</em></p>
<p><code>vm.performances_maintains_value_for_duration?(:column ⇒ "cpu_usage_rate_average", :operator ⇒ "=", :value ⇒ 3.51, :duration ⇒ 20.minutes)</code></p></td>
</tr>
<tr class="even">
<td><p>reboot_guest</p></td>
<td><p>Reboots the guest operating system</p></td>
</tr>
<tr class="odd">
<td><p>reconfigured_hardware_value?</p></td>
<td><p>Checks if hardware value has been reconfigured</p></td>
</tr>
<tr class="even">
<td><p>refresh</p></td>
<td><p>Refresh power states and relationships of the object</p></td>
</tr>
<tr class="odd">
<td><p>registered?</p></td>
<td><p>Is the object registered?</p></td>
</tr>
<tr class="even">
<td><p>remove_all_snapshots</p></td>
<td><p>Remove all of the object’s snapshots</p></td>
</tr>
<tr class="odd">
<td><p>remove_from_disk</p></td>
<td><p>Removes the object from disk</p></td>
</tr>
<tr class="even">
<td><p>remove_from_vmdb</p></td>
<td><p>Removes the object from the VMDB</p></td>
</tr>
<tr class="odd">
<td><p>remove_snapshot(snapshot_id)</p></td>
<td><p>Remove a specific snapshot based on the snapshot_id</p></td>
</tr>
<tr class="even">
<td><p>resource_pool</p></td>
<td><p>Returns object’s Resource Pool</p></td>
</tr>
<tr class="odd">
<td><p>retire_now</p></td>
<td><p>Retire the object immediately</p></td>
</tr>
<tr class="even">
<td><p>retirement_warn=(seconds)</p></td>
<td><p>Send a retirement warning</p></td>
</tr>
<tr class="odd">
<td><p>retires_on=(date)</p></td>
<td><p>Retire the object on date specified</p></td>
</tr>
<tr class="even">
<td><p>revert_to_snapshot(snapshot_id)</p></td>
<td><p>Revert to a snapshot based on the snapshot_id</p></td>
</tr>
<tr class="odd">
<td><p>scan(scan_categories = nil)</p></td>
<td><p>Perform SmartState Analysis on the object. Scan_categories is optional</p></td>
</tr>
<tr class="even">
<td><p>service</p></td>
<td><p>Show the top-level service for a virtual machine in a service hierarchy. For the immediate parent service relationship of a virtual machine, use direct_service</p></td>
</tr>
<tr class="odd">
<td><p>shutdownGuest</p></td>
<td><p>Shuts down the guest operating system of the object</p></td>
</tr>
<tr class="even">
<td><p>snapshots</p></td>
<td><p>Returns list of snapshots for the object</p></td>
</tr>
<tr class="odd">
<td><p>standby_guest</p></td>
<td><p>Puts the operating system on standby</p></td>
</tr>
<tr class="even">
<td><p>start</p></td>
<td><p>Starts the object. See Samples/PowerOn_DHOB</p></td>
</tr>
<tr class="odd">
<td><p>stop</p></td>
<td><p>Stops the object</p></td>
</tr>
<tr class="even">
<td><p>storage</p></td>
<td><p>Returns object’s Datastore</p></td>
</tr>
<tr class="odd">
<td><p>suspend</p></td>
<td><p>Suspends the object</p></td>
</tr>
<tr class="even">
<td><p>to_s</p></td>
<td><p>Converts object to string</p></td>
</tr>
<tr class="odd">
<td><p>unlink_storage</p></td>
<td><p>Removes the reference to the VM’s Datastore</p></td>
</tr>
<tr class="even">
<td><p>unregister</p></td>
<td><p>Unregisters the object from the Management System</p></td>
</tr>
</tbody>
</table>

``` ruby
  #########################
  #
  # Method: dumpVM
  # Inputs: $evm.root['vm']
  # Description: Dump VM information
  #
  ##########################

  def dumpVM(vm)
    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Attributes [vm.attributes]")
    vm.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Attributes - #{k}: #{v.inspect}")}
    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Attributes [vm.attributes]")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Associations [vm.associations]")
    vm.associations.sort.each { |assc| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Associations - #{assc}")}
    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Associations [vm.associations]")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Hardware Attributes [vm.hardware]")
    vm.hardware.attributes.each { |k,v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Hardware - #{k}: #{v.inspect}")}
    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Hardware Attributes [vm.hardware]")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Hardware Associations [vm.hardware.associations]")
    vm.hardware.associations.sort.each { |assc| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> hardware Associations - #{assc}")}
    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End hardware Associations [vm.hardware.associations]")
    $evm.log("info","")

    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Neworks [vm.hardware.nics]")
    vm.hardware.nics.each { |nic| nic.attributes.sort.each { |k,v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> VLAN:<#{nic.device_name}> - #{k}: #{v.inspect}")}}
    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Networks [vm.hardware.nics]")
    $evm.log("info","")

    unless vm.ext_management_system.nil?
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin EMS [vm.ext_management_system]")
      vm.ext_management_system.attributes.sort.each { |ems_k, ems_v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> EMS:<#{vm.ext_management_system.name}> #{ems_k} - #{ems_v.inspect}")}
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End EMS [vm.ext_management_system]")
      $evm.log("info","")
    end

    unless vm.owner.nil?
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Owner [vm.owner]")
      vm.owner.attributes.each { |k,v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Owner - #{k}: #{v.inspect}")}
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Owner [vm.owner]")
      $evm.log("info","")
    end

    unless vm.operating_system.nil?
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Operating System [vm.operating_system]")
      vm.operating_system.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Operating System - #{k}: #{v.inspect}")}
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Operating System [vm.operating_system]")
      $evm.log("info","")
    end

    unless vm.guest_applications.nil?
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Guest Applications")
      vm.guest_applications.each { |guest_app| guest_app.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Guest Application:<#{guest_app.name}> - #{k}: #{v.inspect}")}} unless vm.guest_applications.nil?
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Guest Applications")
      $evm.log("info","")
    end

    unless vm.snapshots.nil?
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Snapshots")
      vm.snapshots.each { |ss| ss.attributes.sort.each { |k, v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Snapshot:<#{ss.name}> - #{k}: #{v.inspect}")}} unless vm.snapshots.nil?
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Snapshots")
      $evm.log("info","")
    end

    unless vm.storage.nil?
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin VM Storage [vm.storage]")
      vm.storage.attributes.sort.each { |stor_k, stor_v| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Storage:<#{vm.storage.name}> #{stor_k} - #{stor_v.inspect}")}
      $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End VM Storage [vm.storage]")
      $evm.log("info","")
    end

    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> Begin Virtual Columns -----")
    vm.virtual_column_names.sort.each { |vcn| $evm.log("info", "#{@log_prefix} - VM:<#{vm.name}> Virtual Columns - #{vcn}: #{vm.send(vcn).inspect}")}
    $evm.log("info","#{@log_prefix} - VM:<#{vm.name}> End Virtual Columns -----")
    $evm.log("info","")
  end
```

``` ruby
  ####################
  #
  # Method: createSnapshot
  #
  ####################

  def createSnapshot(vm, snap_name, snap_desc=snap_name)
    $evm.log("info","#{@method} - VM:<#{vm.name}> Creating Snapshot:<#{snap_name}> Description:<#{snap_desc}>")
    vm.create_snapshot(snap_name, snap_desc)
  end
```

### VMs (vm)

| Method                    | Use                                    |
| ------------------------- | -------------------------------------- |
| add\_to\_service(service) | Adds the VM to a service object        |
| remove\_from\_service     | Removes the VM from its parent service |

The following table lists the metric types available for the
`get_realtime_metric(metric, range, function)` method for virtual
machines.

| Metric                               | Description                                                          |
| ------------------------------------ | -------------------------------------------------------------------- |
| v\_derived\_storage\_used            | Capacity - Used space in bytes                                       |
| v\_pct\_cpu\_ready\_delta\_summation | CPU - Percentage ready                                               |
| v\_pct\_cpu\_wait\_delta\_summation  | CPU - Percentage wait                                                |
| v\_pct\_cpu\_used\_delta\_summation  | CPU - Percentage used                                                |
| v\_derived\_vm\_count                | State - Peak average virtual machines (Hourly Count / Daily Average) |
| v\_derived\_cpu\_reserved\_pct       | CPU - Percentage available                                           |
| v\_derived\_memory\_reserved\_pct    | Memory - Percentage available                                        |

The following Ruby snippet demonstrates using the
`get_realtime_metric(metric, range, function)` method using the
`v_pct_cpu_ready_delta_summation` metric.

``` ruby
host = $evm.root['vm']
cpu_rdy = vm.get_realtime_metric(:v_pct_cpu_ready_delta_summation, [15.minutes.ago.utc,5.minutes.ago.utc], :avg)
```

### VMs for Clouds (vm\_cloud)

| Method             | Use                                |
| ------------------ | ---------------------------------- |
| availability\_zone | Returns object’s availability zone |
| flavor             | Returns object’s favor             |
| cloud\_network     | Returns object’s cloud network     |
| cloud\_subnet      | Returns object’s cloud subnet      |
| floating\_ip       | Returns object’s floating IPs      |
| security\_groups   | Returns object’s security groups   |
| key\_pairs         | Returns object’s key pairs         |

## Windows Image (windows\_image)

| Method                   | Use                                         |
| ------------------------ | ------------------------------------------- |
| customization\_templates | Returns the images customization templates. |
| pxe\_server              | Returns the images pxe server.              |

## Creating Categories and Tags

These methods are invoked using $evm.execute. See after the table for
usage examples.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method(<em>parameter</em>)</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>category_exists?</p></td>
<td><p>Checks to see if a tag category exists. Usually used with unless or if to then create a category that does not exist.</p>
<p><em>Example:</em></p>
<p><code>$evm.execute('category_exists?', "department")</code></p></td>
</tr>
<tr class="even">
<td><p>category_create</p></td>
<td><p>Creates a new category and sets if only one tag value from this category can be assigned to a configuration item (using the single_value option).</p>
<p><em>Example:</em></p>
<p><code>$evm.execute('category_create', :name ⇒ "department", :single_value ⇒ false, :description ⇒ "Department")</code></p></td>
</tr>
<tr class="odd">
<td><p>tag_exists?</p></td>
<td><p>Checks to see if a tag exists in a category.</p>
<p><em>Example:</em></p>
<p><code>$evm.execute(tag_exists?', "department", finance)</code></p></td>
</tr>
<tr class="even">
<td><p>tag_create</p></td>
<td><p>Creates a new tag in the specified category.</p>
<p><em>Example:</em></p>
<p><code>$evm.execute(tag_create', "department", :name ⇒ "finance", :description ⇒ "Finance")</code></p></td>
</tr>
</tbody>
</table>

### Category and Tags Methods Example

In this example, the VMDB is checked to see if the **Department**
category exists. If it does, then a message is logged. If not, the
category is created and a message is logged. Values are then added to
the category.

``` ruby
if $evm.execute('category_exists?', "department")
  $evm.log("info", "Classification department exists")
else
  $evm.log("info", "Classification department doesn't exist, creating category")
  $evm.execute('category_create', :name => "department", :single_value => false, :description => "Department")
  $evm.log("info", "Adding new tag in Department Category")
  $evm.execute(tag_create', "department", :name => "finance", :description => "Finance")
```

## Quota

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method(<em>parameter</em>)</th>
<th>Use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>vms_by_owner, vms_by_group, vms_by_owner_and_group</p></td>
<td><p>Collect stats about existing VMs by owner or in the same LDAP group as the owner in the current request.</p>
<p><em>Example return object:</em></p>
<p><code>{:class_name⇒"Vm", :count⇒5, :ids⇒[22, 120, 121, 122, 117], :cpu⇒6, :memory⇒5120, :allocated_storage⇒29032972288, :used_storage⇒29032972288}</code></p></td>
</tr>
<tr class="even">
<td><p>retired_vms_by_owner, retired_vms_by_group, retired_vms_by_owner_and_group</p></td>
<td><p>Collect stats about retired VMs, that have not been deleted from the host, by owner or in the same LDAP group as the owner in the current request.</p>
<p><em>Example return object:</em></p>
<p><code>{:class_name⇒"Vm", :count⇒5, :ids⇒[22, 120, 121, 122, 117], :cpu⇒6, :memory⇒5120, :allocated_storage⇒29032972288, :used_storage⇒29032972288}</code></p></td>
</tr>
<tr class="odd">
<td><p>provisions_by_owner, provisions_by_group</p></td>
<td><p>Collect stats based on provisions running on the same day as the current request (based on scheduled date or immediate) by owner or in the same LDAP group as the owner. (Results do not include Provision Requests that have not been approved.)</p>
<p><em>Example return object:</em></p>
<p><code>{:class_name⇒"MiqProvisionRequest", :count⇒6, :ids⇒[115, 116, 104, 102, 105, 112], :cpu⇒6, :memory⇒1536, , :storage⇒62914560}</code></p></td>
</tr>
<tr class="even">
<td><p>requests_by_owner, requests_by_group</p></td>
<td><p>Collect stats based on provision requests made the same day as the request by the same owner or LDAP group as the owner in the current request, regardless of when the provision request is scheduled to run. (Results do not include Provision Requests that have been denied.)</p>
<p><em>Example return object:</em></p>
<p><code>{:class_name⇒"MiqProvisionRequest", :count⇒6, :ids⇒[115, 116, 104, 102, 105, 112], :cpu⇒6, :memory⇒1536, , :storage⇒62914560}</code></p></td>
</tr>
<tr class="odd">
<td><p>active_provisions_by_owner, active_provisions_by_group, active_provisions</p></td>
<td><p>Collect stats based on currently active provision requests by the same owner or LDAP group as the owner in the current request.</p>
<p><em>Example return object:</em></p>
<p><code>{:class_name⇒"MiqProvisionRequest", :count⇒6, :ids⇒[115, 116, 104, 102, 105, 112], :cpu⇒6, :memory⇒1536, , :storage⇒62914560}</code></p></td>
</tr>
</tbody>
</table>
