# Overview

Unresolved directive in master.adoc - include::topics/overview.adoc\[\]

# Prerequisites

Unresolved directive in master.adoc -
include::topics/prerequisites.adoc\[\]

# Enabling OpenShift Container Platform Metrics

Unresolved directive in master.adoc -
include::topics/ocp-metrics.adoc\[\]

# Retrieving the OpenShift Container Platform Management Token

Unresolved directive in master.adoc -
include::topics/ocp-retrieve-tokens.adoc\[\]

# Configuring Red Hat CloudForms

Unresolved directive in master.adoc -
include::topics/ocp-config-cfmiq.adoc\[\]

## Enabling SmartState Analysis

After enabling the required server roles, enable SmartState analysis.
See [Smart State Analysis
Support](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/support_matrix/#smart_state_analysis_support)
from the Support Matrix and [Running a SmartState
Analysis](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#running-a-smartstate-analysis)
in the *Managing Providers* guide for more information.

Enabling SmartState analysis is similar to [???](#cf-caputils), in that
the procedure also involves enabling server roles on a specific server.
To do so:

1.  Click i\*Configuration\*.

2.  Select the server to configure from
    <span class="menuchoice">Settings \> Zone</span> in the left pane of
    the appliance.

3.  Navigate to the **Server Roles** list in the
    <span class="menuchoice">Server \> Server Control</span> section.
    From there, set the appropriate SmartState roles to **ON**. Namely:
    
    1.  **SmartProxy**
    
    2.  **SmartState Analysis**

4.  Click **Save**.

# Adding OpenShift Container Platform as a Container Provider

Unresolved directive in master.adoc -
include::topics/add-ocp-provider.adoc\[\]

# Container Image Scanning

Unresolved directive in master.adoc -
include::topics/image-scanning.adoc\[\]
