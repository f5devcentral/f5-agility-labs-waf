Signatures
---------------

#. Navigate to **Security > DoS Protection > DoS Profiles**

   .. image:: /_static/class1/image84.png
     :width: 5.58056in
     :height: 2.81736in

#. **Click** on the ``hackazon_DoS`` profile and then the **Application Security** tab to configure the policy.

   .. image:: /_static/class1/image85.png
     :width: 6.49444in
     :height: 2.86042in

#. Select **Proactive Bot Defense** under the list of **Application Security** options.

#. In the **Application Security >> Proactive Bot Defense**
   section, click the **Edit** link for **Operation Mode** and
   then change the setting from **Always** to **During Attack** and
   click **Update** to complete the policy change.

   .. NOTE:: Ignore the DNS Resolver warning

   .. image:: /_static/class1/image86.png
     :width: 6.50000in
     :height: 3.09514in

#. Run cURL again: ``curl –k https://hackazon.f5demo.com``

   **The site should respond normally now every time.**

#. cURL is considered an **HTTP Library tool** and falls in **the Benign Category**.

   .. NOTE:: Just how benign are HTTP library tools? cURL can easily be
      scripted in a variety of ways and can be used as a downloader to siphon
      off data. Remember the famous media defined “hacking tool” that Snowden
      used? wget? There are many use-cases where you simply do not want a tool
      interacting with your site.

#. Under your ``hackazon_DoS`` profile in **Application Security >> Bot Signatures** click on the **Edit** link for the **Bot Signature Categories** section.

   .. image:: /_static/class1/image88.png
     :width: 6.50000in
     :height: 3.47708in

#. Change the HTTP Library action from **None** to **Block** under the **Benign Categories** section and click **Update** to apply the policy changes.

   .. image:: /_static/class1/image89.png
     :width: 6.50000in
     :height: 2.97847in

#. Run cURL again: ``curl –k https://hackazon.f5demo.com``

   .. image:: /_static/class1/image90.png
     :width: 6.50000in
     :height: 0.55833in

   Whammo!!!... as soon as the BOT is revealed... the connection is dropped. The TLS doesn’t get established.

   If we actually DO want to allow cURL or another automated tool. We may have developers that rely on curl so let’s whitelist just that.

**To Whitelist cURL:**

#. Go to the **Bot Signatures** list and find **curl**. Move it to disabled signatures and click **Update**.

   .. image:: /_static/class1/image91.png
     :width: 4.17587in
     :height: 2.28736in

#. Run cURL again: ``curl –k https://hackazon.f5demo.com`` and you should be back in business. By now you should know the expected output.

#. Change HTTP Library to: **Report**, Remove CURL from the whitelist and set http libraries category to just ``report``

   .. image:: /_static/class1/image92.png
     :width: 6.50000in
     :height: 4.03125in

#. Change Operation Mode to: ``Always``

   .. image:: /_static/class1/image93.png
     :width: 6.50000in
     :height: 3.50694in

   We are going to leverage the IPRep virtual server from the earlier lab to get some randomness.

#. Run the cURL command several times: ``curl –k https://10.128.10.210``

   .. image:: /_static/class1/image94.png
     :width: 6.50000in
     :height: 5.09583in

#. Review the event logs at **Event Logs >> Bot Defense** You will now see geo-data for the BOT connection attempts.

   .. image:: /_static/class1/image95.png
     :width: 6.50000in
     :height: 4.29306in

#. Navigate to **Security > Overview** and review the default report elements.

#. Click **Overview > Application > Traffic**:

   .. image:: /_static/class1/image96.png
     :width: 6.50000in
     :height: 3.08889in

#. Take some time reviewing this screen and practice adding a new widget to see additional reporting elements:

   .. image:: /_static/class1/image97.png
     :width: 6.50000in
     :height: 2.75833in

#. Click the **DoS tab** at the top. The DOS Visibility Screen loads.

   .. image:: /_static/class1/image98.png
     :width: 6.50000in
     :height: 1.72361in

   .. NOTE:: You may need to change your time in the Windows system tray for accurate results.

   Although there have not been any L7 DoS attacks some of the widgets along the right contain statistics from the BOT mitigations.

#. Click the **Analysis** tab at the top and review the graphs available to you.

   .. image:: /_static/class1/image99.png
     :width: 6.50000in
     :height: 3.64722in

#. Click the **URL Latencies** tab at the top and review the graphs available to you.

   .. image:: /_static/class1/image100.png
     :width: 6.50000in
     :height: 3.68750in

#. Click the **Custom Page** tab at the top and review the graphs available to you.

   Please feel free to add widgets and/or explore the ASM interface further.

**This concludes this lab guide!**
