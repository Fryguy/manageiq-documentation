# OpenShift Prometheus Alerts

<div class="note">

This feature is currently available as a technology preview only. For
more information on the support scope for features marked as technology
preview, see [Technology Preview Features Support
Scope](https://access.redhat.com/support/offerings/techpreview).

</div>

Prometheus is used as an external alerting component.
{product-title\_short} integrates Prometheus alerts for use with
OpenShift Container Platform. {product-title\_short} collects events
from Prometheus, generates alerts based on these events, and then
attaches alerts to inventory objects.

It is possible to view ongoing alerts in {product-title\_short} by
navigating to menu:Monitor\[Alerts\] and manage their life cycle,
including the ability to:

  - View active alerts per provider in the **Overview** screen.

  - View alert data and related objects.

  - Comment, assign, and acknowledge alerts in the **All Alerts**
    screen.

<div class="important">

Network utilization metrics for OpenShift Container Platform are only
collected for `eth0` network interfaces. Therefore, network utilization
trend will not be displayed for network interfaces other than `eth0` on
the overview screen of the provider.

</div>

## Configuring Prometheus Alerts in {product-title\_short}

Configuring and enabling Prometheus alerts in {product-title\_short}
comprises the following steps:

1.  Deploying and configuring Prometheus on OpenShift.

2.  Assigning Prometheus alert profiles to the enterprise in
    {product-title\_short}.

3.  Adding an OpenShift Containers Provider with a Prometheus alert
    endpoint in {product-title\_short}.

### Deploying and Configuring Prometheus on OpenShift

1.  Deploy Prometheus on OpenShift by following the steps covered in
    [Prometheus on OpenShift Container
    Platform](https://docs.openshift.com/container-platform/3.7/install_config/cluster_metrics.html#openshift-prometheus).

2.  Add Prometheus to an OpenShift cluster and configure alert
    definitions. See the example code block below for configuring alerts
    (currently must be done on the Prometheus side):
    
        $ oc edit configmap -n openshift-metrics prometheus
        # Supported labels:
        # severity: ERROR|WARNING|INFO. defaults to ERROR.
        # Supported annotations:
        # description: The error message displayed on the screen
        # miqTarget: ContainerNode|ExtManagementSystem, defaults to ContainerNode.
        # miqIgnore: "true|false", should ManageIQ pick up this alert, defaults to true.
          prometheus.rules: |
            groups:
            - name: example-rules
              interval: 30s # defaults to global interval
              rules:
              - alert: "NodeDown" << Alert starts here
                expr: up{job="kubernetes-nodes"} == 0
                annotations:
                  miqTarget: "ContainerNode"
                  severity: "ERROR"
                  url: "https://www.example.com/node_down_fixing_instructions"
                  description: "Node {{$labels.instance}} is down"
              - alert: "TooManyRequests"
                expr: rate(authenticated_user_requests[2m]) > 12
                annotations:
                  miqTarget: "ExtManagementSystem"
                  severity: "ERROR"
                  url: "https://www.example.com/too_many_requests_fixing_instructions"
                  description: "Too many authenticated requests"

3.  Reload the Prometheus configuration. You can do this by deleting the
    Prometheus pod, then redeploying with the new configuration.

### Assigning Prometheus Alert Profiles to the Enterprise

Complete the following procedure to assign Prometheus alert profiles to
the enterprise using the {product-title\_short} user interface.

<div class="note">

Both Node and Provider alert profiles are created automatically during
the installation, so it is not required to create these profiles.

</div>

1.  Navigate to menu:Control\[Explorer\], then click **Alert Profiles**
    in the accordion menu.

2.  Click to expand **Node Alert Profiles**, then click **Prometheus
    Node Profile**.

3.  Click ![Configuration](1847.png) (**Configuration**), then click
    ![1851](1851.png) (**Edit assignments for this Alert Profile**).
    Assign the profile to **The Enterprise** from the **Assign To**
    list.

4.  Click **Save**.

5.  Click to expand **Provider Alert Profiles**, then click **Prometheus
    Provider Profile**.

6.  Click **Configuration**, then click **Edit assignments for this
    Alert Profile**. Assign the profile to **The Enterprise** from the
    **Assign To** list.

7.  Click **Save**.
    
    <div class="note">
    
    Alerts triggered before assigning the profiles to the enterprise
    will not appear in {product-title\_short} at all.
    
    </div>

### Adding an OpenShift Containers Provider with a Prometheus Alert Endpoint

Complete the following procedure to add an OpenShift Containers Provider
with a Prometheus Alert Endpoint using the {product-title\_short} user
interface.

1.  Navigate to menu:Compute\[Containers \> Providers\].

2.  Click ![Configuration](1847.png) (**Configuration**), then click
    ![Add a New Containers Provider](1862.png) (**Add a New Containers
    Provider**).

3.  Enter a **Name** for the provider.

4.  From the **Type** list, select **OpenShift Container Platform**.

5.  Enter the appropriate **Zone** for the provider. If you do not
    specify a zone, it is set to `default`.

6.  From the **Alerts** list, select **Prometheus** to enable external
    alerts. Selecting **Prometheus** adds an **Alerts** tab to the lower
    pane to configure the Prometheus service. Alerts are disabled by
    default.

7.  From the **Metrics** list, select **Hawkular** or **Prometheus** to
    collect capacity and utilization data, or leave as **Disabled**.
    Selecting **Prometheus** or **Hawkular** adds a **Metrics** tab to
    the lower pane for further configuration. Metrics are disabled by
    default.

8.  In the **Default** tab, configure the following for the OpenShift
    provider:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the provider:
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option.
        
          - **SSL trusting custom CA**: Authenticate the provider with a
            self-signed certificate. For this option, copy your
            provider’s CA certificate to the **Trusted CA
            Certificates** box in PEM format.
            
            <div class="note">
            
            You can obtain your OpenShift Container Platform provider’s
            CA certificate for all endpoints (default, metrics, alerts)
            from `/etc/origin/master/ca.crt`. Paste the output (a block
            of text starting with `-----BEGIN CERTIFICATE-----`) into
            the **Trusted CA Certificates** field.
            
            </div>
        
          - **SSL without validation**: Authenticate the provider
            insecurely (not recommended).
    
    2.  Enter the **Hostname** (or IPv4 or IPv6 address) of the
        provider.
        
        <div class="important">
        
        The **Hostname** must use a unique fully qualified domain name.
        
        </div>
    
    3.  Enter the **API Port** of the provider. The default port is
        `8443`.
    
    4.  Enter a token for your provider in the **Token** box.
        
        <div class="note">
        
        To obtain a token for your provider, run the `oc get secret`
        command on your provider; see [Obtaining an OpenShift Container
        Platform Management
        Token](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/managing_providers/#Obtaining_OpenShift_Container_Platform_Management_Token).
        
        For example:
        
        \# oc get secret --namespace management-infra
        management-admin-token-8ixxs --template='{{index .data
        "ca.crt"}}' | base64 --decode
        
        </div>
    
    5.  Click **Validate** to confirm that {product-title} can connect
        to the OpenShift Container Platform provider.

9.  For the **Prometheus** alerts service, add the Prometheus alerts
    endpoint in the **Alerts** tab:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the service:
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option.
        
          - **SSL trusting custom CA**: Authenticate the provider with a
            self-signed certificate. For this option, copy your
            provider’s CA certificate to the **Trusted CA
            Certificates** box in PEM format.
        
          - **SSL without validation**: Authenticate the provider
            insecurely using SSL. (Not recommended)
    
    2.  Enter the **Hostname** (or IPv4 or IPv6 address) or alert
        **Route**.
    
    3.  Enter the **API Port** if your Prometheus provider uses a
        non-standard port for access. The default port is `443`.
    
    4.  Click **Validate** to confirm that {product-title\_short} can
        connect to the alerts service.

10. If you selected a metrics service, configure the service details in
    the **Metrics** tab:
    
    1.  Select a **Security Protocol** method to specify how to
        authenticate the service:
        
          - **SSL**: Authenticate the provider securely using a trusted
            Certificate Authority. Select this option if the provider
            has a valid SSL certificate and it is signed by a trusted
            Certificate Authority. No further configuration is required
            for this option.
        
          - **SSL trusting custom CA**: Authenticate the provider with a
            self-signed certificate. For this option, copy your
            provider’s CA certificate to the **Trusted CA
            Certificates** box in PEM format.
            
            <div class="note">
            
            In OpenShift, the default deployment of the router generates
            certificates during installation, which can be used with the
            **SSL trusting custom CA** option. Connecting a Hawkular
            endpoint with this option requires the CA certificate that
            the cluster uses for service certificates, which is stored
            in `/etc/origin/master/service-signer.crt` on the first
            master in a cluster.
            
            </div>
        
          - **SSL without validation**: Authenticate the provider
            insecurely using SSL. (Not recommended)
    
    2.  Enter the **Hostname** (or IPv4 or IPv6 address) of the
        provider, or use the **Detect** button to find the hostname.
    
    3.  Enter the **API Port** if your Hawkular or Prometheus provider
        uses a non-standard port for access. The default port is `443`.
    
    4.  Click **Validate** to confirm that {product-title} can connect
        to the metrics endpoint.

11. Click the **Advanced** tab to add image inspector settings for
    scanning container images on your provider using OpenSCAP.
    
    <div class="note">
    
      - These settings control downloading the image inspector container
        image from the registry and obtaining the Common Vulnerabilities
        and Exposures (CVE) information (for effective scanning) via a
        proxy.
    
      - CVE URL that {product-title\_short} requires to be open for
        OpenSCAP scanning:
        <https://www.redhat.com/security/data/metrics/ds/>. This
        information is based on the source code of OpenSCAP.
    
    </div>
    
    1.  Enter the proxy information for the provider in either **HTTP**,
        **HTTPS**, or **NO Proxy** depending on your environment.
    
    2.  Enter the **Image-Inspector Repository** information. For
        example, `openshift3/image-inspector`.
    
    3.  Enter the **Image-Inspector Registry** information. For example,
        `registry.access.redhat.com`.
    
    4.  Enter the **Image-Inspector Tag** value. A tag is a mark used to
        differentiate images in a repository, typically by the
        application version stored in the image.
    
    5.  Enter `https://www.redhat.com/security/data/metrics/ds/` in
        **CVE location**.

12. Click **Add**.

<div class="note">

You can also set global default image-inspector settings for all
OpenShift providers in the advanced settings menu by editing the values
under `ems_kubernetes`, instead of setting this for each provider.

For example:

    :image_inspector_registry: registry.access.redhat.com
    :image_inspector_repository: openshift3/image-inspector

</div>

Once you have completed the procedure, you will have OpenShift
Prometheus alerts enabled in {product-title\_short}, and can manage
their life cyle from the menu:Monitor\[Alerts\] screen in the user
interface.
