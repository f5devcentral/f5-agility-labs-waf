Module 4: Proactive Bot Defense
===============================

Objective
---------

-  Create a DoS profile

-  Enable proactive bot defense

-  Apply the policy to the appropriate virtual server

-  Validate that the policy is working as expected

-  Estimated time for completion: **20** **minutes**

Create Policy
-------------

.. IMPORTANT:: To clearly demonstrate just the Bot Defense profile,
   please **disable** the Application Security Policy from the
   ``hackazon.f5demo.com_https_vs`` virtual server!

#. Run the following curl command to verify the site is loading without
   issue from this headless browser. If the curl command is not
   successful (you are getting a “request rejected” error page), please
   let an instructor know.

   ``curl –k https://hackazon.f5demo.com | more``

   |image43|

#. On the Main tab, click **Security > DoS Protection > DoS Profiles**.
   The DoS Profiles screen opens.

   |image44|

#. Click on the **Create** button.

#. Name the policy ``hackazon_DoS`` and click **Finished** to
   complete the creation of this DoS profile.

   |image45|

Configure Policy
----------------

#. **Click** the newly created ``hackazon_DoS`` profile listed under the
   **Security > Dos Protection > DoS Profiles** list.

#. The profile’s properties menu will be displayed initially. **Click**
   on the **Application Security** tab at the top of this menu to
   begin configuring the policy.

   |image46|

#. Under the **Application Security** tab >> General Settings
   click the **Edit** link on the right-hand side of General Settings
   box and then check the ``Enabled`` check box for **Application
   Security** to enable the DoS profile and allow additional settings
   to be configured.

   |image47|

#. Select **Proactive Bot Defense** under the list of **Application
   Security** options for this DoS profile.

#. Click the **Edit** link on the right for the **Application
   Security >> Proactive Bot Defense** menu and select **Always**
   from the drop-down menu for **Operation Mode**.

   |image48|

#. Notice that for **Block requests from suspicious browsers** the
   **Block Suspicious Browsers** setting is enabled by default.

#. Click the **Update** button to complete the Proactive Bot
   Defense ``hackazon_DoS`` profile.

Apply Proactive Bot Defense Policy
----------------------------------

#. Under **Local Traffic > Virtual Servers**, click
   on ``hackazon.f5demo.com_https_vs``.

#. Click on **Policies** under the **Security** tab at the top of
   the ``hackazon.f5demo.com_https_vs`` details menu.

#. In the **DoS Protection Profile** drop down menu,
   select ``Enabled...`` and then select the ``hackazon_DoS`` for
   the profile.

#. Click on the **Update** button to apply the policy.

   |image49|

Create Bot Defense Logging Profile
----------------------------------

#. Open a new tab for the Configuration Utility and navigate to:
    **Security > Event Logs > Logging Profiles** then **click
   the plus icon**.

#. Enter a Profile Name ``bot-defense_allrequests``, select the
   checkbox for ``Bot Defense``.

#. Under the **Bot Defense** logging section, select the checkboxes
   for the following: ``Local Publisher``, ``Log Illegal Requests``, and
   ``Log Challenged Requests``.

#. Click **Finished**.

   .. NOTE:: You could have also modified the existing ``asm_allrequests``
      logging profile and added DoS logging definitions.

   |image50|

Apply Bot Defense Logging Profile
---------------------------------

#. Under **Local Traffic > Virtual Servers**, click
   on ``hackazon.f5demo.com_https_vs``.

#. Click on **Policies** under the **Security** tab at the top

#. Within the Available logging profiles menu,
   select ``bot-defense_allrequests`` and then click
   the ``<<`` arrows to move the logging policy to
   the ``Selected`` profile.

#. Click on the **Update** button to apply the policy.

   .. NOTE:: You can associate multiple logging profiles with a given
      virtual server. F5 allows for an incredible amount of logging
      flexibility. Most commonly you would have DoS, Bot Defense and ASM
      Security Policy events logged to a centralized SIEM platform, but
      there may be additional logging requirements such as a web team that
      would be interested in Bot Defense logs solely, while the SIEM
      continues to receive the union of DoS, Bot Defense and ASM Security
      Policy events.

   |image51|

Test the Proactive Bot Defense Policy
-------------------------------------

#. From the command line execute the following command several times:

   ``curl –k https://hackazon.f5demo.com``

   .. NOTE:: This can take a few minutes and you may get several empty
      responses as shown.

   After a few moments the PBD will initialize and you will Because
   Proactive BOT Defense is always on, this tool will always be
   blocked.

   |image52|

Validate that the Proactive Bot Defense Policy is Working
---------------------------------------------------------

#. Navigate to **Security > Event Logs > Bot Defense > Requests**.

   |image53|

#. Notice that the detected bot activity has been logged and is now
   being displayed for review.

   |image54|

#. Note the stated reason for the request being blocked. You may have to
   scroll to the right to see this reason. What was the stated reason?


BOT Signatures
---------------

#. Navigate to **Security > DoS Protection > DoS Profiles**

   |image55|

#. **Click** on the ``hackazon_DoS`` profile and then the
   **Application Security** tab to configure the policy.

   |image56|

#. Select **Proactive Bot Defense** under the list of **Application
   Security** options.

#. In the **Application Security >> Proactive Bot Defense**
   section, click the **Edit** link for **Operation Mode** and
   then change the setting from **Always** to **During Attack** and
   click **Update** to complete the policy change.

   .. NOTE:: Ignore the DNS Resolver warning

   |image57|

#. Run cURL again: ``curl –k https://hackazon.f5demo.com``

   **The site should respond normally now every time.**

#. cURL is considered an **HTTP Library tool** and falls in **the Benign
   Category**.


