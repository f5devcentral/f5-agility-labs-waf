CPM
---------------------------------------------

Centralized Policy Matching, sometimes referred to as Local Traffic
Policies, allow for granular traffic routing and policy application
based on a user-defined ruleset. In this section, we’ll explore some
common use cases as they relate to ASM.

Return to DVWA and click **Command Injection**, type 8.8.8.8, and click
**submit**.

.. image:: /_static/class2/image20.tiff

Now attempt a command injection attack by typing **;uname -a && whoami
&& cat /etc/passwd** and clicking **submit**. The request should be
blocked.

Now suppose for a moment that the URI /vulnerabilities/exec/ represented
a honeypot that you didn’t want to apply ASM protections to, but wanted
to ensure that the rest of the URIs in the application were protected.
We can use a local traffic policy to make this adjustment.

Return to your BIG-IP management interface in **Chrome**. Go to **Local
Traffic > Policies > Create**. Name the policy dvwa\_cpm and click
**create policy**.

.. image:: /_static/class2/image21.tiff

Click **create** to add a rule.

Name the new rule **disable\_asm**

Click the **+** next to “Match all of the following conditions:” and
select “\ **HTTP URI**\ ” from the first dropdown, “\ **path**\ ” from
the second, “\ **begins with**\ ” from the third “\ **any of**\ ” from
the fourth, and add “\ **/vulnerabilities/exec**\ ” to the list.

Click the + next to “Do the following when traffic is matched:” and
select “\ **Disable**\ ” from the first dropdown, then **asm** from the
second.

The result should look like the following:

.. image:: /_static/class2/image22.tiff

Click **save** then click **create**.

Name the new rule **enable\_asm**

Click the plus next to “Do the following when traffic is matched:” and
select “\ **Enable**\ ” then “\ **ASM”**, then
“\ **lab-rapid-deployment**\ ”.

The result should look like the following:

.. image:: /_static/class2/image23.tiff

Click **save** then select the new policy and click **Publish** on the
next screen.

We’ve just created a policy that will disable ASM for the URLs we’ve
listed but enable it for all other traffic.

You should now have 2 published policies like below:

.. image:: /_static/class2/image24.tiff

The **asm\_auto\_l7\_policy\_\_dvwa\_vs** policy was built automatically
by the policy creation dialog when you created the
“\ **lab-rapid-deployment**\ ” policy. It contains one rule that simply
applies that policy to all traffic. Feel free to examine it in detail if
you wish.

To apply the policy, go to **Local Traffic >> Virtual Servers >> Virtual
Server** List then click **dvwa\_vs**.

Click the resources tab then manage next to Policies.

Remove the automatically created policy and add the dvwa\_cpm policy as
follows:

.. image:: /_static/class2/image25.tiff

Click **Finished**.

Return to Firefox and click on **Command Injection** in DVWA.

Launch the command injection attack again by typing **;uname -a &&
whoami && cat /etc/passwd** and clicking **submit**.

The request should be allowed:

.. image:: /_static/class2/image26.tiff

Return to the SQL Injection page in DVWA and ensure that the attack is
still blocked by typing” **‘ OR 1=1#**

You should see another block page:

.. image:: /_static/class2/image27.tiff

We’ve just created a basic local traffic policy to control the
application of ASM policies, but this is just a small sampling of the
capabilities provided by this feature. You can apply policies based on
various other criteria including (but not limited to) Geolocation, CPU
load, HTTP header contents, and HTTP Referrers.
