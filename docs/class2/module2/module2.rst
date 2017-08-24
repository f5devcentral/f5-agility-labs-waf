Class 2: Policies
============================

+------------------------------------------+
| +------------------------------------+   |
| | |image0|                           |   |
| +====================================+   |
| | Application Security Manager       |   |
| +------------------------------------+   |
| | F5 Technical Hands On Labs (241)   |   |
| +------------------------------------+   |
+------------------------------------------+

Table of Contents 2

Introduction 3

Lab Network Overview 4

ASM Logging Profile and Rapid Deployment 5

Overview of the BIG-IP Application Security Manager

The BIG-IP® Application Security Manager™ protects mission-critical
enterprise web infrastructure against application-layer attacks, and
monitors the protected web applications. The Application Security
Manager can prevent a variety of web application attacks, such as:

-  Manipulation of cookies or hidden fields

-  SQL injection attacks intended to expose confidential information or
       to corrupt content

-  Malicious exploitations of the application memory buffer to stop
       services, to get shell access, and to propagate worms

-  Unauthorized user access to authenticated accounts using cross-site
       request forgery (CSRF)

-  Unauthorized changes to server content using HTTP DELETE and PUT
       methods

-  Attempts aimed at causing the web application to be unavailable or to
       respond slowly to legitimate users

-  Layer 7 denial-of-service, brute force, and web scraping attacks

-  Unknown threats, also known as zero-day threats

    The system can automatically develop a security policy to protect
    against security threats, and you can configure additional
    protections and customize the system response to threats.

Summary of the Application Security Manager features

    The Application Security Manager includes the following features.

Integrated platform guaranteeing the delivery of secure application
traffic

    Built on F5 Networks’ TMOS® architecture, the ICSA-certified,
    positive-security Application Security Manager is fully integrated
    with the BIG-IP Local Traffic Manager™.

Automated security policy building

    Application Security Manager uses an auto-adaptive approach to
    application delivery security, where the security policy is
    automatically built and updated based on observed traffic patterns.
    A deployment wizard helps you create a security policy for your
    environment. Then the automated policy building feature, called the
    Real Traffic Policy Builder®, examines requests and responses, and
    populates the security policy with legitimate security policy
    elements, based on what it finds in the traffic.

Positive security model

The Application Security Manager creates a robust positive security
policy to completely protect web applications from targeted web
application layer threats, such as buffer overflows, SQL injection,
cross-site scripting, parameter tampering, cookie poisoning, and others.

Lab Network Overview
====================

|image1|

Additional notes specific to the ASM 203 to help you follow along with
the guide:

+------------+------------------------------------------------------------+
| |image2|   | **Please use Chrome to Administer the BIG-IP ASM only.**   |
+============+============================================================+
| |image3|   | **Please use Firefox for lab exercises only.**             |
+------------+------------------------------------------------------------+

Lab 1

ASM Logging Profile and Rapid Deployment
========================================

Objective:
----------

-  Create logging profile for ASM to log all HTTP request and HTTP
   response events

-  Bind logging policy to virtual server

-  Create security policy using Rapid Deployment Template

-  Demonstrate logging, detection and mitigation.

-  Estimated time for completion: 20 minutes

Lab Requirements:
-----------------

-  RDP into Jumphost (login/password : student/401elliottW!)

