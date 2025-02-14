Lab 4 – Advanced configuration Options
--------------------------------------
Objective
~~~~~~~~~

Digging deeper into the OWASP Top 10 Compliance Dashboard



Apply additional protections against the OWASP Top 10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Security -> Overview -> OWASP Compliance -> juice_shop_waf** and select **A9 Security Logging and Monitoring Failures**.
    
        .. image:: ../images/a9check.png

    .. NOTE:: Some items within the Compliance Dashboard are designed for you to manually check as a Security Administrator.

    - Click the question mark beside **Log Illegal Requests**. Since we assigned a logging profile to this policy we can mouse over the Log Illegal Requests requirement and click on the check. 
    
        .. image:: ../images/illegal_check.png

    - Click **Review & Update** at the bottom and then **Save and Apply.**

    .. NOTE:: In production you should also setup remote logging to store your logs for the timeline set in your own security policies.  BIG-IP has limited storage for these events locally.


#. Back on the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**. Click on the expand arrow next to **A2 Cryptographic Failures**.  

    - Notice that Data Guard shows **NOT FULLFILLED**
    - Click on NOT FULLFILLED and you should be redirected to the security policy settings for Data Guard.  Click the slider to turn Data Guard from off to on.

        .. image:: ../images/dataguard_off.png

    - Click **Save** at the top to save your changes. 

        .. image:: ../images/dataguard_on.png

        .. NOTE:: Data Guard will mask sensitive PII fields in responses from your application and some are preconfigured.  However, notice that you can create custom patterns and exceptions.

    - Click **Apply Policy** to apply your changes

        .. image:: ../images/app_pol.png

    - Click OK in the window and go back to the OWASP Compliance dashboard once the changes have been applied.



#. On the OWASP COmpliance Dashboard, click on **A3 Injection** and take a look at your options.
    
    - Notice that there are Required Protections in addition to the signature sets that we have already enforced.

        .. image:: ../images/a3check.png

    - Click on **NOT FULLFILLED** next to Evasion Techniques and then click on **Review & Update** at the bottom.

        .. NOTE:: Some mitigations can be configrued direction in the OWASP Dashboard like this. Evasion techniques refer to techniques apoplied by hackers to attempt to access resources or evade what would otherwise be identified as an attack.

        .. image:: ../images/evasion.png

    


Conclusion
~~~~~~~~~~~

You can continue to explore the OWASP Compliance Dashboard until the class is ready to move forward.