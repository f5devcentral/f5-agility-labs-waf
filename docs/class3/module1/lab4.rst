nikto
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open a Putty session to the Kali host

#. Open a Putty session to the Hackazon host

#. On the Hackazon host, tail the web server error log

   * tail -f /var/log/apache2/error.log

#. On the Kali host, use nikto to scan the web host

   * nikto -h http://hackazon.f5agility.com

   * Review the results provided by the tool.

#. On the Hackazon host, observe the error.log.

   * Did it log an error? Why or why not?

   * Press CTRL-C

   * tail access.log

   * Can you see the Kali host IP? User Agent?

.. image:: /_static/class3/image7.png
