Child Policy
-----------------------------------

Create a *Child* Policy for the DVWA site

1. On the BIG-IP, navigate to **Security >> Application Security >>
   Security Policies** and click on the plus sign to create a new
   security policy.

.. image:: /_static/class2/image35.png

1. Click on advanced mode in the upper right corner of the screen.

2. Enter the following (leave the rest with the default settings):

   a. Policy Name: dvwa\_child

   b. Policy Type: Security

   c. Policy Template: Fundamental

   d. Parent Policy: select **‘parent policy’**

   e. Virtual Server: dvwa\_vs

   f. Application Language: Unicode (utf-8)

      i.  Can you change the application language and encoding?

      ii. Why is this the case?

   g. Server Technologies: MySQL and PHP

.. image:: /_static/class2/image36.png

1. Click on **Create Policy**.

Create a *Child* Policy for the F5 Demo Site

1. On the BIG-IP, navigate to **Security >> Application Security >>
   Security Policies** and click on the plus sign to create a new
   security policy.

.. image:: /_static/class2/image37.png

1. Click on advanced mode in the upper right corner of the screen.

2. Enter the following (leave the rest with the default settings):

   a. Policy Name: f5demo\_child

   b. Policy Type: Security

   c. Policy Template: Fundamental

   d. Parent Policy: select **‘parent policy’**

   e. Virtual Server: http\_vs

.. image:: /_static/class2/image38.png

1. Click on **Create Policy**.

Examine Both *Child* Policies

1. On the BIG-IP, navigate to **Security >> Application Security >>
   Policy Building >> Learning and Blocking Settings**.

2. Ensure your current edited parent policy is set to one of the child
   policies ‘dvwa\_child’ or ‘f5demo\_child’.

3. Ensure general settings are set to advanced view.

4. Expand the **HTP protocol compliance failed** section. Are the
   violations related to it enabled or disabled?

.. image:: /_static/class2/image39.png

1. Collapse the **HTTP protocol compliance** failed section.

2. Expand the **Attack Signature** section. Is the generic detection
   signature enabled or disabled?

.. image:: /_static/class2/image40.png

1. Navigate to **Security >> Application Security >> Data Guard**.

2. Can you enable Data Guard?

.. image:: /_static/class2/image41.png
