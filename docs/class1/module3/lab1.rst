Parameter Enforcement
---------------------

#. Open **Security > Application Security > Parameters > Parameters List.**
   You will see that the wildcard parameter ``*`` is still in staging:

   |image28|

#. Check the box next to ``*`` and then click **Enforce**, Accept the
   browser popup confirmation, and then **Apply Policy**.

   |image29|

#. Open a new private browsing window in Firefox and go to
   ``https://hackazon.f5demo.com`` Click **Sign-In** on the top right and
   use the same information from Step 15 in Lab 2 to login. You should
   receive the block page at this point. Close the Firefox window and
   return to the BIG-IP Administrative Interface.

#. Go to **Local Traffic > Profiles > Services > HTTP** and click **Create**.

   |image30|

#. In the new profile complete the following:

   -  Name: ``hackazon_http_profile``

   -  Check ``Accept XFF``

   Click **Finished**.

#. Go to **Local Traffic > Virtual Servers** and click on
   ``hackazon.f5demo.com_https_vs`` and change the HTTP Profile to
   ``hackazon_http_profile`` and click Update.

   |image31|

#. In your Security Policy, **Security > Application Security >
   Policy > Policy Properties** adjust the view from **Basic** to
   **Advanced**

#. Check the box next to **Trust XFF Header** (Navigate to Security ->
   Application Security -> Policy -> Policy Properties.

   |image32|

   |image33|

   .. NOTE:: Keep in mind that for XFF to work correctly it must be set in both
      the ASM policy and the HTTP profile. This may seem redundant however the
      HTTP profile occurs earlier in the order of operations than the ASM
      policy. The HTTP profile is simply adding the header whereas the setting
      in ASM is to trust that header. What would be an example of a situation
      where you might need to trust a 3\ :sup:`rd` part XFF header (set before
      the BIG-IP)?
