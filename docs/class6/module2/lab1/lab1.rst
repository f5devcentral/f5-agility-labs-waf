Lab 2.1: Intro to ASM Rest API using curl
-------------------------------------------

.. note::

        Replace all instances of <bigip> with the management ip of the bigip1, 10.1.1.245. Replace password with the pssword provided by the instructor.

**JSON Key/Value Pairs**

JSON is comprised of key:value pairs ({“key”:”value”}) sometimes referred to as a hash or in python a dictionary. "Keys" are unique within the same context. Each key/value pair belonging to a set will be enclosed in curly braces “{ …. }”, “{” being the opening curly brace, “}” being the closing curly brace. Note the word “pairs”, most of the JSON will have multiple pairs, each pair separated by a comma ( eg { “key1”:”value1”,”key2”:”value2”}. The commas have been removed in the above output by the sed/awk commands to make the output prettier. Take a look at the output (#1) to see the commas. In the above example, each key/value pair is on a newline thanks to the sed/awk filter.

To access a value in a collection, a key must be specified.

For example in the json output:

{“key1”:”value1”,”key2”:”value2”,”key3”:”value3”}

specifying “key2” will yield “value2”. To retrieve “value2”, “key3” must be specified.

.. note::

        Note the difference between an array and a hash, so far we have discussed hashes. Arrays, denoted with [] are similar, they store keys and values, however the keys are numerical, 1,2,3, etc. This is because the key value may be non-existent and is definitely dynamic. More on this later.  Below, you will see an array in the virtualServers entry. 

Here is a real world ASM output example, truncated with a “…” to show the relevant parts:

.. code-block:: json

        "name": "asm1",
        "caseInsensitive": true,
        ...
        "kind": "tm:asm:policies:policystate",
        "virtualServers": [
          "/Common/sharepoint_vs",
          "/Common/exchange_vs"
          ],
        ...
        "whitelistIpReference": {
          "link": "https://localhost/mgmt/tm/asm/policies/ouO97l-EOX-zt3sDWA7Dag/whitelist-ips?ver=13.1.0",
          "isSubCollection": true
          },
        ...
        "id": "ouO97l-EOX-zt3sDWA7Dag",
        "modifierName": "admin",
        "manualVirtualServers": [],
        "versionDatetime": "2018-07-28T20:18:54Z"

|

To access the "name" of the policy, you would use the key "name" and in this case "asm1" would be returned as the value. To retrieve the policy "id", use the "id" key and "ouO97l-EOX-zt3sDWA7Dag" would be returned as the value, more on this later.

For the assigned virtual servers (virtualServers key) if you specify a key of 0, the value would be "/Common/sharepoint_vs". If 1 is used as the key for the virtualServers "/Common/exchange_vs" is returned as the value.



Task 1 - Explore the API using curl 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All scripts in this module are run from the cli (Terminal Emulator icon on the desktop).

|

Run the following command (don't forget to use the correct password):

.. code-block:: bash

        curl -sk -u admin:$password -X GET https://10.1.1.245/mgmt/tm/asm/policies/

|
|

.. note:: The student can add -v to any curl command to see more verbose output, such as the client and server headers.

|

The JSON output (#1) (truncated) should look something similar to:

.. code-block:: json

        {"kind":"tm:asm:policies:policycollectionstate","selfLink":"https://localhost/mgmt/tm/asm/policies?ver=13.1.0","totalItems":1,"items":[{"plainTextProfileReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0","isSubCollection":true},"dataGuardReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/data-guard?ver=13.1.0"},"createdDatetime":"2018-05-21T04:30:17Z","databaseProtectionReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/database-protection?ver=13.1.0"},"csrfUrlReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0","isSubCollection":true},"cookieSettingsReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/cookie-settings?ver=13.1.0"},"versionLastChange":" Security Policy /Common/ansible1 [add] { audit: policy = /Common/ansible1, username = admin, client IP = 10.1.1.51 }","name":"ansible1"

|

Not terribly easy to read, however before working on the output readability, the curl options deserve some explanation.


curl **\-k** -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/policies/


-k: This option tells curl to not verify the server's ssl certificate, since we are connected to a BIG-IP with an untrusted cert signed by its own CA.

|

curl -k **\-u admin:password** -X GET https://10.1.1.245/mgmt/tm/asm/policies/

-u: Specifies the logon credentials. A ":" is used to separate the username and passsword. The user:pass are converted into a Base64 encoded authorization header. This can be seen by adding a -vto the curl command.

|

curl -k -u admin:password **\-X GET** https://10.1.1.245/mgmt/tm/asm/policies/

-X: The HTTP method/verb, since data is being retrieved, GET is used

|

curl -k -u admin:password -X GET **https://10.1.1.245/mgmt/tm/asm/policies/**

Lastly the full url to the resource.

|
|

Now run:

.. code-block:: bash

       curl -sk -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/policies  | sed 's/,/\'$'\n/g'


The JSON output (#2) (truncated) is now more readable

.. code-block:: json

        {"kind":"tm:asm:policies:policycollectionstate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies?ver=13.1.0"
        "totalItems":1
        "items":[{"plainTextProfileReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0"
        "isSubCollection":true}
        "dataGuardReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/data-guard?ver=13.1.0"}
        "createdDatetime":"2018-05-21T04:30:17Z"
        "databaseProtectionReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/database-protection?ver=13.1.0"}
        "csrfUrlReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0"
        "isSubCollection":true}
        "cookieSettingsReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/cookie-settings?ver=13.1.0"}
        "versionLastChange":" Security Policy /Common/ansible1 [add] { audit: policy = /Common/ansible1
        username = admin
        client IP = 10.1.1.51 }"
        "name":"ansible1"

 
