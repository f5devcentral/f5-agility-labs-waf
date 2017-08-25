Lab Environment
===============

F5 v13 VE
---------

F5’s latest version of the BIG-IP platform running as a virtual
appliance. The BIG-IP instance we are using today will be provisioned
for both Local Traffic Management as well as Web Application Firewall,
to allow us to detect and respond to various application attacks.

Kali Linux
----------

A Debian-based Linux distro designed for digital forensics and
penetration testing, and comes pre-loaded with many of the tools we will
be using in today’s lab. Reasons to give it a try:

-  Single user, root access by design

-  Network services disabled by default

-  Custom Linux Kernel

-  A *minimal* and *trusted* set of repositories

Other Tools
-----------

Hackazon
~~~~~~~~

Our vulnerable web app. Designed with the best of intentions, but with
more holes than a sieve.

GoldenEye
~~~~~~~~~

HTTP DoS test tool.

-  Attack Vector: HTTP Keep Alive + NoCache

SLOWHTTPTEST
~~~~~~~~~~~~

HTTP DoS test tool.

-  Attack Vector: Prolonging HTTP connections

-  Slowloris

-  Slowread

-  Slowpost

SQLMAP
~~~~~~

Automatic SQL injection and database takeover tool

METASPLOIT
~~~~~~~~~~

Penetration Testing Tool

Access Jumpbox and Browse Lab Resources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Use Remote Desktop to access jumpbox

2. Access BIG-IP GUI via chrome

   a. https://10.0.0.4

      i. username / password

         1. admin / 401elliottW!

   b. Examine virtual server configs

      |image0|

   c. Examine ASM policies

      |image1|

3. Open Putty session to Kali host

   a. username / password

      i. root / 401elliottW!

4. Open Putty session to Hackazon host

   a. username / password

      i. root / default
