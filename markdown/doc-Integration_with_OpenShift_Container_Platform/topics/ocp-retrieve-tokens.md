After enabling cluster metrics on your OpenShift Container Platform
deployment, retrieve the *management token* while you are still logged
in to the OpenShift Container Platform host. This will be required later
in [???](#integration).

  - For OpenShift Container Platform 3.3 or later  
    Provide the token needed to add an OpenShift Container Platform 3.3
    (or later) provider.

Run the following to obtain the token needed to add an OpenShift
Container Platform 3.3 (or later) provider:

    # oc sa get-token -n management-infra management-admin
    eyJhbGciOiJSUzI1NiI...

  - For OpenShift Enterprise 3.2  
    Provide the token needed to add an OpenShift Enterprise 3.2
    provider.

Run the following to obtain the token needed to add an OpenShift
Enterprise 3.2 provider:

    # oc sa get-token -n management-infra management-admin
    eyJhbGciOiJSUzI1NiI...

  - For OpenShift Enterprise 3.1  
    Provide the token needed to add an OpenShift Enterprise 3.1
    provider.

Run the following to obtain the token needed to add an OpenShift
Enterprise 3.1 provider:

1.  Obtain the `management` service account token name:
    
        # oc describe sa -n management-infra management-admin
        ...
        Tokens:  management-admin-token-0f3fh
                 management-admin-token-q7a87

2.  Select and describe one of the tokens to retrieve the full token
    output, replacing `management-admin-token-0f3fh` with the name of
    your token:
    
        # oc describe secret -n management-infra management-admin-token-0f3fh
        ...
        Data
        ====
        token:  eyJhbGciOiJSUzI1NiI...
