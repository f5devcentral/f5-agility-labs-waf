Module 1: Ansible 
===================================================
Expected time to complete: **1 hours**


**Intro**

Ansible is an automated configuration tool that uses config files written in YAML to push configurations to devices and rollback. 

Some benefits of Ansible:



**Agentless** -  As long as the system can be ssh’d into and has python, it can be configured with Ansible.

**Idempotent** - Ansible’s whole architecture is structured around the concept of idempotency. The core idea here is that you only do things if they are needed and that things are repeatable without side effects. More than anything else this sold me over Puppet and Chef.

**Declarative Not Procedural** - Other configuration tools tend to be procedural — do this and then do that and so on. Ansible works by writing a description of the state of the machine that you want and then it takes steps to fulfill that description.

**Learning Curve** - Ansible typically take much less time to understand than tools like Chef or Puppet. 


Although the ASM Ansible functionality is currently limited to policy creation/importation, F5 has invested heavily in developing an Ansible library to interact with the BIG-IP iControl Rest API. Curiosity has grown greatly over the last year and we want to demonstrate how to get started with Ansible and ASM, as future releases will enhance Ansible's ASM capabilities.


This first module covers the following topics:

.. toctree::
   :maxdepth: 1
   :glob:

   lab*/lab*
   review

