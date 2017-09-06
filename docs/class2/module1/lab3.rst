SQL-Injection
---------------------------------

Navigate to **Security >> Application Security >> Active Security
Polices** page and ensure **lab-rapid-deployment** is selected.

Scroll down and click **View Learning and Blocking Settings**:

.. image:: /_static/class2/image15.tiff

On the next screen, change the enforcement mode to **Blocking** and
click **save**, then click **Apply Policy**:

.. image:: /_static/class2/image16.tiff

Now, run the SQL injection attack again. The request should now be
blocked:

.. image:: /_static/class2/image17.tiff

This blocking page can be customized to fit your organization’s needs.
In practice, this would often include contact information for a helpdesk
or perhaps a form to open a ticket to review the event. The support ID
uniquely identifies the offending request in the ASM database so it can
be used to lookup all of data associated with the request as well as
ASM’s response to it.

To lookup the event by the support ID, copy the support ID to your
clipboard and go back to **Security > Event Logs > Application >
Requests. Click the Magnifying Glass** in the upper left corner, **paste
the Support ID** in the **Support ID box**, and click **Apply Filter:**

.. image:: /_static/class2/image18.tiff

You should have been taken to the alert tied directly to the SQL
injection attack you just launched:

.. image:: /_static/class2/image19.tiff

This is a useful way to get policy tuning feedback from the users of
your application.
