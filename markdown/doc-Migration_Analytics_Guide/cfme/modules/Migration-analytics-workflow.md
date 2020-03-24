The following workflow describes how Migration Analytics works.

![Migration Analytics](Migration_Analytics.png)

![20](circle_1.png) In the CloudForms user interface, you perform a
SmartState analysis scan on your VMware virtual machines.

![20](circle_2.png) Data about operating systems and workloads is
collected from the VMware virtual machines.

The following workloads are currently supported:

  - JBoss Core Service Apache HTTP server with `mod_cluster` configured

  - JBoss EAP

  - PostgreSQL

  - SAP HANA

  - Apache Tomcat

  - Oracle Weblogic

  - IBM WebSphere

  - Microsoft SQL

![20](circle_3.png) The data from the VMware virtual machines is
collected in an inventory data file, which you can download to your
local machine to view.

![20](circle_4.png) In a browser, you navigate to the [Migration
Analytics service](https://cloud.redhat.com/beta) and create a report.
The Migration Analytics service uploads the inventory data file and
analyzes it.

![20](circle_5.png) The Migration Analytics service generates a report
describing the estimated savings, the complexity of the migration, and
migration recommendations.
