Lab 1.2: Credential Stuffing
----------------------------

Credential stuffing is a type of brute force attack that leverages stolen credentials from another source. This source is most commonly the breach of a widely used online service.  These leaked credentials are then levered in an attempt to compromise higher value targets in instances where users used the same credentials across multiple services. BIG-IP now has the capability to detect these types of attacks by employing a database of credentials that are known to have been compromised in a previous breach. The credentials are stored as one-way hashed usernames and passwords to protect them from further disclosure. In a production environment, Client Side Integrity Defense (or both), may be a more effective form of mitigation during an actual attack.  Feel free to experiment with this in the lab.

Task 1 - Configure Credential Stuffing Detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open the BIG-IP GUI interface. 
    
#. Navigate to **Security -> Application Security  -> Brute Force Attack Prevention**.

#. Click on the /rest/user/login configuration created earlier.

#. Configure **Credential Stuffing** detection within the **Distributed Brute Force Protection** Section as follows:

   .. image:: images/dist_brute_force_protection.PNG
      :width: 600 px

#. Click **Save** .
    
#. Click **Apply Policy**.

Task 2 - Test Credential Stuffing Detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
#. Open a new Private Browsing window in **Chrome or Firefox** .

#. Go to the to Juice Shop login page at ``https://juiceshop.f5agility.com/#/login`` 

#. Attempt to login using the username ``demo33@fidnet.com`` and password ``mountainman01``. One the THIRD attempt, you should receive a blocking page.

   .. image:: images/blocking_page.PNG
      :width: 600 px

#. Examine the most recent requests in the event log by navigating to Security -> Event Logs -> Applications -> Requests

   .. image:: images/brute_force_events.PNG
      :width: 600 px

   Take note of the username field.  The request was matched as a potential credential stuffing attack.

#. Near the **Brute force: Maximum Login Attempts are exceeded** header at the top of the event window click on the number under **Occurrences**:


   The message indicates the number of login attempts that matched the internal database.

#. Now check out the reporting under **Event Logs -> Application -> Brute Force Attacks**:

   .. image:: images/brute_force_enent_log.PNG
      :width: 600 px

#. Click on one of the attack entries to get some more detail about the attack:

#. For fun, head over to ``https://haveibeenpwned.com/`` and put in the email address of the account we used in the lab to get some details.  It may also be interesting to put in your own account(s) to see if any of your credentials have been breached.  You could also try some of your old username/password combinations against the credential stuffing database on the F5.  While on the main page explore some of the breach data on the bottom to get a sense of how big this problem is.

#. In order to release any blocking that's currently in place, navigate to **Security -> Application Security -> Brute Force Attack Prevention** and **Delete** the Brute Force configuration we created previously.

#. Click **Apply Policy** .

#. Navigate to **Local Traffic > Virtual Servers > Virtual Server List > owasp_juice_shop_443_vs > Security > Policies** and ensure that the juice_shop_waf policy and the Log All requests log profile are enabled on the owasp_juice_shop_443_vs virtual server as shown below removing the Bot Profile.

   .. image:: images/vs_config.PNG
      :width: 600 px

|
|

**This concludes Lab 1.2**
