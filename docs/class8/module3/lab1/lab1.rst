API L7 DoS attacks and TPS based protection
===========================================

.. toctree::
   :maxdepth: 1
   :glob:

In this module you will examine L7 DoS attacks against API, detection and mitigation based on the transaction rate per second per individual source.

DoS profile configuration
-----------------------------------

1. In the BIG-IP GUI navigate to Security -> DoS Protection -> DoS Profile and click Create; Define the name **API_DoS** and click Finished

2. Click on just created DoS profile and go to **Application Security** tab; click **Edit**,  set the checkbox for enabled on **Application Security** and examine configuration options

3. Proceed to **TPS-Based Detection**, make sure it is enabled and set mitigation criteria **By Source IP**: **reached at least** value to **2** and **absolute threshold TPS reached** to **3** tps, then click Update

 .. image:: images/image414.png

4. Navigate to Local Traffic -> Virtual Servers -> **api.vlab.f5demo.com** -> Security -> Policies and enable DoS Protection Profile; choose just configured **API_DOS** profile from the dropdown menu

 .. image:: images/image415.png

Examine protected API environment
-----------------------------------

1. Go to Postman, expand **HR_API_DoS** collection and click on **DoS** API call

2. Make sure authorization type is set to **OAuth 2.0**. From the list of available tokens select **hruser** and click **Preview Request**. Then click **Send**. Make sure you are getting expected response and click **Save**

 .. image:: images/image416.png

3. Click **Runner** in the Postman

 .. image:: images/image417.png

4. Click on **HR_API_DoS** collection, select the **Environment** - API Protection Lab, set Iterations to **500**, Log Responses set to **For no requests** and click Run

 .. image:: images/image418.png

5. After short period of time Postman Runner should report failing transactions (it may not and gracefully handle the rate limiting, proceed to check logs in next steps anyway)

 .. image:: images/image419.png

6. In the BIG-IP GUI navigate to Security -> Event Logs -> DoS -> Application Events and examine messages in the logs
