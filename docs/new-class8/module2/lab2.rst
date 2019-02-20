Configuring Brute Force Protection
----------------------------------

Before we can protect a login page from brute force attacks, we must
define the login page and its properties. This defines the URL for
the login page, what parameters are used for username and password,
and how to differentiate a successful login from a failed login
attempt.

In this lab we will use the information gathered in the previous exercise to configure a login page in the WAF policy.

Define Login Page
~~~~~~~~~~~~~~~~~

  Browse to **Security >> Application Security >> Sessions and Logins >> Login Pages List**. Click **Create**.

  In the **Login Page Properties** screen, complete the configuration using the information you collected in the previous exercise. When finished click **Create**.

  |image12|

  .. TIP::
    Review the properties on this page. There are multiple ways to configure ASM to tell the difference between a successful login and a failed login attempt.

Enable Brute Force Protection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  Now that the login page is defined in the policy, we can configure
  Brute Force (and Credential Stuffing) protections for it.

  Browse to **Security >> Application Security >> Brute Force Attack Prevention**. Click **Create.**

  In the **Brute Force Protection Configuration** screen, select the Login Page you created in the previous exercise.

  For the purposes of this lab we will change the **Detection Period** and **Maximum Prevention Duration** to **2** minutes. Also, change the Leave all other settings are their defaults.

  .. NOTE::
    This will help us more quickly separate the different detection methods as we move through the lab.

  |image13|

  When finished click **Create**.

  .. WARNING::
    Click **Apply Policy** to make these changes effective in the policy.
    |image14|




.. |image4| image:: /_static/class8/credstuff/image5.png
.. |image5| image:: /_static/class8/credstuff/image6.png
.. |image6| image:: /_static/class8/credstuff/image7.png
.. |image7| image:: /_static/class8/credstuff/image8.png
.. |image8| image:: /_static/class8/credstuff/image9.png
.. |image9| image:: /_static/class8/credstuff/image10.png
.. |image10| image:: /_static/class8/credstuff/image7.png
.. |image11| image:: /_static/class8/credstuff/image11.png
.. |image12| image:: /_static/class8/credstuff/image12.png
.. |image13| image:: /_static/class8/credstuff/image13.png
.. |image14| image:: /_static/class8/credstuff/image14.png
.. |image15| image:: /_static/class8/credstuff/image15.png
.. |image16| image:: /_static/class8/credstuff/image16.png
.. |image17| image:: /_static/class8/credstuff/image17.png
.. |image18| image:: /_static/class8/credstuff/image18.png
.. |image19| image:: /_static/class8/credstuff/image19.png
.. |image20| image:: /_static/class8/credstuff/image20.png
.. |image21| image:: /_static/class8/credstuff/image21.png
.. |image22| image:: /_static/class8/credstuff/image22.png
.. |image23| image:: /_static/class8/credstuff/image23.png
.. |image24| image:: /_static/class8/credstuff/image24.png
.. |image25| image:: /_static/class8/credstuff/image25.png
.. |image26| image:: /_static/class8/credstuff/image26.png
.. |image27| image:: /_static/class8/credstuff/image27.png
.. |image28| image:: /_static/class8/credstuff/image28.png
.. |image29| image:: /_static/class8/credstuff/image29.png
.. |image30| image:: /_static/class8/credstuff/image30.png
.. |image31| image:: /_static/class8/credstuff/image31.png
.. |image32| image:: /_static/class8/credstuff/image32.png
.. |image33| image:: /_static/class8/credstuff/image33.png
.. |image34| image:: /_static/class8/credstuff/image34.png
