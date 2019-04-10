Lab 2.3: Server-side json filtering
------------------------------------------------

Task 1 - Server-side json filtering using uri parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Queries to ASM's REST API yields lots of useful information, but can be a little extraneous.  Fortunately, the data can be filtered. 

F5 has documented a number of query parameters that can be passed into iControl REST calls in order to modify their behavior. The first set follows the OData (open data protocol) standard. The filter parameter also supports several operators.

Note that the filtering takes places on the server-side or at the BIG-IP.

$filter - filter on key/value pairs, such as name eq ansible1 which would only display the ansible1 policy. eq stands for equals

$select - without select all data is displayed, with select, one can specify which keys to display. Such as displaying only the name field, select=name

$skip - in conjunction with $top, acts as a pageanator, specifying how many objects to skip.

$top - takes a numeric value, used to display the top number of objects specified.

Yes, the dollar sign is important and necessary on these parameters. The operators you can use on these parameters are below. Note that the eq operator can only be used with the filter.


eq - equal

ne - not equal

lt - less than

le - less than or equal

gt - greater than

ge - greater than or equal

|

**Logical Operators:**

and - both conditions must be true

or - either condition can be true

not - to negate the condition

|

Beyond the OData parameters, there are a few custom parameters as well.

expandSubcollections - allows you to get the subcollection data in the initial request for objects that have subcollections. Examples of subcollections are any key that ends in "reference" such as whitelistIpReference as seen in lab1 of this module. The options follows the "link" to retrieve that configuration data automatically.

.. code-block:: json

    {"whitelistIpReference": {
        "link":"https://localhost/mgmt/tm/asm/policies/ouO97l-EOX-zt3sDWA7Dag/whitelist-ips?ver=13.1.0",
        "isSubCollection": true
        },
    }

options - allows you to add arguments to the tmsh equivalent command. An example will be shown below.

ver - This is for the specific TMOS version. Setting this parameter guarantees consistent behavior through code upgrades.

|

Run the following code to get just the names of the existing policies:

.. code-block:: bash

        curl -sk -u admin:$password https://10.1.1.245/mgmt/tm/asm/policies/?\$select=name | sed 's/,/\'$'\n/g'

.. code-block:: json

        {"kind":"tm:asm:policies:policycollectionstate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies?$select=name&ver=13.1.0"
        "totalItems":2
        "items":[{"kind":"tm:asm:policies:policystate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg?ver=13.1.0"
        "name":"ansible1"}
        {"kind":"tm:asm:policies:policystate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies/r3deT9IMy0gBkM65PTVlzA?ver=13.1.0"
        "name":"WebScrapingPolicy"}]}

|
|

.. note:: Note the escape character \ for the $ and & characters.

|
|

Run the following code to filter on just the policy named "ansible1" and only the display its "name" field.

.. code-block:: bash

        curl -sk -u admin:$password https://10.1.1.245/mgmt/tm/asm/policies?\$filter=name+eq+ansible1\&\$select=name | sed 's/,/\'$'\n/g' 

.. code-block:: json

        {
        "kind": "tm:asm:policies:policycollectionstate",
        "selfLink": "https://localhost/mgmt/tm/asm/policies?$select=name&ver=13.1.0&$filter=name%20eq%20ansible1",
        "totalItems": 1,
        "items": [
                {
                "kind": "tm:asm:policies:policystate",
                "selfLink": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg?ver=13.1.0",
                "name": "ansible1"
                }
                ]
        }              
