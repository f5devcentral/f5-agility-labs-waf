Create Bot Defense Logging Profile
----------------------------------

#. Open a new tab for the Configuration Utility and navigate to:
    **Security > Event Logs > Logging Profiles** then **click
   the plus icon**.

#. Enter a Profile Name ``bot-defense_allrequests``, select the
   checkbox for ``Bot Defense``.

#. Under the **Bot Defense** logging section, select the checkboxes
   for the following: ``Local Publisher``, ``Log Illegal Requests``, and
   ``Log Challenged Requests``.

#. Click **Finished**.

   .. NOTE:: You could have also modified the existing ``asm_allrequests``
      logging profile and added DoS logging definitions.

   |image50|
