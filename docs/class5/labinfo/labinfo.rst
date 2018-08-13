Lab Environment & Topology 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  |lab-diag| image:: images/Agility2018LabDiagram.png

.. WARNING:: All work is done from the Linux client/jumphost (client01), which can be access via RDP (Windows Remote Desktop) or ssh. No installation or interaction with your local system is required.

All pre-built environments implement the Lab Topology shown below.  Please
review the topology first, then find the section matching the lab environment
you are using for connection instructions.

Environment
-----------

Linux client (client01):

* Web Attack Tools: (Only used in 141,241,341 classes)

 * `Goldeneye <https://github.com/jseidl/GoldenEye>`_ - HTTP DOS Tool
 * `Metasploit <https://www.metasploit.com/>`_ - Pen testing framework
 * `nmap/nping <https://nmap.org/>`_ - Network mapper
 * `Slowhttptest <https://github.com/shekyan/slowhttptest>`_ - HTTP DOS Tool
 * `wapiti <http://wapiti.sourceforge.net/>`_ - web application auditor
 * `w3af <http://w3af.org/>`_ - web application auditor
 * `Burp Suite Community Edition <https://portswigger.net/burp>`_ - HTTP Request Manipulation

* Api Tools: (Only used in 342 Programmability class)

 * `Ansible <https://www.ansible.com/>`_ - Automation platform
 * `curl <https://curl.haxx.se/>`_ - command line webclient, will be used to interact with the iControl Rest API
 * `Postman <https://www.getpostman.com/>`_ - Graphical based Restful Client, will be used to interact with the iControl Rest API
 * `python <https://www.python.org/>`_ - general programming language used to interact with the iControl Rest API 

Linux server (server01): (Only used in 141,241,341 classes)

* `WebGoat 8 <https://github.com/WebGoat/WebGoat/wiki>`_ - deliberately insecure web application

.. _lab-topology:

Lab Topology
------------

The network topology implemented for this lab is very simple, since the
focus of the lab is Control Plane programmability rather than Data Plane
traffic flow we can keep the data plane fairly simple. The following
components have been included in your lab environment:

-  1 x Ubuntu Linux 18.04 client, with client tools installed - aptly named: client01
-  1 x F5 BIG-IP VE (v13.1.0.5) running ASM and LTM - aptly named: bigip01
-  1 x Ubuntu Linux 18.04 server, with webgoat 8 installed - aptly named: server01 

.. nwdiag:: labtopology.diag
   :width: 800
   :caption: Lab Topology
   :name: lab-topology-diagram
   :scale: 110%

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
     - https-``f5student:password``
   * - Bigip (bigip01)
     - 10.1.1.245
     - 10.1.10.245
     - 10.1.20.245
     - https - ``admin:password`` ssh - ``f5student:password``
   * - Linux Server (server01)
     - 10.1.1.252
     - N/A
     - 10.1.20.252
     - ssh - ``f5student:password``

|
|

A graphical representation of the lab:

	|lab-diag|

|

.. note:: 
        
        External links are not required reading for the lab, rather supplemental if you you would like to get a different take or additional info.

|

.. note::

        Replace all instances of <bigip> with the management ip of the bigip1, 10.1.1.245. Replace password with the pssword provided by the instructor.
