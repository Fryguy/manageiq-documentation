You can also configure {product-title\_short} to perform a *SmartState
Analysis*. This type of analysis collects details such as accounts,
drivers, network information, hardware, and security patches on assets
managed by the OpenStack provider. Enabling SmartState Analysis involves
two steps:

1.  [Configuring {product-title\_short} Capacity and
    Utilization](#cf-caputils), and

2.  [Enabling SmartState Analysis](#cf-smartproxy)

These steps are required to allow {product-title\_short} to collect
metrics from OpenStack and use them to perform a SmartState analysis.
You can choose different servers to perform either function; the
following sections assume that you will.

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
Collection](https://access.redhat.com/documentation/en/red-hat-cloudforms/4.1/deployment-planning-guide/#capacity_and_utilization_collection)
from the *Deployment Planning Guide*.

# Enabling SmartState Analysis

After enabling the required server roles, enable SmartState analysis.
See [Smart State Analysis
Support](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/support_matrix/#smart_state_analysis_support)
from the Support Matrix and [Running a SmartState
Analysis](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#running-a-smartstate-analysis)
in the *Managing Providers* guide for more information.

Enabling SmartState analysis is similar to [Configuring
{product-title\_short} Capacity and Utilization](#cf-caputils), in that
the procedure also involves enabling server roles on a specific server.
To do so:

1.  Click i\*Configuration\*.

2.  Select the server to configure from menu:Settings\[Zone\] in the
    left pane of the appliance.

3.  Navigate to the **Server Roles** list in the menu:Server\[Server
    Control\] section. From there, set the appropriate SmartState roles
    to **ON**. Namely:
    
    1.  **SmartProxy**
    
    2.  **SmartState Analysis**

4.  Click **Save**.
