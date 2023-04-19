Lab Environment & Topology 
==========================

.. NOTE:: Some of the activities in this lab will be perform from the Client Workstation, which can be accessed via RDP (Windows Remote Desktop), Web Shell or Web Proxy. No installation or interaction with your local system is required.

Environment
-----------

**Tools used in this lab:**

- `Postman <www.postman.com>`_ - An API platform for building and using APIs
- `curl <https://curl.haxx.se/>`_ - command line webclient. Very useful for debugging and request crafting
- `jsonmate <https://jsonmate.com>`_ - Build, test and share your JSON, transformations and schemas
- `Docker <www.docker.com>`_ - Service to run containerized workloads

Lab Topology
------------

The network topology implemented for this lab is very simple. The following
components have been included in your lab environment:

-  1 x Windowser Server 2019, with client tools installed
-  1 x F5 BIG-IP VE (v16.1.2.1) running ASM, APM, and LTM
-  1 x Ubuntu Linux 20.04 server, with Docker installed hosting the Arcadia Finance application

.. nwdiag:: labtopology.diag
   :width: 800
   :name: lab-topology-diagram
   :scale: 110%

The following table lists VLANS, IP Addresses and Credentials for all
components:

.. list-table::
   :widths: 15 15 15 15 15 
   :header-rows: 1


   * - **Component**
     - **Management**
     - **Front**
     - **Back**
     - **Credentials/Access**
   * - Client Workstation
     - 10.1.1.7
     - 10.1.10.6
     - N/A
     - https-``f5student:password``
   * - F5 BIG-IP (BIG-IP)
     - 10.1.1.4
     - 10.1.10.4
     - 10.1.20.4
     - https - ``admin:admin``
   * - App Server
     - 10.1.1.252
     - N/A
     - 10.1.20.252
     - webshell - ``Via UDF``

.. note:: External links are not required reading for the lab, rather
   supplemental if you you would like to get a different take or
   additional info.
