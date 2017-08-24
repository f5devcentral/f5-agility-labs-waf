BOT Signatures
---------------

#. Navigate to **Security > DoS Protection > DoS Profiles**

   |image55|

#. **Click** on the ``hackazon_DoS`` profile and then the
   **Application Security** tab to configure the policy.

   |image56|

#. Select **Proactive Bot Defense** under the list of **Application
   Security** options.

#. In the **Application Security >> Proactive Bot Defense**
   section, click the **Edit** link for **Operation Mode** and
   then change the setting from **Always** to **During Attack** and
   click **Update** to complete the policy change.

   .. NOTE:: Ignore the DNS Resolver warning

   |image57|

#. Run cURL again: ``curl –k https://hackazon.f5demo.com``

   **The site should respond normally now every time.**

#. cURL is considered an **HTTP Library tool** and falls in **the Benign
   Category**.


.. NOTE:: Just how benign are HTTP library tools? cURL can easily be
   scripted in a variety of ways and can be used as a downloader to siphon
   off data. Remember the famous media defined “hacking tool” that Snowden
   used? wget? There are many use-cases where you simply do not want a tool
   interacting with your site.
