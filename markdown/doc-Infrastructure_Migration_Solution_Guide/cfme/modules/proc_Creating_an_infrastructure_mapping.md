The infrastructure mapping maps the resources of your VMware and Red Hat
environments.

<div class="important">

If you add or remove providers or provider objects from an
infrastructure mapping, the mapping will have missing resource errors.
You must delete the infrastructure mapping and create a new one.

</div>

1.  Click **Compute** → **Migration** → **Infrastructure Mappings**.

2.  Click **Create Infrastructure Mapping**. The **Create Infrastructure
    Mapping** wizard is displayed.
    
    ![Creating infrastructure
    mapping](Creating_infrastructure_mapping.png)

3.  In the **General** screen, enter the infrastructure mapping name and
    (optional) description.

4.  Select the **Target Provider** and click **Next**.

5.  Click **Next**.

6.  Click **Add Mapping**. You can map additional datastores.

7.  Click **Next**.

8.  In the **Map Networks** screen, select a source cluster.

9.  Select one or more networks from **Source Provider \\ Datacenter \\
    Network** and **Target Project \\ Network**.

10. Click **Add Mapping**. You can map the networks of additional source
    clusters.

11. Click **Create**.

12. Click **Close**. The infrastructure mapping is saved in **Compute**
    → **Migration** → **Infrastructure Mappings**.

You can click an infrastructure mapping element to view its details:

**Infrastructure Mappings list.**

![Infra mappings list](Infra_mappings_list.png)
