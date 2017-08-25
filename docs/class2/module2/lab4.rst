Lab Cleanup
--------------------
Remove Existing Security Policies from VS for future Labs

1. On the BIG-IP, navigate to **Local Traffic >> Virtual Servers >>
   Virtual Server List.**

.. image:: /_static/class2/image50.png

1. Select the VS **dvwa\_vs** and select **Security >> Security
   Policies.**

.. image:: /_static/class2/image51.png

1. In the Application Security Policy section change Enabled to
   **Disabled** and then click the **Update** button to apply the
   change. Notice the Policy name is now gone.

.. image:: /_static/class2/image52.png

1. Using the same procedure, select the VS **http\_vs** and disable the
   application security policy as well.

.. image:: /_static/class2/image53.png
