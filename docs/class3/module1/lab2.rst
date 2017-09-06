wget
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open a Putty session to the Kali host

#. Open a Putty session to the Hackazon host

#. On the Hackazon host, tail the web server error log

   * tail -f /var/log/apache2/error.log

#. On the Kali host, use wget to inspect the web server information

   * wget - - saveheaders http://hackazon.f5agility.com

   .. image:: /_static/class3/image5.png

   * head -15 index.html

   .. image:: /_static/class3/image4.png

   * What do you see at the beginning of the index.html file? Is this the same information as you got from nc?

   * cat -100 index.html

   * What more information can you glean from viewing the source code of the page?

#. On the Hackazon host, observe the error.log.

   * Did it log an error? Why or why not?

   * Press CTRL-C

   * tail access.log

   * Do you see the Kali host IP? Do you see the HTTP method? Do you see a User Agent?
