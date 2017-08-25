Nikto
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open a Putty session to the Kali host

   a. username / password

      i. root / 401elliottW!

2. Open a Putty session to the Hackazon host

   a. username / password

      i. root / default

3. On the Hackazon host, tail the web server error log

   a. tail -f /var/log/apache2/error.log

4. On the Kali host, use nikto to scan the web host

   a. nikto -h http://hackazon.f5agility.com

   b. Review the results provided by the tool.

1. On the Hackazon host, observe the error.log.

   a. Did it log an error? Why or why not?

   b. Press CTRL-C

   c. tail access.log

   d. Can you see the Kali host IP? User Agent?

|image5|
