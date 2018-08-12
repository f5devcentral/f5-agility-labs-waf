Lab 8: XXE Protection
----------------------------------------

In this lab you will learn how to utilize ASM to mitigate the use of malicious XML External Entities

Connect to the lab environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From the jumphost, launch Chrome, click the BIG-IP bookmark and login to TMUI. admin/password

|

.. note::
	While you can use firefox for connecting to the BIG-IP in this lab, you will be intercepting firefox traffic.
	It may be easier to use two browsers instead of two tabs.

|

2. From the jumphost, launch firefox, which we will use to access WebGoat.

3. In firefox go to the right-hand side icon and select "Preferences". 

|

.. image:: images/settings.png
        :width: 600px

|

4. Then select Advanced > Network, under “Connection” click “Settings”.

|

.. image:: images/ffAdvanced.png
        :width: 600px

|

5. Set your proxy settings to manual as shown in the screenshot below, click “Ok”.

|

.. image:: images/proxy.png
        :width: 600px

|

5. From the jumphost desktop, launch Burp Suite using the icon on the desktop. If you are prompted to update Burp, ignore this pop-up by clicking “Close”.

  - Select Temporary Projects and click Next.
  - Leave Defaults checked and click "Start Burp"
  - Select the "Proxy" tab and then turn intercept off.

|

.. image:: images/proxyoff.png
        :width: 600px

|

An XXE Vulnerability
~~~~~~~~~~~~~~~~~~~~

1. Login to WebGoat using firefox f5student/password.

2. Select "Injection Flaws" and then select "XXE".

3. If XML or XML External Entities are new to you, then please start from the begging and read through parts 1 and 2 in the WebGoat Lesson.

4. Under part 3, enter a comment to familiarize yourself with the application.
*To complete the lesson, you will need to figure out how to list the contents of the root directory utilizing this submission form.*

5. Enter the following statment in the field and click submit. What does this tell us?

:: &xxe;

6. So we know that an XML External Entity can be utilized with this form, but we will need to manipulate a request.


Manipulating the Request
~~~~~~~~~~~~~~~~~~~~~~~~

1. In Burp Suite turn Intercept back to on.

|

.. note::
	The firefox browser is being pointed to localhost as a proxy and therefore Burp may intercept the request.

|

2. Submit another comment using something simple like "test" or "abc".

3. Burp should come back to the front, but if not switch to Burp to examine the request.

|

.. image:: images/examplereq.png
        :width: 600px

|

4. Edit the request with the following XML.

|

.. code-block:: xml

        <?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///" >]>
        <comment>
        <text>abc&xxe;</text>
        </comment>

|

*There should be an XML document on your desktop named xxe which you may paste from to save time, but please read and understand the request.*

|

.. image:: images/editedreq.png
        :width: 600px

|


5. Click Forward to pass the request on to the server and make sure you forward any remaining requests before turning intercept back off.

6. What was the result?


Mitigate an XXE attack
~~~~~~~~~~~~~~~~~~~~~~

1. Login to the BIG-IP as before with admin/password.

2. Browse to Local Traffic > Virtual Servers > asm_vs and select "Policies" under the security tab.

3. Make sure "ASM241" is selected as your Application Security Policy and that you have "Log Illegal Requests" as your Log Profile. Click "Update" if any changes are made.

|

.. image:: images/ltmsettings.png
        :width: 600px

|

4. Go to Security > Application Security > Attack Signatures and make sure your current edited policy is ASM241.

5. Under Policy Attack Signatures, select "Signature name contains" and enter "External" before clicking Go.

6. Select the following signatures and click enforce. Click "Apply Policy".

|

.. image:: images/attacksig.png
        :width: 600px

|     

7. Using Burp suite and firefox, turn intercept back on we will run the same test, manipulating the request. 
   
8. Submit another comment that is different from the previous, something simple like “test1” or “abc1”.
 
9. Burp should come back to the front, but if not switch to Burp to examine the request.

10. Edit the request with the following XML.

|

.. code-block:: xml

        <?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///" >]>
        <comment>
        <text>abc1&xxe;</text>
        </comment>

|


.. image:: images/burpXxe.png
        :width: 600px

|

11. Forward the request. What happens this time?

|

Check your logs
~~~~~~~~~~~~~~~

1. On BIG-IP go to Security > Application Security > Event Logs > Application > Requests.

2. You should see an entry that trigger the now enforced Attack Signatures.

|

.. image:: images/xxe_event.png
        :width: 600px

|

     
3. What is another way that ASM could be used to mitigate XXE injection?

*Hint: Take a look at the Application Security > Content Profiles > XML Profiles.*
*The Default profile is applied to all http and https requests.*

4. Turn intercept back to off and close Burp Suite.  Then return to your firefox settings and change the proxy settings back to "No Proxy".
