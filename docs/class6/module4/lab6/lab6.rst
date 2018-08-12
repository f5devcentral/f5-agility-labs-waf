Lab 4.6: Getting data across all policies and providing a report 
------------------------------------------------------------------

Task 1 - Using Python to report on the CVE that each policy provides protection against
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This script loops through all attack signatures installed and inventories which CVE each signature protects against. Then it will loop through all policies, determining if the policy has signatures applied to it that protect against a CVE. The script thens generates a report displaying which CVE each policy protects against.

Run the following script:

.. code-block:: bash
        
        python3 /home/f5student/agility2018/asm342/python/Module4Lab6-ex1-getCveProtectedPerPolicy.py

|

Wait until the script is finished, this will take several minutes.

The instructor will talk through the script after all students have completed this task. Feel free to open the script to analyze it and run any of the curl commands to guide you through the flow.

