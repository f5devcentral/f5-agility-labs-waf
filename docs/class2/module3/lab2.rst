AppScan
------------------------------------------------------------

Create the ASM Policy

1. Via **Chrome**, navigate to to the BIG-IP GUI
   `**https://10.0.0.4** <https://10.0.0.4>`__ **or**
   `**https://bigip1.agility.f5.com** <https://bigip1.agility.f5.com>`__

2. Navigate to **Security** >> **Application Security** >> **Security
   Policies**

3. Click the **Create New Policy..** button:

.. image:: /_static/class2/image57.png

1. Toggle the Policy from Basic to **Advanced**

2. Enter the following (leave the rest with the default settings):

   a. Policy Name: appscan-dvwa

   b. Policy Template: Vulnerability Assessment Baseline

   c. Virtual Server: dvwa\_vs

   d. Enforcement Mode: Blocking

3. Click **Create Policy**

.. image:: /_static/class2/image58.png

The system creates a baseline security policy for your web application
with the enforcement mode set to blocking, and the learning mode set to
manual. The policy already protects against malformed HTTP protocol,
evasion techniques, and CSRF attacks. But it does not yet protect
against the vulnerabilities found by the scanner.

.. image:: /_static/class2/image59.png

Import the Vulnerability Scan

1. Navigate to **Security** >> **Application Security** >>
   **Vulnerability Assessments >> Settings**

2. Ensure the current edited policy selected is **appscan-dvwa**

3. Change the Vulnerability Assessment Tool to **IBM®AppScan®,** Hit OK
   on the dialog box

.. image:: /_static/class2/image60.png

1. Click on **Apply Policy**, followed by **OK** on the dialog box

.. image:: /_static/class2/image61.png

1. Navigate to **Security** >> **Application Security** >>
   **Vulnerability Assessments >> Vulnerabilities**

.. image:: /_static/class2/image62.png

1. Select **Import** and choose the vulnerability file
   **appscan-dvwa.xml**

    (Located on the Desktop in the Lab 3 folder)

.. image:: /_static/class2/image63.png

1. Select **Import** to verify the validity of the vulnerability file

.. image:: /_static/class2/image64.png

1. Select **Import** again to import the vulnerabilities into the system
   for the selected domain

.. image:: /_static/class2/image65.png

1. Click on **Close** to be brought back to the scan results

.. image:: /_static/class2/image66.png

Resolve the Vulnerabilities

1. Highlight SQL Injection

2. Click the checkbox in the SQL Injection Vulnerability List and click
   **Resolve**

.. image:: /_static/class2/image67.png

1. Click **Resolve** again to resolve the vulnerabilities

.. image:: /_static/class2/image68.png

1. Hit **Close**

.. image:: /_static/class2/image69.png

1. Click the **Apply Policy** button to save your changes to the policy
   and apply them to the virtual server

.. image:: /_static/class2/image70.png

Once completed, you will see the following screen indicating the
operation completed successfully

.. image:: /_static/class2/image71.png
