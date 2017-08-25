Generate Traffic
------------------------

To begin, re-enable the “lab-rapid-deployment” policy you created in lab
1. Go to **Local Traffic > Virtual Servers > Virtual Server List >
dvwa\_vs**, click on the **security tab**, and select **policies**.
Select **Enabled** from the dropdown next to **Application Security
Policy**, and ensure **lab-rapid-deployment** is selected like below:

.. image:: /_static/class2/image77.tiff

Click **Update**.

Go to **Security > Application Security > Security Policies** and select
**lab-rapid-deployment**.

Scroll down to Enforcement Mode and click “\ **View Learning and
Blocking Settings**\ ”:

.. image:: /_static/class2/image78.tiff

Select “Transparent” from the dropdown list, click **save**, then click
**Apply Policy**.

.. image:: /_static/class2/image79.tiff

This will make it easier for us to generate numerous ASM violations to
populate the reports.

Open putty and login to the DoSServer with the username **root** and the
same password we’ve used throughout the lab.

Type the command **w3af\_console -s ./dvwa\_script.w3af** and hit enter:

.. image:: /_static/class2/image80.tiff

You’ve just used **w3af** (a web app vulnerability scanner) to launch
multiple preconfigured vulnerability scans against DVWA which will
produce a number of violations to examine in Part 2.
