Replication to child
-------------------------------------------------------

Create a new signature to represent a Zero-Day exploit

1. On the BIG-IP, navigate to **Security >> Options >> Application
   Security >> Attack Signatures >>Attack Signature List**.

.. image:: /_static/class2/image42.png

1. Click on **Create** to create a new signature

2. Enter the following:

   a. Name: Zero-Day

   b. Rule: content:”zero\_day\_sig”;

.. image:: /_static/class2/image43.png

1. Click on **Create**

2. Navigate to **Security >> Options >> Application Security >> Attack
   Signatures >>Attack Signature Sets**.

3. Click on **Create** to create a new signature set

4. Create and select the following:

   a. Name: Zero-Day-Set

   b. From the User-defined option select ‘Yes’

   c. Choose the signature we just created ‘Zero-Day’

.. image:: /_static/class2/image44.png

1. Click on **Create**.

Add the new signature set to the parent policy

1. On the BIG-IP, navigate to **Security >> Application Security >>
   Policy Building >> Learning and Blocking Settings**.

2. Ensure your current edited parent policy is set to the parent policy
   ‘parent\_policy’.

3. Expand the Attack Signatures section.

.. image:: /_static/class2/image45.png

1. Click the **Change** button in the attack signatures section.

2. Select the new signature set we created named ‘Zero-Day-Set’ and
   select **Change**.

.. image:: /_static/class2/image46.png

1. Click **Save** and **Apply Policy**.

.. image:: /_static/class2/image47.png

Examine Both *Child* Policies

1. On the BIG-IP, navigate to **Security >> Application Security >>
   Policy Building >> Learning and Blocking Settings**.

2. Ensure your current edited parent policy is set to one of the child
   policies ‘dvwa\_child’ or ‘f5demo\_child’.

3. Expand the Attack Signatures section.
   .. image:: /_static/class2/image48.png

   .. image:: /_static/class2/image49.png

1. Do you see the new signature set and signature applied?

2. Can you remove or modify the settings of the ‘Zero-Day-Set’?

3. What would be the steps to add this signature to both policies
   manually?

4. What if there were 10 policies that required this signature, how many
   actions would have been needed?
