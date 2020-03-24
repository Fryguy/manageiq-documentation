You can configure Red Hat CloudForms for Migration Analytics.

1.  Log in to the CloudForms user interface.

2.  In the header bar, click ![config gear](config-gear.png)
    (**Configuration**).

3.  Click the **Settings** accordion and then click **Zones**.

4.  Click the zone in which the EVM server is located and select your
    EVM server.

5.  In the **Server** tab, scroll down to **Server Roles**.

6.  Set **SmartProxy** to **On**.
    
    <div class="note">
    
    **SmartState analysis** is **On** by default. Do not change this
    setting.
    
    </div>

7.  In the **Advanced** tab, under `:prototype::migration_analytics:`,
    change the value of the `enabled` parameter to `true`:
    
    ``` yaml
    :prototype:
      :migration_analytics:
        :enabled: true
    ```

8.  Click **Save**.

9.  Log out of the CloudForms user interface.

10. Log in to the CloudForms machine as root.

11. Restart the EVM server:
    
        # systemctl restart evmserverd.service
