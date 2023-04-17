Module 2: AWAF Policy Template Creation on BIG-IP (secops engineer) 
===================================================================

**Intro**

As the security engineer, you are tasked with building a WAF policy template that will be used by the application teams. 

Since the policy is used by multiple teams, it will mostly contain negative security controls (signatures, ip reputation...) 

During the exercise, think which settings should be enabled and how changes to the template will be managed. 

Also, think about how you can test your policy since it's not going to be deployed by the security engineer. 

**In this lab, we will cover the following:**

- Creation of an AWAF base policy (lab1) 
- Creating a template from a base policy (lab2)
- Creating ASM Policies via Importing JSON Files (lab3)
- Deploying to a 'secops testing' environemnt (lab4) 

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
