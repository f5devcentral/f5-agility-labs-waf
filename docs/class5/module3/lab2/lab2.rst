Lab 3.2: Protection from Parameter Exploits
-----------------------

F5 Advanced WAF includes DataSafe which can protect your web applications from credential theft by MITB malware. In this exercise you will configure DataSafe to protect the Webgoat login page from credential theft.

.. |lab3-01| image:: images/lab3-01.png
        :width: 800px
.. |lab3-02| image:: images/lab3-02.png
        :width: 800px
.. |lab3-03| image:: images/lab3-03.png
        :width: 800px
.. |lab3-04| image:: images/lab3-04.png
        :width: 800px
.. |lab3-05| image:: images/lab3-05.png
        :width: 800px
.. |lab3-06| image:: images/lab3-06.png
        :width: 800px
.. |lab3-07| image:: images/lab3-07.png
        :width: 800px
.. |lab3-08| image:: images/lab3-08.png
        :width: 800px
.. |lab3-09| image:: images/lab3-09.png
        :width: 800px
.. |lab3-10| image:: images/lab3-10.png
        :width: 800px




Task 1 - Create Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. Browse to the BIGIP GUI.

#. Navigate to **Security -> Application Security -> Parameters List** and click create. Create the username and password parameters as seen below

  'username' parameter
  |lab3-01|
  'account' parameter
  |lab3-02|

Task 2 - Modify Learning and Blocking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Navigate to **Security -> Application Security -> Policy Building -> Learning and Blocking Settings** and enable setting for 'illegal parameter value length' and 'illegal meta character in value' as seen below.

    |lab3-03|



Task 3 - Test Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open a new Firefox Private Browsing window and go to the to WebGoat login page at ``https://insecureapp1.f5.demo/WebGoat/login``

#. login as f5student

#. Your login should be blocked.

#. Examine the recent event logs

   |lab3-04|

#. Navigate to **Security -> Application Security -> Policy Building -> Traffic Learning**

#. Review the entry for 'illegal parameter value length'

  |lab3-05|

#. Click Accept Suggestion and the **Apply Policy**

#. Open a new Firefox Private Browsing window and go to the to WebGoat login page at ``https://insecureapp1.f5.demo/WebGoat/login``

#. login as f5student

#. Your login should be allowed.

#. Return to **Security -> Application Security -> Parameters List**

  |lab3-06|


#. Open a new Firefox Private Browsing window and go to the to WebGoat login page at ``https://insecureapp1.f5.demo/WebGoat/login``

#. login as f5student

#. Choose Injection Flaws -> SQL Injection from the menu on the left then chose page 9 from the top.

  |lab3-07|

#. Adjust settings as seen and click 'get account info'. You should see a list of accounts that start with 'John'.

  |lab3-08|

#. Return to **Security -> Application Security -> Parameters List** and remove the 'account' parameter from staging. Click Update then apply policy.

  |lab3-09|

#. Open a new Firefox Private Browsing window and go to the to WebGoat login page at ``https://insecureapp1.f5.demo/WebGoat/login``

#. login as f5student

#. Choose Injection Flaws -> SQL Injection from the menu on the left then chose page 9 from the top.

#. Adjust settings as seen and click 'get account info'. You should see a list of accounts that start with 'John'.

#. The attack should fail since you are enforcing metacharacters on your parameter. In this case the ' character is not allowed.

#. Review the logs

  |lab3-10|


This concludes Lab 3.2
