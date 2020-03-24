The below examples illustrate how to use the ManageIQ REST API with the
Client for URLs (cURL), Ruby and Python. All examples shown use the
default admin credentials with insecure methods.

Three basic examples will be shown, a **GET**, a **POST** with a simple
payload and a **GET** with filtering

All examples use IP Address **192.0.2.0** to represent the ManageIQ
appliance, with the default HTTPS port omitted.

  - [cURL](#curl)
    
      - [Example 1: A simple **GET** with cURL](#curl-example1)
    
      - [Example 2: Using **POST** to edit a group with
        cURL](#curl-example2)
    
      - [Example 3: A **GET** using filtering with cURL](#curl-example3)

  - [Ruby](#ruby)
    
      - [Example 1: A simple **GET** with Ruby](#ruby-example1)
    
      - [Example 2: Using **POST** to edit a group with
        Ruby](#ruby-example2)
    
      - [Example 3: A **GET** using filtering with Ruby](#ruby-example3)

  - [Python](#python)
    
      - [Example 1: A simple **GET** with Python](#python-example1)
    
      - [Example 2: Using **POST** to edit a group with
        Python](#python-example2)
    
      - [Example 3: A **GET** using filtering with
        Python](#python-example3)

# cURL

The cURL command can be used from the shell. However the shell’s
interpretation of some characters, for example **&**, can make it
awkward to use for complex cases. To help alleviate this the payload can
be passed to cURL using the **--data** flag, where the JSON payload is
provided in a file.

The JSON returned is formated in the examples using **python -m
json.tool**

## Example 1: A simple **GET** with cURL

Get the collection **groups**

    curl --user admin:smartvm --insecure --request GET https://192.0.2.0/api/groups | python -m json.tool

### Example 1: Result

Result truncated and showing only the returned **resources**.

    {
        ...
        "resources": [
            {
                "href": "https://192.0.2.0/api/groups/2"
            },
            {
                "href": "https://192.0.2.0/api/groups/3"
            },
            ...
            {
                "href": "https://192.0.2.0/api/groups/23"
            }
        ],
        ...
    }

## Example 2: Using **POST** to edit a group with cURL

Edit an instance of the collection **groups**

In this example the payload **data** is read from a file.

    $ cat request.json
    {
      "action" : "edit",
      "resource" : {
        "description" : "updated group description from cURL"
      }
    }

Use the data in file request.json to edit an instance of the collection
**groups**

    curl --data @request.json \
         --header "Content-Type: application/json" \
         --user admin:smartvm \
         --insecure \
         --request POST https://192.0.2.0/api/groups/23 | python -m json.tool

### Example 2: Result

    {
        "created_on": "2019-04-15T19:49:42Z",
        "description": "updated group description from cURL",
        "group_type": "user",
        "href": "https://192.0.2.0/api/groups/23",
        "id": "23",
        "sequence": 22,
        "settings": null,
        "tenant_id": "2",
        "updated_on": "2019-06-19T19:15:51Z"
    }

## Example 3: A **GET** using filtering with cURL

Filtering can be done by passing parameters in the URL. Parameters are
preceded by the **&** character, which can cause problems as the shell
interprets the **&** character as an instruction to: **run this command
in the background**. To avoid this the parameters can instead be passed
to curl using the **--get** flag combined with each parameter being
passed with the **--data** flags.

    curl --user admin:smartvm \
         --insecure \
         --request GET \
         --header "Content-Type: application/json" https://192.0.2.0/api/groups \
         --get \
         --data "expand=resources" \
         --data "attributes=description,miq_user_role_name" \
         --data "filter[]=miq_user_role_name='*user*'" | python -m json.tool

### Example 3: Result

Result truncated and showing only the returned **resources**.

    ...
      "resources": [
          {
              "description": "EvmGroup-user",
              "href": "https://192.0.2.0/api/groups/4",
              "id": "4",
              "miq_user_role_name": "EvmRole-user"
          },
          {
              "description": "EvmGroup-vm_user",
              "href": "https://192.0.2.0/api/groups/9",
              "id": "9",
              "miq_user_role_name": "EvmRole-vm_user"
          },
          {
              "description": "EvmGroup-user_self_service",
              "href": "https://192.0.2.0/api/groups/12",
              "id": "12",
              "miq_user_role_name": "EvmRole-user_self_service"
          },
          {
              "description": "EvmGroup-user_limited_self_service",
              "href": "https://192.0.2.0/api/groups/13",
              "id": "13",
              "miq_user_role_name": "EvmRole-user_limited_self_service"
          }
      ],
    ...

## Ruby

The same three examples shown above are illustrated here using Ruby.

The ManageIQ hostname or IP Address is being made available through the
environment variable **MIQ** :

    export MIQ="192.0.2.0"

### Example 1: A simple **GET** with Ruby

Get the collection **groups**

    #!/usr/bin/env ruby
    
    require 'json'
    require 'net/http'
    require 'openssl'
    require 'uri'
    
    uri = URI.parse("https://#{ENV['MIQ']}/api/groups")
    
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_NONE
    
    request = Net::HTTP::Get.new(uri.request_uri)
    request.basic_auth("admin", "smartvm")
    
    response = http.request(request)
    
    puts "Reply:\n " + JSON.pretty_generate(JSON.parse(response.body.strip))

#### Example 1: Result

Result truncated and showing only the returned **resources**.

    {
        ...
        "resources": [
            {
                "href": "https://192.0.2.0/api/groups/2"
            },
            {
                "href": "https://192.0.2.0/api/groups/3"
            },
            ...
            {
                "href": "https://192.0.2.0/api/groups/23"
            }
        ],
        ...
    }

### Example 2: Using **POST** to edit a group with Ruby

Edit an instance of the collection **groups**

    #!/usr/bin/env ruby
    
    require 'json'
    require 'net/http'
    require 'openssl'
    require 'uri'
    
    uri = URI.parse("https://#{ENV['MIQ']}/api/groups/23")
    
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_NONE
    
    request = Net::HTTP::Post.new(uri.request_uri)
    request.basic_auth("admin", "smartvm")
    request.body = '
    {
      "action" : "edit",
      "resource" : {
        "description" : "updated group description from ruby"
      }
    }
    '
    response = http.request(request)
    puts JSON.pretty_generate(JSON.parse(response.body.strip))

#### Example 2: Result

    {
      "href": "https://192.0.2.0/api/groups/23",
      "id": "23",
      "description": "updated group description from ruby",
      "tenant_id": "2",
      "group_type": "user",
      "sequence": 22,
      "created_on": "2019-04-15T19:49:42Z",
      "updated_on": "2019-06-20T18:55:40Z",
      "settings": null
    }

### Example 3: A **GET** using filtering with Ruby

    #!/usr/bin/env ruby
    
    require 'json'
    require 'net/http'
    require 'openssl'
    require 'uri'
    
    
    expand_resources="expand=resources&attributes=description,miq_user_role_name"
    uri = URI.parse("https://#{ENV['MIQ']}/api/groups/?#{expand_resources}&filter[]=miq_user_role_name='*user*'")
    
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_NONE
    
    request = Net::HTTP::Get.new(uri.request_uri)
    request.basic_auth("admin", "smartvm")
    
    response = http.request(request)
    
    puts "Reply:\n " + JSON.pretty_generate(JSON.parse(response.body.strip))

#### Example 3: Result

Result truncated and showing only the returned **resources**.

    ...
      "resources": [
          {
              "description": "EvmGroup-user",
              "href": "https://192.0.2.0/api/groups/4",
              "id": "4",
              "miq_user_role_name": "EvmRole-user"
          },
          {
              "description": "EvmGroup-vm_user",
              "href": "https://192.0.2.0/api/groups/9",
              "id": "9",
              "miq_user_role_name": "EvmRole-vm_user"
          },
          {
              "description": "EvmGroup-user_self_service",
              "href": "https://192.0.2.0/api/groups/12",
              "id": "12",
              "miq_user_role_name": "EvmRole-user_self_service"
          },
          {
              "description": "EvmGroup-user_limited_self_service",
              "href": "https://192.0.2.0/api/groups/13",
              "id": "13",
              "miq_user_role_name": "EvmRole-user_limited_self_service"
          }
      ],
    ...

## Python

The same three examples shown above are illustrated here using Python.

The ManageIQ hostname or IP Address is being made available through the
environment variable **MIQ** :

    export MIQ="192.0.2.0"

### Example 1: A simple **GET** with Python

Get the collection **groups**

    #!/usr/bin/env python
    
    import requests
    import json
    import os
    
    url = 'https://' + str(os.environ["MIQ"]) + '/api/groups'
    response = requests.get(url, auth=('admin', 'smartvm'), verify=False)
    print("Result:\n" + json.dumps(json.loads(response.text), indent=4, sort_keys=True))

#### Example 1: Result

Result truncated and showing only the returned **resources**.

    {
        ...
        "resources": [
            {
                "href": "https://192.0.2.0/api/groups/2"
            },
            {
                "href": "https://192.0.2.0/api/groups/3"
            },
            ...
            {
                "href": "https://192.0.2.0/api/groups/23"
            }
        ],
        ...
    }

### Example 2: Using **POST** to edit a group with Python

Edit an instance of the collection **groups**

    #!/usr/bin/env python
    
    import requests
    import json
    import os
    
    url = 'https://' + str(os.environ["MIQ"]) + '/api/groups/23'
    
    request_body = { 'action':  'edit', 'resource' : { 'description' : 'updated group description from python' } }
    headers = {'Content-type': 'application/json'}
    response = requests.post(url, data=json.dumps(request_body), headers=headers, auth=('admin', 'smartvm'), verify=False)
    print("Result:\n" + json.dumps(json.loads(response.text), indent=4, sort_keys=True))

#### Example 2: Result

    {
        "created_on": "2019-04-15T19:49:42Z",
        "description": "updated group description from python",
        "group_type": "user",
        "href": "https://192.0.2.0/api/groups/23",
        "id": "23",
        "sequence": 22,
        "settings": null,
        "tenant_id": "2",
        "updated_on": "2019-06-20T20:48:47Z"
    }

### Example 3: A **GET** using filtering with Python

    #!/usr/bin/env python
    
    import requests
    import json
    import os
    
    expand_resources="expand=resources&attributes=description,miq_user_role_name"
    url = "https://" + str(os.environ["MIQ"]) + "/api/groups/?" + str(expand_resources) + "&filter[]=miq_user_role_name='*user*'"
    response = requests.get(url, auth=('admin', 'smartvm'), verify=False)
    print("Result:\n" + json.dumps(json.loads(response.text), indent=4, sort_keys=True))

#### Example 3: Result

Result truncated and showing only the returned **resources**.

    ...
      "resources": [
          {
              "description": "EvmGroup-user",
              "href": "https://192.0.2.0/api/groups/4",
              "id": "4",
              "miq_user_role_name": "EvmRole-user"
          },
          {
              "description": "EvmGroup-vm_user",
              "href": "https://192.0.2.0/api/groups/9",
              "id": "9",
              "miq_user_role_name": "EvmRole-vm_user"
          },
          {
              "description": "EvmGroup-user_self_service",
              "href": "https://192.0.2.0/api/groups/12",
              "id": "12",
              "miq_user_role_name": "EvmRole-user_self_service"
          },
          {
              "description": "EvmGroup-user_limited_self_service",
              "href": "https://192.0.2.0/api/groups/13",
              "id": "13",
              "miq_user_role_name": "EvmRole-user_limited_self_service"
          }
      ],
    ...
