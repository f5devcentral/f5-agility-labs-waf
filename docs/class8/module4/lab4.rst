Impersonating Bot Detection
---------------------------

  In each of the previous examples, the bot traffic was easily identified by the user agent header.  It is trivial
  for attackers to change the user-agent header to a value to "impersonate" a valid browser.

  In this exercise we will see how **F5 Unified Bot Defense** handles this type of Impersonating Bot.

Using cURL with custom User-Agent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  Return to the Windows command prompt and run the following request:

  .. code-block:: console

    curl -H "User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36" http://hackazon.f5demo.com/

  Note in this request we are using a valid Chrome user agent header.

.. _review-bot-defense-logs-1:

Review Bot Defense Logs
~~~~~~~~~~~~~~~~~~~~~~~

  Return to the Bot Defense Request Logs at **Security >> Event Logs >> Bot Defense >> Bot Requests** and
  select the most recent request.

  |image24|

  Notice that the **Request Status** is **Challenged**.  Also, the **Mitigation Reason** is**Suspicious Browser**.

  Also, notice in the **Bot Details** section that the *Detected Anomalies** indicates **Suspicious HTTP Headers Presence or Order**.
  This anomaly is part of the Challenge-Free verifications and is triggered when a request is claiming to be a browser but the HTTP headers
  that browsers sends are either missing or in the wrong order.

  The **Suspicious HTTP Headers Presence or Order** anomaly is included in the **Suspicious Browser** class.  There is a similar anomaly named
  **Invalid HTTP Headers Presence or Order** which is included in the **Malicious Bot** class which fires when the HTTP headers are significantly
  different than the headers the claimed browser would normally send.




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
