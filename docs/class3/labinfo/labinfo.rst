Lab Environment & Topology
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE:: All work is done from the Linux client/jumphost (client01), which can be accessed via RDP (Windows Remote Desktop) or ssh. No installation or interaction with your local system is required.

Environment
-----------

**Linux client (client01):**

**Web Attack Tools used in this lab:**

 * `OWASP ZAP <https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project>`_ - DAST
 * `BURP Community Edition <https://portswigger.net/burp/>`_ - Packet Crafting

**Api Tools:**

 * `Ansible <https://www.ansible.com/>`_ - Automation platform
 * `curl <https://curl.haxx.se/>`_ - command line webclient, will be used to interact with the iControl Rest API
 * `Postman <https://www.getpostman.com/>`_ - Graphical based Restful Client, will be used to interact with the iControl Rest API
 * `python <https://www.python.org/>`_ - general programming language used to interact with the iControl Rest API

**Linux server (server01):**

* `WebGoat 8 <https://github.com/WebGoat/WebGoat/wiki>`_ - WebGoat is a deliberately insecure web application maintained by OWASP designed to teach web application security lessons. Why the name "WebGoat"? Developers should not feel bad about not knowing security. Even the best programmers make security errors. What they need is a scapegoat, right? Just blame it on the **Goat!**

.. _lab-topology:

Lab Topology
---------------

The network topology implemented for this lab is very simple. The following
components have been included in your lab environment:

-  1 x Ubuntu Linux 18.04 client
-  1 x F5 BIG-IP VE (v14.1.0.2) running WAF and LTM
-  1 x Ubuntu Linux 18.04 server

The following table lists VLANS, IP Addresses and Credentials for all
components:

.. list-table::
   :widths: 15 15 15 15 15
   :header-rows: 1
   :stub-columns: 1


   * - **Component**
     - **mgmtnet IP**
     - **clientnet IP**
     - **servernet IP**
     - **Credentials**
   * - Linux Client (client01)
     - 10.1.1.51
     - 10.1.10.51
     - N/A
     - rdp-``f5student:password``
   * - Bigip (bigip01)
     - 10.1.1.245
     - 10.1.10.245
     - 10.1.20.245
     - https - ``admin:password``  ssh - ``f5student:password``
   * - Linux Server & WebGOAT app (server01)
     - 10.1.1.252
     - N/A
     - 10.1.20.252
     - ssh - ``f5student:password``

