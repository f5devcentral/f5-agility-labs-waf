Lab 3 – Refine your security posture using the OWASP Dashboard
---------------------------------------------------------------
Objective
~~~~~~~~~~~~~~~~

- Continue to apply protections to your security policy

- Protect a logon page

- Assess the rest of the dashbard to apply more protections and document other best practices in your policy

Task – We will continue applying protections while working down the Dashboard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. On the Main tab, click **Security > Overview > OWASP Compliance**. Click on the expand arrow next to A1 Injection.  At the bottom you can see the missing piece for 100% Injection protection is applying **Evasion Techniques**.  

#. At this point clicking on the checkmark and applying would implement Evasion Technique protection.  You are welcome to do this from the dashboard, but let's see how the dashboard interacts with a manual change to the policy.  Perform the following steps to apply in the policy.

    - Go to **Security -> Application Security -> Policy Building -> Learning and Blocking Settings**
    - Click and expand the section titled **Evasion Technique detected** 
    - Click the checkbox for **Enable** all
    - Press **Save** at the bottom of that screen
    - Press **Apply Policy** button at the top right corner of your screen

    .. image:: ../images/evasiontechniques.png

#. Go back to the Dashboard.  Click **Security > Overview > OWASP Compliance**.  You now see you are 100% protected against A1 Injection.  Now expand **A2 Broken Authentication**.  You can see with some of the default protections, and the previous attack signatures we applied are providing some protections.  The signatures we applied previously protect against some auth attacks, and cookie tampering protection is on by default when applying a base policy.

    - To the right of **Session Highjacking Protection** click on the **Enforce** checkmark.  You will now see the potential protections percentage for Broken Authentication increase. Press the blue **Review & Update** button below.  Then the  **Save & Apply Policy** button.

    .. Note:: Unfortunately protecting against all of the OWASP top 10 is not always as easy as applying attack signatures. In some cases you need to apply more app specific protections such as a logon page.  If your application does not have a logon page, this would be a good example of when to select the no symbol (we call it the ghostbuster symbol) button, which will ignore the requirement since it does not apply.

#. The following steps will declare our login page for the Juice Shop app, then we will apply more A2 Broken Authenticaton protections against it.

    - Under A2 click the link named **Not Fulfilled** next to Login Enforcement.  This is just a link/shortcut to the login page settings.  

        .. image:: ../images/loginenforcement.png

    - This opens a new tab in the policy where you declare the info for your login page.  Press **Create** on the top right corner of the page.  
    - In the login URL field enter ``/#/login``
    - In **Authentication Type** select **HTML Form**
    - Type ``email`` in the **Username Parameter Name**
    - Type ``password`` in the **Password Parameter Name**
    - Type ``Invalid`` in the **A string that should NOT appear in the response** field

        .. image:: ../images/loginform.png

    .. Note:: You can identify the strings and parameters listed above by either getting info from the application developers or by using tools built into your own browser.  Here is a method from one of our F5 videos, the link brings you right to that discovery method https://youtu.be/YqswibSgMyk?t=178

    - Click the **Create** button at the bottom of the page.  

#. Now we will apply brute force protection to the login page we created

    - Go to **Security -> Application Security -> Brute Force Attack Prevention**
    - Click **Create** in the top right corner
    - On **Login Page** select the login page we just created ``/#/login``
    - Here you can view the mitigatons and thresholds for Brute Force Protection.  For the lab, we will leave the settings at their defaults, and press the **Create** button below.
    - Press the **Apply Policy** button in the top right corner.
    - You can close that tab and now go back to your other OWASP tab and refresh the page.

    .. Note:: Notice we are not at 100% completion for A2 risks.  We will return to this in the next section as the configurations are a little more advanced.  

#. Back on the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**. Click on the expand arrow next to **A3 Sensitive Data Exposure** and notice that previous protections we put in place satisfied many of the requirements.  Applying DataGuard will inspect outbound traffic for any sensitive information being sent from your application.  The power of our full proxy archetecture makes this protection possible.

    - To the right of **DataGuard** click on the **Enforce** checkmark.  You will now see the potential protections increase to 100%.  Press the blue **Review & Update** button below.  Then the  **Save & Apply Policy** button.

    .. Note:: The default settings of Data Guard will prevent the transmission of number sequences matching credit card and social security numbers.  This can be customized to match patterns sensitive within your organization, but is out of scope for this level of class.  To see these settings though, go to menu **Security -> Application Security -> Data Guard**

#. Back on the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**. At this time we are going to skip a few of the next controls, as their configuration is a little more advanced.  Click on the expand arrow next to **A6 Security Misconfiguration**.

    .. Note:: The catagories A6, A9, and the 10th (notice how we refuse to write that one out) cover practices that require controls outside the scope of a WAF. The administrator will need to manually evaluate whether these conditions are being met for this application.

    - In the A6 list, these may be processes you currently run, or they can be left as a reminder that you are not currently applying these controls. Click the **?** next to each best practice to see a more detailed description.
    - Click on the **checkmark** for all processes that your organization is currently following for the application.  You can also click the **No/Ghostbuster** symbol here if the condition is not met.
    - Below is an example, but you may complete this any way you choose.

        .. image:: ../images/securitymisconfig.png

        .. Note:: In this example, we have marked that we are performing application and vulnerability scanning.  We have chosen to ignore the app and system patching (An example why would be a legacy system or app that no longer recieves patching).  In this instance, we want to ignore that requirement as it is not applicable to the application. In our example, App System hardening is a practice that we have not yet implemented, so we will leave this unsatisfied until that is complete. 

#. On the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**. Click on the expand arrow next to **A8 Insecure Deserialization**.  You can see we are already at 100% coverage for this risk.  Previously applied signatures that covered other risks are also protecting us here.  You can click around in this area to see more info on the risks and each signature set.  

#. On the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**. Click on the expand arrow next to **A9 Using Components with Known Vulnerabilities**.  While the risk is different than A6, the best practices that best mitigate this risk are the same.  This can give more validity to start applying these practices in your process.

#. On the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**. Click on the expand arrow next to the 10th risk **Insufficient Logging & Monitoring**.  This will be another manual risk protection.  Since logging profiles are added in the virtual server confiuration the dashboard cannot read if there is logging in the WAF policy.  The good news is in we already did this work.  If you remember we added a logging profile right after we built our initial configuration using the guided configuration.  

    - Click on the **Checkmark** next to **Log Illegal Requests**.  Since we already added this type of logging to our virtual server.  
    - We do not and never will have a remote logging server or SIEM in this environemnt, so I will choose to ignore it by clicking our **No/Ghostbuster Symbol**
    - Click **Review & Update** button below and then **Save & Apply**.

#. Way to go!  You now have a WAF policy that is protecting against a significant portion of the OWASP Top 10.
