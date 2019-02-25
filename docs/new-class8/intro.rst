Getting Started
---------------

Please follow the instructions provided by the instructor to start your
lab and access your jump host.

.. NOTE::
	 All work for this lab will be performed exclusively from the Windows
	 jumphost. No installation or interaction with your local system is
	 required.

.. WARNING::
	To ensure consistent behavior with the lab guide, **all lab exercises should be through the Chrome browser** on the
	Windows Jumphost.

Lab Topology
~~~~~~~~~~~~

The following components have been included in your lab environment:

- 1 x F5 BIG-IP VE (v14.1)
- 1 x Linux LAMP Webserver (xubuntu 14.04)
- 1 x Windows Jumphost
- 1 x Kali Linux (not used in this lab)

Lab Components
^^^^^^^^^^^^^^

The following table lists VLANS, IP Addresses and Credentials for all
components:

.. list-table::
    :widths: 20 40 40
    :header-rows: 1

    * - **Component**
      - **VLAN/IP Address(es)**
      - **Credentials**
    * - Windows Jumphost
      - - **Management:** 10.1.1.6
        - **External:** 10.1.10.4
        - **Internal:** 10.1.20.4
      - ``admin``/``F5LabDays!``
    * - F5 BIG-IP
      - - **Management:** 10.1.1.8
        - **External:** 10.1.10.7
        - **Internal:** 10.1.20.7
      - ``admin``/``F5LabDays!``
    * - LAMP Server
      - - **Management:** 10.1.1.4
        - **External:** N/A
        - **Internal:** 10.1.20.11
      - ``root``/``default``
