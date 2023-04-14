Module 2: Deploying a development instance of Arcadia Finance
===================================================================

**Intro**
~~~~~~~~~

In this lab, we will cover the following:

- Deploying to F5 BIG-IP using AS3 and Postman
- Implementing WAAP policy improvements in BiG-IP Advanced WAF
- Implementing WAAP policy improvements from an imported OpenAPI Swagger Definition file

Objective
~~~~~~~~~~~~

You will use F5’s declarative API, known as AS3, for deploying your new application instance. In your production security policy, recall that there is no Swagger/OAS file being used. While you could manually upload an OAS file to an existing policy, that is not the strategy Arcadia’s management wants to rely on going forward. For this lab, we will deploy the application along with the security policy which will be configured based on the OpenAPI spec file that is ready for testing.


.. toctree::
   :maxdepth: 1
   :glob:

   lab*
   review