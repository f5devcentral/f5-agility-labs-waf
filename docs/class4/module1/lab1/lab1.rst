Lab 1: Bot Defense
-------------------------------------------

..  |log_profile| image:: images/log_profile.png
        :width: 800px
..  |blank_vs| image:: images/blank_vs.png
        :width: 800px
..  |bot_profile| image:: images/bot_profile.png
        :width: 800px
..  |bot_vs| image:: images/bot_vs.png
        :width: 800px
..  |setblock| image:: images/setblock.png
        :width: 800px
..  |pbd| image:: images/pbd.png
        :width: 800px
..  |block_req| image:: images/block_req.png
        :width: 800px
..  |except_search| image:: images/except_search.png
        :width: 800px
..  |captcha| image:: images/captcha.png
        :width: 800px
..  |honey| image:: images/honey.png
        :width: 800px
..  |dashboard| image:: images/dashboard.png
        :width: 800px
..  |clean_prof| image:: images/clean_prof.png
        :width: 800px



Objective
~~~~~~~~~

- Create a Bot Defense profile with a balanced approach
- Understand the difference in Bot Defense Templates and Bot Categories
- Block a Bot Request

-  Estimated time for completion: **20** **minutes**

        .. IMPORTANT:: To clearly demonstrate the Bot Defense profile, please disable any previously configured security profiles on the virtual server.”

        |blank_vs|

Enabling Bot Defense 
~~~~~~~~~~~~~~~~~~~~

#.  Navigate to **Security > Event Logs > Logging Profiles** and check to see if the Bot_Log Profile is created.  If not, create a new Logging Profile with the settings shown in the screenshot below and click **create**. 

        |log_profile|

#.  Navigate to **Security > Bot Defense > Bot Defense Profiles** and check to see if insecureApp1_botprofile has been created.  If not, click **Create**.
#.  Name: **insecureApp1_botprofile**
#.  Profile Template: **Relaxed**
#.  Click the **Learn more** link to see an explanation of the options. 

        |bot_profile|

#.  Click on the **Bot Mitigation Settings** tab and review the default configuration.
#.  Click on the **Signature Enforcement** tab and review the default configuration.
#.  Click **Save**.
#.  Navigate to **Local Traffic > Virtual Servers > Virtual Server List > insecureApp1_vs > Security > Policies**
#.  Check to make sure that Bot Defense is enabled and select the  **insecureApp1_botprofile** and the **Bot_Log** profiles. 
#.  Click **Update**

        |bot_vs|


A Balanced Approach 
~~~~~~~~~~~~~~~~~~~

In WAF141 we viewed logs showing that bots were indeed connecting to our app.  In your environment, there may be some bots that are welcome, while others are unknown or malicious.  Please note that these next steps are to give you an idea on how some bots can be mitigated, but every envrionment is different.

#.  Navigate to **Security > Bot Defense > Bot Defense Profiles** and click on **insecureApp1_botprofile**

    .. NOTE:: The profile we are using was created with a "Relaxed" template.  In order to start with a Balanced Approach, you would need to create a new Profile.  Instead, here we will change individual settings.  Click on **Learn More** if you are interested in the other default options.


#.  Under General Settings, change the Enforcement Mode to Blocking

        |setblock|

#.  Click on the Browsers tab on the left and Change the Browser Verification setting to **Verify Before Access**, then ensure that the grace period is set to **10 Seconds**.

        |pbd|

#.  Save the changes to your Bot Defense profile.


Block a Bot Request
~~~~~~~~~~~~~~~~~~~

#.  Open Terminal on the Client Workstation
#.  Run the same Curl command we have previously used in WAF141

        ``curl https://10.1.10.145/WebGoat/login -k -v``

#.  Navigate to **Security > Event Logs > Bot Defense > Bot Requests** and review the event logs. Was the Request blocked?
#.  Navigate to **Security > Bot Defense > Bot Defense Profiles** and select **insecureApp1_botprofile**
#.  Look at your Mitigation Settings.  Curl is listed as an Untrusted Bot, and the action is **Alarm**
#.  Make sure the Mitigation Setting for Malicious Bots is set to **Block**
#.  Open Terminal on the Client Workstation and run the following curl command

        ``curl https://10.1.10.145/WebGoat/login -k -H "User-Agent: Mozilla/5.00 (Nikto/2.1.6) (Evasions:None) (Test:Port Check)"``

#.  Navigate to **Security > Event Logs > Bot Defense > Bot Requests** and review the event logs again.  You should now see a blocked request.

        |block_req|


Mitigations by Category
~~~~~~~~~~~~~~~~~~~~~~~

    .. NOTE:: Mitigations are now managed by Category and specific known bots, allowing a Security Administrator to customize the Bot Profile for their Application.

#.  Navigate to **Security > Bot Defense > Bot Defense Profiles** and select **insecureApp1_botprofile**
#.  Click on the tab for **Bot Mitigation Settings**
#.  Select **CAPTCHA** for **Malicious Bot** and click **Save**

	|captcha|

#.  Open Terminal on the Client Workstation and run the previous Nikto curl command.

	``curl https://10.1.10.145/WebGoat/login -k -H "User-Agent: Mozilla/5.00 (Nikto/2.1.6) (Evasions:None) (Test:Port Check)"``

#.  Take a look at the response and check the Bot Request logs on BIG-IP again.
#.  Navingate to **Security > Bot Defense > Bot Defense Profiles** and select **insecureApp1_botprofile**
#.  Click on the tab for **Bot Mitigation Settings**
#.  Select **Add Exceptions** and search for **nikto**

	|except_search|

#.  Click **Add** and change the Mitigation to **Honeypot Page**

	|honey|

#.  Click **Save**.
#.  Run the curl command again from above and take a look at the results.
#.  Navigate to **Security > Event Logs > Bot Defense > Bot Traffic** and take a look at the dashboard. This dashboard will show all of your mitigations for each Virtual Server that has a Bot Profile

	|dashboard|

Remove the Bot Profile
~~~~~~~~~~~~~~~~~~~~~~

#.  Navigate to **Local Traffic > Virtual Servers > Virtual Server List > insecureApp1_vs > Security > Policies**
#.  Change Bot Defense pofile to **Disabled**
#.  Click **Update**


	|clean_prof|


**This completes Lab 1**
