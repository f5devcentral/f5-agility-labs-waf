Exercise 3.1: Blocking Policy
----------------------------------------

Objective
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You will explore the blocking policy and settings.  The blocking policy used for this lab will focus on negative security using attack signatures.

.. IMPORTANT:: Remove the existing transparent policy from your virtual before proceeding. Your virtual should look like this

.. image:: images/image1.PNG
    :width: 600 px

Task 1 - Creating Blocking policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1.  Go to **Security > Application Security > Security Policies** and click the Plus sign.

2.  At the far right change the setting to Advanced

.. image:: images/image15_3_1.png
    :width: 600 px

Fill out the following -
  - Policy name - ``Blocking_Policy``
  - Description - ``leave blank``
  - Policy type -  ``Security``
  - Policy Template -  ``Rapid Deployment Policy``
  - Virtual Server -  ``webgoat.f5demo.com_https_vs (HTTPS)``
  - Learning Mode -  ``Manual``
  - Enforcement Mode -  ``Blocking``
  - Application Language -  ``Unicode (utf-8)``
  - Server Technologies - ``(leave blank)`` (we will cover this option in a later exercise)
  - Signature Staging -  ``Disable``  (in a production environment consider leaving this set at 7 days)
  - Policy is Case Sensitive -  ``Disabled``
  - Differentiate between HTTP/WS and HTTPS/WSS URLs -  ``Enabled``

.. image:: images/image1-1.png
    :width: 600 px

3.  Click **Create Policy**

4.  Go to **Security > Application Security > Policy Building > Learning and Blocking settings**

5.  Make sure ``Blocking_Policy`` is selected in the Current edited security policy.

6.  At the far right across from General Settings ensure Advanced is selected.

.. image:: images/image16_3_1.png
    :width: 600 px

7.  Click on **Blocking Settings**

.. image:: images/image1_3_1.png
    :width: 600 px

8.  Click the **Block** Check box at the top of to select all then click it again to clear Block from all entries.  Then click **Change**.

.. image:: images/image2_3_1.png
    :width: 600 px

9.  Under Policy Building Settings  expand the Attack Signatures options

.. image:: images/image2.PNG
    :width: 600 px

10.  Click on the **Change** button at the far right to bring up the **Select Policy Attack Signature sets** and choose to add both **High Accuracy signature sets and SQL Injection Signatures** then click **Change**.

.. image:: images/image9_3_1.png
    :width: 600 px
.. image:: images/image10_3_1.png
    :width: 600 px

.. NOTE:: For this lab Signature Staging has been disbaled.  In a production environment you should consider using staging to allow yourself mitigation time before new signatures are implemented.

11.  Ensure that the blocking checkbox has been unchecked for all signatures.

.. image:: images/image17_3_1.png
    :width: 600 px

12.  You will click Save and Apply Policy at this point.

.. image:: images/images11_3_1.png
    :width: 600 px

.. NOTE:: You will see that the policy will apply with errors.  This is because the Policy is set to blocking but we do not have any settings currently in blocking since we unchecked the blocking options.  At this point you will think this is counter intuitive.  Why would you set a policy in blocking and then not block anything?  This is to illustrate that you can begin building your policy in blocking mode from the start.  The policy will operate as if it were in transparent mode.  When you are ready to begin blocking traffic check the block option for that function(s).  At this point we will test the blocking policy, which is in blocking mode, but no functions are currently in blocking.

.. image:: images/image12_3_1.png
    :width: 600 px

Task 2 - Tuning policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. ATTENTION::  For this lab we will explore the settings for tuning the policy but will not change the settings.

1.  Go to **Security > Application Security > Policy Building > Learning and Blocking Settings**

2.  Under the **General Settings** you will see various settings for Enforcement, Learning Mode and Learning Speed.  For this lab the policy should be set to **Blocking with Manual Learning and a learning speed of fast.**

.. image:: images/image4_3_1.png
    :width: 600 px

.. NOTE:: Depending on the setting you choose for Learning Mode you may find additional options but don't save any changes.
.. image:: images/image5_3_1.png
    :width: 600 px

3.  Under Policy Building Process you will find there are settings for Loosen Policy and Tighten Policy.

Loosen Policy would be used when there have been changes to the application.  Policy Builder will identify legitmate traffic based on repeated behavior from a sufficient number of sources that you set.
Tighten Policy only applies when you are using automatic learning.  The policy builder will refine the policy until the number of security policy changes has been reached.
Track Site Changes only applies to automatic learning.  If enabled this setting allows Policy Builder to discover changes to a web application.  Policy builder logs the changes and temporarily loosens the policy to make suggestions and adjustments.

.. image:: images/image6_3_1.png
    :width: 600 px

4.  When you have made changes to this page make sure to always **Save and Apply the policy.**

.. image:: images/image7_3_1.png
    :width: 600 px
.. image:: images/image8_3_1.png
    :width: 600 px
