Parent Policy
------------------------------------

Create a Parent Policy

1. On the BIG-IP, navigate to Security >> Application Security >>
   Security Policies and click on the plus sign to create a new security
   policy.

.. image:: /_static/class2/image29.png

1. Click on advanced mode in the upper right corner of the screen.

2. Enter the following (leave the rest with the default settings):

   a. Policy Name: parent\_policy

   b. Policy Type: Parent

   c. Policy Template: Fundamental

.. image:: /_static/class2/image30.png

1. Click on **Create Policy**.

2. Click on the policy **‘parent\_policy’** that just created.

3. Click on **Inheritance Settings.**

4. Set the following inheritance options:

   a. Attack Signatures Sets – Optional

   b. Server Technology – Optional

   c. Data Guard – Mandatory

   d. HTTP Protocol Compliance – Mandatory

5. Click on **Save Changes** to update the parent policy.

.. image:: /_static/class2/image31.png

Examine the *Parent* Policy

1. On the BIG-IP, navigate to **Security >> Application Security >>
   Policy Building >> Learning and Blocking Settings**.

2. Ensure your current edited parent policy is set to ‘parent\_policy’.

3. Change general settings from basic to advanced view.

4. Expand the **HTP protocol compliance failed** section. Are the
   violations related to it enabled or disabled?

.. image:: /_static/class2/image32.png

1. Collapse the **HTTP protocol compliance** failed section.

2. Expand the **Attack Signature** section. Is the generic detection
   signature enabled or disabled?

.. image:: /_static/class2/image33.png

1. Navigate to **Security >> Application Security >> Data Guard**.

2. Can you enable Data Guard?

.. image:: /_static/class2/image34.png
