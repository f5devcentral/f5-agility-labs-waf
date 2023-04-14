Lab 2.1: Review and Deploy AS3 Declaration
============================================



2.1.2 - Install Python
~~~~~~~~~~~~~~~~~~~~~~~

In Postman, expand the *Arcadia Finance* >> *Dev* >> *Test API* >> *Deploy DEV w/ OAS* folder and select on **Deploy DEV w/ OAS**. Do not send this payload just yet. 


.. image:: images/postman-deploydev.png

In the declaration, we are deploying a new security policy called **arcadia_dev_policy**.
Near the bottom, you can see we are defining this policy by calling a json file.
Let’s take a look at this policy file

In the Components section click Access under the App Server (Ubuntu) and select Web Shell or SSH if you provided your own keypair.

In the CLI type: 

.. code-block:: bash

        cat /home/ubuntu/repo/arcadia/dev/policy-api-arcadia-dev.json

.. image:: images/ubuntu-policyjson.png

This is a basic Owasp Top 10 policy based on our Production instance with one difference.

Notice at the bottom we are referencing an OpenAPI file. Let’s review this file.

From CLI type: 

.. code-block:: 

        bashless /home/ubuntu/repo/arcadia/dev/arcadia-oas3-dev.json

Hit SPACE or Enter to scroll through the file and review the settings.
The paths and parameters should look familiar as you’ve already used them in Postman.
Hit Q when you’re done.

Now that you have examined how the declaration ties these files together, it’s time to start your repo service and deploy the Development VIP

In Ubuntu cd /home/ubuntu and type:

.. code-block:: 

        ./start-web-server.sh

and hit Enter a couple times

.. image:: images/ubuntu-startwebserver.png

From Postman click *Arcadia Finance* >> *Dev* >> *Test API* >> *Deploy Dev w/ OAS* and hit **Send** (will take a few seconds)

You should get a *200 OK response* with the details of your deployment.

.. image:: images/postman-results.png

Verify the deployment was a success by clicking the *Arcadia Finance* >> *Dev* >> *Test API* >> *DEV - Buy stocks* request and hit **Send** (JSON response body should indicate Success)

In the BIG-IP select the new **arcadia-dev** partition at the top-right

.. image:: images/big-ip-arcadia-dev.png

Go to *Security* >> *Application Security* > *Security Policies* and click on the **arcadia_dev_policy**

Unlike our previously reviewed arcadia-prod policy, notice how now we are referencing an OpenAPI file in the security policy

 .. image:: images/big-ip-swagger.png

Under *Application Security* go to *URLs* >> *Allowed URLs*
No more wildcard paths allowed since this is for API gateway enforcement not just basic web security.

Select */trading/rest/buy_stocks.php* URL and click *URL Parameters* at the top. 
Notice how there are no wildcard parameters and parameters names are now defined.

.. image:: images/big-ip-urls-buystocks.png

