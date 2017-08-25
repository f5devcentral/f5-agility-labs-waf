Wget
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open a Putty session to the Kali host

   a. username / password

      i. root / 401elliottW!

2. Open a Putty session to the Hackazon host

   a. username / password

      i. root / default

3. On the Hackazon host, tail the web server error log

   a. tail -f /var/log/apache2/error.log

4. On the Kali host, use wget to inspect the web server information

   a. |image3|\ wget - - saveheaders http://hackazon.f5agility.com

   b. |image4|\ head -15 index.html

   c. What do you see at the beginning of the index.html file? Is this
      the same information as you got from nc?

   d. cat -100 index.html

   e. What more information can you glean from viewing the source code
      of the page?

5. On the Hackazon host, observe the error.log.

   a. Did it log an error? Why or why not?

   b. Press CTRL-C

   c. tail access.log

   d. Do you see the Kali host IP? Do you see the HTTP method? Do you
      see a User Agent?
