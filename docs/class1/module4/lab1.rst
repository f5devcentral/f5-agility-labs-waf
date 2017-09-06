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

.. image:: /_static/class1/image69.png
   :width: 6.50000in
   :height: 5.44375in

#. On the Main tab, click **Security > DoS Protection > DoS Profiles**.
   The DoS Profiles screen opens.

.. image:: /_static/class1/image70.png
   :width: 4.30087in
   :height: 2.39266in

#. Click on the **Create** button.

#. Name the policy ``hackazon_DoS`` and click **Finished** to
   complete the creation of this DoS profile.

.. image:: /_static/class1/image71.png
   :width: 5.55894in
   :height: 1.41598in
