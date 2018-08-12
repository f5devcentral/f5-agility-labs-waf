Lab 2.4: Client-side json filtering 
--------------------------------------------------------------

Task 1 - Client-side json filtering using jq
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Another way to parse JSON data is to use a program called jq. jq understands json and provides another way of filtering on data. 
This differs from passing uri parameters in that the request retrieves all data and the filtering is done on the client-side.
Of course client programs like jq can be used in conjunction with uri parameters. This lab does not cover this scenario.

Run the following command to view the output of all ASM policies filtered through jq:

.. code-block:: bash

       curl -sk -u admin:$password -X GET https://10.1.1.245/mgmt/tm/asm/policies | jq 

The output (truncated) will look something similar to:

.. code-block:: json


        {
          "kind": "tm:asm:policies:policycollectionstate",
          "selfLink": "https://localhost/mgmt/tm/asm/policies?ver=13.1.0",
          "totalItems": 2,
          "items": [
            {
              "plainTextProfileReference": {
              "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0",
              "isSubCollection": true
              },
              "dataGuardReference": {
                "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/data-guard?ver=13.1.0"
              },
              "createdDatetime": "2018-05-21T04:30:17Z",
              "databaseProtectionReference": {
                "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/database-protection?ver=13.1.0"
              },
              "csrfUrlReference": {
                "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0",
                "isSubCollection": true
              },
              "cookieSettingsReference": {
                "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/cookie-settings?ver=13.1.0"
              },
              "versionLastChange": " Security Policy /Common/ansible1 [add] { audit: policy = /Common/ansible1, username = admin, client IP = 10.1.1.51 }",
              "name": "ansible1",


jq really helps to show the JSON structure and different layers, which helps give you an idea of how to access different items.

Recall from lab1 that there are 2 items (we know this from the totalItems value of 2, which represents "ansible1" and "curl1") and that each item represents a policy.

To display the first policy (index starts at 0), run the following command:

.. code-block:: bash

        curl -sk -u admin:$password -X GET https://10.1.1.245/mgmt/tm/asm/policies | jq .items[0]

The output should look similar to, which is the entire configuration for the first policy, in this case "ansible1":

.. code-block:: json



        {
          "plainTextProfileReference": {
            "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0",
            "isSubCollection": true
        },
          "dataGuardReference": {
           "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/data-guard?ver=13.1.0"
        },
          "createdDatetime": "2018-05-21T04:30:17Z",
          "databaseProtectionReference": {
           "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/database-protection?ver=13.1.0"
        },
          "csrfUrlReference": {
           "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0",
           "isSubCollection": true
        },
         "cookieSettingsReference": {
          "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/cookie-settings?ver=13.1.0"
        },
         "versionLastChange": " Security Policy /Common/ansible1 [add] { audit: policy = /Common/ansible1, username = admin, client IP = 10.1.1.51 }",
         "name": "ansible1"

Notice the lines leading up to and including items are not displayed
 
.. code-block:: json

       {
        "kind":"tm:asm:policies:policycollectionstate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies?ver=13.1.0"
        "totalItems":2 
        "items":[{"plainTextProfileReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0"

We have told jq to only display collections within the items values, specifically we are specifying the first one, which again, is the first ASM policy.

|

Now get the policy id of the first ASM policy.

Run the following command:

.. code-block:: bash
        
        curl -sk -u admin:$password -X GET https://10.1.1.245/mgmt/tm/asm/policies | jq .items[0].id

|

The policy id should be output.

Since the id is attribute of the policy, you add a '.' in to jump into that item's (policy) id field.

|
|

Recall that ASM policy id are actually a random string and not the actually name, think about how one could extract the name using jq for the first policy. 
Can you come up with this on your own?


`Answer jq Name <answermodule2lab4-jqName.html>`_

How would one extract the enforcement mode?

`Answer jq Enforcement Mode <answermodule2lab4-jqEnforcement.html>`_




|
|
|

Next take a look at the parameter settings for this policy, run the following:


.. code-block:: bash

        curl -sk -u admin:$password -X GET https://10.1.1.245/mgmt/tm/asm/policies | jq .items[0].parameterReference


The output will look something like:

.. code-block:: json

        {
          "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/parameters?ver=13.1.0",
            "isSubCollection": true
        }


|

Recall any item with a "isSubCollection" with a value of true, will have a link to the actual items, a subCollection of the collection.

|

What would the request look like to retrieve the subCollection (the actual parameters configuration of the policy)?

`Answer jq Parameters <answermodule2lab4-jqParameters.html>`_

|

.. note::

        Hint you cannot use localhost

|

What if you wanted to display only select values, more than one? 

First run the following to get the policy id of the "ansible1" policy. This tells jq to display the name and id fields of any policy (items[], hence the empty square brackets meaning we are not specifying a specific policy, its any policy).

.. code-block:: bash

        curl -sk -u admin:$password -X GET https://10.1.1.245/mgmt/tm/asm/policies | jq '.items[] | "\(.name) \(.id)"'

|
        
The output should display the name and policy id of all policies.

|

What if you wanted to display a parameter named "displaymode"?

Run the following using a policy id from the previous command as the <ansible1PolicyId>

.. code-block:: bash

        curl -sk -u admin:$password -X GET https://10.1.1.245/mgmt/tm/asm/policies/<ansible1PolicyId>/parameters | jq '.items[] | select(.name ==  "displaymode")'


The output should resemble:

.. code-block:: json

        {
          "isBase64": false,
          "dataType": "alpha-numeric",
          "sensitiveParameter": false,
          "valueType": "user-input",
          "kind": "tm:asm:policies:parameters:parameterstate",
          "selfLink": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/parameters/_Ott1aSMBOPupVbKbovX0A?ver=13.1.0",
          "inClassification": false,
          "metacharsOnParameterValueCheck": true,
          "id": "_Ott1aSMBOPupVbKbovX0A",
          "allowEmptyValue": false,
          "checkMaxValueLength": false,
          "valueMetacharOverrides": [],
          "name": "displaymode",
          "lastUpdateMicros": 1526877023000000,
          "allowRepeatedParameterName": false,
          "level": "global",
          "attackSignaturesCheck": true,
          "signatureOverrides": [],
          "performStaging": true,
          "type": "explicit",
          "enableRegularExpression": false
         }

|
|

