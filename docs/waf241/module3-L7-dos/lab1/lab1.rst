Lab 3: Behavioral DoS Protection
----------------------------------

In this lab you will use a baseline traffic generation script and an Apache Bench based attack script against a Virtual Server in both transparent and blocking mode to trigger Behavioral DoS Protection. **Unlimited Behavioral DoS protection profiles are a feature of Advanced WAF.**. 


Test Default Site Behavior
~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. Navigate to **Local Traffic > Virtual Servers > owasp-juiceshop_443_vs > Security > Policies**. 
#. **Disable** all Policies and Logging Profiles so that we can effectively demonstrate just the DoS mitigation.  
#. Click **Update**.

   Your Virtual Server should look like this:

   .. image:: images/dos_vs.png
    :width: 600 px

#. Open a new **Terminal** window and run the **baseline_menu.sh** script in the **Agility2021wafTools** directory.

   .. code-block:: bash

    cd ~/Agility2021wafTools/
    ./baseline_menu.sh

5. Choose **Option 2** and hit the **Return Key or Enter key**. 
#. You will see the script start sending traffic to the site and you should see all responses with an http code of **status: 200**.

.. image:: images/status.png
  :width: 600 px

7. While the script is still running, open a new browser tab and click on the **OWASP JuiceShop** bookmark. 
8. Browse around the site and refresh the page a few times. You should not notice any lag in response time and everything should load relatively quickly in the browser even with the baseline script running in the background.

Start the Attack
~~~~~~~~~~~~~~~~~~~~

#. Open a new **Terminal** tab and ensure you are in the **~/Agility2021wafTools/** directory and run the AB_SSL_DOS.sh script.

    .. code-block:: bash

        cd ~/Agility2021wafTools/
        ./AB_SSL_DOS.sh
    ..

2. Choose **Option 1** and hit the **Return Key or Enter key**. 
3. Back in Chrome browser, attempt to refresh the site. **There are no smoke and mirrors here.** The Apache Bench script almost instantly knocked this single container site offline. If it isn't offline, then it's horribly slow and un-usable. **There was no special configuration on the server side.**
4. Stop the Apache Bench script by hitting (Ctrl + C) and then type the # **4** and hit the **Return Key or Enter key**.
5. In JuiceShop refresh the page a few times. The site should recover quickly as the connections die down. 
6. **Leave the baseline_menu script running**. 

**Questions**: What do you do when you are shopping online and a site is behaving like this? Do you think attackers and/or competing entities ever use this to their advantage?

Advanced WAF to the Rescue
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For demonstration purposes in this lab, we will simply configure Source IP based DoS Protection, although there are several selectors available including DoS mitigation based on Device ID, Geolocation, URL, and even Site Wide. 

