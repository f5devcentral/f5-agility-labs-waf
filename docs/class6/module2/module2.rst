Module 2: Viewing and Manipulating the Rest API via curl 
========================================================

Expected time to complete: **1 hours**

**Intro**

If you have experience with another RestFul API, the F5 RestFul API will be very familiar. If you have no familiarity with a RestFul API, don't worry there are only a few key concepts to understand.

The Rest API uses HTTP requests with a combination certain uri and HTTP verbs/commands 

All queries to ASM begin with the uri /mgmt/tm/asm .

For example, querying the uri /mgmt/tm/asm/policies (https://<mgmt ip>/mgmt/tm/asm/policies) will display all asm policies in JSON format.

**Other URIs:**

/mgmt/tm/asm (root asm configuration)

/mgmt/tm/asm/signatures (lists all attack signatures that are installed)

/mgmt/tm/asm/events (lists asm events)

/mgmt/tm/asm/requests (lists asm requests)

/mgmt/tm/asm/policies/MrLpFzRHNarvj_zuAOD0fw (Whoa what is this? Its a way of accessing a policy directly. We will investigate this in detail later.)

HTTP uses commands/verbs such as POST, GET, etc. What roles do they play? HTTP commands determine the operation/type of the request. In other words whether data is simply retrieved or created/modified.

|
|

.. list-table:: HTTP Method Uses
   :widths: 15 45
   :header-rows: 1

   * - METHOD
     - RESULT 
   * - GET
     - retrieves configuration properties or run-time statistics on the resource specified by the URI in the request 
   * - PATCH
     - modifies only the properties of the resource specified in the URI
   * - PUT 
     - modifies the properties of the resource specified in the URI and sets the remaining properties to either default values or empty values
   * - POST
     - creates a new resource based on the URI (eg new ASM policy)     
   * - DELETE
     - deletes a resource based on the URI (eg delete an ASM policy) *Note: this method only takes a URI as an option*

|
|

.. list-table:: HTTP Method Use Cases
                :widths: 15 10 15
                :header-rows: 1

                * - USE CASE
                  - METHOD
                  - Example
                * - Create a new asm policy 
                  - POST
                  - curl -sk -u admin:password -X POST https://<bigip>/mgmt/tm/asm/policies -d '{"name":<policyName>}'
                * - View the settings of the new asm policy
                  - GET
                  - curl -sk -u admin:password -X GET https://<bigip>/mgmt/tm/asm/policies
                * - Add a whitelist ip to the new APM policy
                  - POST
                  - curl -sk -u admin:password -X POST https://<bigip>/mgmt/tm/asm/policies/<policyId>/whitelist-ips -H "Content-Type: application/json" -d '{"ipAddress":"<whitelist ip>", "ipMask":"<netmask>"}'
                * - Enable the "Policy Builder trusted IP" settings for the whitelist IP (by default disabled), leaving all other whitelist settings alone 
                  - PATCH
                  - curl -sk -u admin:password -X PATCH https://<bigip>/mgmt/tm/asm/policies/<policyId>/whitelist-ips/<whitelistIpId> -H “Content-Type: application/json” -d '{"trustedByPolicyBuilder":"true"}'
                * - Delete a policy 
		  - DELETE
		  - curl -sk -u admin:password -X DELETE https://<bigip>/mgmt/tm/asm/policies/<policyId> -H “Content-Type: application/json”
                * - Delete a whitelist ip from policy
                  - DELETE
                  - curl -sk -u admin:password -X DELETE https://<bigip>/mgmt/tm/asm/policies/<policyId>/whitelist-ips/<whitelistIpId> -H “Content-Type: application/json”

Topics:

.. toctree::
   :maxdepth: 1
   :glob:

   lab*/lab*
   review
   lab*/answer*
