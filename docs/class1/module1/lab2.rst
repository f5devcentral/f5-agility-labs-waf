Configure
----------------

#. Click the **Advanced** button (Top-Right) to ensure that all the
   available policy creation options are displayed.

#. Name the security policy ``hackazon_asm`` and ensure that
   the **Policy Type** is ``Security``.

#. Verify the **Policy Template** is set to ``Fundamental``.

#. Assign this policy to the ``hackazon.f5demo.com_https_vs``
   from the **Virtual Server** drop down.

#. Set the Application Language to UTF-8 (This is required to set
   the Learning Mode, why might this be necessary?)

#. Go back up two settings to **Learning Mode** and set it
   to ``Manual``.

#. Set the **Enforcement Mode** to ``Transparent``

