Exercise 1.1: IP Intelligence Policies
---------------------------------------
Objective
~~~~~~~~~

- Configure Global IPI Profile & Logging
- Review Global IPI Logs
- Configure Custom Category and add an IP 
- Create your first WAF Policy and implement IPI w/ XFF inspection

- Estimated time for completion: **30** **minutes**.

Create Your 1st L3 IPI Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
An IPI policy can be created and applied globally, at the virtual server (VS) level or within the WAF policy itself. 
We will follow security best-practice by applying IPI via a Global Policy to secure layer 3 device-wide and within the layer 7 WAF policy to protect the App by inspecting the X-Forwarded-For Header.

.. image:: images/ipi_options.png
  :width: 600 px

In this first lab, we will start by enabling a Global IPI Policy; much like you would do, as a day 1 task for your WAF:

#. RDP to Linux Client and launch Google Chrome Browser. **Do not click multiple times**. It can take a few moments for the browser to launch the first time. 

#. Click the **F5 Advanced WAF bookmark** and login to TMUI. admin/<password>. 

#. On the Main tab, click **Security > Network Firewall > IP Intelligence > Policies**. 

.. image:: images/ipi.png
  :width: 600 px

4. Click on the **Create** button.

#. For the name:  **global_ipi** 

#. Under **IP Intelligence Policy Properties** For the Default Log Action choose **yes** to **Log Category Matches**.

#. Browse to the inline **Help** tab at the top left of the GUI and examine the Default Log Action settings. Inline help is very useful when navigating the myriad of options available within any configuration screen.

.. Note:: Notice in the setting descriptions that hardware acceleration is not available when "logging all matches". This exercise is to familiarize you with inline help and will not affect our virtual lab.

8. To the right of the screen, click **Add** under the categories section. 

#. From the category section choose **botnets** and click **Done editing**.

#. Repeat this process and add the following additional categories: **infected_sources**, **scanners**, **spam_sources**, & **denial_of_service**.

.. image:: images/ipi_global.png
  :width: 600 px

11. Commit the Changes to the System.

#. Apply the **global_ipi** policy and click **Update**.

.. image:: images/global_policy.png
  :width: 600 px

Setup Logging for Global IPI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. From the "Main tab" (top left of screen), navigate to **Security > Event Logs > Logging Profiles** and click on **global-network**
#. Under the Network Firewall section configure the IP Intelligence publisher to use **local-db-publisher**
#. Check **Log GEO Events**
#. Click **Update**

.. image:: images/ipi_global_log.png
  :width: 600 px

Test 
~~~~~~~~~~~~~~~~
#. On the Linux Client, open a terminal and **cd** to **Agility2021wafTools**
#. Run the following command to send some traffic to the site: **./ipi_tester**.

.. NOTE:: The script should continue to run for the remainder of Lab 1 & 2. Do NOT stop the script. 

#. Navigate to **Security > Event Logs > Network > Ip Intelligence** and review the entries. Notice the Geolocation Data as well as the Black List Class to the right of the log screen. 

.. image:: images/global_event.png
  :width: 600 px

Create Custom Category 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. Navigate to: **Security > Network Firewall > IP Intelligence > Blacklist Categories** and click **create**.
#. Name: **my_bad_ips** with a match type of **Source**
#. Click **Finished**
#. Select the category name **my_bad_ips** and click **Add To Category**

.. image:: images/add_to_cat.png
  :width: 600 px

#. Enter the ip address: **42.231.162.22** and set the seconds to **3600** (1 hour)
#. Click **Insert Entry**

.. image:: images/add_ip.png
  :width: 600 px


Create your first WAF Policy & Configure L7 IPI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. Navigate to **Security > Application Security > Security Policies** and click the Plus (+) button. 
#. Name the policy: **insecureApp1_asmpolicy**
#. Select Policy Template: **Rapid Deployment Policy**
#. Select Virtual Server: **insecureApp1_vs**
#. Notice that the enforement mode is already in **Transparent Mode** and Signature Staging is **Enabled**
#. Click **Save**.

.. image:: images/waf_policy.png
  :width: 600 px

#. Navigate to **Security > Application Security > Policy Building > Learning and Blocking Settings** and expand the **IP Addresses and Geolocations** section. Notice that **Access from malicious IP address** is set to **Alarm** and **Block**. We will cover these concepts later in the lab but for now the policy is still transparent so the blocking setting has no effect. 

.. image:: images/ipi_asm.png
  :width: 600 px

#. Navigate to **Local Traffic > Virtual Servers** and click on **insecureApp1_vs**.
#. Under the Security tab in the top middle of the GUI click on **Policies** and your policy settings should look like this. 

.. image:: images/policy_setting.png
  :width: 600 px

#. Disable the IP Intelligence Profile and enable the **Log all requests** logging profile as shown below, then click **update**. 

.. image:: images/policy_mod.png
  :width: 600 px

#. Navigate to **Security > Network Firewall > IP Intelligence > Policies** and set the Global IP Intelligence Policy to **none** and click **update**. 

.. image:: images/disable_global.png
  :width: 600 px

#. Navigate to **Security > Application Security > IP Addresses > IP Intelligence** and enable IP Intelligence. 
#. Notice at the top left that you are working within the insecureApp1_asmpolicy policy context. Enable **Alarm** and **Block** for each category. 
#. Click **Save** and **Apply Policy**

.. image:: images/waf_ipi.png
  :width: 600 px


#. Navigate to **Security > Event Logs > Application > Requests** and review the entries. You should now see IPI violations. If you browse to the site via Firefox on Client01 you should see good traffic as well in the event logs since we are logging all requests and not all IP's are malicious. 

.. image:: images/events.png
  :width: 600 px

#. Click on one of the alerts and review the violation details. Note that you can see the entire request details even though this site was using strong TLS for encryption. 

.. image:: images/alert.png
  :width: 600 px

.. NOTE:: It is best practice to enable Trust XFF in the policy when configuring IPI via WAF policy. XFF inspection is one of the advantages to consider when deploying IPI and can only be done via WAF policy. Although this setting is not needed to demonstrate this lab, it is strongly recommended to have it enabled. 

.. image:: images/trust_xff.png
  :width: 600 px

As you can see, there are several methods of configuring IP Intelligence on the BIG-IP and each has it's own pro's and con's. It will be up to you to decide which method works best for your organization but at least now you know and knowing is most of the battle in IT. 

**This completes Lab 1.1**
