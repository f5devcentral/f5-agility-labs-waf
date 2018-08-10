Exercise 3: Metasploit Utilities
--------------------------------

Update Metasploit application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to stay current, you need to update your copy of the Metasploit
regularly. Issue the following command from the Kali bash command shell:

root@kali# sudo apt-get update

Note on non-Kali installs of Metasploit, you can issue the command
*msfupdate* within the Metasploit console but this is disabled in recent
releases of Kali in favor of using the apt-get command.

Update the Exploit database
~~~~~~~~~~~~~~~~~~~~~~~~~~~

This process is a little more involved. First you need to locate the
exploits you want to download (or even write your own!). The best
database for this is at https://www.exploit-db.com/ for viewing the
exploits but you can use the git tool grab specific items. The github
repository is located at
https://github.com/offensive-security/exploit-database

There is also a tool available on the git repository called searchsploit
which will search the database for you and list the exploits for you.

To find a new Windows exploit, you can execute from the Kali server:

On the Kali bash shell:

git clone https://github.com/offensive-security/exploit-database.git
/opt/exploit-database

cd /opt/exploit-database

Say you want to find the exploit which works with the recent NSA Hacks
released in May/June 2017, known as ‘eternalblue’ for SMB hacking:

./searchsploit eternalblue Windows

{ a list of exploits will be returned }

Now you can choose which one you want to load, we will load the one for
Windows 7/2008 or the file 42031.py. Looking at the output of the
command, you will see that the files are in the
platforms/win\_x86-64/remote directory. This file is the Ruby on Rails
code that will be executed by Metasploit, and it will need to be copied
to the proper folder.

cd ~/.msf4/modules

ls –ls

If the ‘exploits’ directory doesn’t exist, create it:

mkdir ~/.msf4/modules/exploits

cd exploits

Do the same for the directory tree: win\_86-64 and remote so you have
the following directory structure:

/root/.msf4/modules/exploits/win\_x86-64/remote

Now copy the Ruby files from the source location

cp /opt/exploit-database/platforms/win\_x86-64/remote/42031.py .

**Note that there is a period at the end of the previous line**

Now open Metasploit

msfconsole

And search for the newly added exploit

search eternalblue

And the exploit will be displayed and is available for use.