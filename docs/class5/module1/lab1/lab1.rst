ab 1: Brute Force Attack Prevention
----------------------------

..  |lab1-1| image:: images/lab1-1.png
        :width: 800px
..  |lab1-2| image:: images/lab1-2.png
        :width: 800px
..  |lab1-3| image:: images/lab1-3.png
        :width: 800px
..  |lab1-4| image:: images/lab1-4.png
        :width: 800px
..  |lab1-5| image:: images/lab1-5.png
        :width: 800px
..  |lab1-6| image:: images/lab1-6.png
        :width: 800px
..  |lab1-7| image:: images/lab1-7.png
        :width: 800px

There is more than one kind of brute force attack. In the classic version, hackers attempt to log in to an application by repeatedly guessing users’ account credentials. Because of these attacks, most applications now lock an account when it encounters multiple unsuccessful authentication attempts, at least temporarily. However, this strategy only protects against attack on a single account.

In another version of this attack, commonly called “credential stuffing,” hackers make only one attempt to log in to users’ accounts. They obtain a collection of user name and password combinations from a compromised application and programmatically evaluate them against their target application, looking for accounts where users reused their compromised credentials. When they finish, the hackers know those accounts for which they have valid credentials on the target application.

.. note:: If you are continuing on from 141 Lab please do X. If you are continuing on from 241 lab please do y. Else :


Task 1 - Configure Brute Force Attack Prevention
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Open the BIG-IP interface in Firefox. 
    
#.  Navigate to **Security -> Application Security -> Anomaly Detection -> Brute Force Attack Prevention** and click **Create**.

    .. note:: F5 WAF has a number of brute force attack detection capabilities that are beyond the scope of this exercise.  Take some time to examine some of the other options as you work through this lab.  For more information see:  ``https://techdocs.f5.com/en-us/bigip-15-0-0/big-ip-asm-implementations/mitigating-brute-force-attacks.html`` .

#.  Select the login page you created earlier.

    |lab1-1|

#.  Configure **Source-based Brute Force Protection** settings as follows:

    |lab1-2|

#.  Click **Create** .

    
#.  Click **Apply Policy**, then click **OK** .


Task 2 - Test username based Brute Force Protection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
#.  Open a new Private Browsing window in **Firefox** .

#.  Go to the to WebGoat login page at ``https://insecureapp1.f5.demo/WebGoat/login`` but **do not login as f5student** .

#.  Attempt to login using any username (not f5student) and password at least 4 times.


#.  Examine the most recent **illegal** request in the event log:

    |lab1-3|

    Take note of the username field.  The request was blocked as a brute force attack.

#.  Click the **Brute force: Maximum Login Attempts are exceeded** header at the top of the event window:

    |lab1-4|

    The message indicates the number of login attempts by a user exceeded the threshold.

Task 3 - Enable Device ID
~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Security -> Bot Defense -> Bot Defense Profiles** and edit the profile **insecureApp1_botprofile** to enable Device ID mode to "Generate Before Access" for browsers.  The Device ID is a unique identifier that F5 WAF creates by sending JavaScript to get information about the client device

#. Click **SAVE**

    |lab1-5|


Task 4 - Test Device ID based Brute Force Protection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Open a new Private Browsing window in **Firefox** .

#.  Go to the to WebGoat login page at ``https://insecureapp1.f5.demo/WebGoat/login`` but **do not login as f5student** .

#.  Attempt to login using any username and password at least 4 times.

#. Once Blocked close the browser and re-open a new Private Browsing window in Firefox

#. Attempt to login using a different username as in step 3, your first request should be blocked.

#. Examine the most recent illegal request in the event log:

    |lab1-6|

#. Click on the Occurrences and notice the Device ID for the request. 

    |lab1-7|


|
|


**This concludes Lab 1.**

