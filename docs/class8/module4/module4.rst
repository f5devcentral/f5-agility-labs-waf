Module – Bot Detection and Mitigation
=====================================

More than half of the traffic on the Internet is automated, or bot, traffic. About a third of this automated/bot traffic is malicious.
Bots are capable of various types of activity including web scraping, vulnerability scanning, credential stuffing, DoS attacks, and much more.
`OWASP has a project <https://www.owasp.org/index.php/OWASP_Automated_Threats_to_Web_Applications>`__ dedicated to these automated threats.

In protecting web applications from bot traffic it is important to consider that what may be malicious to one website may be benign to another.
For example, a airlines may want and even encourage web scraping of their flight prices so that they can be sold through third parties.
Whereas, a site that is hosting some specific intellectual property may consider web scraping very malicious.

In this lab we will configure and review the new **Unified Bot Defense** in 14.1. The name Unified Bot Defense signifies the unification
and enhancement of bot protections from disparate places in the configuration.  Bot Signatures and Proactive Bot Defense were taken from the
Layer7 DoS Profiles and Web Scraping was taken from the WAF profiles and combined with significant enhancements to create **Unified Bot Defense**.

.. WARNING::
	To ensure consistent behavior with the lab guide, **all lab exercises should be through the Chrome browser** on the
	Windows Jumphost.

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