|

Lets decipher this JSON output (#2). 

After the opening "{", is the first key of collection "kind". The value is "tm:asm:policies:policycollectionstate" which tells us we are looking the asm policies.

.. code-block:: json

        {"kind":"tm:asm:policies:policycollectionstate"}

|

Next is the key "selfLink" and its value of "https://localhost/mgmt/tm/asm/policies?ver=13.1.0". This tells us how to get to the resource. Its usefulness may not be completely apprarent now, but will be in subsequent excercises.
Also note that it is essentially the same url used in the curl command. The "?ver" is a parameter passed to the Rest API to request the use of API version 13.1.0.  Ignore this for now.

|

.. code-block:: json

   {"selfLink":"https://localhost/mgmt/tm/asm/policies?ver=13.1.0"}

Next is the "totalItems" key which has value of 1, meaning there is one policy. Go to Security->Application Security->Security Policies in Web Gui to verify the value from your output of totalItems matches the number of asm security policies from the Web Gui. 

Now onto the interesting stuff. The next key is "items" which is a nested collection of polciies, the actual ASM policies and their settings. Items contains multiple collections, that is why the value begins with a opening square bracket "[". Remember if it is an array, it's dynamic, you could have zero policies.  The value of items contains the AWAF policy with links to its policy settings such as the link to the csrfUrlReference "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0"

If you followed this url, of course substituting localhost for the mgmt ip of the BIGIP, you would get the setting for the csrf Url for that policy. That is the power of the link value, you can use it to get to other configuration items. Later in the class, we will go into how to get at this data programmatically. This also demonstrates that not all configuration data can be retrieved by a single query, depending on the need, you may have to make more than one HTTP request.

What about the crazy string "u-6T62j_f0XMkjJ_s_Z-gg" after /policies/ ? This is a randomly generated (as such your value will not be u-6T62j_f0XMkjJ_s_Z-gg, rather something similar) id for the ASM security policy. In other words you cannot simply access the ansible1 security policy by going to https://10.1.1.245/mgmt/tm/asm/polciies/ansible1, you have to search for the "name" key in the JSON output until it matches ansible1 to figure which generated id is ansible1. 

.. note:: All ASM objects, which include policies, parameters, and URLs have a randomly generated unique id, where the name you see in the Web Gui is just a display name. Therefore to get at these objects via the REST API, you must filter on each unique ID until you find the "name" key's value equal to the name you are looking for. 

Wouldn't it be nice if we had something that could do the filtering for us?

We have covered a lot, time for questions and a discussion as these are all important topics.


