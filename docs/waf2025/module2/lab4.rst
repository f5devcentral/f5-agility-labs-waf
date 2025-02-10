Lab 4 – Advanced configuration Options
--------------------------------------
Objective
~~~~~~~~~~~

- Apply some configurations to protect against the remaining OWASP Top 10



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





Conclusion
~~~~~~~~~~~

Now for our last step, once again go back to the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**.
You should now be mostly compliant in all categories that a WAF can control and reduce risk in those areas. The compliance topics of A6 and A9 a WAF cannot mitigate these risks. The user would need to go into each of these sections and mark accordingly how their environment is configured. While it is nice to see completion, the goal of the dashboard is not always to immediately reach 100% in all categories. The true value is providing visibility and measuring the security controls that are applyed to our applications. 
