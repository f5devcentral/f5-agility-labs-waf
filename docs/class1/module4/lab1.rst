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
