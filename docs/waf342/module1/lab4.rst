Lab 1.4: Deploying to secops testing environment 
================================================

Now that we have a template created, we’re now done with the BIG-IP for now and are moving onto Postman.  
Postman will be interacting with our BIG-IP via AS3 making API calls.  
Launch Postman from the Linux desktop icon shown below:

    .. image:: images/10-module1.png

    **1.4.1** Once Postman is open, we need to import the collection (series of declarations we’ll be using on our BIG-IP) from GitHub.  To do so, click on ‘Import’ on the top left of Postman and select ‘Import From Link’ option.  Paste the following into the field where you enter the URL and click ‘Import’
    
.. NOTE:: If the collection already exists choose 'replace'

        http://gitlab.lab/waf_labs/waf_cicd/raw/master/WAF_301_postman_collection.json?inline=false

        .. image:: images/11-module1.png

        **1.** With the collection imported, on the left-hand pane of Postman, you’ll see the collection titled ‘WAF_301’ with several declarations under it:

        .. image:: images/12-module1.png

        **2.** The first collection does a simple GET request against the lab BIG-IP to ensure that AS3 is installed and running.  
        It will also show you the version of AS3. 

        **3.** Click on the selection ‘check if AS3 is ready’ and click ‘Send’.  You should see the BIG IP report back with the following:

        .. image:: images/13-module1.png

        **4.** This validates that AS3 is running and responded with version 3.32.1

**1.4.2:** We’re now going to make an AS3 declaration to the BIG-IP.  To view the JSON declaration, click on the declaration titled **as3 with_declarative_waf_and_vs** and select :guilabel:`Body` and :guilabel:`raw` as shown below:

    .. image:: images/14-module1.png

    In this declaration, we’re going to be creating a new Virtual Server on the BIG-IP, creating an ASM policy by referencing the template created earlier and applying it to the new Virtual Server. This virtual server front-ends a pool member that is running OWASP’s Juice Shop application that has all of the OWASP top 10 vulnerabilities.  

    Also note that the declaration is calling an external URL hosted on Gitlab and is our WAF JSON declaration that will be creating all of the configuration items mentioned above.  If you’d like, you can view the JSON declaration by using the bookmark bar in FireFox on the Linux Desktop and clicking on the ‘WAF_342’ Bookmark folder and clicking on ‘Gitlab’. login with the cached credentials and  The following screen appears:

        .. image:: images/15-module1.png

    **1** Click on ‘waf_labs / waf_cicd’ and at the bottom of the page you’ll see ‘waf_policy.json’.  Click on that to view the JSON file:

.. NOTE:: in the top section you’ll see the name 'owasptop10_agility2020'.  This refers to the template we created on the BIG-IP to build the ASM policy and matches the name of the template we created in the BIG-IP.

        .. image:: images/16-module1.png

    **2** Return to Postman and run the declaration titled ‘as3_with_declarative_waf_VS_create’ by clicking ‘Send’ on the far right of the screen.  If it finished successfully, you’ll see the following response from the BIG-IP in Postman.

        .. image:: images/17-module1.png

    **3** Validate that the ASM policy has been created via the previous step by logging into the BIG-IP with the following credentials.  

        Username:	admin
		Password:	f5DEMOs4u!

		Once logged in, go to: 

            Security  ››  Application Security : Security Policies : Policies List
	
            There you’ll see the policy titled ‘waf_juiceshop_secops_testing’ under the newly created ‘secops_testing’ partition:

.. NOTE:: Be sure and switch to the 'secops_testing' partition or you will not see the changes. They're not in the 'common' partition. 

                .. image:: images/18-module1.png

            This declaration also created a VS on the BIG-IP called ‘juiceshop_secops_testing’ with the security policy ‘waf_juiceshop_secops_testing’ WAF policy applied.

                .. image:: images/18-module1.png
