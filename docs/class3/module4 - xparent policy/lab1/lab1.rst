Exercise 4.1: Transparent Policy 
----------------------------------------

Objective
~~~~~~~~~~
We created a transparent policy way back in Lab 1 to configure IPI and Geolocation. We then tested out the Threat Campaign signatures in Lab 3. Now we will explore and test some of the first things you should get amiliar with when developing a WAF policy. 


- Review Learning & Blocking & Policy Building Process settings
Review Trusted IP and IP address exception properties. 

The Dangers of learning from Internet IP's 

- Enable Server Technologies https://clouddocs.f5.com/training/community/waf/html/class3/module3/lab3/lab3.html

- Review Default Attack Signature Configuration. 

- Test with a XSS attack

- Implement HTTP Protocol Compliancy checks

- Test with HTTP attack HTTP Compliancy Check - Bad Host Header Value - triggers both attack signature and protocol check

- Implement Evasion Techniques

- Test Evasion Techniques

- Review Event Correlation

Bonus- Review Login Page Protection and Brute Force Configuration protection. 
 

- Estimated time for completion **45** **minutes**.

Apply Security Policy
~~~~~~~~~~~~~~~~~~~~~

.. IMPORTANT:: To clearly demonstrate just the protocol compliance , on the ``webgoat.f5.demo_https_vs`` virtual server; PLEASE PERFORM THE FOLLOWING TWO STEPS:

#. Navigate to the **webgoat.f5.demo_https_vs** virtual, then its **Security** tab.
#. **Remove** the previously created Bot Defense **(webgoat_bot)** profile and bot logging profile **(bot-defense)**.
#. **Enable** the ``lab1_webgoat_waf`` Security Policy

Your virtual should look like this

.. image:: images/image1.png
    :width: 600 px

Burp'ing the App
~~~~~~~~~~~~~~~~

In this section we are going to use the free/community version of an excellent DAST tool; Burp. Unfortunately, the free version does not actually allow DAST but it is still an excellent tool for packet crafting and that's exactly how we are going to use it.
We will be manually sending two different attack types to demonstrate the protocol compliance features of ASM.

HTTP Compliancy Check - Enforce Host Header
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE:: By way of RFC; HTTP/1.1 requires a host header. Many servers will still process the request without one. We want to enforce RFC compliant HTTP.

1. Open Burp by clicking the icon in the system tray at the top of the screen. (If it offers an update, please decline)

.. image:: images/burp.png

2. This will be a temporary project so click **next** to proceed and choose "Use Burp Defaults" on the next screen.

3. Click **Start Burp** and navigate to the **Repeater** tab once opened.

4. Under the **Request** tab paste in the following http request, remove any whitespace or use the text version on the desktop (go to waf141 folder on Desktop, file is called NoHostHeader.txt), and click **Go**.

Attack 1: No Host Header - **Run this 10 times.**

::

  POST https://webgoat.f5.demo/WebGoat/login HTTP/1.1
  User-Agent: R2D2
  Pragma: no-cache
  Cache-Control: no-cache
  Content-Type: application/x-www-form-urlencoded
  Content-Length: 38

  username=f5student&password=password


.. IMPORTANT:: When you copy and paste there may be whitespace in front of the headers. You will need to remove this manually or the request will not be sent. The requests can also be found in txt docs on the client desktop. If you copy and paste from there rather than this site, the whitespace will not be a problem.

5. A popup will appear asking for target details. Fill out the form as shown below.

.. image:: images/image101.png
    :width: 600 px

Request and Response should look like this

.. image:: images/image5.png
    :width: 600 px

6. Navigate to **Security > Event Logs > Application > Requests** (the illegal request filter should be cleared). You should see these requests being logged as legal but you may want to implement policy per the "Good WAF  recommendations", to not allow this since it is not RFC compliant HTTP/1.1

.. image:: images/image20.png
    :width: 600 px

Learning and Blocking
~~~~~~~~~~~~~~~~~~~~~~

1. Navigate to **Security > Application Security > Policy Building > Learning and Blocking Settings** and look for **HTTP Protocol Compliance failed**

.. image:: images/module2Lab1Excercise3-image1.png
    :width: 600 px

2. Notice the violation is set to learn only and is not enabled by default in a Rapid Deployment Policy. That is why the request was seen as legal and there was no alert in the event logs.

3. Since learning **was** on by default there must be a learning suggestion ready for us. Let's go take a look.

4. We want to specifically find the learning suggestion for **HTTP protocol compliance failed - HTTP Check: No Host header in HTTP/1.1 request**

5. Navigate to **Security > Application Security > Policy Building > Traffic Learning** and click on the search.

6. In the suggestion section select **HTTP Protocol Compiance**.

.. image:: images/module2Lab1Excercise3-image2.png
        :width: 600 px

|

6. Under the Advanced Tab move the slider to the left so you can see alerts with a learning score of less than 50 and click **Apply Filter**

