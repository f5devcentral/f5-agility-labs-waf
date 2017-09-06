IP Reputation
-------------

#. Navigate to **Security > Application Security > IP Addresses > IP
   Address Intelligence** and click **Enabled**. For all categories
   **select Alarm**. Click on **Save** and then on **Apply Policy**.

   .. NOTE:: On the top right you should see that your IP Intelligence
      database has been updated at some point.

   .. image:: /_static/class1/image65.png
     :width: 6.50000in
     :height: 2.94306in

   .. NOTE:: In order to create traffic with malicious sources for the purposes of
      this lab we have created added additional configuration items for you.

   There is a Virtual Server (VS) called ``ip_rep_target_https_vs`` which
   has a SNAT pool predefined with 5 known malicious IP addresses.

   There is an iRule applied to that VS which then points the traffic to
   the VS you have been working on ``hackazon.f5demo.com_https_vs`` which has
   your ASM policy applied. This configuration will cause ASM to see the
   inbound traffic as having the malicious sources.

#. Please review the Virtual Server configuration for
   ``ip_rep_target_https_vs``. No changes are needed. Also, please
   review the iRule assigned under the VS Resource tab.

#. Open a new private browsing window in Firefox and use the bookmark
   for **IP Rep Lab** to browse the site. Click on one or two items
   until you get the block page.

   .. image:: /_static/class1/image66.png
     :width: 2.77339in
     :height: 1.28638in

#. Navigate to **Security > Event Logs > Application > Requests** and
   review the log entries. Since you configured IP Intelligence
   violations to alarm you will not need change the filter. Select the
   most recent entry and examine why the request is illegal. What IP
   address did the request come from?

   .. image:: /_static/class1/image68.png
     :width: 6.50000in
     :height: 2.41667in

   **Bonus:** You can browse to ``http://www.brightcloud.com/tools/url-ip-lookup.php``
   and look up the IP address in question for further information. There is also
   a tool to report IP addresses that have been incorrectly flagged.

   Further, you can use Putty on the Win7 box to access the BIG-IP via SSH
   (bookmarked as F5-WAF) and login with ``root`` / ``401elliottW!`` to run
   the ``iprep_lookup`` command, similar to:

   .. code-block:: console

      [root@bigip1:Active:Standalone] config # iprep_lookup 77.222.40.121
      opening database in /var/IpRep/F5IpRep.dat
      size of IP reputation database = 39492859
      iprep threats list for ip = 77.222.40.121 is:
      bit 7 - Phishing
      bit 8 - Proxy

#. Close the Firefox Private Browsing window.
