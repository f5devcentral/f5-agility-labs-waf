Class 2: Policies
============================

+------------------------------------------+
| +------------------------------------+   |
| | |image0|                           |   |
| +====================================+   |
| | Application Security Manager       |   |
| +------------------------------------+   |
| | F5 Technical Hands On Labs (241)   |   |
| +------------------------------------+   |
+------------------------------------------+

Table of Contents 2

Introduction 3

Lab Network Overview 4

ASM Logging Profile and Rapid Deployment 5

Overview of the BIG-IP Application Security Manager

The BIG-IP® Application Security Manager™ protects mission-critical
enterprise web infrastructure against application-layer attacks, and
monitors the protected web applications. The Application Security
Manager can prevent a variety of web application attacks, such as:

-  Manipulation of cookies or hidden fields

-  SQL injection attacks intended to expose confidential information or
       to corrupt content

-  Malicious exploitations of the application memory buffer to stop
       services, to get shell access, and to propagate worms

-  Unauthorized user access to authenticated accounts using cross-site
       request forgery (CSRF)

-  Unauthorized changes to server content using HTTP DELETE and PUT
       methods

-  Attempts aimed at causing the web application to be unavailable or to
       respond slowly to legitimate users

-  Layer 7 denial-of-service, brute force, and web scraping attacks

-  Unknown threats, also known as zero-day threats

    The system can automatically develop a security policy to protect
    against security threats, and you can configure additional
    protections and customize the system response to threats.

Summary of the Application Security Manager features

    The Application Security Manager includes the following features.

Integrated platform guaranteeing the delivery of secure application
traffic

    Built on F5 Networks’ TMOS® architecture, the ICSA-certified,
    positive-security Application Security Manager is fully integrated
    with the BIG-IP Local Traffic Manager™.

Automated security policy building

    Application Security Manager uses an auto-adaptive approach to
    application delivery security, where the security policy is
    automatically built and updated based on observed traffic patterns.
    A deployment wizard helps you create a security policy for your
    environment. Then the automated policy building feature, called the
    Real Traffic Policy Builder®, examines requests and responses, and
    populates the security policy with legitimate security policy
    elements, based on what it finds in the traffic.

Positive security model

The Application Security Manager creates a robust positive security
policy to completely protect web applications from targeted web
application layer threats, such as buffer overflows, SQL injection,
cross-site scripting, parameter tampering, cookie poisoning, and others.

Lab Network Overview

|image1|

Additional notes specific to the ASM 203 to help you follow along with
the guide:

+------------+------------------------------------------------------------+
| |image2|   | **Please use Chrome to Administer the BIG-IP ASM only.**   |
+============+============================================================+
| |image3|   | **Please use Firefox for lab exercises only.**             |
+------------+------------------------------------------------------------+
