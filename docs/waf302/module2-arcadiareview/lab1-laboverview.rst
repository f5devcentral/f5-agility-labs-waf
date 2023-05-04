Lab 2.1: Lab Environment 
=================================

We’re going to be working in the BIG-IP, AS3, and Postman to deploy an ASM template with reference to a hosted swagger definition file. 

1. In the Lab Components deployment page > Click the **Access** menu under the “Client Workstation” and select **RDP** 

.. image:: images/udf-rdp.png

Open RDP to the Windows Client
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2. Log into the Windows Client via RDP using the following credentials:

	Username:	:guilabel:`user`

	Password: 	:guilabel:`user`

3. Within the Windows Desktop, Open Chrome and Postman (will take several seconds).

4. In Chrome > click the **Arcadia Finance** bookmark

5. Within **Arcadia Finance**, find the Login page and login using admin/iloveblue as user/password

	Username:	:guilabel:`admin`

	Password: 	:guilabel:`iloveblue`

5. Navigate the site and perform a couple of actions to familiarize yourself with the apps running. i.e., *Buy Stocks*, *Sell Stocks*, *View Your Last Transactions*.

.. image:: images/arcadia-admin.png

These three applications (Buy, Sell, Last Transactions) that are serviced by APIs populated by your selections on this frontend site.

Notice the **Coming Soon** countdown on the right side.  We will be deploying that feature later in this lab.

Now that you're familiar with the lay of the land, let's move to the next section of this lab.
