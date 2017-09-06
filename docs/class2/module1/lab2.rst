Rapid Deployment
--------------------------------------------------------

Navigate to **Security >> Application Security >> Security Policies**
page and then click **Create**.

On the **Policy Creation** screen click **Advanced** and configure as
follows:

+----------------------------------------------------------------------------+-----------------------+-------------------------------+
| **Configuration utility**                                                  |                                                       |
+============================================================================+=======================+===============================+
| **Security ›› Application Security : Security Policies : Policies List**   |                                                       |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
| Logging Profile Properties                                                 |                                                       |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Mode                  | **Advanced**                  |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Policy Name           | **lab-rapid-deployment**      |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Policy Template       | **Rapid Deployment Policy**   |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Virtual Server        | **dvwa\_vs**                  |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Server Technologies   | **Apache/NCSA HTTP Server**   |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            |                       | **MySQL**                     |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            |                       | **PHP**                       |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            |                       | **Unix/Linux**                |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
|                                                                            | Signature Staging     | **Disabled**                  |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+
| When finished, click…                                                      | **Create Policy**     |                               |
+----------------------------------------------------------------------------+-----------------------+-------------------------------+

.. image:: /_static/class2/image4.tiff

.. image:: /_static/class2/image5.tiff

Click **Create Policy**\ …

.. image:: /_static/class2/image6.tiff

Congratulations, the rapid deployment security policy has been deployed
in transparent enforcement mode.

Next, we will verify that the policy is observing the application
traffic. Open Firefox and click the **Damn Vunerable Web App (DVWA)**
shortcut, or browse to
`**https://10.128.10.20/login.php** <https://10.128.10.20/login.php>`__

.. image:: /_static/class2/image7.tiff

**Login** with the username **admin** and the password **password**.

Switch back the **Chrome** to administer the BIG-IP. Navigate to
**Security** >> **Event Logs** >> **Application** >> **Requests.** Click
the **X** next to **Illegal Requests** to view all requests\ **.** You
should have some events from the previous login.

.. image:: /_static/class2/image8.tiff

Now that we are certain that traffic is passing through the policy,
we’ll generate some malicious traffic and observe the effect.

We’ll first start with a basic SQL injection attack. Return to Firefox
and click the SQL Injection link along the left side of the page. You
should see a field that looks like this:

.. image:: /_static/class2/image9.tiff

Enter **‘or 1=1**\ # into the text box and click **Submit.**

If the attack was successful, you should be presented with a list of
usernames from the database like the one below:

.. image:: /_static/class2/image10.tiff

Switch back to Chrome and navigate to **Security** >> **Event Logs** >>
**Application** >> **Requests.** You will see one or more Illegal
Requests associated with the attack:

.. image:: /_static/class2/image11.tiff

Click on the first event associated with **/vulnerabilities/sqli/** and
click **All Details**. Notice that the violation was identified as
**Attack signature detected.** Clicking on this header will provide
detailed information about the signature or signatures and why they’ve
tripped:

.. image:: /_static/class2/image12.tiff

Scroll down to view details about the attack, the content of the decoded
request, the original request, and the response it generated from the
application:

.. image:: /_static/class2/image13.tiff

.. image:: /_static/class2/image14.tiff
