Lab 1.3 - Viewing oAuth Analytics 
=================================

Reviewing OAuth Analytics
~~~~~~~~~~~~~~~~~~~~~~~~~

Go to the **Access** module > select **Overview** > **OAuth Reports** > **Server**

|
|


.. image:: images/apm-rpt1.png
 :width: 600 px

|
|


This report gives a summary of JWT token requests that are processed by the OAuth server.
Mouse over the information you see on the graph. Make a few more requests, come back to
this graph, and click on **Refresh** at the top right-hand side. 
|
|



.. image:: images/apm-rpt2.png
  :width: 600 px

|
|


In the next report, we will review the Client / Resource Server report. 


Click on **Overview** > **OAuth Reports** > **Client / Resource Server**

|
|


.. image:: images/apm-rpt3.png
  :width: 600 px
  
|
|



Access Policy Manager is acting as an OAuth client, so it logs token validations, along with
authorization failures. Mouse over the graph to see the different request metrics. If you don’t
have enough dataset, go back to Postman, and send a few more requests, with and without the
JWT token. Come back to this report and click **Refresh** in the top right corner.

Yay! You have completed Lab 1.