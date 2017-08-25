Class 3: Counter Measures
###############################################

.. toctree::
   :hidden:
   :numbered:
   :maxdepth: 2
   :glob:

   module*/module*

In this session we will be exploring some common application attacks
and the tools at our disposal to respond to them.

We will begin by submitting various attacks against an unprotected web
resource to examine their effectiveness. Then use the tools provided by
BIG-IP to identify the attacks and protect the application.

* Lab Environment

#. F5 v13 VE

   F5’s latest version of the BIG-IP platform running as a virtual
   appliance. The BIG-IP instance we are using today will be provisioned
   for both Local Traffic Management as well as Web Application Firewall,
   to allow us to detect and respond to various application attacks.

#. Kali Linux

   A Debian-based Linux distro designed for digital forensics and
   penetration testing, and comes pre-loaded with many of the tools we will
   be using in today’s lab. Reasons to give it a try:

   - Single user, root access by design

   - Network services disabled by default

   - Custom Linux Kernel

   - A *minimal* and *trusted* set of repositories

#. Hackazon

   Our vulnerable web app. Designed with the best of intentions, but with more holes than a sieve.

#. GoldenEye

   HTTP DoS test tool.

   - Attack Vector: HTTP Keep Alive + NoCache

#. SLOWHTTPTEST

   HTTP DoS test tool.

   - Attack Vector: Prolonging HTTP connections

   - Slowloris

   - Slowread

   - Slowpost

#. SQLMAP

   Automatic SQL injection and database takeover tool

#. METASPLOIT

   Penetration Testing Tool

* Accessing Lab Environment

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

.. |image0| image:: /_static/class3/image2.png
   :width: 4.70347in
   :height: 2.00000in
.. |image1| image:: /_static/class3/image3.png
   :width: 4.70139in
   :height: 2.26042in
.. |image2| image:: /_static/class3/image4.png
   :width: 6.23681in
   :height: 1.78611in
.. |image3| image:: /_static/class3/image5.png
   :width: 6.23681in
   :height: 1.70833in
.. |image4| image:: /_static/class3/image6.png
   :width: 6.19514in
   :height: 1.70833in
.. |image5| image:: /_static/class3/image7.png
   :width: 5.62431in
   :height: 4.35764in
.. |image6| image:: /_static/class3/image8.png
   :width: 5.14097in
   :height: 2.30417in
.. |image7| image:: /_static/class3/image9.png
   :width: 5.25208in
   :height: 2.00000in
.. |image8| image:: /_static/class3/image10.png
   :width: 5.30000in
   :height: 1.63472in
.. |image9| image:: /_static/class3/image11.png
   :width: 4.79722in
   :height: 2.35069in
.. |image10| image:: /_static/class3/image12.png
   :width: 4.74028in
   :height: 3.74583in
.. |image11| image:: /_static/class3/image13.png
   :width: 5.30000in
   :height: 1.84246in
.. |image12| image:: /_static/class3/image14.png
   :width: 4.62609in
   :height: 3.75390in
.. |image13| image:: /_static/class3/image15.png
   :width: 5.80208in
   :height: 3.05208in
.. |image14| image:: /_static/class3/image16.png
   :width: 6.23681in
   :height: 3.04097in
.. |image15| image:: /_static/class3/image17.png
   :width: 6.06458in
   :height: 3.50408in
.. |image16| image:: /_static/class3/image18.png
   :width: 4.96458in
   :height: 2.57361in
.. |image17| image:: /_static/class3/image19.png
   :width: 4.95625in
   :height: 2.73819in
.. |image18| image:: /_static/class3/image20.png
   :width: 5.34167in
   :height: 3.23542in
.. |image19| image:: /_static/class3/image21.png
   :width: 6.37222in
   :height: 3.59097in
.. |image20| image:: /_static/class3/image22.png
   :width: 5.55462in
   :height: 3.00870in
.. |image21| image:: /_static/class3/image23.png
   :width: 5.56458in
   :height: 3.19097in
.. |image22| image:: /_static/class3/image24.png
   :width: 6.52986in
   :height: 5.79722in
