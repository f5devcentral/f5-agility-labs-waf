Mitigation
---------------------------------------------

1. Via **Firefox**, navigate to https://10.128.10.20/login.php and login
   (login/password : admin/password)

.. image:: /_static/class2/image74.png

1. Navigate to the **SQL Injection** tab from the left side menu

2. Enter **%' or 1='1** into the User ID: field and click **Submit**

    Instead of executing the SQLi, you are presented with the block
    page:

.. image:: /_static/class2/image75.tiff

1. You can also check using the other SQLi attack that dumped out user
   IDs and hashed passwords by entering the below into the User ID field
   and hitting **Submit**

**%' or 1=1 union select null, concat ( 0x0a, user\_id, 0x0a,
first\_name, 0x0a, last\_name, 0x0a, user, 0x0a, password) from users
#**

You are presented with the block page again:

.. image:: /_static/class2/image76.tiff

1. Via **Chrome**, navigate to to the BIG-IP GUI
   `**https://10.0.0.4** <https://10.0.0.4>`__ **or**
   `**https://bigip1.agility.f5.com** <https://bigip1.agility.f5.com>`__

2. Navigate to **Security** >> **Event Logs** >> **Applications >>
   Requests**

3. Highlight the row for one of the requests made to
   /vulnerabilities/sqli/ to view details on the request that was
   blocked including attack type of SQL-Injection

.. image:: /_static/class2/image77.tiff

1. Click on the box **All Details** to see the full details of the
   blocked request including the Support ID displayed in the rejected
   request page displayed in the browser

.. image:: /_static/class2/image78.tiff

Supplemental Lab 3 Info:

In the Desktop\\Lab3\\Additional Resources folder we exported a few
reports from AppScan against the DVWA site should you be interested in
reviewing. These reports are:

-  OWASP Top 10

-  Regulatory Compliance Report for HIPAA

-  Detailed Security Report