.. image:: images/module2Lab1Excercise3-image3.png
        :width: 600 px

|

7. Note the action ASM is suggesting that you take - **"Enable HTTP Check"**. As in the example, you may ahve multiple suggestion for HTTP Protocol Compliance Failed, they should all be from the burp test.

.. image:: images/module2Lab1Excercise3-image4.png
    :width: 600 px

|

8. Click **Accept Suggestion** and then browse back to **Security > Application Security > Policy Building > Learning and Blocking Settings > HTTP Protocol Compliance failed** and notice that by accepting the learning suggestion ASM has now enabled the  but it is still in learning mode so **uncheck** that manually.

.. image:: images/module2Lab1Excercise3-image5.png
    :width: 600 px

9. **Be sure you have clicked "Save" and Apply the Policy prior to proceeding.**


10. Go back to **Burp** and run the attack again one or more times.

11. Browse to **Security > Event Logs > Application > Requests** on the BIG-IP GUI. 
You should now see the alerts since we have enabled this compliancy check and turned off learning.

.. image:: images/module2Lab1Excercise3-image6.png
    :width: 600 px

HTTP Compliancy Check - Bad Host Header Value
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The **Bad Host Header Value** check is an HTTP Parser Attack and definitely something that should be implemented as part of **Good WAF Security**.

**Risk:**
If we allow bad host header values they can be used to Fuzz web servers and gather system information. Successful exploitation of this attack could allow for the execution of XSS arbitrary code.

1. Navigate to **Security > Application Security > Policy Building > Learning and Blocking Settings > HTTP Protocol Compliance failed** and find **Bad host header value**
Notice that by default this is also in learning mode but disabled by default in a Rapid Deployment Policy.

.. image:: images/module2Lab1Excercise4-image1.png
        :width: 600 px

|

2. **Uncheck** the Learn box and **Check** the Enable box. Scroll up, click **Save** and **Apply Policy**.

3. Go back to **Burp** and under the **Request** tab paste in the following http request, remove any whitespace, or use the text version on the desktop (go to the waf141 folder on the Desktop, file is called BadHostHeader.txt), and click **Go**.
Replace password with the password provided by the instructor.

|

Attack 2: XSS in HOST Header

::

  POST https://webgoat.f5.demo/WebGoat/login HTTP/1.1
  User-Agent: BB8
  Pragma: no-cache
  Cache-Control: no-cache
  Content-Type: application/x-www-form-urlencoded
  Content-Length: 38
  Host: <script>alert(document.cookie);</script>

  username=f5student&password=password

.. image:: images/module2Lab1Excercise4-image2.png
    :width: 600 px

4. Browse to **Security > Event Logs > Application > Requests** and review the alert for this attempted attack. Note the alert severity is much higher (4) for this attack type due to the risk it presents.

.. image:: images/module2Lab1Excercise4-image3.png
        :width: 600 px

5. Click **Export Request** and review the detailed report. Notice the XSS alerts and how they are currently still in staging. We will cover this in the next module.

HTTP Compliancy Check - Multiple Host Headers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Description - Examines requests to ensure that they contain only a single "Host" header.
This is an example of an HTTP Request Smuggling Attack

Risk - An attacker may try to evade security checks by confusing ASM and/or application servers as to which hostname is being accessed.

Example - The website may be accessed by non-browser clients attempting to bypass security gateways.

.. NOTE:: There will be little guidance on this section. Use what you have learned above to complete this lab. Please ask an instructor if you need help.

**Order of Operations**

1. Disable learning and Enable the Compliancy Check for **Multiple Host Headers** in learning and blocking settings.
2. Use **BURP** to perform the Attack

::

  POST https://webgoat.f5.demo/WebGoat/login HTTP/1.1
  User-Agent: BB8
  Pragma: no-cache
  Cache-Control: no-cache
  Content-Type: application/x-www-form-urlencoded
  Content-Length: 38
  Host: LordVader
  Host: LukeSkywalker

  username=f5student&password=password

3. Review Event Logs to ensure the attack is being mitigated. Notice the alert level is lower for this attack type due to less risk than a potential XSS as seen in the previous exercise.

.. image:: images/module2Lab1Excercise5-image1.png
    :width: 600 px

|

.. image:: images/module2Lab1Excercise5-image2.png
    :width: 600 px

Evasion Techniques
~~~~~~~~~~~~~~~~~~~~~

1.  Open a new Private Window in Firefox and navigate to the WebGoat login page (https://webgoat.f5.demo/WebGoat/login).

2. Enter **%253Cscript%253E** in Username field and **a** for the Password field. Click **Sign-in**. Of course this user does not exist in the WebGoat database and will not be logged in. What would expect in the ASM events? 

|

.. image:: images/module1Lab1Excercise1-image18.png
        :width: 600px

|

3. Go to **Security > Event Logs > Application > Requests**. Do you see anything? 

4. If you don't, what do you think needs to be done? This excercise if left up to the student. 

**This concludes module 2**