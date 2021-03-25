---
title: "The API and SDK"
chapter: false
weight: 100
---

The workload security API is a Restful API that you use to make HTTP requests with workload security. The SDK includes a python package to make it easy to use API in python..

The  API references provide a bunch  of APIs to interact with your resources such as:  
 1-Description of operations that you would like to perform.
 2-Request paths, headers, and payloads.  
 3-Provide examples of requests and response messages.


### prepare your environment

     -Network Access to workload security.  
     -AN SDK client library,if you don't have have it please visit this link [Python SDK ](https://cloudone.trendmicro.com/docs/workload-security/sdk-python/).  
     -The runtime environment for the programming language of your client library.

### Create API key
In workload security, you need to create an API key to authenticate any request with workload security. When you create an API key you must provide a name, role that associates with the key(auditor, full access...), and expiry date of this key.

      -In the Workload Security console, click Administration > User Management > System API Keys.  
      -Click New and enter the property values for the key.  
      -Click Next. The secret is presented. This is the only time that you can obtain the secret.
      -Copy the secret and securely store it.
      -Click Close.
### Structure of API 
   Basically,The workload security uses API keys for authenticating HTTP request,each request must be included ```api-secret-key``` and it can perform GET & POST requests,the Header will like be classified like this: 
   ```
     -GET /api/(the request you want to do it) HTTP/1.1
     -Host: localhost:4119
     -api-secret-key: 2:vJC6lckDygB6FYURIvR0WK2ZTAhIY8rb0Amy9UMn4mo=
     -api-version: v1
     
   ```
   
### Examples of API and SDK usage

