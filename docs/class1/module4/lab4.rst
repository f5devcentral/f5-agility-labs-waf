Logging
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

   .. image:: /_static/class1/image77.png
      :width: 6.50000in
      :height: 5.05278in

#. Under **Local Traffic > Virtual Servers**, click
   on ``hackazon.f5demo.com_https_vs``.

#. Click on **Policies** under the **Security** tab at the top

#. Within the Available logging profiles menu,
   select ``bot-defense_allrequests`` and then click
   the ``<<`` arrows to move the logging policy to
   the ``Selected`` profile.

#. Click on the **Update** button to apply the policy.

   .. NOTE:: You can associate multiple logging profiles with a given
      virtual server. F5 allows for an incredible amount of logging
      flexibility. Most commonly you would have DoS, Bot Defense and ASM
      Security Policy events logged to a centralized SIEM platform, but
      there may be additional logging requirements such as a web team that
      would be interested in Bot Defense logs solely, while the SIEM
      continues to receive the union of DoS, Bot Defense and ASM Security
      Policy events.

.. image:: /_static/class1/image79.png
   :width: 6.50000in
   :height: 4.74375in
