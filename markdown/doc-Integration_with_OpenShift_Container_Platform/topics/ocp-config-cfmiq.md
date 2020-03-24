Configuring {product-title\_short} involves two steps:

1.  [Configuring {product-title\_short} Capacity and
    Utilization](#cf-caputils), and

2.  [???](#cf-smartproxy)

These steps are required to allow {product-title\_short} to collect
metrics from OpenShift Container Platform ([???](#ocp-metrics)) and use
them to perform a SmartState analysis. You can choose different servers
to perform either function; the following sections assume that you will.

# Configuring {product-title\_short} Capacity and Utilization

For metrics collection to work properly, you also need to configure
{product-title} to allow for all three **Capacity & Utilization** server
roles, which are available from the settings menu under
menu:Configuration\[Server \> Server Control\].

To enable these server roles:

1.  Click **Configuration**, then select the server to configure from
    menu:Settings\[Zone\] in the accordion menu on the left.

2.  Navigate to the **Server Roles** list in the menu:Server\[Server
    Control\] section. From there, set the required capacity and
    utilization roles to **ON**, namely:
    
    1.  **Capacity & Utilization Coordinator**
    
    2.  **Capacity & Utilization Data Collector**
    
    3.  **Capacity & Utilization Data Processor**

3.  Click **Save**.

Data collection is enabled immediately. However, the first collection
begins 5 minutes after the server is started, and every 10 minutes after
that. Therefore, the longest the collection takes after enabling the
Capacity & Utilization Collector role is 10 minutes. The first
collection from a particular provider may take a few minutes since
{product-title} is gathering data points going one month back in time.

For more information, see [Capacity and Utilization
Collection](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/deployment_planning_guide/#capacity-and-utilization-collection)
in the *Deployment Planning Guide*.
