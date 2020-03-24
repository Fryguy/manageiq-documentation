You can verify your conversion hosts in a browser:

1.  In the address bar of a browser, enter the following:
    
        https://<CloudForms_FQDN>/api/conversion_hosts 
    
      - Specify the FQDN of the CloudForms machine.
    
    A log-in screen is displayed.

2.  Enter your CloudForms **Username** and **Password** and click **Sign
    in**.
    
    The conversion hosts and their IDs are displayed in JSON format in
    the output:
    
        {"name":"conversion_hosts","count":3,"subcount":3,"pages":1,"resources":[{"href":"https://cloudforms.example.com/api/conversion_hosts/10000000000001"},{"href":"https://cloudforms.example.com/api/conversion_hosts/10000000000002"},{"href":"https://cloudforms.example.com/api/conversion_hosts/10000000000003"}],"actions":[{"name":"create","method":"post","href":"https://cloudforms.example.com/api/conversion_hosts"},{"name":"edit","method":"post","href":"https://cloudforms.example.com/api/conversion_hosts"},{"name":"delete","method":"post","href":"https://cloudforms.example.com/api/conversion_hosts"}],"links":{"self":"https://cloudforms.example.com/api/conversion_hosts?offset=0","first":"https://cloudforms.example.com/api/conversion_hosts?offset=0","last":"https://cloudforms.example.com/api/conversion_hosts?offset=0"}}
