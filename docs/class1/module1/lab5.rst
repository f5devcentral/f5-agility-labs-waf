Logging
-------------------------------------------

#. In the Configuration Utility, navigate to:  **Security >
   Event Logs > Logging Profiles** then **click the plus icon**.

#. Enter a Profile Name ``asm_allrequests``, select the checkbox
   for ``Application Security``.

#. Change the **Configuration** dropdown to ``Advanced`` under
   the **Application Security** logging section, and then set
   the **Response Logging** dropdown to: ``For All Requests``.

#. Change the **Request Type** under **Storage Filter** to 
   ``All Requests``. Click **Finished**.

.. image:: /_static/class1/image14.png
   :width: 6.50000in
   :height: 5.44653in

**Question:** Would logging all requests and responses in a production
environment be a best practice?

* Apply Logging Profile

#. Under **Local Traffic > Virtual Servers**, click
   on ``hackazon.f5demo.com_https_vs``.

#. Click on **Policies** under the **Security** tab at the top of
   the ``hackazon.f5demo.com_https_vs`` details menu.

#. In the **Log Profile** drop down menu, select ``Enabled...``

#. Within the Available logging profiles menu,
   select ``asm_allrequests`` and then click the ``<<`` arrows to
   move the logging policy to the **Selected** profile.

#. Click on the **Update** button to apply the policy.

.. image:: /_static/class1/image17.png
   :width: 6.50000in
   :height: 5.24444in
