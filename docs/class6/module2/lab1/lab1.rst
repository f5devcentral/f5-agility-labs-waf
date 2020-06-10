Lab 2.1: Installation of f5's WAF Tester
=========================================


**Installation**
~~~~~~~~~~~~~~~~

This tool runs on a linux based host and requires Python 2.7+.  

To install Python:

2.1.1 - Open RDP to the Linux client
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Log into the Linux client via RDP using the following credentials and open the Terminal application:

        Username: f5student
        
        Password: f5DEMOs4u!

	.. image:: images/terminal.png

2.1.2 - Install Python
~~~~~~~~~~~~~~~~~~~~~~~

Within the terminal type:

Password for 'sudo': f5DEMOs4u!

.. code-block:: bash

        sudo apt-get install -y python-pip


2.1.3 - Install f5 WAF tester tool
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install the tool using the following command:

.. code-block:: bash

        pip install git+https://github.com/f5devcentral/f5-waf-tester.git