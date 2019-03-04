Detection Per Username
----------------------

.. _attempt-invalid-logins-1:

Attempt invalid logins
~~~~~~~~~~~~~~~~~~~~~~

  .. IMPORTANT::
   In order for F5 Advanced WAF to inject or respond with CAPTCHA or JavaScript responses, it must first determine if it
   is appropriate to respond to the requested URL with HTML content.  F5 AWAF does this by watching requests and the associated
   responses from the server.  This process is called qualifying a URL.  This takes at least 10 requests/responses for a URL
   to be qualified for AWAF-initiated injection/response.
   In each of the following exercises, **pre-qualify the /user/login URL by refreshing the page at least 10 times** before attempting to login.

  Return to the Chrome browser with the Hackazon webpage.

  If you are still logged in, select **Logout** in the top right corner.

  Close the dev tools pane if it is still open.

  In the browser address bar change to the login page URL at **http://hackazon.f5demo.com/user/login**.

  Try to login with the same username and various incorrect passwords.

  After three failed login attempts you should get the CAPTCHA page.

  Complete the CAPTCHA. You should be returned to the login screen.

.. _review-asm-request-log-1:

Review ASM Request log
~~~~~~~~~~~~~~~~~~~~~~

  In the BIG-IP browse to the ASM Request log at **Security >> Event Logs >> Application >> Requests**.

  Look through the request log for the illegal request to /user/login.

  |image15|

  .. NOTE::
    What **Violation** was detected for this request?

    What other details about this request are visible when you select the “occurrence”?

    What indicator is there that this Brute Force violation was detected by username?




.. |image12| image:: /_static/class8/credstuff/image12.png
.. |image13| image:: /_static/class8/credstuff/image13.png
.. |image14| image:: /_static/class8/credstuff/image14.png
.. |image15| image:: /_static/class8/credstuff/image15.png
.. |image16| image:: /_static/class8/credstuff/image16.png
.. |image17| image:: /_static/class8/credstuff/image17.png
.. |image18| image:: /_static/class8/credstuff/image18.png
.. |image19| image:: /_static/class8/credstuff/image19.png
.. |image20| image:: /_static/class8/credstuff/image20.png
.. |image21| image:: /_static/class8/credstuff/image21.png
.. |image22| image:: /_static/class8/credstuff/image22.png
.. |image23| image:: /_static/class8/credstuff/image23.png
.. |image24| image:: /_static/class8/credstuff/image24.png
.. |image25| image:: /_static/class8/credstuff/image25.png
.. |image26| image:: /_static/class8/credstuff/image26.png
.. |image27| image:: /_static/class8/credstuff/image27.png
.. |image28| image:: /_static/class8/credstuff/image28.png
.. |image29| image:: /_static/class8/credstuff/image29.png
.. |image30| image:: /_static/class8/credstuff/image30.png
.. |image31| image:: /_static/class8/credstuff/image31.png
.. |image32| image:: /_static/class8/credstuff/image32.png
.. |image33| image:: /_static/class8/credstuff/image33.png
.. |image34| image:: /_static/class8/credstuff/image34.png
