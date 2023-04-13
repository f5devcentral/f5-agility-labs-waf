Lab 1.4: Test the Arcadia Finance Prod Security Policy
========================================================

Now go back to Postman, *Arcadia Finance* >> *Prod* >> *Test API* >> *PROD - buy_stocks* and click **Send** (You should get a 200 response)
Select *Headers* and change the content-type to **text/plain** instead of *application/json* and click **Send** again. 

 .. image:: images/postman-text-plain.png

Q: Given that our backend API should only accept JSON requests, is this acceptable?


Go back to the Arcadia Prod security policy and select allowed URLs > asterisk and review the Header-based Content profiles again. Notice there is a default rule that allows “Any” header value if it passes signature check validation. That is why your request was accepted.

.. image:: images/big-ip-securitypolicy-urls-contenttype-default.png

First Strike!
~~~~~~~~~~~~~ 

Let’s see if something more malicious will get through...

From the Windows RDP go to Postman and expand the *Prod* >> *Attacks* folder
Select *Buy Stocks – Header* and then select *Headers* on the right pane

That Keep-Alive header looks suspicious!

 .. image:: images/postman-attack-header.png

Click Send on the request. Was it a success?  
Review the ASM Security Event Logs under Security >> Event Logs >> Application >> Requests

Go back to Postman and *Arcadia Finance* >> *Prod* >> *Test API* folder and click send on the *PROD - sell stocks* and *PROD - last transactions* requests to verify they work

Now that we have reviewed our Production instance, let’s deploy our development version.
