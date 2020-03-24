You can create a `default` analysis profile for Migration Analytics by
copying the `Sample` analysis profile provided in CloudForms.

<div class="note">

If you create an analysis profile with a name other than `default`, you
must [create a control
policy](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/5.0/html-single/assigning_a_custom_analysis_profile_to_a_virtual_machine/index#create-vm-control-policy)
and assign it to the vSphere provider.

If a `default` analysis profile does not exist or if you have not
created a control policy to assign a different analysis profile, no
profile is used for the scan.

</div>

1.  Log in to the CloudForms user interface.

2.  In the header bar, click ![config gear](config-gear.png)
    (**Configuration**).

3.  Click the **Settings** accordion and then click **Analysis
    Profiles**.

4.  Select the `Sample` analysis profile.

5.  Click **Configuration** → **Copy this selected Analysis Profile**.

6.  Enter `default` in the **Name** field and click **Add**.
    
    The `default` profile appears under **Analysis Profiles**.
