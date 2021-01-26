Lab Environment & Topology
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE:: All work is done from the Linux Client, which can
   be accessed via RDP (Remote Desktop Client) or SSH. No installation or
   interaction with your local system is required.

Environment
-----------

**Linux Client:**

**Web Attack Tools used in this lab:**

- `BURP Community Edition <https://portswigger.net/burp/>`_ - Packet Crafting
- `curl <https://curl.haxx.se/>`_ - command line webclient. Very useful for debugging and request crafting
- `Postman <https://www.postman.com/>`_ - API Development and request crafting

**Linux server:**

- `JuiceShop <https://owasp.org/www-project-juice-shop/>`_ - OWASP Juice Shop is probably the most modern and sophisticated insecure web application! 

**Lab Topology**
---------------

The network topology implemented for this lab is very simple. The following
components have been included in your lab environment:

-  1 x Ubuntu Linux 20.04 client
-  1 x F5 BIG-IP VE (v16.0.1) running Advanced WAF with IP Intelligence & Threat Campaign Subscription Services.  
-  1 x Ubuntu Linux 20.04 server

The following table lists VLANS, IP Addresses and Credentials for all
components. **The "password" will be provided by your instructor.**

.. list-table::
   :widths: 15 15 15 15 15
   :header-rows: 1
   :stub-columns: 1


   * - **Component**
     - **mgt IP**
     - **ClientSide IP**
     - **ServerSide IP**
     - **Credentials**
   * - Linux Client
     - 10.1.1.7
     - 10.1.10.51
     - N/A
     - rdp-``f5student:password``
   * - BIG-IP
     - 10.1.1.4
     - 10.1.10.245
     - 10.1.20.245
     - https - ``admin:password``  ssh - ``f5student:password``
   * - Linux Server 
     - 10.1.1.6
     - N/A
     - 10.1.20.252
     - ssh - ``f5student:password``

