Lab 1.1 - Unprotected API
==========================================

Observe and simulate attacks on unprotected API endpoints
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Go to the UDF course and Log into the Client Workstation

|
|

.. image:: images/access_method.png

|
|


2. Click the **Access** > **RDP** and this will download the RDP shortcut link locally
   
|


3. Open the RDP session, and type the following username/password: **user**/**user** > Click **Continue**

|
|


.. image:: images/rdp_win.png

|
|


4. You may get a certificate validatity security warning, click **Continue.**
   
|
|


.. image:: images/certificate-warning.png

|
|


5. In the Windows Client Workstation open the **Postman Desktop** application. There should be a shortcut on the desktop. 
   
|
|


.. image:: images/postman_icon.png

|
|



6. In the *Postman Desktop* application, expand the **PetStore Collection**, and **Test API** folder 

|
|


.. image::  images/postman_test_api1.png

|
|


7. Click on **List Available Pets** request but **'do not'** click **Send** yet. Observe Authorization method, Headers, and URL for the GET request.  

|
|


8. Click on **Send** at the far-right side of the Postman window.
Observe the response Status is 200 Ok, in the body of the API response lists all the available pets.

|
|


9.	Let’s run through the same steps above on the **Place Order for Pet** and **Check Status of Order** requests.



What is the cause for concern with these last two requests? What will happen if numerous requests are sent to the server? 

|
|


10.	Let’s run through the same steps as the previous two exercises but this time we will simulate an injection attack. 
In Postman, click on the **Attacks** folder under **PetStore**, and click on the **Injection Attack request**. 
Observe the request URL, and the Parameters, click **Send**. Observe the response. Was the request successful? Why is this a concern?

|
|


.. image:: images/pm-injection-attack1.png

|
|


What these exercises demonstrated are common security vulnerabilities of unprotected API endpoints. 
Even simple API queries like List Available Pets can be susceptible when hundreds or thousands of requests are sent to the server causing resource starvation. 
To protect API endpoints from attacks, ensure proper authorization, and reduce resource starvation, we can implement F5 Application Security Manager using API Security Protection guided configuration.

|
|

We will explore how to do this in the next lab.

|
|