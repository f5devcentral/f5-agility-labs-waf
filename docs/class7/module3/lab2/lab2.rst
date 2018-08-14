API L7 DoS attacks and TLS based fingerprinting
===============================================

.. toctree::
   :maxdepth: 1
   :glob:

In this module you will examine L7 DoS attacks against API, detection based on transaction rate per second per individual client OS or browser. Each client OS or browser have got fairly unique combination of supported ciphers, TLS extensions, compressions settings and other options exposed during TLS handshake. BIG-IP is capturing those options and producing fairly unique TLS fingerprint which can be used to identify bad actors with better granularity than traditional source based approach. The environment is already preconfigured for this use case.

Examine protected API environment
-----------------------------------

1. Go to Postman, expand **TLS_fingerprint** collection and rapidly run **List Departments** API call a few times - you should be able to get blocking response from BIG-IP

2. In the BIG-IP GUI navigate to Security -> Event Logs -> Application - Requests and examine the last log message; Note violation type and TLS fingerprint

 .. image:: images/image420.png

3. Open the browser and access **https://aapi.vlab.f5demo.com/department** - quickly update the page a few times to get the blocking response

4. In the BIG-IP GUI navigate to Security -> Event Logs -> Application - Requests and examine the last log message; Note the difference between TLS fingerprint from Postman and web browser
