netcat again
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open a Putty session to the Kali host

#. Open a Putty session to the Hackazon host

#. On the Hackazon host, tail the web server error log

   * tail -f /var/log/apache2/error.log

#. On the Kali host, use netcat to probe for HTTP methods

   * nc hackazon.f5agility.com 80

   * OPTIONS /robots.txt HTTP/1.0 //r/n

   * [Press ENTER twice]

   * What methods are allowed?

#. On the Kali host, use netcat to verify that HTTP methods are enforced

   * nc hackazon.f5agility.com 80

   * DELETE /robots.txt HTTP/1.0 //r/n

   * [Press ENTER twice]

   * Were you able to use the DELETE method?

#. On the Hackazon host, observe the error.log.

   * Did it log an error? Why or why not?

   * Press CTRL-C

   * tail access.log

   * Do you see the Kali host IP? Do you see the HTTP method? Do you
      see a User Agent?