.. NOTE:: Just how benign are HTTP library tools? cURL can easily be
   scripted in a variety of ways and can be used as a downloader to siphon
   off data. Remember the famous media defined “hacking tool” that Snowden
   used? wget? There are many use-cases where you simply do not want a tool
   interacting with your site.

Selectively Blocking BOT Categories
-----------------------------------

#. Under your ``hackazon_DoS`` profile in **Application Security >> Bot
   Signatures** click on the **Edit** link for the **Bot Signature
   Categories** section.

   |image58|

#. Change the HTTP Library action from **None** to **Block** under
   the **Benign Categories** section and click **Update** to apply
   the policy changes.

   |image59|

#. Run cURL again: ``curl –k https://hackazon.f5demo.com``

   |image60|

   Whammo!!!... as soon as the BOT is revealed... the connection is dropped.
   The TLS doesn’t get established.

   Let’s say we actually DO want to allow cURL or another automated
   tool. We may have developers that rely on curl so let’s whitelist
   just that.

**To Whitelist cURL:**

#. Go to the **Bot Signatures** list and find **curl**. Move it
   to disabled signatures and click **Update**.

   |image61|


#. Run cURL again: ``curl –k https://hackazon.f5demo.com`` and you should
   be back in business. By now you should know the expected output.

#. Change HTTP Library to: **Report**
   Remove CURL from the whitelist and set http libraries category to
   just ``report``

   |image62|

#. Change Operation Mode to: ``Always``

   |image63|

   We are going to leverage the IPRep virtual server from the earlier lab
   to get some randomness.

#. Run the cURL command several times: ``curl –k https://10.128.10.210``

   |image64|

#. Review the event logs at **Event Logs >> Bot Defense** You will
   now see geo-data for the BOT connection attempts.

   |image65|

#. Navigate to **Security > Overview** and review the default
   report elements.

#. Click **Overview > Application > Traffic**:

   |image66|

#. Take some time reviewing this screen and practice adding a new widget
   to see additional reporting elements:

   |image67|

#. Click the **DoS tab** at the top. The DOS Visibility Screen loads.

   |image68|

   .. NOTE:: You may need to change your time in the Windows system tray for
      accurate results.

   Although there have not been any L7 DoS attacks some of the widgets
   along the right contain statistics from the BOT mitigations.

#. Click the **Analysis** tab at the top and review the graphs
   available to you.

   |image69|

#. Click the **URL Latencies** tab at the top and review the graphs
   available to you.

   |image70|

#. Click the **Custom Page** tab at the top and review the graphs
   available to you.

   Please feel free to add widgets and/or explore the ASM interface
   further.

**This concludes this lab guide!**

.. |image43| image:: /_static/class1/image69.png
   :width: 6.50000in
   :height: 5.44375in
.. |image44| image:: /_static/class1/image70.png
   :width: 4.30087in
   :height: 2.39266in
.. |image45| image:: /_static/class1/image71.png
   :width: 5.55894in
   :height: 1.41598in
.. |image46| image:: /_static/class1/image72.png
   :width: 6.33194in
   :height: 2.42980in
.. |image47| image:: /_static/class1/image73.png
   :width: 6.41806in
   :height: 3.30032in
.. |image48| image:: /_static/class1/image74.png
   :width: 6.35347in
   :height: 3.84931in
.. |image49| image:: /_static/class1/image75.png
   :width: 6.31944in
   :height: 4.51389in
.. |image50| image:: /_static/class1/image77.png
   :width: 6.50000in
   :height: 5.05278in
.. |image51| image:: /_static/class1/image79.png
   :width: 6.50000in
   :height: 4.74375in
.. |image52| image:: /_static/class1/image80.png
   :width: 6.49444in
   :height: 3.24722in
.. |image53| image:: /_static/class1/image82.png
   :width: 5.00000in
   :height: 3.12500in
.. |image54| image:: /_static/class1/image83.png
   :width: 6.49444in
   :height: 1.69861in
.. |image55| image:: /_static/class1/image84.png
   :width: 5.58056in
   :height: 2.81736in
.. |image56| image:: /_static/class1/image85.png
   :width: 6.49444in
   :height: 2.86042in
.. |image57| image:: /_static/class1/image86.png
   :width: 6.50000in
   :height: 3.09514in
.. |image58| image:: /_static/class1/image88.png
   :width: 6.50000in
   :height: 3.47708in
.. |image59| image:: /_static/class1/image89.png
   :width: 6.50000in
   :height: 2.97847in
.. |image60| image:: /_static/class1/image90.png
   :width: 6.50000in
   :height: 0.55833in
.. |image61| image:: /_static/class1/image91.png
   :width: 4.17587in
   :height: 2.28736in
.. |image62| image:: /_static/class1/image92.png
   :width: 6.50000in
   :height: 4.03125in
.. |image63| image:: /_static/class1/image93.png
   :width: 6.50000in
   :height: 3.50694in
.. |image64| image:: /_static/class1/image94.png
   :width: 6.50000in
   :height: 5.09583in
.. |image65| image:: /_static/class1/image95.png
   :width: 6.50000in
   :height: 4.29306in
.. |image66| image:: /_static/class1/image96.png
   :width: 6.50000in
   :height: 3.08889in
.. |image67| image:: /_static/class1/image97.png
   :width: 6.50000in
   :height: 2.75833in
.. |image68| image:: /_static/class1/image98.png
   :width: 6.50000in
   :height: 1.72361in
.. |image69| image:: /_static/class1/image99.png
   :width: 6.50000in
   :height: 3.64722in
.. |image70| image:: /_static/class1/image100.png
   :width: 6.50000in
   :height: 3.68750in
