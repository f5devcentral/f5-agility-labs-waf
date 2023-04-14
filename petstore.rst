BIG-IP Security: Enabling API Protection with AWAF and APM
==========================================================

Intro
-----

Welcome to F5's Agility Labs, 2023 edition!

By the end of this lab, you should be able to:

1. Use Postman to interact with F5 BIG-IP using F5’s declarative App Services API (AS3)

2. Leverage OpenAPI Swagger definition files to deploy and improve security

Module 1 - API Protection Using APM oAuth 
==========================================


PetStore has exposed their web application API to streamline the ability to check pet availability, ordering, and status of shipment. 
The web application is deployed in their production environment on a NGINX web server, that is frontended by a BIG-IP.


Objective - PetStore would like to secure these API endpoints by implementing authentication and authorization methods. 
Their requirement is to use an OAuth to authorize JSON web token for API requests, set a rate limit on how often API requests are received, and run a report on the number of API requests.  




In this lab, we will cover the following topics below.  

-	Explore how to protect API using F5 Access Policy Manager, and F5 Application Security Manager 
-	Set rate limiting on API requests 
-	Protect API from known attacks signatures


The lab is pre-staged with the Pet Store application in the petstore-prod partition.  


.. toctree::
   :maxdepth: 1
   :caption: Contents:
   :glob:

   labinfo/labinfo
   module*/module*
