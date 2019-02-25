Testing Threat Campaigns
----------------------------

In this exercise we will execute a few attacks that mimic current threat campaigns and review the resulting ASM logs.

Threat Campaign Attack
~~~~~~~~~~~~~~~~~~~~~~

  From the Windows Desktop, open a command prompt.

  .. NOTE::
    In this lab, for ease of use, we are using cURL to mimic the attacks.  In the real world various other tools (NMAP, metasploit, etc.) are used.

  Change to the Documents directory.

  .. code-block:: console

    cd Documents

  Copy the following command and paste into the Windows command prompt, then press **Enter**:

  .. code-block:: console

    curl -X HEAD http://hackazon.f5demo.com/ -H "User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)" -H "cache-control: no-cache"

  .. NOTE::
    This is a basic NMAP scan but is frequently used by attackers for reconnaissance.

  Copy following command and paste into the Windows command prompt, then press **Enter**:

  .. code-block:: console

    curl -X POST http://hackazon.f5demo.com/index.php -H "Content-Type: text/plain" -H "cache-control: no-cache" -d @TC-post-data.txt

  .. NOTE::
    This attack attempts to exploit an Apache Struts2 vulnerability to deliver malware.

  You should see a blocking response from the BIG-IP similar to this:

  |image6|


Review ASM Request Logs
~~~~~~~~~~~~~~~~~~~~~~~

  In the BIG-IP browse to the ASM Request log at **Security >> Event Logs >> Application >> Requests**.

  The top two requests should be blocked.

  |image7|

  Select the lower request to "/".  Notice that the **Threat Campaign detected** violation has fired.
  Select the "1" in the **Occurrences** column to see details about which threat campaign signature was detected.

  |image8|


  Select the top request to "/index.php".  Notice that the **Threat Campaign detected** violation has fired.

  How many **Occurrences** of threat campaign signatures were detected in this request?

  |image9|

  You can get more details about the Threat Campaign from within this screen by clicking on the |image10| icon next to the Threat Campaign name.

  |image11|





.. |image6| image:: /_static/class8/threatcampaigns/image6.png
.. |image7| image:: /_static/class8/threatcampaigns/image7.png
.. |image8| image:: /_static/class8/threatcampaigns/image8.png
.. |image9| image:: /_static/class8/threatcampaigns/image9.png
.. |image10| image:: /_static/class8/threatcampaigns/image10.png
.. |image11| image:: /_static/class8/threatcampaigns/image11.png
