You can add the conversion host’s SSH private key to CloudForms.

If you deploy multiple conversion hosts, all the conversion hosts must
use the same key pair.

1.  Log in to the CloudForms user interface.

2.  Click **Compute** → **Clouds** → **Providers**.

3.  Select the Red Hat OpenStack Platform provider, click
    **Configuration** and select **Edit Selected Cloud Provider.**

4.  Click the **RSA key pair** tab in the **Endpoints** section.

5.  Enter the **Username** `cloud-user` and the **Private Key** of the
    conversion host.