-  Access to BIG-IP GUI (https://10.0.0.4/ or
   https://bigip1.agility.f5.com/ ) via Google Chrome

   (login/password : admin/401elliottW!)

TASK 1: Create an ASM Logging Profile
-------------------------------------

Navigate to **Security** >> **Event Logs** >> **Logging Profiles** page
and then click **Create**.

+----------------------------------------------------------------------+------------------------+------------------------+
| **Configuration utility**                                            |
+======================================================================+========================+========================+
| **Security » Event Logs : Logging Profiles** then click **Create**   |
+----------------------------------------------------------------------+------------------------+------------------------+
| Logging Profile Properties                                           |
+----------------------------------------------------------------------+------------------------+------------------------+
|                                                                      | Profile Name           | **log-all**            |
+----------------------------------------------------------------------+------------------------+------------------------+
|                                                                      | Application Security   | **checked**            |
+----------------------------------------------------------------------+------------------------+------------------------+
|                                                                      | Configuration          | **Advanced**           |
+----------------------------------------------------------------------+------------------------+------------------------+
|                                                                      | Response Logging       | **For all Requests**   |
+----------------------------------------------------------------------+------------------------+------------------------+
|                                                                      | Request Type           | **All Requests**       |
+----------------------------------------------------------------------+------------------------+------------------------+
| When finished, click…                                                | **Finished**           |
+----------------------------------------------------------------------+------------------------+------------------------+

|image4|
--------

Navigate to **Local Traffic** >> **Virtual Servers.** Click on
**dvwa\_vs** >> **Security** >> **Policies**. Change the **Log Profile**
from **Disabled** to **Enabled.** From the available list, choose
**log-all** and click the << box to enable it. Then click **Update.**

|image5|

Task 2: Rapid Policy Deployment
-------------------------------

Create a security policy using Rapid Deployment
-----------------------------------------------

Navigate to **Security** >> **Application** **Security** >> **Security**
**Policies** page and then click **Create**.

On the **Policy Creation** screen click **Advanced** and configure as
follows:

+----------------------------------------------------------------------------+-----------------------+-------------------------------+
| **Configuration utility**                                                  |
+============================================================================+=======================+===============================+
| **Security ›› Application Security : Security Policies : Policies List**   |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
| Logging Profile Properties                                                 |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Policy Name           | **lab-rapid-deployment**      |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Policy Template       | **Rapid Deployment Policy**   |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Virtual Server        | **dvwa\_vs**                  |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Server Technologies   | **Apache Tomcat**             |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            |                       | **Apache/NCSA HTTP Server**   |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            |                       | **MySQL**                     |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            |                       | **PHP**                       |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Signature Staging     | **Disabled**                  |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
| When finished, click…                                                      | **Finished**          |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+

|image6|

|image7|

Then click **Create Policy…**

|image8|

Congratulations, the rapid deployment security policy has been deployed
in transparent enforcement mode.

Next, we will validate that the policy is seeing traffic and logging it.
Open **Firefox** and click the **Damn Vunerable Web App (DVWA)**
shortcut, or browse to
`**https://10.128.10.20/login.php** <https://10.128.10.20/login.php>`__

|image9|

**Login** with the username **admin** and the password **password**.

Switch back the **Chrome** to administer the F5. Navigate to
**Security** >> **Event Logs** >> **Application** >> **Requests.**
Change **Request List** from **Illegal Requests** to **All Requests.**
You should have some events from when you browsed
https://auction.f5.com.

**Was your request blocked? Why or Why not?**

|image10|

Now that we are certain that traffic is passing thru the policy, let’s
generate some malicious traffic. To be specific, we will generate a SQL
Injection (SQLi).

Under **User Login**, enter **‘or 1=1**\ # into the **Username** text
box and click **Go!**

Once you’ve clicked **Go!** You will be logged in via SQLi):

.. |image0| image:: media/image1.jpeg
   :width: 1.26181in
   :height: 1.11319in
.. |image1| image:: media/image2.png
   :width: 6.50000in
   :height: 2.82286in
.. |image2| image:: media/image3.jpg
   :width: 1.00000in
   :height: 1.00000in
.. |image3| image:: media/image4.jpg
   :width: 0.96000in
   :height: 1.00000in
.. |image4| image:: media/image5.tiff
   :width: 4.97569in
   :height: 4.36543in
.. |image5| image:: media/image6.tiff
   :width: 5.01042in
   :height: 5.57837in
.. |image6| image:: media/image7.tiff
   :width: 6.50000in
   :height: 3.00764in
.. |image7| image:: media/image8.tiff
   :width: 6.50000in
   :height: 2.56736in
.. |image8| image:: media/image9.tiff
   :width: 6.50000in
   :height: 2.97639in
.. |image9| image:: media/image10.tiff
   :width: 4.99028in
   :height: 4.12284in
.. |image10| image:: media/image11.gif
   :width: 6.48611in
   :height: 2.72222in