#. In the Advanced WAF tab of Chrome, navigate to **Security > DoS Protection > Protection Profiles** and click **Create**.
#. Name the profile **juiceshop_dos** and click **Behavioral & Stress-based Detection** to the left. 
#. Configure the **Behavioral & Stress-based Detection** settings like below:
  
  * Operation Mode: **Transparent** (It's an F5 recommended best practice to add new features to a policy in transparent mode until you fully understand the impacts.) 

  * Thresholds Mode: **Manual**
  
  * Stress-based Detection and Mitigation: 
  
    * By Source IP: Click **Edit** and check the box at the bottom for **Client-Side Integrity Defense** which tells the WAF to send an Active JS challenge when under attack to verify the browser vs an attacking bot.

* Set the Relative Threshold to 500% and **15** transactions per second. 
* Set the Absolute Threshold TPS to **20**. 

.. image:: images/behav.png
  :width: 600 px
  
* Behavioral Detection and Mitigation: > click **Edit** 
  
    * **Check** the box for **Use TLS patterns as part of host identification**
    
    * **Check** the box for **TLS fingerprinting signatures**

    * Under **Mitigation** read the description of **Standard Protection**.

* Prevention Duration: > click **Edit**
    
    * Escalation Period: **90** seconds
    * De-escalation Period: **360** seconds
  
.. image:: images/bdos.png
  :width: 600 px

4. Click **Finished**

.. IMPORTANT:: What you essentially just configured was a DoS "Client Source IP" traffic categorizer with step-up mitigations. In this case, mitigations will fire in the order that they are shown in the GUI and progress every 90 seconds. First, a client-side integrity check is performed (JS injection) and if necessary the WAF will escalate to issuing a CAPTCHA to offending clients. Finally, Rate-Limiting kicks in as a last resort. You could use any combination of these three mitigation tactics with any of the DoS categorizer types in the profile.  

Apply the Dos Profile and Test
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Local Traffic > Virtual Servers > owasp-juiceshop_443_vs > Security > Policies**. 
#. **Enable** the Dos Protection Profile and choose our new **juiceshop_dos** profile and also **Enable** the **local-dos** Logging Profile. 
#. Click **Update**.

Your virtual server should look like this: 

.. image:: images/vs.png
  :width: 600 px

4. Open a new tab to JuiceShop and browse the site. There should not be any perceivable effect of having applied the DoS profile. 
#. Browse the photo wall from the hamburger menu (top left) and leave some arbitrary Customer Feedback. Spend about a minute browsing the site.
#. Open a new **Terminal** tab and start the attack script again and choose option **1**:

    .. code-block:: bash

        cd ~/Agility2021wafTools/
        ./AB_SSL_DOS.sh

7. Navigate to **Security > Event Logs > DoS > Application Events** and review the entry. It may take a few moments for the event to appear in the dashboard. 
#. Click on the Attack ID #. 

.. image:: images/dos.png
  :width: 600 px
  
1. Once the Dashboard loads, turn on **Real Time** by checking the box at the top of the dashboard. **It will take a few moments for the data to populate. "Real Time" is relative here.**

.. image:: images/bdoslog.png
  :width: 600 px

10. **Eventually...it may take several minutes**, click on the attack graphic and then select the virtual server to the right. You may have to wait a few moments for the Virtual Server to appear.
#. There is alot of information on DoS Visibility Dashboard including the type of attack, the severity, duration and much more. You can use the **Real Time** filters on the right to further dissect the traffic and drill down for analysis. **It may take some time for various data fields to load**.
#. From the right hand filters menu expand **Client IP Addresses**, **Pool Members** and **URLS** and review the attack data. You can drag the boxes to group them closer together as shown here and there is also a flyout. 


.. image:: images/client.png
  :width: 600 px


13. In the top middle of the GUI click the **Analysis** tab and review the system health overview of the BIG-IP device itself. Scroll down and check out the CPU, Connection and Throughput stats. 
14. At the bottom you will get to the HTTP stats which should be of most interest. 

.. image:: images/sys.png
   :width: 600 px
   
|

.. image:: images/http_stats.png
  :width: 600 px

Stop the Baseline and Attack Scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. In each of your terminal windows or tabs type **Ctrl+C** to terminate **all** the scripts including the baseline. The **AB_SSL_DOS.sh** script will require you to enter **4** to completely stop the attacks. 


Enable Blocking in the DoS Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. In the Advanced WAF tab, navigate to **Security > DoS Protection > Protection Profiles > juiceshop_dos** and click on **Behavioral & Stress-based Detection**.
#. Under **Operation Mode** click **Edit** and from the dropdown choose **Blocking** and click **Update**. 
#. Open a new tab to JuiceShop and ensure the site is operating normally. 
#. Open a new Terminal Tab and run the AB_SSL_DOS script again. Choose **Option 1**. 

    .. code-block:: bash

        cd ~/Agility2021wafTools/
        ./AB_SSL_DOS.sh

5. Attempt to refresh JuiceShop..initially it is down, but within about a minute and a few refreshes later, the WAF has figured out the attack and taken mitigation action. 
#. Navigate to **Security > Event Logs > DoS > Application Events** and review the new entries. We can see that the attack was picked up by behavioral mitigation first.
#. Next we can see that the mitigation was changed to **DOS L7 Attack** with **Source IP-Based Client Side Integrity Defense**. This means that the WAF is actively challenging these IP addresses with JS. 
#. Expand the **+** and you will be able to see more details about the mitigation for each of the client IPs. 

.. image:: images/events1.png
  :width: 600 px

.. NOTE:: The Linux client uses 10.1.10.100 as it's primary source IP. This is the IP you are coming from when using the browser. The Apache Bench script is configured to use alternate source IPs (10.1.10.51, .52, and .53).

Verifying Behaviors
~~~~~~~~~~~~~~~~~~~~~~

#. Notice JuiceShop continues to load fine in the browser now that mitigations are in place for the attacking IPs. 
#. Open a new terminal tab and run the following command: ``curl -k https://juiceshop.f5agility.com``
#. Notice the default HTML being returned for the site. You are coming from the **.100** IP address. 

.. image:: images/curl1.png
  :width: 600 px

4. Stop the Apache Bench attack in the terminal window by typing **CTRL + C** and then **4** and hit **Return**. 
#. Now run this command in terminal to send the request from an IP that is being mitigated by DoS profile. ``curl -k --interface 10.1.10.51 https://juiceshop.f5agility.com``.
#. Notice the JavaScript challenge. This IP will continue to be challenged for the duration of the de-escalation period of 360 seconds that we set earlier or as long as the server is under stress from this IP. You should also observe JS injection if you substitute **10.1.10.52 and 10.1.10.53** in the curl request.
#. If for some reason you notice that the JS challenge is not appearing in the response to your curl request, it's possible that the cool-off period (configured in your DoS Profile) has already elapsed. If so, restart the attack (**./AB_SSL_DOS.sh > Option 1**) and let it run for a minute or so, then repeat steps 4 and 5 respectively.
#. You should now observe a JS challenge when submitting a curl request from any of the three IP addresses (.51, .52, or .53), even though the attack has ceased.

.. image:: images/curl2.png
  :width: 600 px

**This concludes Lab 3.**