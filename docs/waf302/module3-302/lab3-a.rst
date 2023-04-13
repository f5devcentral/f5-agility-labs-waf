Lab 3.3: Deploy Juice-shop Web App to Production ENV and run DAST
=================================================================


3.3.1 Deploy Juice-Shop App to Production
-----------------------------------------

Production deployment is triggered by creating a Tag. 
This is a common development practice that allows tagging and simultaneous release/delivery of the App code into Production environment.
You can read a bit more about deployment strategies at |dev.to| or similar websites

**Why do we use tags?**

* Useful for marking deployments and releases
* Annotated tags are an unchangeable part of Git history
* Soft/lightweight tags can be set and removed at will
* Many projects combine an annotated release tag with a stable branch
* Consider setting deployment/release tags automatically

More on tagging at |git|

.. |git| raw:: html

            <a href="https://git-scm.com/book/en/v2/Git-Basics-Tagging" target="_blank">Git Basics - Tagging</a>


.. |dev.to| raw:: html

            <a href="https://dev.to/mostlyjason/intro-to-deployment-strategies-blue-green-canary-and-more-3a3" target="_blank">Intro to deployment strategies</a>

3.3.2 Tag the repo in gitlab
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:guilabel:`client RDP` -> :guilabel:`firefox` -> :guilabel:`waf-301` -> :guilabel:`GitLab`

Click on :guilabel:`waflabs / waf_cicd` Project

Navigate to :guilabel:`Repository` -> :guilabel:`Tags` and click on :guilabel:`New tag`

.. image:: images/tags.png

Fill out a **Tag name** field and click on :guilabel:`Create tag`. You can use **prod-v1.0** as suggested Tag name.

.. image:: images/new_tag.png


3.3.3 Pipeline progress
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Navigate to :guilabel:`CI / CD` -> :guilabel:`Pipelines` and click on the pipeline that is currently running and has a **Commit** message set to a Tag name created in previous step

3.3.4 Connect to Production Juice-Shop App
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Upon successful pipeline completion you can access Juice-Shop App by selecting :guilabel:`firefox` --> :guilabel:`favorites` --> :guilabel:`WAF-301` --> :guilabel:`Production` --> :guilabel:`OWASP juice shop - PRODUCTION`

Pipeline Summary
----------------

Demonstrated pipeline uses same WAF Policy for Production as it did for Staging environment, making both environments identical from the security perspective. Additionally, Production pipeline uses DAST testing to rule out any runtime vulnerabilities.
 * Deploy WAF Policy
 * Test and update policy as necessary
 * Repeat

What's Next? 
