Lab 1.1: Ansible Policy Creation 
----------------------------------------

Task 1 - Using Ansible to create a ASM Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All scripts in this module are run from the cli (Terminal Emulator icon on the desktop).


Run the following command to create an ASM policy named **ansible1** (this may take a couple of minutes):

.. code-block:: bash
        
       ansible-playbook /etc/ansible/playbooks/ansible1.yaml -i /etc/ansible/inventory/  -vvv 


Go to the Bigip WebUI and navigate to Security->Application Security->Security Policies->Policies List

You should now see a policy named ansible1

Inspect the policy


**Ansible Configuration Explained**

First ansible must know which hosts to apply the configuration, here we have defined a group called "bigips".

**ansible1.yaml:** 

.. literalinclude:: ansible1.yaml
        :emphasize-lines: 6 
        :linenos:

The group bigips is pulled from /etc/ansible/inventory/hosts, here we only have one host defined, more can be added under the [bigips] stanza.

**hosts:** 

.. literalinclude:: hosts
        :linenos:

The environment variables are pulled from /etc/ansible/inventory/groups_vars/bigips/all.yaml

.. literalinclude:: ansible1.yaml
        :emphasize-lines: 9-14
        :linenos:

**all.yaml:** 

.. note:: Note that the password variable is masked.

.. literalinclude:: group_vars_all.yaml
        :linenos:

In line 18, the bigip_asm_policy directive is used to tell ansible we are going to modify/create a policy.
Line 19 is the name of the policy, line 20 is the Rapid Deployment template that we will use.


**ansible1.yaml:** 


.. literalinclude:: ansible1.yaml
        :emphasize-lines: 18-20
        :linenos:

Starting with line 22, post tasks are declared. These are tasks that will take place after the policy has been created.  Here we will save the policy to disk (otherwise it is only in the running config).

**ansible1.yaml:**

.. literalinclude:: ansible1.yaml
        :emphasize-lines: 22-26
        :linenos:

|


**Why Ansible and Limitations of the F5 ASM Ansible module**

More information on F5's ansible module can be found here `F5 and Ansible <https://www.ansible.com/integrations/networks/f5>`_
`On GitHub <https://github.com/F5Networks/f5-ansible>`_

F5's SYS and LTM Ansible module are more feature rich (close to covering all features), the ASM module is currently limited to policy import, activation/deactivation and creation.
Over time this will change as F5 has a strong partnership with Ansible.

**Current F5 ASM Ansible Capabilities**

|

        Policy Activation/Deactivation

        Blank Policy Creation

        XML Policy Import

        Binary Policy Import

        Policy Creation using Application-Ready Templates

