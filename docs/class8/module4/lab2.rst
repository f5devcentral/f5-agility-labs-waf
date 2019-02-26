Basic Bot Detection
===================

In this series of exercises we will progress through examples of very simple bots up to very sophisticated automated browsers.
We will review the Bot Defense logs to see how and why Bot Defense mitigates these automated requests.

Basic Bot and Vulnerability Scanners
------------------------------------

From the Windows Desktop, open a command prompt.

Paste and run each of the following commands:

cURL request to home page:

.. code-block:: console

  curl http://hackazon.f5demo.com/

cURL request to login page:

.. code-block:: console

  curl http://hackazon.f5demo.com/user/login

.. NOTE::
  How was the response to the second cURL request different from the response to the first cURL request?
  Why do you think this was?
  We will see the answer when we review the Bot Defense logs in the next step.

Paste and run the following command:

Nikto request to home page:

.. code-block:: console

  curl http://hackazon.f5demo.com/ -H "User-Agent: Mozilla/5.00 (Nikto/2.1.6) (Evasions:None) (Test:Port Check)"

Review Bot Defense Logs
-----------------------

  In the BIG-IP, browse to **Security >> Event Logs >> Bot Defense >> Bot Requests**.


First cURL Request
------------------
Select the third request down (this should be the first cURL request you sent to the home page).

In the top right corner, select to display **All Details**.

|image13|

Note the Request status is **Alarmed**. and the **Mitigation Reason** indicates that is was "alarmed" because
the request was classified as **Untrusted Bot** which is set in the Bot Defense profile to **Alarm**.

Note that the **Browser Verification Status** is **None**.  Because this request was not classified as a browser,
no browser verification was needed.

In the **Bot Details** section of the log we can see that this request was identified with the "curl" Bot Signature.
We can also see that this is classified as an **Untrusted Bot** and in the **HTTP Library** category.

Second cURL Request
-------------------
Select the second request down (this should be the second cURL request you sent to /user/login).

In the top right corner, select to display **All Details**.

|image14|

Note the Request status is **Denied** and the **Mitigation Reason** indicates that is was "blocked" because
the request was classified as **Untrusted Bot** which is set in the Bot Defense profile to **Block**.

Why is this different than the first request?

Recall that we defined a Microservice for the Hackazon login page. You see this indicated under **Microservice** in the log.
In the Microservice configuration for /user/login only the **Browser** category was allowed.  All other categories were set to **block**.

Nikto Request
-------------
Select the top request (this should be the Nikto request you sent to the home page).

In the top right corner, select to display **All Details**.

|image15|

What is the **Request Status**?  According to the **Mitigation Reason**, why was this request blocked?

In the **Bot Details** section of the log, what **Bot Class** and **Bot Category** are assigned to this request?

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
