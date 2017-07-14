Getting Started
---------------

.. TODO:: Complete getting started instructions

Please follow the instructions provided by the instructor to start your
lab and access your jump host.

.. NOTE::
	 All work for this lab will be performed exclusively from the Windows
	 jumphost. No installation or interaction with your local system is
	 required.

Lab Network Overview
~~~~~~~~~~~~

Each student will have access to a Windows 7 “Jumpbox”. Information
required to gain RDP access to the Jumpbox will be provided in each
session.

Each student will have a BIG-IP VE environment with IP addressing as
below:

    10.0.0.0/24 – Management Subnet

    10.0.0.4/24 – BIGIP mgmt IP

    10.0.0.100/24 – Win7 “Jumpbox” mgmt IP

    10.128.10.0/24 – External Subnet

    10.128.10.200 – auction.f5demo.com virtual server

    10.128.20.0/24 – Internal Subnet

    10.128.20.245 – BIGIP self IP

    10.128.20.210 – Hackazon.f5demo.com webserver

All operations in this lab will be performed from within a Windows 7
“Jumpbox” running in the cloud, which you’ll reach using a Microsoft
Remote Desktop Connection client running on your personal workstation.
Lab instructors will provide a hostname for you to use to access your
personal lab environment.

**Important: If you are using a *VPN client* inform your instructors. We
are using an IP filter on the cloud environment that restricts access**
**to known IP’s.**

+---------------------+--------------+----------------+
| *Device*            | *Username*   | *Password*     |
+=====================+==============+================+
| Windows 7 Jumpbox   | student      | 401elliottW!   |
+---------------------+--------------+----------------+
| BIG-IP (HTTPS)      | admin        | 401elliottW!   |
+---------------------+--------------+----------------+
| BIG-IP (SSH)        | root         | 401elliottW!   |
+---------------------+--------------+----------------+

Please use the **Chrome web browser** to access the BIG-IP Configuration
Utility (WebUI) which is accessible at: https://10.128.1.245.


.. list-table::
    :widths: 20 40 40
    :header-rows: 1
    :stub-columns: 1

    * - **Component**
      - **VLAN/IP Address(es)**
      - **Credentials**
    * - Sample Host
      - - **Management:** 10.1.1.250
        - **Internal:** 10.1.10.250
        - **External:** 10.1.20.250
      - ``admin``/``admin``


