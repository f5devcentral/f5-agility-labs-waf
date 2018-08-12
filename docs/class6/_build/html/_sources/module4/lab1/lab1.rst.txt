Lab 4: CSRF (Cross-Site Request Forgery)
---------------------------------------------

This lab will simulate a Cross-Site Request Forgery against WebGoat Application.
It is designed to show how ASM can mitigate similar real world vulnerabilities. 

|

Connect to the Lab Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the jumphost, launch firefox, click the BIG-IP bookmark and login to TMUI. admin/password

#. In separate tab connect to http://webgoat.local/WebGoat/login or click the bookmark and login as f5student/password

|

Test CSRF Behavior
~~~~~~~~~~~~~~~~~~

1. In the WebGoat App, go to Request Forgeries, then click Cross-Site Request Forgeries

2. Click the tab/button for #4 and read through the lesson.

	*In this lesson you will use a common comment/review page for an online seller.*

|

.. image:: images/webgoatlesson.png
        :width: 600px

|

3. Minimize the browser and open the CSRF.html file on your desktop.

	*This is an example of a website asking you to register for a mailing list.*

4. Type in "f5student@example.com" and click Sign Up. This should open a new tab, leave the tab open. 

|

.. image:: images/attackersite.png
        :width: 600px

|

.. note:: This type of tab would not normally pop up upon a successfull CSRF attack and is purley here for illustration purposes

|

5. Click back on your webgoat browser tab. Then refresh (you ust refresh the page to view the changes) the reviews section.  What do you notice?

	*The attacker site took advantage of the fact that you were already logged in to WebGoat Application and used your account to post a review.*

6. Go back to the attacker site tab, right-click and select view source.  Examine the code to see the hidden form fields that were used for the attack.

|

Mitigate the Attack
~~~~~~~~~~~~~~~~~~~

1. Apply the ASM241 Security Policy to the asm_vs. On the BIG-IP TMUI, go to Local traffic > Virtual Servers > asm_vs

2. Click the Security tab and make sure “Application Security Policy” is set to “asm241”. 
   
3. Make sure the logging Profile is set to “Log Illegal Requests”

4. Click Update to apply the policy to asm_vs.

|

.. image:: images/ltmsettings.png
        :width: 600px

|

5. Apply CSRF Protection to the ASM241 policy. Go to Security > Application Security > CSRF Protection, ensuring the "Currently edited security policy" is ASM241.

6. Check enabled and in the New URL field type "/WebGoat/start.mvc*"

|

.. image:: images/csrfpol.png
        :width: 600px

|

5. Click Add and Save, then click Apply Policy in the top right and OK.

6. Go to Security > Application Security > Policy Building > Learning and Blocking Settings and select “Advanced” in the drop-down on the right.

7. Expand CSRF Protection and ensure all checkboxes are checked for “CSRF attack detected”.

|

.. image:: images/csrfprotect.png
        :width: 600px

|

Test the CSRF attack again
~~~~~~~~~~~~~~~~~~~~~~~~~~


1. Browse to http://webgoat.local/WebGoat/login and login as “f5student”.

2. On the left menu click Request Forgeries, then click Cross-Site Request Forgeries.

3. Click the number “4” near the top of the page.

4. Open the “CSRF.html” file on your desktop again or click back on the “Attacker site” tab in your browser if it is still open.

5. Type anything into the text field and click the Sign Up! Button.

	*The request should be blocked by ASM*

6. On the BIG-IP, go to Security, and click on Event Logs.

	*You should see the CSRF attempt blocked and logged*

