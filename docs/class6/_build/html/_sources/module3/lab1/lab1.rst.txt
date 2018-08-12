Lab 3: Web Scraping Protection
--------------------------------------

This lab will show you how to configure protection against webscraping activity using a Firefox loop macro.

Connect to the lab environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the jumphost, launch chrome, click the BIG-IP bookmark and login to TMUI. admin/password

#. From the jumphost, launch firefox, which we will use to create the macro.


Remove any existing security policy from the Webgoat Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. On the BIG-IP TMUI, Go to Local Traffic > Virtual Servers > asm_vs

#. Click the Security > Policies tab at the top 

#. Change the Application Security Policy to “Disabled” 

#. The Logging Profile should be set to “Log Illegal Requests” and click update


Connect to the Webgoat Application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Using Firefox, click on the shortcut for WEBGOAT login

   ``http://10.1.10.145/WebGoat/login``

.. note::
        Note that you may use Chrome for BIG-IP access but you must use Firefox for the macro creation. 




Create a web scraping macro
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Launch the iMacros sidebar by clicking on the icon at the top-right of Firefox

|

.. image:: images/iMacro.png
        :width: 100px

|


2. Click the iMacro Rec menu, then click the Record button

3. On the pop-up that asks to close all tabs, select No

4. Click Stop to save the current macro (URI should be /Webgoat/login )

5. Click the Play menu and set the Max to 12 and click Play Loop

6. Did the pages load successfully?  


Create a security policy to prevent webscraping
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log into the BigIP through the browser

#. Click on Security > Application Security > Security Policies and Create 

#. Select the Advanced view instead of Basic (default)

#. Name the policy “webscraping” 

#. Select “Rapid Deployment Policy” for the "Policy Template", this will bring up a prompt asking if you want to continue, click "Ok"

#. Select “asm_vs” for Virtual Server and click Create Policy (upper left)

#. Change Enforcement Mode to “Blocking”

#. Once created, go to Application Security > Anomaly Detection > Web Scraping

#. Click Bot Detection and select “Alarm and Block”.  This will bring up a "Bot Detection" menu below

#. Edit the settings per the screenshot, click Save and then Apply Policy

|

.. image:: images/bot_detection_settings.png
        :width: 600px

|

Create a DNS Resolver 
~~~~~~~~~~~~~~~~~~~~~

|

.. note:: A DNS Resolver (allows the Bigip to do DNS lookups) is required for effective anomaly detection

|

#. You can either follow the link in the warning as you enable Web Scraping, or go to Network > DNS Resolvers > DNS Resolver List and Create

#. Assign a name to the Resolver profile and click Finished


Attempt to scrape the Webgoat Login Page
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Go back to your Webgoat tab in Firefox and re-run the macro you created

#. Did the page hits load successfully?


Review the Security Event Logs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Go to Security > Event Logs > Application > Requests

2. You should see some current illegal requests, as in the example below, click on one and examine the details

|

.. image:: images/webScrapingLog.png
        :width: 600px

|


3. What caused ASM to block the request?

4. Now go to Security > Event Logs > Application > Web Scraping Statistics

5. Do you see any events?  


Reset the Virtual Server config for the next lab
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Clear the app security event log by going to Secuirty > Application Security -> Event Logs > Requests and clicking the check box to select all "Illegal Requests". Then click "Delete Requests".

#. Remove the webscraping security profile from the asm_vs virtual server by going to Local Traffic > Virtual Servers > asm_vs, then click Security > Policies tab. Then set "Application Security Policy" to Disabled and click Update.

