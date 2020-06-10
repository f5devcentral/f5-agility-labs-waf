Lab 2 – Hacking the Juice Shop
------------------------------

Objective
~~~~~~~~~

- Demonstrate the vulnerabilities in the Juice Shop web application.

- Demonstrate a cross site scripting (XSS) vulnerability.

- Demonstrate a SQL injection vulnerability.

- Demonstrate a privilege escalation vulnerability.

- Demonstrate an unauthorized file access.

Task – Demonstrate a server side cross site scripting (XSS) vulnerability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Visit the About page so you can see that it hasn't been hacked yet by clicking on the hamburger menu in the top left corner of the page:

.. image:: /_static/class9/hamburger_menu.png

and then click on **About Us**.

.. image:: /_static/class9/aboutus_menu.png

You should see a bunch of lorem ipsum text and a slider of customer feedback entries retrieved from the database.

.. image:: /_static/class9/aboutus_page.png

We will insert our cross site scripting hack into the database via the Customer Feedback form. Click on the hamburger menu again and then click on **Customer Feedback**.

.. image:: /_static/class9/customer_feedback.png

In the comment area paste the following:

.. code-block:: none

    <<script>FUD</script>iframe allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&auto_play=true>

Then, choose any amount of stars for the rating and answer the math challenge and then click Submit.

.. image:: /_static/class9/xss_cust_feedback_form.png

Now head back over to the About page by clicking on the hamburger menu and then clicking on About. You should hear a jingle about the Juice Shop.

Task – Demonstrate a SQL injection vulnerability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Paste the following path in your browser's location bar after the FQDN of the Juice Shop:


.. code-block:: none
   
    /rest/products/search?q=qwert%27%29%29%20UNION%20SELECT%20id%2C%20email%2C%20password%2C%20%274%27%2C%20%275%27%2C%20%276%27%2C%20%277%27%2C%20%278%27%2C%20%279%27%20FROM%20Users--

The location bar should look something like (don't copy this since your FQDN will be different):

.. code-block:: none

    https://ba3eff45-2f23-49ab-8122-2e3bdc1ed9ad.access.udf.f5.com/rest/products/search?q=qwert%27%29%29%20UNION%20SELECT%20id%2C%20email%2C%20password%2C%20%274%27%2C%20%275%27%2C%20%276%27%2C%20%277%27%2C%20%278%27%2C%20%279%27%20FROM%20Users--

The result should be a list of all the users in the database including their hashed passwords.

.. image:: /_static/class9/juice_shop_users.png


Task - Demonstrate a privilege escalation vulnerability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use a rainbow lookup table to expose the admin user's password by navigating to https://crackstation.net/ and entering the hash


.. image:: /_static/class9/juice_shop_crackstation.png


Task - Demonstrate an unauthorized file access vulnerability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Navigate to /encryptionkeys to expose an unwanted directory listing

.. image:: /_static/class9/juice_shop_encryptionkeys.png

Click on the file ``premium.key`` and attempt to download it.

The files in this directory can be downloaded. A good WAF policy should block access to sensitive file types.