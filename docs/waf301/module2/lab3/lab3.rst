Lab 2.3: Verify ASM Policy with f5 WAF Tester
=====================================================

According to sources, Capital One suffered a data breach which was announced in late July of 2019.  
Although protected by a WAF, it was misconfigured and not able to stop the attack executed by Paige Thompson, 
aka "erratic".  Paige used an exploit called Server Side Request Forgery (SSRF) to compromise a web server
and access roughly 100 million credit card applications among other PII data. Capital One is estimating this data breach will 
cost the company $100 to $150 million dollars in the near term.  

We will look through the report of the f5 WAF tester to see if any SSRF attacks failed.

2.3.1 - Review f5 WAF Tester report
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Look for any failed Server Side Request Forgery.

To quickly search the report we will issue a simple jq command.

	From the Terminal type (make sure you are in directory ~/.local/bin): 

		.. code-block:: bash

			cat report.json | jq '.details[]| select(.attack_type | contains ("Server Side Request Forgery")) | .attack_type, .results[]'

    You should see that both SSRF protections passed, and that your policy will thwart an attack like Capital One experienced.
	
    .. image:: images/report.png

	





    **End of Module 2**