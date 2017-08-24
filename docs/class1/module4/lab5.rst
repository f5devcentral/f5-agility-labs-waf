Apply Bot Defense Logging Profile
---------------------------------

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

   |image51|
