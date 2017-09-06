Netcat
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open a Putty session to the Kali host

#. Open a Putty session to the Hackazon host

#. On the Hackazon host, tail the web server error log

   * tail -f /var/log/apache2/error.log

#. On the Kali host, use netcat to inspect the web server information

   * nc hackazon.f5agility.com 80

   * HEAD / HTTP/1.0 //r/n

   * [Press ENTER twice]

   * What information is returned ?

   .. image:: /_static/class3/image4.png

#. On the Hackazon host, observe the error.log.

   * Did it log an error? Why or why not?

   * Press CTRL-C

   * tail access.log

   * Do you see the Kali host IP? Do you see the HTTP method? Do you see a User Agent?
