Parameters enforcement in API calls
=========================================

In this module you will examine security enforcement controls in regards to parameter values of API. If you are using prebuilt objects proceed to `policy validation. <#validation>`__  Keep in mind, you will have to use objects with **prebuilt** suffix.


Examine unprotected API environment
-----------------------------------

1. Launch Postman application

2. Click Collections -> HR_API_Illegal -> Parameter Length&Security. Click **Body** and examine the payload of API POST call

3. Make sure authorization type is set to **OAuth 2.0**. From the list of available tokens select **hruser** and click **Preview Request**. Then click **Send**

 .. image:: images/image390.png

4. Examine the output

5. Navigate to BIG-IP GUI (Security -> Event Logs -> Application -> Requests and clear the filter for illegal requests

 .. image:: images/image402.png

6. Examine the log entry from the last API call. Notice, all parameter values are stored as a plain text

The goal of this exercise is to keep the value of parameter "salary" confidential and enforce middle_initial parameter to one symbol length

Parameters enforcement configuration
-------------------------------------

1. Navigate to to Security -> Application Security -> Parameters -> Parameters List and delete **_Viewstate** parameter

2. Create parameter **middle_initial**, uncheck **Perform Staging** and define the value for **Maximum Length** as **1**, then click Create

 .. image:: images/image403.png

3. Create parameter **salary**, uncheck **Perform Staging** and check **Sensitive Parameter**, then click Create

 .. image:: images/image404.png

4. Navigate to Security -> Application Security -> Policy Building -> Learning and Blocking Settings and expand **Parameters** section

5. Set checkboxes against Alarm and Block for **Illegal parameter value length** violation, then click Save and Apply Policy

 .. image:: images/image407.png

Validation
-----------------------------------

1. Go back to Postman and run **Parameter Length&Security** again - this API call should be blocked

2. In the BIG-IP GUI to Security -> Event Logs -> Application - Requests and examine the last log message

 .. image:: images/image405.png

Note, the parameter's value for "salary" should be masked:

 .. image:: images/image406.png

3. Go back to Postman, expand **body** section of **Parameter Length&Security** and modify **middle_initial** parameter value to **B**, then click Save and Send - API call should go through

 .. image:: images/image408.png

4.  In the BIG-IP GUI go to Security -> Event Logs -> Application - Requests clear the illegal filter and examine the request.  Is Salary still protected?
