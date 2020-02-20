Lab 1: Bot Defense
-------------------------------------------

Objective
~~~~~~~~

- Create a Bot Defense profile with a balanced approach
- Understand the difference in Bot Defense Templates and Bot Categories
- Block a Bot Request

-  Estimated time for completion: **20** **minutes**

.. IMPORTANT:: To clearly demonstrate just the Bot Defense profile, please **disable all security policy on the virtual server**.

.. image:: images/blank_vs.png
  :width: 600 px

Enabling Bot Defense 
~~~~~~~~~~~~~~~~~~~

#.  Navigate to **Security > Event Logs > Logging Profiles** and check to see if the Bot_Log Profile is created.  If not, create a new Logging Profile with the settings shown in the screenshot below and click **create**. 

.. image:: images/log_profile.png
  :width: 600 px

#.  Navigate to **Security > Bot Defense > Bot Defense Profiles** and check to see if insecureApp1_botprofile has been created.  If not, click **Create**.
#.  Name: **insecureApp1_botprofile**
#.  Profile Template: **Relaxed**
#.  Click the **Learn more** link to see an explanation of the options. 

.. image:: images/bot_profile.png
  :width: 600 px

#.  Click on the **Bot Mitigation Settings** tab and review the default configuration.
#.  Click on the **Signature Enforcement** tab and review the default configuration.
#.  Click **Save**.
#.  Navigate to **Local Traffic > Virtual Servers > Virtual Server List > insecureApp1_vs > Security > Policies**
#.  Check to make sure that Bot Defense is enabled and select the  **insecureApp1_botprofile** and the **Bot_Log** profiles. 
#.  Click **Update**

.. image:: images/bot_vs.png
  :width: 600 px


A Balanced Approach 
~~~~~~~~~~~~~~~~~~

In WAF141 we viewed logs showing that bots were indeed connecting to our app.  In your environment, there may be some bots that are welcome, while others are unknown or malicious.  Please note that these next steps are to give you an idea on how some bots can be mitigated, but every envrionment is different.

#.  Navigate to **Security > Bot Defense > Bot Defense Profiles** and click on **insecureApp1_botprofile**
.. NOTE:: The profile we are using was created with a "Relaxed" template.  In order to start with a Balanced Approach, you would need to create a new Profile.  Instead, here we will change individual settings.  Click on **Learn More** if you are interested in the other default options.

#.  Under General Settings, change the Enforcement Mode to Blocking and click Save.

.. image:: images/setblock.png
  :width: 600 px

#.  Click on the Browsers tab on the left and Change the Browser Verification setting to **Verify Before Access**

.. image:: images/pbd.png
  :width: 600 px

Before The Unified Bot Defense Profile was introduced in 14.1, this was the default and only setting if ProActive Bot Defense was enabled.

#.  Save the changes to your Bot Defense profile.
 


Block a Bot Request
~~~~~~~~~~~~~~~~~~

#.  Open Terminal on the Client Workstation
#.  Run the same Curl command we have previously used in WAF141

.. code-block:: bash
        curl https://10.1.10.145/WebGoat/login -k -v

#.  Navigate to **Security > Event Logs > Bot Defense > Bot Requests** and review the event logs.
Was the Request blocked?

#.  Navigate to **Security > Bot Defense > Bot Defense Profiles** and select **insecureApp1_botprofile**
#.  Look at your Mitigation Settings.  Curl is listed as an Untrusted Bot, and the action is **Alarm**
#.  Make sure the Mitigation Setting for Malicious Bots is set to **Block**
#.  Open Terminal on the Client Workstation and run the following curl command

.. code-block:: bash

        curl https://10.1.10.145/WebGoat/login -k -H "User-Agent: Mozilla/5.00 (Nikto/2.1.6) (Evasions:None) (Test:Port Check)"


#.  Navigate to **Security > Event Logs > Bot Defense > Bot Requests** and review the event logs again.  You should now see a blocked request.

.. image:: images/block_req.png
  :width: 600 px

**This completes Lab 1**
