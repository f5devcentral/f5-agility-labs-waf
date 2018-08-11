Lab 2.2: Session Hijacking Protection
-------------------------------------

..  |lab22-1| image:: images/lab22-1.png
        :width: 800px
..  |lab22-2| image:: images/lab22-2.png
        :width: 800px
..  |lab22-3| image:: images/lab22-3.png
        :width: 800px
..  |lab22-4| image:: images/lab22-4.png
        :width: 800px
..  |lab22-5| image:: images/lab22-5.png
        :width: 800px
..  |lab22-6| image:: images/lab22-6.png
        :width: 800px
..  |lab22-7| image:: images/lab22-7.png
        :width: 800px
..  |lab22-8| image:: images/lab22-8.png
        :width: 800px
..  |lab22-9| image:: images/lab22-9.png
        :width: 800px


.. note:: Items in this section depend on steps in prior sections, please ensure you've completed all sections in lab 2 up to this point before beginning this lab.


Task 1 - Configure Session Hijacking Protection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Open the BIG-IP interface in **Firefox** and navigate to **Security -> Application Security -> Sessions and Logins -> Session Tracking**.

#.  **Click** the checkbox to enable **Detect Session Hijacking by Device ID Tracking** and click **Save**. Then, follow the link to **Learning and Blocking Settings**.

    |lab22-1|

#.  Change the enforcement mode to **Blocking**.

#.  Expand the **Sessions and Logins** section and select **Alarm** and **Block** for **ASM Cookie Hijacking**, then click **Save**.

#.  Click **Apply Policy** then click **OK**.

|
|
|
    **Session Hijacking protection is now enabled.**


|
|

Task 2 - Test Session Hijacking Protection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Open a Linux terminal and run ``BurpSuiteCommunity &``.  Accept the defaults and click through to the main window.

#.  Go to the proxy tab and disable intercept so background requests from Chrome don't get hung up.

#.  Run ``google-chrome-stable --incognito --proxy-server="http://127.0.0.1:8080"`` in the same or a different terminal.

#.  Open the WebGoat login page (``http://10.1.10.145/WebGoat/login``) in **Chrome** but do not log in.

#.  Open a new private browsing window in **Firefox**, then type ``ctrl+shift+i`` to open inspector, and click the network tab.
    
#.  Navigate to WebGoat (in **Firefox**) at ``http://10.1.10.145/WebGoat/login`` and refresh the page 12 times.

#.  Login to WebGoat (in **Firefox**).

#.  Find the 200 request for ``start.mvc`` in the network debugging window and click on it. It should look like this:

    |lab22-2|

    The request and response headers should then appear to the right.

#.  Click **Raw headers**, highlight the entire ``Cookies:`` and ``DNT:`` sections and copy them to the clipboard.

#.  Go back to Chrome and refresh the WebGoat login page 12 times to generate some traffic.

#.  Go back to burp and re-enable intercept.

#.  Go back to Chrome and go to ``http://10.1.10.145/WebGoat/start.mvc#lesson/WebGoatIntroduction.lesson`` (avoid copying and pasting as you'll loose your cookie data).

#.  Go back to burp and quickly **replace** the **cookie** and **DNT** headers in the dialog with the one in your clipboard, then click **Forward** several times until the button turns grey.

    |lab22-9|

#.  Disable intercept in burp.

#.  Click refresh in **Chrome** if necessary (sometimes more than one is required).  You should get an ASM block page.

#.  Return to the BIG-IP and navigate back to **Security -> Event Logs -> Application -> Requests**.  You should see one or more illegal requests.

#.  Click on the most recent illegal request, click **all details** and make note of the attributes (particularly the DeviceID):

    |lab22-3|

#.  If you click on **ASM Cookie Hijacking** you should also see the following explanation:

    |lab22-4|

#.  Now click the **magnifying glass** in the upper left corner of the log frame and use the **search** feature find a **legal** request from ``f5student``.  ASM's session tracking capabilities extend to search as well.

    |lab22-6| |lab22-7|

#.  Compare the device IDs in this request vs the illegal request we just looked at. They should be different:

    |lab22-8|

    .. note:: The Device ID is essentially a fingerprint computed from a number of different browser and system attributes. They are unique identifiers that do not depend on browser session data. ASM uses these computed values to uniquely identify clients and tie them to user and session data. In this exercise we triggered an ASM Cooking Hijacking violation by replacing the cookies in the HTTP request with those of an existing valid session. ASM was able to detect this because the cookie data did not match the Device ID of the new browser.

#.  If this were a production configuration, we would likely enable the blocking settings back on the **Session Tracking** page so that these attacks would not be allowed to continue, but for the purposes of maintaining access to the lab environment we've elected not to do so.  Feel free to circle back and explore these options at the end of the lab:

    |lab22-5|

|
|

**This Concludes Section 2.2.**