To start exploring the API of workload security,you can visit this link[API reference](https://cloudone.trendmicro.com/docs/workload-security/api-reference/).

 **1-perform GET Request example**  
  An example of GET requests will be list policies. You can visit this link to see API & python SDK for this request [API list policies ](https://cloudone.trendmicro.com/docs/workload-security/api-reference/#operation/listPolicies).
**Use a HTTP Client**  
To send your request,you can use one of these tools
such as postmann,paw,or curl,follow the steps to create your first request:
```

-URL : https://localhost:4119/api/policies  
-First header:
  -Key: api-secret-key
  -Value:<your key secret>
-Second header:
  -Key:api-version
  -Value:v1
  the output of of this request will be
  look like this using curl: curl -X GET https://&nbsp;localhost:4119/api/policies -H 'api-secret-key: 5:W+lC8YHIaYHeQuDbJZLkqwM5b8xjxla2pHtBNoiifF8=' -H 'api-version: v1'
```
**Use a client library**
The following example creates an ```ApiClient``` object that configures authentication with Workload Security. A PoliciesApi object is then created and used to list all policies.
Create a file named ```first_steps_get_example.py``` and copy the following example code to the file:
```
import deepsecurity as api
from deepsecurity.rest import ApiException as api_exception

def get_policies_list(api, configuration, api_version, api_exception):
    """ Gets a list of policies on Workload Security

    :return: A PoliciesApi object that contains a list of policies.
    """
    # Create a PoliciesApi object
    policies_api = api.PoliciesApi(api.ApiClient(configuration))

    # List policies using version v1 of the API
    policies_list = policies_api.list_policies(api_version)
    # View the list of policies
    return policies_list

if __name__ == '__main__':
    # Add Workload Security host information to the api client configuration
    configuration = api.Configuration()
    configuration.host = 'https://&nbsp;192.168.17.149:4119/api'

    # Authentication
    configuration.api_key['api-secret-key'] = '2:l069trAePqPRxZUfBqyw442z1DWm9s4u0F/g9bewnFE='

    # Version
    api_version = 'v1'

    print(get_policies_list(api, configuration, api_version, api_exception))
```
Locate the following code and change the URL and secret key according to your environment:
```
configuration.host = 'https://192.168.17.149:4119/api'
configuration.api_key['api-secret-key'] = '2:l069trAePqPRxZUfBqyw442z1DWm9s4u0F/g9bewnFE='
```
Open a Command Prompt (Windows) or terminal (Linux) and enter the following command:
```
python first_steps_get_example.py
```
 **2-perform POST Request example**   
 The example of POST request will be search firewall rules.You can visit this link to see API & python SDK reference this request [API Search firewall rules](https://cloudone.trendmicro.com/docs/workload-security/api-reference/#operation/searchFirewallRules),The API reference also shows a series of parameters that you use in the request body. For Search Firewall Rules, each parameter is a search criterium. In this example we search for the ID of 3.You can use postman or Paw to do POST request..  
 **Use an HTTP client to post**
```
-URL: https://localhost:4119/api/firewallrules/search 
-First header:
  -Key:api-secret-key
  -Value:Your key secret
-Second header:
  -Key: api-version
  -Value:v1
-Third header:
  -Key:Content-Type
  -application/json
also add the following to the body:  
{
  "searchCriteria": [{
    "idTest":"equal",
    "idValue":3
  }]
}

the output of of this request will be
look like this using curl:
curl -X POST https://&nbsp;localhost:4119/api/firewallrules/search \
-H 'Cache-Control: no-cache' \
-H 'api-secret-key: 3:zNi5ag8xPGpfEMElV0GxAIpTs5Ji8BQoCtXaTAgKkVM=' \
-H 'api-version: v1' \
-H 'content-type: application/json' \
-d '{
  "searchCriteria": [{
    "idTest":"equal",
    "idValue":3
  }]
}'
```
 **Use a client library to post**  
 In this example, we will create a SearchFilter object that defines search criteria. The SearchFilter object is then used as a parameter of the searchFirewallRules method of aModuleFirewallApi object.Create file names ```first_steps_post_example.py ``` and copy the following example code to this file :
  ``` 
  import deepsecurity as api
from deepsecurity.rest import ApiException as api_exception

def search_firewall_rules(api, configuration, api_version, api_exception):
    """ Searches the firewall rules for any rule that contains DHCP in the rule name.

    :param api: The Deep Security API modules.
    :param configuration: Configuration object to pass to the api client.
    :param api_version: The version of the API to use.
    :param api_exception: The Deep Security API exception module.
    :return: A list containing all firewall rules that match the search criteria.

    """

    # Define the search criteria
    search_criteria = api.SearchCriteria()
    search_criteria.field_name = "name"
    search_criteria.string_value = "%DHCP%"
    search_criteria.string_test = "equal"
    search_criteria.string_wildcards = True

    # Create search filter to find the rule
    search_filter = api.SearchFilter(None,[search_criteria])

    # Create a FirewallRulesApi object
    firewall_rules_api = api.FirewallRulesApi(api.ApiClient(configuration))

    # Perform the search
    firewall_rules = firewall_rules_api.search_firewall_rules(api_version, search_filter=search_filter)
    firewall_rules_list = []
    for rule in firewall_rules.firewall_rules:
        firewall_rules_list.append(rule)

    return firewall_rules

if __name__ == '__main__':
    # Add Workload Security host information to the api client configuration
    configuration = api.Configuration()
    configuration.host = 'https://192.168.17.149:4119/api'

    # Authentication
    configuration.api_key['api-secret-key'] = '2:l069trAePqPRxZUfBqyw442z1DWm9s4u0F/g9bewnFE='

    # Version
    api_version = 'v1'
    print(search_firewall_rules(api, configuration, api_version, api_exception))
    
 ```
Locate the following codes below and change the URL of secret key that you already created for your environment:
 ```
 configuration.host = 'https://192.168.17.149:4119/api'</code></li>
configuration.api_key['api-secret-key'] = '2:l069trAePqPRxZUfBqyw442z1DWm9s4u0F/g9bewnFE='
 ```
 Open a Command Prompt (Windows) or terminal (Linux) and enter the following command:  
  ```
  python first_steps_post_example.py
 ```
Congrats!!! :satisfied: you have been successfully finished API section.. see you in next section :alien: