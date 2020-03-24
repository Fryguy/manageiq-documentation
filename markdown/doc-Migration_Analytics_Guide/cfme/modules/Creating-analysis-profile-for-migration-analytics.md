You must create a VM analysis profile called `default` and assign it to
the vSphere provider in Red Hat CloudForms.

<div class="note">

The name of the analysis profile must be `default` because the default
control policy is called `default`.

If you create an alternate analysis profile, you must create a new
control policy to assign it.

If a `default` analysis profile does not exist or if you have not
created a control profile to assign an alternate analysis profile, no
profile will be used for the analysis scan.

</div>

1.  Log in to the CloudForms user interface.

2.  In the header bar, click ![config gear](config-gear.png)
    (**Configuration**).

3.  Click the **Settings** accordion and then click **Analysis
    Profiles**.

4.  Click **Configuration** and select **Add VM Analysis Profile**.

5.  Fill in the following fields:
    
      - **Name**: `default`. This name is mandatory unless you create a
        control policy to assign an alternate analysis profile.
    
      - **Description**: Enter a description. This field is mandatory.

6.  Click the **File** tab.

7.  In the **File Entry** area, add each line individually and click
    **Save**:
    
        C:/Program Files/Microsoft SQL Server/110
        C:/Program Files/Microsoft SQL Server/120
        C:/Program Files/Microsoft SQL Server/130
        C:/Program Files/Microsoft SQL Server/140
        C:/Program Files/IBM/WebSphere/AppServer
        /etc/group 
        /etc/oraInst.loc 
        /u01/app/oraInventory
        /opt/mssql/bin/mssql-conf
        /usr/sap/hostctrl/exe/saphostctrl
        /etc/.ibm/registry/InstallationManager.dat
        /opt/IBM/WebSphere/AppServer
        /opt/IBM/WebSphere/AppServer/profiles/AppSrv01
        /opt/rh/eap7/root/usr/share/wildfly/domain/configuration/domain.xml
        /opt/rh/eap7/root/usr/share/wildfly/standalone/configuration/standalone.xml
        /opt/tomcat/bin/catalina.sh
        /opt/tomcat/conf/server.xml
        /u01/app/oracle/domains/base/bin/startNodeManager.sh
        /u01/app/oracle/domains/base/startWebLogic.sh
        /home/oracle/oraInventory
        /u01/app/oracle/domains/base/config/config.xml
        /var/lib/pgsql/data/postgresql.conf
    
      - Set **Collect Contents?** to `true`.
    
      - Set **Collect Contents?** to `true`.

8.  Click **Add**.

9.  Navigate to **Compute** → **Infrastructure** → **Providers** and
    select the **vSphere** provider.

10. Click **Policy** → **Manage Policies**.

11. Check **VM SmartState Analysis profile** to enable the new profile.
