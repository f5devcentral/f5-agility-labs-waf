Attacks mitigation
=========================================

In this module you will examine security controls allowing to protect against known attack patterns against API infrastructure. If you are using prebuilt objects proceed to `policy validation. <#validation>`__  Keep in mind, you will have to use objects with **prebuilt** suffix.

Examine unprotected API environment
-----------------------------------


1. Launch Postman application

2. Click Collections -> HR_API_Illegal -> Shellshock. Click **Headers** and examine the value for **User-Agent**

 .. image:: images/image409.png

This string is trying to exploit well known vulnerability CVE 2014-6271 also known as Shellshock

https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2014-6271

3. Make sure authorization type is set to **OAuth 2.0**. From the list of available tokens select **hruser** and click **Preview Request**. Then click **Send**

 .. image:: images/image390.png

4. The API call is able to come through along with remote command execution embedded into User-Agent string

Attacks protection configuration
-----------------------------------

1. In the BIG-IP GUI navigate to Security -> Options -> Application Security -> Attack Signatures -> Attack Signature Sets

2. Tap Create, define a name **API_Lab_SigSet2**, select all items in the **Available Systems** list and move it into **Assigned Systems**. Specify **Risk** as **Greater Than/Equal Medium** and tap Create

 .. image:: images/image410.png

3. Navigate to Security -> Application Security -> Policy Building -> Learning and Blocking Setting, expand **Attack Signatures** section and click **Change**

 .. image:: images/image411.png

4. Uncheck **Generic Detection Signatures** and check **API_Lab_SigSet**, then click Change, Save and Apply Policy

You can choose the prebuilt set or the set you just created.

 .. image:: images/image412.png

Validation
-----------------------------------

1. Go back to Postman and run **Shellshock** API call again - the API call should be blocked

2. In the BIG-IP GUI to Security -> Event Logs -> Application - Requests and examine the last log message

 .. image:: images/image413.png

API call is matching the signature and hence being blocked
