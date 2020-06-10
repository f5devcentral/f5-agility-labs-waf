Lab Environment & Topology
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE:: All work is done from the Linux client/jumphost (client01), which can be accessed via RDP (Windows Remote Desktop) or ssh. No installation or interaction with your local system is required.

Environment
-----------

**Linux client (client01):**

**Web Attack Tools used in this lab:**

* `BURP Community Edition <https://portswigger.net/burp/>`_ - Packet Crafting
* `curl <https://curl.haxx.se/>`_ - command line webclient. Very useful for debugging and request crafting
* `ab (Apache Bench) <https://httpd.apache.org/docs/2.4/programs/ab.html>`_ - HTTP Load Testing
 
**Linux server (server01):**

* `WebGoat 8 <https://github.com/WebGoat/WebGoat/wiki>`_ - WebGoat is a deliberately insecure web application maintained by OWASP designed to teach web application security lessons. The primary goal of the WebGoat project is simple: create a de-facto interactive teaching environment for web application security.

Lab Topology
---------------

The network topology implemented for this lab is very simple. The following
components have been included in your lab environment:

-  1 x Ubuntu Linux 16.04 client
-  1 x F5 BIG-IP VE (v15.1.0.1) running Advanced WAF with Ip Intelligence & Threat Campaigns Subscription Services.  
-  1 x Ubuntu Linux 16.04 server

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
     - 10.1.1.5
     - 10.1.10.51
     - N/A
     - rdp - ``f5student:(pw from instructor)``
   * - Bigip (bigip01)
     - 10.1.1.8
     - 10.1.10.245
     - 10.1.20.245
     - https - ``admin:(pw from instructor)``  ssh - ``admin:(pw from instructor)``
   * - Linux Server & WebGOAT app (server01)
     - 10.1.1.6
     - N/A
     - 10.1.20.252
     - ssh - ``f5student:(pw from instructor)``
