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
