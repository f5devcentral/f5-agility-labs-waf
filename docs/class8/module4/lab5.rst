Advanced Impersonating Bot Detection
------------------------------------

  It is still possible for automated traffic to completely impersonate a real browser by sending all of the appropriate headers and in the correct order.

  In this exercise we will use cURL to exactly impersonate a Chrome request.

Using cURL with custom Headers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  Return to the Windows command prompt and run the following request:

  .. code-block:: console

    curl -H "Connection: keep-alive" -H "User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36" http://hackazon.f5demo.com/ -H "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8" -H "Referer: http://hackazon.f5demo.com/" -H "Accept-Encoding: gzip, deflate" -H "Accept-Language: en-US,en;q=0.9"

  Note in this request we are sending all of the same headers that the Chrome browser normally sends and in the correct order.

.. _review-bot-defense-logs-2:

Review Bot Defense Logs
~~~~~~~~~~~~~~~~~~~~~~~

  Return to the Bot Defense Request Logs at **Security >> Event Logs >> Bot Defense >> Bot Requests** and
  select the most recent request.

  |image25|

  Notice that the **Request Status** is **Accepted**.  Because no bot signatures were triggered and all the Challenge-Free verification
  checks were passed this request was allowed through.

  Also, as indicated in the **Verification Action and Challenge Status** the Bot Defense profile is configured to verify AFTER access.
  So the response to this request would have included the client-side JavaScript to do further verification of this client.
  As cURL is unable to process javascript, subsequent requests from this client would eventually be blocked after the
  **Grace Period** defined in the profile.

  .. NOTE::
    IN this request log in the **Verification Action and Challenge Status** section the **Actual Verification Action Reason** is
    "URL Not Qualified for Injection Yet but Challenge Possible".  Recall from the Credential Stuffing lab that URLs must be "qualified"
    for injection of javascript and CAPTCHA challenges.  IN a real world scenario, enough requests would come to the homepage of the
    web application to keep the URL qualified ALWAYS.




.. |image1| image:: /_static/class8/bots/image1.png
.. |image2| image:: /_static/class8/bots/image2.png
.. |image3| image:: /_static/class8/bots/image3.png
.. |image4| image:: /_static/class8/bots/image4.png
.. |image5| image:: /_static/class8/bots/image5.png
.. |image6| image:: /_static/class8/bots/image6.png
.. |image7| image:: /_static/class8/bots/image7.png
.. |image8| image:: /_static/class8/bots/image8.png
.. |image9| image:: /_static/class8/bots/image9.png
.. |image10| image:: /_static/class8/bots/image10.png
.. |image11| image:: /_static/class8/bots/image11.png
.. |image12| image:: /_static/class8/bots/image12.png
.. |image13| image:: /_static/class8/bots/image13.png
.. |image14| image:: /_static/class8/bots/image14.png
.. |image15| image:: /_static/class8/bots/image15.png
.. |image16| image:: /_static/class8/bots/image16.png
.. |image17| image:: /_static/class8/bots/image17.png
.. |image18| image:: /_static/class8/bots/image18.png
.. |image19| image:: /_static/class8/bots/image19.png
.. |image20| image:: /_static/class8/bots/image20.png
.. |image21| image:: /_static/class8/bots/image21.png
.. |image22| image:: /_static/class8/bots/image22.png
.. |image23| image:: /_static/class8/bots/image23.png
.. |image24| image:: /_static/class8/bots/image24.png
.. |image25| image:: /_static/class8/bots/image25.png
.. |image26| image:: /_static/class8/bots/image26.png
.. |image27| image:: /_static/class8/bots/image27.png
.. |image28| image:: /_static/class8/bots/image28.png
.. |image29| image:: /_static/class8/bots/image29.png
.. |image30| image:: /_static/class8/bots/image30.png
.. |image31| image:: /_static/class8/bots/image31.png
