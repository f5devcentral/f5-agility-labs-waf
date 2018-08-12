Lab 2.2: Curl Policy Creation and Modification
--------------------------------------------------

Task 1 - Using curl to create a ASM policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Now that you've run a few curl commands yourself, we'll now make it a little easier (this is an automation lab, after all). 

|

Run the following command to create a new ASM policy "curl1" (this may take a couple of minutes). JSON will be displayed showing the policy creation and the policy's attributes:

.. code-block:: bash
        
        curl -sk -u admin:$password -X POST https://10.1.1.245/mgmt/tm/asm/policies -d '{"name":"curl1"}' | sed 's/,/\'$'\n/g'

|

Navigate to Security->Application Security->Security Policies->Policies List to verify the "curl1" policy was created


Before running the below command, navigate to Security->Application Security->IP Addresses->IP Address Exceptions for the “curl1" policy, noting the configuration. 

.. note:: 

        To select the different policies by using the “Current edited security policy” dropdown.

Run the following command to modify the policy by adding a whitelist ip, using the policy id from the output of "curl1" policy creation:

.. code-block:: bash

        curl -sk -u admin:$password -X POST https://10.1.1.245/mgmt/tm/asm/policies/<policyId>/whitelist-ips -H "Content-Type: application/json" -d '{"ipAddress":"165.25.76.234", "ipMask":"255.255.255.255"}'

|

Refresh the IP Address Exceptions to verify the whitelist ip 165.25.76.234/255.255.255.255 was added.

Notice the policy was not applied, click “Apply Policy”.  Applying the policy requires a separate REST call.  This will be covered in subsequent labs.
