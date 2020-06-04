Lab 1 – Attempt to Hack the Juice Shop
--------------------------------------

Objective
~~~~~~~~~

- Close the Juice Shop tab or window.
- Restart the Juice Shop application.
- Load the Juice Shop application.
- Attempt the server side XSS hack.
- View the illegal request log entry.
- Attempt the SQL injection hack.
- View the illegal request log entry.
- Compare results of an unauthorized file access attempt.
- Search for log entry using a Support ID.
- View the illegal request log entry.

Task - Close the Juice Shop tab or window
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Make sure to close the tab or window that you have the Juice Shop running in to avoid any issues with cached content or metadata.

Task - Restart the Juice Shop Application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Juice Shop application must be restarted to reset the database. Log onto the Internal LAMP Server by navigating to the Systems column, clicking on the Access dropdown and then clicking on **WEB SHELL**

.. image:: /_static/class9/web_shell_internal_lamp.png

At the shell prompt, type the following commands to restart the Juice Shop application. The first command will list the running docker containers. Note the STATUS. The second command restarts the Juice Shop docker container (only the first 3 unique charcters of the container ID are required) and the third command will list the running container where you should see the STATUS listed as Up for a few seconds which confirms the application was restarted.

In the web shell run the command ``docker ps``. The output will look like the following:

.. code-block:: none

    CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                    NAMES
    b0b868b1af95        bkimminich/juice-shop   "docker-entrypoint.s…"   4 hours ago         Up 2 hours          0.0.0.0:3000->3000/tcp   reverent_raman
    
    
Run the command ``docker restart b0b``, but make sure to type the first 3 characters of your Juice Shop container ID. The output will be the first 3 characters of the container ID:

.. code-block:: none

    b0b


Run the command ``docker ps`` to ensure the container was restarted. Your web shell should look very similar to the following:

.. code-block:: none

    root@ip-10-1-1-5:~# docker ps
    CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                    NAMES
    b0b868b1af95        bkimminich/juice-shop   "docker-entrypoint.s…"   4 hours ago         Up 2 hours          0.0.0.0:3000->3000/tcp   reverent_raman
    root@ip-10-1-1-5:~# docker restart b0b
    b0b
    root@ip-10-1-1-5:~# docker ps
    CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                    NAMES
    b0b868b1af95        bkimminich/juice-shop   "docker-entrypoint.s…"   4 hours ago         Up 1 second         0.0.0.0:3000->3000/tcp   reverent_raman
    root@ip-10-1-1-5:~#


Task - Load the Juice Shop application.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After restarting the Juice Shop application you can go back to the UDF Deployment screen and open the newly started application by clicking on the Access link under the BIG-IP section and then clicking on Juice Shop.
 
Task - Try hacking the Juice Shop application again.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Go back to the Module 1 / Lab 3 page and run through the hacks. They should fail. Click `here <../module0/lab3.html>`_ to jump to that page and then click the browser back button to come back to this page to compare your results.

Task - Compare results of XSS hacking attempt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The attempt to injected the XSS hack via the feedback form should fail and the you should see something similar to this on the page:

.. image:: /_static/class9/block_xss.png

If you visit the Customer Feedback page you should NOT hear the jingle.

Task - View the Application Request Logs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Navigate to **Security -> Event Logs -> Application -> Requests** where you should see an illegal request for the URI ``/api/Feedbacks/``. Click on that request and explore details of the rejected request by clicking on the Violation listed and the Attack Type. Also, make sure to scroll to the bottom of the Decoded Request section to see the string that was entered in the form.

.. image:: /_static/class9/event_log_xss.png

Task - Compare results of SQL injection hacking attempt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The attempt to inject the malicious SQL query should fail and the you should see something similar to the following in your browser:

.. image:: /_static/class9/block_sql_injection.png

Task - View the Application Request Logs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Navigate to **Security -> Event Logs -> Application -> Requests** where you should see an illegal request for the URI ``/rest/products/search``. Click on that request and explore details of the rejected request by clicking on the Violation listed and the Attack Type. You can see the query at the top of the Decoded Request section.

.. image:: /_static/class9/log_sql_injection.png

Task - Compare results of an unauthorized file access attempt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The attempt to download the file in the ``/ftp`` directory fails with the following message:

.. image:: /_static/class9/support_id_file.png

Task - Search for log entry using a Support ID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Navigate to **Security -> Event Logs -> Application -> Requests** and then click on the ``Open Filter`` icon (beside Order by Date / Newest) and then enter the support ID shown on the blocked page in the Support ID field at the bottom of the filter window then click the ``Apply Filter`` button:

.. image:: /_static/class9/support_id.png

Task - View the Application Request Logs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the filter is applied you should only see one illegal request for the URI ``/ftp/package.json.bak``. Click on that request and explore details of the rejected request by clicking on the Violation listed and the Attack Type.

.. image:: /_static/class9/log_file_access.png