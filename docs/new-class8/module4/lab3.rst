Mitigation Setting Exceptions
-----------------------------

  While the Bot Defense Profile default classifications and categorizations are generally appropriate for many web applications,
  you may want to create exceptions to block requests that are allowed, or allow requests that are blocked.

  In this exercise we will create a couple of exceptions in the Bot Defense Profile.

Create Exceptions
~~~~~~~~~~~~~~~~~

  Perhaps we consider automated requests from curl to be malicious and we do not want to allow these requests, even for initial access.
  We can create an exception to block curl requests while still allowing other requests that are in the HTTPLibrary category.

  In the BIG-IP, return to **Security >> Bot Defense >> Bot Defense Profiles** and select the **Hackazon-bots** profile.

  |image16|

  Select the **Mitigation Settings** section.  Click **Add Exceptions** in the bottom right corner.

  Recall from the Bot Request logs that cURL was classified as an **Untrusted Bot** and in the **HTTP Library** category.
  We can add an exception by selecting the Untrusted Bot class, then the HTTP Library category, and finally,
  selecting the curl Bot Signature.

  |image17| |image18| |image19|

  Click **Add** to add the exception for curl.

  Change the mitigation to **Block**.

  |image20|

  .. NOTE::
   Exceptions can be made at the category or signature/anomaly level.  for example, we could have created
   an exception for the entire HTTP Library category.

  You can also add exceptions by searching for the category, anomaly, or signature.

  Imagine we are receiving complaints from some users that they are getting CAPTCHA pages.  IN reviewing the Bot Defense request logs
  we see that the are receiving the CAPTCHA page because Bot Defense has detected the iMacros extension in their browser.

  Create another exception by searching for "iMacros" by using the search feature.

  |image21|

  Set the mitigation to **Alarm** so we are no longer sending a CAPTCHA to these users.  Click **Save**.

  |image22|

(OPTIONAL) Test Exceptions
~~~~~~~~~~~~~~~~~~~~~~~~~~

 From the Windows command prompt, re-run the cURL request to the Hackazon home page:

    .. code-block:: console

      curl http://hackazon.f5demo.com/

  Return to the Bot Defense Request Logs at **Security >> Event Logs >> Bot Defense >> Bot Requests**.

  Review the most recent request.  Was it blocked? Why?

  |image23|




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
