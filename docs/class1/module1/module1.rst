Module 1: Base Policy Creation
==============================

Objective
---------

-  Create a security policy using manual policy building

-  Enable application security logging profile

-  Validate that both the policy and logging profile are working

-  Review the auto-detection of web server capabilities (i.e. Apache,
   jQuery, etc)

-  Estimated time for completion: **30 minutes**

   This lab will demonstrate how to create and build a security policy
   using manual policy building.

   Before we begin, ensure that you have three virtual servers:

   - ``hackazon.f5demo.com_https_vs``
   - ``hackazon.f5demo.com_http_vs``
   - ``ip_rep_target_https_vs``

   You will be working primarily with ``hackazon.f5demo.com_https_vs``.

   Screenshot below:

   |image1|

Create Policy
-------------

#. On the Main tab, click **Security > Application Security 
   > Security Policies**. The Active Policies screen opens.

#. Click on **Policies List**

   |image2|

#. Click the **Create New Policy** button. The policy creation wizard
   opens.

   |image3|

Configure Policy
----------------

#. Click the **Advanced** button (Top-Right) to ensure that all the
   available policy creation options are displayed.

#. Name the security policy ``hackazon_asm`` and ensure that
   the **Policy Type** is ``Security``.

#. Verify the **Policy Template** is set to ``Fundamental``.

#. Assign this policy to the ``hackazon.f5demo.com_https_vs``
   from the **Virtual Server** drop down.

#. Set the Application Language to UTF-8 (This is required to set
   the Learning Mode, why might this be necessary?)

#. Go back up two settings to **Learning Mode** and set it
   to ``Manual``.

#. Set the **Enforcement Mode** to ``Transparent``

Accept Remaining Default Policy Settings
----------------------------------------

**Your settings should reflect this figure:**

|image4|

#. Click **Create Policy** to complete the policy creation process.

#. After policy creation is complete, the properties will be displayed
   for review within the Policies List menu.

#. Click **Apply** while the ``hackazon_asm`` policy is selected.

   .. NOTE:: ASM behaves differently than LTM regarding changes. When
      editing BIG-IP LTM Configurations in the Configuration Utility (Web
      UI) changes are saved and applied immediately. In BIG-IP ASM,
      changes **must be saved first** and then at the time of the
      Administrator's choosing, they can be Applied (or activated) to
      BIG-IP ASM. This can be viewed as a "Deferred Commit" behavior. ASM
      allows for rollbacks of configuration.

   |image5|

Verify ASM Profile is Applied
-----------------------------

#. Under **Local Traffic > Virtual Servers**, click
   on ``hackazon.f5demo.com_https_vs``.

#. Click on **Policies** under the **Security** tab at the top of
   the ``hackazon.f5demo.com_https_vs`` details menu.

#. In the **Application Security Policy** drop down menu, ensure
   Application Security Policy is ``Enabled...`` and the **Policy:**
   drop-down selection shows the ``hackazon_asm`` policy.

#. Notice Log Profile is set to ``Disabled``

Create Application Security Logging Profile
-------------------------------------------

#. In the Configuration Utility, navigate to:  **Security >
   Event Logs > Logging Profiles** then **click the plus icon**.

#. Enter a Profile Name ``asm_allrequests``, select the checkbox
   for ``Application Security``.

#. Change the **Configuration** dropdown to ``Advanced`` under
   the **Application Security** logging section, and then set
   the **Response Logging** dropdown to: ``For All Requests``.

#. Change the **Request Type** under **Storage Filter** to 
   ``All Requests``. Click **Finished**.

   |image6|

**Question:** Would logging all requests and responses in a production
environment be a best practice?

Apply ASM Logging Profile
-------------------------

#. Under **Local Traffic > Virtual Servers**, click
   on ``hackazon.f5demo.com_https_vs``.

#. Click on **Policies** under the **Security** tab at the top of
   the ``hackazon.f5demo.com_https_vs`` details menu.

#. In the **Log Profile** drop down menu, select ``Enabled...``

#. Within the Available logging profiles menu,
   select ``asm_allrequests`` and then click the ``<<`` arrows to
   move the logging policy to the **Selected** profile.

#. Click on the **Update** button to apply the policy.

   |image7|

Test ASM Policy
---------------

#. Open Firefox and navigate to ``https://hackazon.f5demo.com``

#. *(You'll find a toolbar shortcut for the Hackazon link and this can
   be used.)*

   |image8|

#. Interact with the application by clicking the Hackazon logo and any
   of the items under the Special Selection title that appear on the
   front page. **Please** refrain from experimenting with the site using
   any "exploit" techniques that you might be familiar with.

#. On the BIG-IP, navigate to **Security > Event Logs > Application >
   Requests** and verify that requests are being observed.

#. **Tip:** You will need to clear the “Illegal Requests” only filter:

   |image9|

   You should be able to see both the raw client request and server
   response for the event that you selected.

   **For example:**

   |image10|

Review Server Technologies
~~~~~~~~~~~~~~~~~~~~~~~~~~

#. On the BIG-IP, navigate to **Security > Application Security > Policy
   Building > Traffic Learning**

#. You will see that ASM has detected 4 or more Server Technologies just
   from the site browsing you did in the previous section.

   |image11|

#. Select all the **Add Server Technology recommendations** and click
   **Accept Suggestions**.

#. Be sure to click "Apply Policy" at the top right:

   |image12|

   **Question:** What about the other suggestion regarding “Add Valid
   Host Name”? Should this be accepted, why or why not?

   **Question:** How does accepting Server Technologies affect
   Signatures?

.. |image0| image:: /_static/class1/image1.png
   :width: 1.93667in
   :height: 0.61667in
.. |image1| image:: /_static/class1/image4.png
   :width: 6.40625in
   :height: 1.60156in
.. |image2| image:: /_static/class1/image5.png
   :width: 5.81875in
   :height: 1.52742in
.. |image3| image:: /_static/class1/image6.png
   :width: 5.87937in
   :height: 3.13315in
.. |image4| image:: /_static/class1/image11.png
   :width: 6.50000in
   :height: 3.54931in
.. |image5| image:: /_static/class1/image12.png
   :width: 6.50000in
   :height: 2.35833in
.. |image6| image:: /_static/class1/image14.png
   :width: 6.50000in
   :height: 5.44653in
.. |image7| image:: /_static/class1/image17.png
   :width: 6.50000in
   :height: 5.24444in
.. |image8| image:: /_static/class1/image19.png
   :width: 5.00000in
   :height: 2.53125in
.. |image9| image:: /_static/class1/image20.png
   :width: 6.50000in
   :height: 3.10278in
.. |image10| image:: /_static/class1/image21.png
   :width: 6.50000in
   :height: 2.88681in
.. |image11| image:: /_static/class1/image22.png
   :width: 6.50000in
   :height: 2.36458in
.. |image12| image:: /_static/class1/image23.png
   :width: 5.63131in
   :height: 2.39391in
