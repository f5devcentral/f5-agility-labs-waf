Module – Threat Campaigns
=========================

Attackers are constantly looking for ways to exploit the latest vulnerabilities and/or new ways to exploit old vulnerabilities.
F5's Threat Research team is constantly monitoring malicious activity around the globe and creating signatures specific to these exploits.
These Threat Campaign signatures are based on current "in-the-wild" attacks.  Threat Campaign signatures
contain contextual information about the nature and purpose of the attack.

As an example, a normal WAF signature might tell you that SQL injection was attempted.
A Threat Campaign signature will tell you that a known threat actor used a specific exploit of the latest Apache Struts vulnerability in an attempt
to deploy ransomware for cryptomining software.

.. WARNING::
	To ensure consistent behavior with the lab guide, **all lab exercises should be through the Chrome browser** on the
	Windows Jumphost.
  

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
