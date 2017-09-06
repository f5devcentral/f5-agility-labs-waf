Demonstrate vulnerability
----------------------------------

1. Via **Firefox**, navigate to https://10.128.10.20/login.php and login
   (login/password : admin/password)

.. image:: /_static/class2/image52.png

1. Navigate to the **SQL Injection** tab from the left side menu

2. Enter **%' or 1='1** into the User ID: field and click **Submit**

.. image:: /_static/class2/image53.png

As you can see you have dumped the whole user table.

1. To see another vulnerability, enter the below into the User ID field
   and hit **Submit**:

**%' or 1=1 union select null, concat ( 0x0a, user\_id, 0x0a,
first\_name, 0x0a, last\_name, 0x0a, user, 0x0a, password) from users
#**

.. image:: /_static/class2/image54.png

With this query, you have now dumped out the entire user table, but this
time with first/last names, user IDs, along with their hashed passwords.
