Automated Browser Detection
---------------------------

  While command line tools and scripts are unable to process javascript challenges, there are many tools available to attackers to bypass these basic
  javascript challenges.  There are also, tools such as Selenium that can be configured to "drive" real browsers through sophisticated web applications.

  In this exercise we will use the Kantu extension for Chrome to test the ability of F5 Unified Bot Defense to detect and mitigate automated browsers.
  Kantu is a free Selenium-based extension available for most browsers.

Using Selenium Automated Browsers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  In the Chrome browser, browse to the Hackazon home page at hackazon.f5demo.com.

  Refresh the home page at least 10 times to ensure it is qualified for injection of the Javascripts that are necessary to detect this
  type of automated activity on the client side.

  You can validate this by checking the Bot Defense Request Logs and look for a value in the DeviceID field.

  |image26|

  To the right of the address bar in Chrome click on the |image27| icon to open the Kantu extension.

  |image28|

  .. NOTE::
    A macro has already been recorded of browsing various pages on the Hackazon website.

  In the Kantu window ensure the "Browse Hackazon" macro is selected on the left.

  Select the drop down menu next to "Play Macro" and choose **Play loop...**.

  |image29|

  Leave the default to play the loop 3 times and click **Play**.

  Kantu will attempt to browse the Hackazon website, following the links recorded in the macro.

  After several requests you will see the blocking page and Kantu will stop progressing through the macro.

  |image30|


.. _review-bot-defense-logs-3:

Review Bot Defense Logs
~~~~~~~~~~~~~~~~~~~~~~~

  Return to the Bot Defense Request Logs at **Security >> Event Logs >> Bot Defense >> Bot Requests** and
  select the most recent request.

  |image31|

  The **Request Status** and **Mitigation Reason** indicate this request was classified as a **Malicious Bot** and **Blocked**.

  Further information in the **Bot Details** section of the log indicate that this request was categorized as an **Automated Browser**
  because it detected **Surfing Without Human Action**.

  F5 Unified Bot Defense is able to detect and mitigate even very sophisticated automated browsers.


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
