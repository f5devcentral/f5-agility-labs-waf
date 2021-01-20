Lab 1 – Setting Up SSH Access 
-----------------------------

Objective
~~~~~~~~~

- generate a SSH key or use an existing one

- add the SSH key to the lab

- test SSH to Linux instances in lab


Task – Add a SSH Key to the Lab
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After logging into UDF, navigate to your preferences by clicking on the icon in the top right and then clicking Preferences

    .. image:: /_static/class9/udf_prefs.png

On the next page click the ``Create SSH Key`` button

    .. image:: /_static/class9/udf_create_key.png

Copy and paste your SSH public key into the field provided.

    .. image:: /_static/class9/udf_add_key.png


On MacOS you can run the following commands to generate a new key:

::

    ssh-keygen -f ~/.ssh/agility

After following the prompts dump the contents of the public key file.

::

    cat ~/.ssh/agility.pub

Copy and paste that into the Create SSH Key window in the field labled ``Key`` as shown in the image above and then click ``Save``


Try connecting via SSH to the External Jump Host by navigating to the ``Components`` tab and using the ``Access`` dropdown in the External Jump Host box under the ``Systems`` column where you can click on the SSH option.

    .. image:: /_static/class9/udf_ssh_external.png

You should be promted to open the connection using the default SSH application such as Terminal or iTerm on MacOS and putty on Windows.