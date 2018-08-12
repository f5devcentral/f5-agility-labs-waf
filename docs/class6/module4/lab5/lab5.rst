Lab 4.5: Adding to a policy using Python 
-------------------------------------------

Task 1 - Using Python to make whitelisted IPs the same across all policies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This script finds all whitelist ip addresses across all policies, building a list. It then goes to each policy and adds any missing ip addresses not found in the policy using the POST method. This script does not take any other settings into account other than ip and netmask. When the ip is added to the whitelist, it is added with the default settings.

Before running the script, navigate to Security->Application Security->IP Addresses->IP Address Exceptions for the "python1", "curl1", "postman1" and "ansible1" policies, note the whitelist ip address configuration for each policy.
Note in order to select the different policies use the "Current edited security policy" dropdown.

When ready, run the following:


.. code-block:: bash
        
        python3 /home/f5student/agility2018/asm342/python/Module4Lab5-ex1-whitelistIpNormalizer.py

|

Wait until the script is finished.

After the script has completed, look at the whitelist ip in Security->Application Security->IP Addresses->IP Address Exceptions for each policy. All policies should have the exact same list of ip addresses.

The instructor will talk through the script after all students have completed this task. Feel free to open the script to analyze it and run any of the curl commands to guide you through the flow.

