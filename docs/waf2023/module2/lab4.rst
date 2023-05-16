Lab 4 – Advanced configuration using the OWASP Dashboard
---------------------------------------------------------------------
Objective
~~~~~~~~~~~

- Apply some final configurations to protect against the remaining OWASP Top 10

- Do a final review of the OWASP Compliance Dashboard

Apply additional protections against the OWASP Top 10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Security -> Application Security -> Security Policies -> Policies List** and select the Juice_Shop_WAF policy we created.
    
    - Select **Sessions and Logins** 
    - In the Authenticated URLs field enter ``/#/privacy-security/`` and press the add button and ``/#/wallet`` and press the add button.  Based on app exploration we can identify that these URIs should only be accessible after successful login.
    - Press the **Save** button in the upper right of the Policy Configuration. Then press the **Apply Policy** Button in the top right corner. 
    - Now press the link in the note message below titled **Learning and Blocking Settings Screen**

        .. image:: ../images/login_enforcement_16_1_2.png
    
    - On this screen add a checkmark in the **Alarm** and **Block** checkboxes.
    - Press **Save** below and **Apply Policy** in the top right.
    - These protections are now applied to A2, and also the Login Enforcement protections in A5.

        .. image:: ../images/Sessions-logins.png



#. Back on the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**. Click on the expand arrow next to **A4  XML External Entities**.  Previous signature protections already are helping to mitigate these other XML exploits.  Here are the steps to apply disallowing DTDs (Document Type Definitions).  

    - Navigate to **Security -> Application Security -> Content Profiles -> XML Profiles**.
    - Click the name of the default XML profile. (Typically we create a new profile, and we do not modify a default profile, but for simplicity and since we only have one application we will do so here)
    - Under Profile Properties, click the XML Firewall Configuration tab.
    - On the Defense Configuration list, click Advanced.
    - Clear the Allow DTDs check box.
    - Click the **Update** button.

        .. image:: ../images/dtds-steps.png

    - After the Update is completed, you will land back on XML Profiles list. Click the **Apply Policy** button in the upper right.
    - Now navigate to **Security -> Application Security -> Policy Building -> Learning and Blocking Settings**.
    - Expand the **Content Profiles** section.  Place a check in the  **Alarm** and the **Block** settings next to **XML data does not comply with format settings**.  

        .. image:: ../images/dtds-learning-blocking.png

    - Press **Save** at the upper right of the screen and **Apply Policy** in the top right corner.  
    - Browsing back to the OWASP Compliance dashboard, the A4 XML External Entities sections is still not at 100%. This is because of a known bug in the dashboard UI. Since we have enabled protections against this vulnerablity, we can use the ghostbuster icon to ignore the risk on the dashboard. This action will get the A4 catagory to 100%.
    - Click **Review & Update**, then **Save & Apply**.

        .. image:: ../images/dtds-in-xml.png


#. Navigate to **Security -> Application Security -> Security Policies -> Policies List** and select the Juice_Shop_WAF policy we created.  We now need to block **Disallowed File Types**.  

    - Expand HTTP Message Protection and Select File Types.
    - Here you can view/edit the pre-configured allowed and disallowed file types.  You can just view, and no changes need to made here.
    - To apply these blocks now go to **Security -> Application Security -> Policy Building -> Learning and Blocking Settings**.
    -  Expand the **File Types** section.  Place a check in the **Alarm** and **Block** boxes for **Illegal file type**. 
    - Press **Save** at the bottom of the screen and **Apply Policy** in the top right corner.  
    - If you want to view the dashboard again you will see the A5 catagory is now at 80%. Disallowed URLs would still need to be configured to get to 100% compliance for A5.

#. On the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**. Click on the expand arrow next to **A7 Cross-Site Scripting (XSS)**.  If you remember, A1 Injection included the protections against a lot of signatures and one of those catagories was XSS.  We are not using any HttpOnly cookies in this app so the last requirement to earn us 100% needed is applying the blocking of **Disallowed Meta Characters in Parameters**.

    - To view/edit the pre-configured allowed and disallowed Meta Characters go to **Security -> Application Security -> Parameters -> Character Sets -> Parameter Value**.  No changes need to made here.
    - To apply these blocks now go to **Security -> Application Security -> Policy Building -> Learning and Blocking Settings**.
    -  Expand the **Parameters Section**.  Place a check in the **Alarm** and **Block** boxes for both **Illegal meta character in parameter name** and **Illegal meta character in value**

        .. image:: ../images/Illegalmetachar.png

    - Press **Save** at the upper right of the screen and **Apply Policy** in the top right corner.  
    - If you want to view the dshboard again you will see the A7 catagory is now at 100%.

Conclusion
~~~~~~~~~~~

Now for our last step, once again go back to the OWASP Dashboard, path **Security -> Overview -> OWASP Compliance**.
You should now be mostly compliant in all categories that a WAF can control and reduce risk in those areas. The compliance topics of A6 and A9 a WAF cannot mitigate these risks. The user would need to go into each of these sections and mark accordingly how their environment is configured. While it is nice to see completion, the goal of the dashboard is not always to immediately reach 100% in all categories. The true value is providing visibility and measuring the security controls that are applyed to our applications. 
