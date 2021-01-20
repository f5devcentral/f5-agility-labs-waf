Lab 3.2: Apply WAF suggestions for trusted traffic
==================================================

.. _lab2:

3.2.1 Reviewing policy suggestions in the GIT repo  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The pipeline performs the following steps:

1. sends trusted traffic 

2. check if trusted traffic is blocked 

3. if trusted traffic is blocked, use the BIGIP API to get policy suggestions (from policy builder)

4. pushes the updated policy declaration with the new suggestions to a new git branch (dev)

3.2.2 Explore the updated policy JSON
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In GitLab navigate to :guilabel:`Repository` -> :guilabel:`Branches` and click on **dev**

.. image:: images/dev_branch.png

Click on  :guilabel:`Suggestions` folder and finally click on :guilabel:`new_waf_policy.json`

.. image:: images/suggestions.png

Explore the policy and pay attention to the **modifications** section. It should contain a few suggested changes to allow  Trusted traffic:

.. code-block:: json

    {
      "entityChanges": {
        "type": "explicit"
      },
      "entity": {
        "name": "bak"
      },
      "entityKind": "tm:asm:policies:filetypes:filetypestate",
      "action": "delete",
      "description": "Delete Disallowed File Type"
    }

.. code-block:: json

    {
      "entityChanges": {
        "allowedResponseCodes": [
          403
        ]
      },
      "entity": {},
      "entityKind": "tm:asm:policies:general:generalstate",
      "action": "update-append",
      "description": "Add 403 to Allowed Response Codes."
    }

.. note:: For the purposes of this lab, in order to avoid copy/paste errors, we have the script configured to build an entire new policy definition file rather than copy and paste just the modifications section

3.2.3 Update original WAF Policy JSON
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Click on :guilabel:`Copy file contents` button for new_waf_policy.json content and navigate back to root folder of the repo:

On the root folder of the repo open `waf_policy.json` file for editing and perform `CTRL-A/CTRL-V` to paste the content of `new_waf_policy.json` and overwrite the original policy file:

.. note:: Depending on Web Browser type, it is possible that during copy/paste `new_waf_policy.json` is "minified" i.e. you see a single line instead of a multi-line structured file. This format **does not** affect the JSON structure but can be "prettified" to be more "human-readable" using one of many available tools, for example |Beautifier|

    .. |Beautifier| raw:: html

            <a href="https://www.csvjson.com/json_beautifier" target="_blank">JSON Beautifier</a>

Click on :guilabel:`Commit changes` radio button

.. image:: images/commit.png

3.2.4 Merge dev to master and run staging CI/CD pipeline
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a new merge request by clicking on :guilabel:`Create merge request` Then scroll down to the botton of the page and click :guilabel:`Submit merge request`

.. image:: images/submit_merge_request.png

.. note: Normally App owner would approve or close a merge request based on the nature of the change, number of changes etc.

Once merge request is submitted, click on :guilabel:`Merge` radio button to synchronize dev and master branches and trigger a Staging Pipeline.
You can click on Pipeline # to get to the status page of that pipeline:

.. image:: images/merge.png


3.2.5 Pipeline progress
~~~~~~~~~~~~~~~~~~~~~~~

Watch the pipeline as it progresses through its stages. You can see the output of individual stage by clicking on corresponding Job in the pipeline.

It is expected that the pipeline will succeed and *Staging Juice-Shop App* will be deployed with corresponding WAF Policy attached.


.. image:: images/staging_passed.png


3.2.6 OPTIONAL: Test WAF Policy by manually sending trusted and then malicious traffic 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

With automated WAF Policy testing built into the pipeline there is no need to run any manual testing, 
however in this lab you can still test WAF policy blocking by running the following commands:
in the client linux terminal: 

    .. code-block:: console

        curl http://10.1.10.150/ftp/packages.json -v
        curl http://10.1.10.150/ftp/errors.yml -v
        curl http://10.1.10.150/ftp/security_report.json.bak -v


Since we applied an updated WAF Policy, it now allows trusted traffic to pass through. 

Now we should ensure that malicious traffic is blocked by WAF by running a malicious_traffic

.. note:: The pipeline uses 4 different requests that simulate cross-site scripting, access to FTP directory, login and password "guessing" attempts. This is just an example. In real customer environment these tests will be much more comprehensive and may include a 3rd party software designed for penetration testing.

    .. code-block:: console
    
        curl "http://10.1.10.150/api/Products/1" -H "Content-Type:application/json" --data-binary '{"description":"<script>alert(\"XSS3\")</script>"}'
        curl "http://10.1.10.150/ftp/package.json.bak%2500.md"
        curl "http://10.1.10.150/index.php?username=1'%20or%20'1'%20=%20'1&password=1'%20or%20'1'%20=%20'1"
        curl "http://10.1.10.150/rest/user/change-password?current=abcde&new=slurmCl4ssic&repeat=slurmCl4ssic"

At this point WAF Policy appears to be allowing trusted traffic while blocking malicious requests. 
Pipeline jobs reported the same result so it's time to test the connectivity to **staging** Juice-Shop App

3.2.7 Staging Juice-Shop App
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Upon successful pipeline completion you can access Juice-Shop App by selecting :guilabel:`firefox` --> :guilabel:`favorites` --> :guilabel:`WAF-342` --> :guilabel:`Staging` --> :guilabel:`OWASP juice shop`

.. image:: images/juiceshop_staging.png

Pipeline Summary
~~~~~~~~~~~~~~~~

Demonstrated pipeline uses new AWAF capabilities to deploy a base WAF Policy, 
Test the policy against Trusted Traffic and Malicious requests. 
Furthermore, WAF Policy was updated to allow certain requests to pass, as an outcome of an automated policy update following the export of Policy Suggestions from AWAF.

* Deploy WAF Policy
* Test and update policy as necessary
* Repeat

What's Next?

:doc:`Deploy Juice-Shop App to Production <lab3>`
