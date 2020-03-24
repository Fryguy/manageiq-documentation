You can add the cloud-user’s SSH public key to the RHV conversion host
with cloud-init.

  - The conversion host is shut down.

<!-- end list -->

1.  Log in to the Administration Portal.

2.  Click **Compute** \> **Virtual Machines**.

3.  Select the conversion host and click **Edit**.

4.  Click **Show Advanced Options**.

5.  In the **Initial Run** tab, select **Use Cloud-Init/Sysprep**.

6.  Enter the following in **Custom Script**:
    
    ``` yaml
    users:
      - name: cloud-user
        ssh_authorized_keys:
          - <ssh_public_key> 
    ```
    
      - Specify the SSH public key of the cloud-user user.

7.  Click **OK**.
