Module 2: False Positive Scenarios
==================================

Objective
---------

-  Demonstrate False Positive (FP) meta violation

-  Signature and Parameter staging behavior

-  Identify FP in event viewer, review learning suggestions, modify,
   test


**Estimated time for completion: 30 minutes**

Demonstrate a False Positive
----------------------------

**Transition to Blocking**

#. Navigate to **Security > Application Security > Policy Building > Learning and Blocking Settings**

#. Under General Settings change the Enforcement Mode to Blocking.

   |image13|

#. Click **Save**

#. and then click **Apply Policy**

   **Use cURL to retrieve the web content**

#. On the jump host, you'll find a toolbar shortcut as shown for the
   Windows Command Prompt. Please click that shortcut to open a Windows
   Command Shell:\ |image14|

   From the command line execute the command:

   ``curl -k https://hackazon.f5demo.com | more``

   |image15|

You may need to scroll back/forward to see all the output.

**Question**: cURL is an awesome tool with dozens of options. Try:
``curl --help`` for a full listing.

What is the purpose of the ``-k`` option?

**Examine Event Logs**

#. Review the log at **Security > Event Logs > Application > Requests**
   and find the “Attack Signature Detected” event for your request.

#. Don’t forget to **remove** the **“illegal requests filter”** to view “all requests”.

#. Click the request entry at the top of the list of requests

   |image16|

#. In the request details view click the “down arrow” next to the “Attack Signature
   Detected” title:

   |image17|

   **Questions:** Based on the output answer the following:

   What aspect of the request triggered ASM?

   Why did you not receive the block page?

   **Disable Signature Staging and Attempt an Illegal Request**

#. Navigate to **Security > Application Security > Policy Building >
   Learning and Blocking Settings** and in the Attack Signatures
   section (Click the triangle to expand) uncheck “Signature Staging.”
   Be certain to click both save and apply policy.

  |image18|

#. Return to your command prompt and execute the command using the ip
   address instead: **curl -k** **https://10.128.10.200** **\| more**

   **Question:** What is different about this request from the previous?
   Is an IP address treated differently from a FQDN? Why did removing
   the signatures from staging cause the block page to now appear?

    |image19|

#. Make a note of the last four digits of the Support ID returned to
   cURL in the blocking response page.

#. Go to **Security > Event Logs > Application > Requests**. You should
   now see an Illegal Request.

  |image20|

.. NOTE:: In a production environment you may have thousands of blocked
   events and you will need to respond to issues quickly. Searching via the
   support ID is the fastest way to achieve this.

   **Find a blocked request in the event logs using the Support ID**

#. Click the magnifying glass. In the pop out box enter the last four
   digits of the Support ID you noted previously and click “Apply
   Filter.”

   |image21|

#. Review the log entry after clicking “All Details.”

   |image22|

   **SQL Injection**

#. From your Firefox window, open a New Private Window as shown in the
   screenshot and then open URL: **https://hackazon.f5demo.com** using
   the Hackazon shortcut in the toolbar.

   |image23|

#. In the top right click “Sign In” and type in the following string in
   the username field: ``or 1=1#`` Enter ``a`` in the password
   field, and click Sign In. (Without quotes)

   |image24|

**Question:** Did you receive the block page? If not, why do you think
you were not blocked? (*Answer: At this point, we do not expect the
traffic to be blocked. This will be clarified later in the lab*)

#. In the Configuration Utility, open the **Security > Application Security
   > Policy Building > Traffic Learning.**

   There may be several Suggestions listed. The Username field in the
   login pop up, uses the parameter name “username”. Please review the
   related suggestions, there are two related to the SQL injection, and
   note the signature ID’s.

   |image25|

   Select the request and then click the down arrow to the right of the
   “Attack Signature Detected”

   Then click on the request that shows up as a "sample" that prompted
   the suggestion

   |image26|

   This will expand the view to include information about why the
   signature triggered. You can see the Applied Blocking Setting is
   “Staged.”

   |image27|

   **Question:** This alert is triggered by the signature but in what
   context per the above screen shot? How is a parameter treated
   differently from a signature?

.. |image13| image:: /_static/class1/image24.png
   :width: 4.61111in
   :height: 0.72222in
.. |image14| image:: /_static/class1/image28.png
   :width: 5.00000in
   :height: 0.44792in
.. |image15| image:: /_static/class1/image29.png
   :width: 6.50000in
   :height: 2.07569in
.. |image16| image:: /_static/class1/image30.png
   :width: 6.50000in
   :height: 2.59236in
.. |image17| image:: /_static/class1/image35.png
   :width: 6.43056in
   :height: 4.00000in
.. |image18| image:: /_static/class1/image36.png
   :width: 5.19375in
   :height: 1.61139in
.. |image19| image:: /_static/class1/image38.png
   :width: 6.50000in
   :height: 1.29792in
.. |image20| image:: /_static/class1/image41.png
   :width: 6.50000in
   :height: 2.56319in
.. |image21| image:: /_static/class1/image43.png
   :width: 6.50000in
   :height: 3.81458in
.. |image22| image:: /_static/class1/image44.png
   :width: 6.50000in
   :height: 2.30625in
.. |image23| image:: /_static/class1/image46.png
   :width: 2.93750in
   :height: 2.33164in
.. |image24| image:: /_static/class1/image47.png
   :width: 2.71905in
   :height: 2.02593in
.. |image25| image:: /_static/class1/image48.png
   :width: 6.19106in
   :height: 1.49419in
.. |image26| image:: /_static/class1/image49.png
   :width: 6.50000in
   :height: 3.16667in
.. |image27| image:: /_static/class1/image50.png
   :width: 5.61643in
   :height: 3.71882in
