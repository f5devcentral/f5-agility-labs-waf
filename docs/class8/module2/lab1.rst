Login Page discovery
--------------------

In this exercise we will review the properties and elements of the Hackazon login page so that we can define it
as a login page in the ASM policy.  We will then configure **Brute Force Protection** for that login page.

Review login page parameters and responses.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  In Chrome, browse to the Hackazon home page. **http://hackazon.f5demo.com/**

  In the top right corner of the web page, select **Sign In**.

  Right click on the **Username** field and select **Inspect**.

  |image4|

  This will open the browser developer tools. The DOM will be displayed, and the username field will be selected.

  |image5|

  .. IMPORTANT::
    **Record** the **name** attribute of this field. We will need it later to configure the login page.

  This field is part of a form. Look just above the username field in the dev tools pane for the **<form** object.

  .. IMPORTANT::
    **Record** the **form action** URL. You will need this to configure the login page.

  In the web page pane, right click on the **Password** field and select **Inspect Element**.

  Now the password field will be selected in the dev tools pane.

  .. IMPORTANT::
    **Record** the **name** attribute of this field.

  In the dev tools pane, switch to the **Network** tab. Click the |image6| icon to clear any requests. Ensure the **Preserve Log** check box is checked.

  |image7|

  In the web page pane enter **"user"** for the username and **"12345"** for the password. Click **Sign In**.

  .. NOTE::
    These are invalid credentials, but we want to look at the response for a failed login.

  In the dev tools pane scroll to the top of the list and select the top request to **login**.

  |image8|

  In the Request Details pane look at the headers.

  |image9|

  .. IMPORTANT::
    **Record** the status code for a failed login.

  Click the |image10| icon to clear these requests.

  In the web page pane enter **"bob"** for the username and **"bob"** for the password. Click **Sign In**.

  .. NOTE::
    This is the correct password and we want to look at the response for a successful login.

  In the dev tools pane scroll to the top of the list and select the **POST** request to **login**.

  |image11|

  .. IMPORTANT::
    **Record** the status code for a failed login.
    **Record** the value of the Location response header.




.. |image4| image:: /_static/class8/credstuff/image4.png
.. |image5| image:: /_static/class8/credstuff/image5.png
.. |image6| image:: /_static/class8/credstuff/image6.png
.. |image7| image:: /_static/class8/credstuff/image7.png
.. |image8| image:: /_static/class8/credstuff/image8.png
.. |image9| image:: /_static/class8/credstuff/image9.png
.. |image10| image:: /_static/class8/credstuff/image6.png
.. |image11| image:: /_static/class8/credstuff/image11.png
.. |image12| image:: /_static/class8/credstuff/image12.png
.. |image13| image:: /_static/class8/credstuff/image13.png
.. |image14| image:: /_static/class8/credstuff/image14.png
.. |image15| image:: /_static/class8/credstuff/image15.png
.. |image16| image:: /_static/class8/credstuff/image16.png
.. |image17| image:: /_static/class8/credstuff/image17.png
.. |image18| image:: /_static/class8/credstuff/image18.png
.. |image19| image:: /_static/class8/credstuff/image19.png
.. |image20| image:: /_static/class8/credstuff/image20.png
.. |image21| image:: /_static/class8/credstuff/image21.png
.. |image22| image:: /_static/class8/credstuff/image22.png
.. |image23| image:: /_static/class8/credstuff/image23.png
.. |image24| image:: /_static/class8/credstuff/image24.png
.. |image25| image:: /_static/class8/credstuff/image25.png
.. |image26| image:: /_static/class8/credstuff/image26.png
.. |image27| image:: /_static/class8/credstuff/image27.png
.. |image28| image:: /_static/class8/credstuff/image28.png
.. |image29| image:: /_static/class8/credstuff/image29.png
.. |image30| image:: /_static/class8/credstuff/image30.png
.. |image31| image:: /_static/class8/credstuff/image31.png
.. |image32| image:: /_static/class8/credstuff/image32.png
.. |image33| image:: /_static/class8/credstuff/image33.png
.. |image34| image:: /_static/class8/credstuff/image34.png
