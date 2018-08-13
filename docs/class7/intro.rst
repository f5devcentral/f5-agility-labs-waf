Getting Started
---------------

Open your browser, proceed to http://training.f5agility.com and enter class# and student#

 .. image:: _static/home.png

You should be able to see Virtual Machines as shown below. Click on **RDP** for Windows Jumpbox and connect via RDP. Picture below is an example, you should see virtual machines with different names. 

 .. image:: _static/home1.png

.. NOTE::
	 All work for this lab will be performed exclusively from the Windows
	 Jumpbox. No installation or interaction with your local system is
	 required.

Lab Credentials
~~~~~~~~~~~~

The following table lists access credential for all required components:

.. list-table::
    :widths: 20 20
    :header-rows: 1
    :stub-columns: 1

    * - **Component**
      - **Credentials**
    * - Windows Jumpbox
      - ``admin``/``admin``
    * - F5 BIG-IP VE
      - ``admin``/``admin``

The BIG-IP VE is accessible from the Windows Jumpbox at https://192.168.1.5


Lab Topology
~~~~~~~~~~~~

The following components have been included in your lab environment:

- 1 x F5 BIG-IP VE (v13.1)
- 1 x Linux Webserver (xubuntu 14.04)
- 1 x Windows Jumphost

On the picture below you can see network topology. Basically, you will be sending various API calls to API server proxied through BIG-IP VE.

 .. image:: _static/diagram.png

Traffic from Windows Jumpbox will be proxied through the BIG-IP to API Server.

Lab tools
~~~~~~~~~~~~~~~~

You will use Postman application to run API calls from Windows Jumpbox. Postman provides friendly and easy to use GUI for interacting with various APIs. Moreover, it is frequently used for designing, debugging, automated testing, debugging and overall lifecycle management for the APIs.

.. HINT::
   More information can be found at https://www.getpostman.com/
