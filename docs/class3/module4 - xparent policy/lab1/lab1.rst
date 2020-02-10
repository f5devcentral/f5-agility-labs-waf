Exercise 4.1: Transparent Policy 
----------------------------------------

Objective
~~~~~~~~~~
We created a transparent policy way back in Lab 1 to configure IPI and Geolocation. We then tested out the Threat Campaign signatures in Lab 3. Now we will explore and test some of the first things you should get familiar with when developing a WAF policy. 


- Review Learning & Blocking & Policy Building Process settings
- Implement HTTP Protocol Compliancy checks and test
- Test with a HTTP Protocol violation plus XSS attack
- Enable Server Technologies https://clouddocs.f5.com/training/community/waf/html/class3/module3/lab3/lab3.html
- Review Default Attack Signature Configuration. 
- Review Reporting


Bonus- Review Login Page Protection and Brute Force Configuration protection. 
 

- Estimated time for completion **45** **minutes**.

Learning & Blocking & Policy Building
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Recall from Lab 1, that we used the Rapid Deployment Policy template to create our policy and we deployed it in manual learning mode. This means as violations and/or false positives occur, the system will make recommendations to modify the policy and the admin will manually evaluate the changes.  

#. Navigate to **Security > Application Security >  Policy Building > Traffic Learning** and explore each of the sections under **Traffic Learning Summary**. 
#. You will see many Suggestions and a learning score that the system assigns based on how many times it has seen an occurence and from what source. You can **Accept**, **Delete**, **Ignore** or **Export**  the suggestion. Look very carefully at the suggested action before deciding on which action to take.  

.. image:: images/learning.png
  :width: 600 px

#. Click the **Learning and Blocking Settings** tab at the top of the GUI and expand the **HTTP protocol compliance failed** section. Enforcing HTTP protocol compliance is a good practice and should not cause administrative burden. Notice we are already set to learn for most of the violations in case a webapp is poorly written or configured. By learning we will have the opportunity to weed out any false positives caused by HTTP Protocol Compliance violations prior to enabling blocking. 
#. Uncheck the box for learning under **Bad Host header Value** and check the **Enable** box. 
#. Check the box to enable learning for **Host header contains IP address**.
#. Hit **Save** at the bottom of the screen and then **Apply Policy** at the top of the screen. 

.. image:: images/http.png
  :width: 600 px

#. From Firefox on client01, load the insecureApp1 bookmark and refresh several times. 
#. Navigate to **Security > Application Security >  Policy Building > Traffic Learning** then scroll down to the bottom under **Suggestions** and notice the new learning suggestion for **Host header contains IP address** since we are browsing the site by IP and not hostname. 
#. If we accept this suggestion it will actually enable the HTTP Check for **Host header contains IP address**. Click **Accept** and **Apply Policy**
#. Return to the **Learning and Blocking Settings** tab at the top of the GUI to review the effect of your action. 
#. Notice that the **Enable** box is now checked for **Host header contains IP address**.

.. image:: images/enabled.png
  :width: 600 px

This means as violations occur you will now see them in the event logs. 

#. From Firefox on client01, load the insecureApp1 bookmark and refresh several times. 
#. Navigate to **Security > Event Logs > Application > Requests** and review the latest Sev3 alert. Notice the Violation type and then click on the **1** under Occurrences to see more information. 

.. image:: images/violation.png
  :width: 600 px


Burp'ing the App
~~~~~~~~~~~~~~~~

In this section we are going to use the free/community version of an excellent DAST tool; Burp. Unfortunately, the free version does not actually allow DAST but it is still an excellent tool for packet crafting and that's exactly how we are going to use it.
We will be manually sending two different attack types to demonstrate the protocol compliance features of ASM.

HTTP Compliancy Check - Bad Host Header Value
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The **Bad Host Header Value** check is an HTTP Parser Attack and definitely something that should be implemented as part of **Good WAF Security**.

**Risk:**
If we allow bad host header values they can be used to Fuzz web servers and gather system information. Successful exploitation of this attack could allow for the execution of XSS arbitrary code.

#. Launch **Burp** from the dock and ignore the java warning. 

.. image:: images/burp.png

**DO NOT update**. 

#. Choose **Temporary Project** and click **Next** and then click **Start Burp**. 

#. Click the **Repeater** tab and paste in the following http request (**Replace password with the password provided by the instructor.**) and click **Send**.
#. A popup window will appear to Configure the target details. For host use: **10.1.10.145**. For port use: **443**. Check the **Use HTTPS** box. 

|

XSS in HOST Header

::

  POST https://10.1.10.145/WebGoat/login HTTP/1.1
  User-Agent: BabyYoda
  Pragma: no-cache
  Cache-Control: no-cache
  Content-Type: application/x-www-form-urlencoded
  Content-Length: 38
  Host: <script>alert(document.cookie);</script>

  username=f5student&password=password


#. Browse to **Security > Event Logs > Application > Requests** and review the alert for this Sev5 attack. Note the alert severity is much higher (5) for this attack type due to several violations occuring.
#. Review all the details and then click the **3** under the **Attack Signature Detected** violation to see all of the XSS Attack Signatures that were triggered. 
