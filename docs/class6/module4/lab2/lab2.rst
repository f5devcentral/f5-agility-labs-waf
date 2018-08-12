Lab 4.2: Python Policy Creation and Modification
--------------------------------------------------

Task 1 - Using Python to create a ASM policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the following script to create a new ASM policy "python1"

.. code-block:: bash
        
        python3 /home/f5student/agility2018/asm342/python/Module4Lab2-ex1-createAsmPolicy.py

|

Navigate to Security->Application Security->Security Policies->Policies List to verify the "python1" policy was created.

The instructor will talk through the script after all students have completed this task. Feel free to open the script to analyze it and run any of the curl commands to guide you through the flow.


Task 2 - Using Python to modify an ASM policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First navigate via the Gui to Security->Application Security->IP Addresses->IP Address Exceptions to verify the whitelist configuration for the python1 policy.

Run the following script to add a whitelist ip address to the ASM policy "python1"

.. code-block:: bash

        python3 /home/f5student/agility2018/asm342/python/Module4Lab2-ex2-addWhitelistIp.py

|

Refresh the IP Address Exceptions configuration, the new ip should be added. The policy should be applied or be in the process of being applied, this can take a minute or two.

The instructor will talk through the script after all students have completed this task. Feel free to open the script to analyze it and run any of the curl commands to guide you through the flow.
