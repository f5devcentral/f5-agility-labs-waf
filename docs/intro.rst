Lab Network Overview
~~~~~~~~~~~~~~~~~~~~

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
Utility (WebUI) which is accessible at: https://10.0.0.4/

