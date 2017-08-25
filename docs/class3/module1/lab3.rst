netcat again
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open a Putty session to the Kali host

   a. username / password

      i. root / 401elliottW!

2. Open a Putty session to the Hackazon host

   a. username / password

      i. root / default

3. On the Hackazon host, tail the web server error log

   a. tail -f /var/log/apache2/error.log

4. On the Kali host, use netcat to probe for HTTP methods

   a. nc hackazon.f5agility.com 80

   b. OPTIONS /robots.txt HTTP/1.0 //r/n

   c. [Press ENTER twice]

   d. What methods are allowed?

5. On the Kali host, use netcat to verify that HTTP methods are enforced

   a. nc hackazon.f5agility.com 80

   b. DELETE /robots.txt HTTP/1.0 //r/n

   c. [Press ENTER twice]

   d. Were you able to use the DELETE method?

1. On the Hackazon host, observe the error.log.

   a. Did it log an error? Why or why not?

   b. Press CTRL-C

   c. tail access.log

   d. Do you see the Kali host IP? Do you see the HTTP method? Do you
      see a User Agent?
