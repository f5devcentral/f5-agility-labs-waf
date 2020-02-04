Exercise 1.3: Bot Defense with Signatures
-------------------------------------------

Objective
~~~~~~~~~

- Create a Bot Defense logging profile
- Create and apply a transparent Bot Defense Profile with Signatures
- Test and verify logs 
- Add a signature to the whitelist

-  Estimated time for completion: **20** **minutes**

.. IMPORTANT:: To clearly demonstrate just the Bot Defense profile, please **disable all security policy on the virtual server** 

.. image:: images/blank_vs.png
  :width: 600 px

Create Loging Profile 
~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Security > Event Logs > Logging Profiles** and create a new Logging Profile with the settings shown in the screenshot below and click **create**. 

.. image:: images/log_profile.png
  :width: 600 px

#. Navigate to **Security > Bot Defense > Bot Defense Profiles** and click **Create**.
#. Name: **insecureApp1_botprofile**
#. Profile Template: **Relaxed**

.. image:: images/bot_profile.png
  :width: 600 px

#. Click on the **Bot Mitigation Settings** tab and review the default configuration.
#. Click on the **Signature Enforcement** tab and review the default configuration.
#. Click **Save**.
#. Navigate to **Local Traffic > Virtual Servers > Virtual Server List > insecureApp1_vs > Security > Policies**
#. Enable the  Bot Defense Profile: **insecureApp1_botprofile** and the **Bot Log** profile. 
#. Click **Update**

.. image:: images/bot_vs.png
  :width: 600 px

#. Navigate to **Security > Event Logs > Bot Defense > Bot Requests** and review the event logs. 

.. image:: images/bot_log.png
  :width: 600 px