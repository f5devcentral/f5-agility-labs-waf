Configuring DataSafe Credential Protections
-------------------------------------------

F5 Advanced WAF includes DataSafe which can protect your web applications from credential theft by MITB malware.
In this exercise you will configure DataSafe to protect the Hackazon login page from credential theft.

Create DataSafe Profile
~~~~~~~~~~~~~~~~~~~~~~~

  In the BIG-IP. browse to **Security >> Data Protection >> DataSafe Profiles**.

  Click **Create** to create a new DataSafe profile.

  For the Profile Name enter **Hackazon-login**, then click on the **URL List**.

  |image15|

Define protected URL
~~~~~~~~~~~~~~~~~~~~

  In the URL List screen click **Create URL**.

  In the Create New URL screen enter **/user/login** in the **URL Path** field.

  This defines the URL to be protected.  We also need to define the fields that we want to protect and how we want to protect them.
  Click on the **Parameters** section.

  |image16|

  In the Parameters screen, click **Add**.

  In the **New Parameter** screen enter **username** for the **Parameter name**.
  Select to enable the **Obfuscate** feature for this parameter. Click **Repeat**.

  |image17|

  In the **New Parameter** screen enter **password** for the **Parameter name**.
  Select to enable the **Encrypt**, **Substitute Value**, and **Obfuscate** features for this parameter.
  Click **Create**.

  |image18|

  .. NOTE::
    We will discuss each of these features and their purpose in the **Validating DataSafe Configuration** section later in this lab.

  You are returned to the Parameters screen.  You should see the password and username parameters listed
  with the respective settings configured in the previous steps.

  |image19|

  Click **Application Layer Encryption** to review and configure the settings there.

Configure ALE Options
~~~~~~~~~~~~~~~~~~~~~

  In the **Application Layer Encryption** screen, select to enable **Add Decoy Inputs** and **Remove Element IDs**.  Click **Save**.

  |image20|

  .. NOTE::
    We will discuss each of these features and their purpose in the **Validating DataSafe Configuration** section later in this lab.

  The DataSafe profile is now created and configured to protect the Hackazon login page.  However,
  it must be assigned to the Hackazon virtual server to protect the page.

Associate DataSafe Profile with Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  IN the BIG-IP, browse to **Local Traffic >> Virtual Servers >> Virtual Server List**.

  Click on the **Hackazon_protected_virtual** .  Then, from the **Security** tab, choose **Policies**.

  |image21|

  For the **Anti-Fraud Profile** select **Enabled...** and choose the DataSafe profile you created in the previous exercise.
  Click **Update**.

  |image22|




.. |image1| image:: /_static/class8/credprotect/image1.png
.. |image2| image:: /_static/class8/credprotect/image2.png
.. |image3| image:: /_static/class8/credprotect/image3.png
.. |image4| image:: /_static/class8/credprotect/image4.png
.. |image5| image:: /_static/class8/credprotect/image5.png
.. |image6| image:: /_static/class8/credprotect/image6.png
.. |image7| image:: /_static/class8/credprotect/image7.png
.. |image8| image:: /_static/class8/credprotect/image8.png
.. |image9| image:: /_static/class8/credprotect/image9.png
.. |image10| image:: /_static/class8/credprotect/image10.png
.. |image11| image:: /_static/class8/credprotect/image11.png
.. |image12| image:: /_static/class8/credprotect/image12.png
.. |image13| image:: /_static/class8/credprotect/image13.png
.. |image14| image:: /_static/class8/credprotect/image14.png
.. |image15| image:: /_static/class8/credprotect/image15.png
.. |image16| image:: /_static/class8/credprotect/image16.png
.. |image17| image:: /_static/class8/credprotect/image17.png
.. |image18| image:: /_static/class8/credprotect/image18.png
.. |image19| image:: /_static/class8/credprotect/image19.png
.. |image20| image:: /_static/class8/credprotect/image20.png
.. |image21| image:: /_static/class8/credprotect/image21.png
.. |image22| image:: /_static/class8/credprotect/image22.png
.. |image23| image:: /_static/class8/credprotect/image23.png
.. |image24| image:: /_static/class8/credprotect/image24.png
.. |image25| image:: /_static/class8/credprotect/image25.png
.. |image26| image:: /_static/class8/credprotect/image26.png
.. |image27| image:: /_static/class8/credprotect/image27.png
