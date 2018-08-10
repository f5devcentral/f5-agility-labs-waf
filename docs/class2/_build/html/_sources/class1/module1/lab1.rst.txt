Exercise 1 : Scanning the Network
---------------------------------

MSFconsole
~~~~~~~~~~

MSFconsole is a command line interface to access the modules of
Metasploit. It is the most commonly used component of Metasploit and
quite likely where you’d spend most of your time for testing
vulnerabilities. The only possible downside is that you need to be ‘on’
the Metasploit computer itself – either via ssh or logged in locally.

To access MSFconsole, do the following:

| Use putty on the Win 7 Client to SSH to the Kali Linux host CLI
  (10.1.10.240):
| root / 401elliottW!

..  image:: /_static/putty3.png

..  image:: /_static/putty4.png

Intelligence Gathering
~~~~~~~~~~~~~~~~~~~~~~

When a hacker wants to infiltrate your network, they start with
gathering Intel. There are many tools which can search for and identify
devices and applications on the network. Some are larger tools such as
nmap (discussed below), Nessus from Tenable
(`www.tenable.com <http://www.tenable.com>`__), Nexpose from Rapid7
(https://www.rapid7.com/free-tools/) or even fing (https://www.fing.io/)
which runs on your Smartphone!

nmap
~~~~

Before starting an attack, a hacker will probe for applications running
within the network. nmap is a freeware tool which can be used to probe a
subnet or a specific IP address to ports as well as attempt to classify
what the application on the port is.

Execute nmap against the DMZ network to see if there are any
‘interesting’ computers we can see.. From the ssh connection to the Kali
linux server, run the following command:

nmap -Pn -sS -A -oX /tmp/nmap.xml 10.1.10.0/24

This will initiate a scan which should take up to 10 minutes to
complete. The output will be stored in an XML file that we will import
into Metasploit.

Sample Output

Starting Nmap 6.49BETA4 ( https://nmap.org ) at 2017-06-26 14:32 EDT

Nmap scan report for 10.1.10.1

Host is up (0.0015s latency).

All 1000 scanned ports on 10.1.10.1 are filtered

MAC Address: 2C:C2:60:FF:00:01 (Ravello Systems)

Too many fingerprints match this host to give specific OS details

Network Distance: 1 hop

TRACEROUTE

HOP RTT ADDRESS

1 1.47 ms 10.1.10.1

Nmap scan report for 10.1.10.14

Host is up (0.0012s latency).

Not shown: 999 closed ports

PORT STATE SERVICE VERSION

80/tcp open http?

MAC Address: 2C:C2:60:4E:15:D2 (Ravello Systems)

No exact OS matches for host (If you know what OS is running on it, see
https://nmap.org/submit/ ).

TCP/IP fingerprint:

OS:SCAN(V=6.49BETA4%E=4%D=6/26%OT=80%CT=1%CU=31425%PV=Y%DS=1%DC=D%G=Y%M=2CC

OS:260%TM=5951553A%P=x86\_64-pc-linux-gnu)SEQ(SP=FC%GCD=1%ISR=10D%TI=RD%CI=R

OS:I%TS=A)OPS(O1=M5B4NNT11SLL%O2=M5B4NNT11SLL%O3=M5B4NNT11%O4=M5B4NNT11SLL%

OS:O5=M5B4NNT11SLL%O6=M5B4NNT11SLL)WIN(W1=111C%W2=1068%W3=780%W4=648%W5=648

OS:%W6=31B)ECN(R=Y%DF=Y%T=FF%W=111C%O=M5B4SLL%CC=N%Q=)T1(R=Y%DF=Y%T=FF%S=O%

OS:A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=FF%W=0%S=A%A=S%F=AR%O=%RD=

OS:0%Q=)T5(R=Y%DF=Y%T=FF%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=FF%W=0%

OS:S=A%A=S%F=AR%O=%RD=0%Q=)T7(R=N)U1(R=Y%DF=Y%T=FF%IPL=38%UN=0%RIPL=G%RID=G

OS:%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=Y%T=FF%CD=S)

***… snip …***

OS and Service detection performed. Please report any incorrect results
at https://nmap.org/submit/ .

Nmap done: 256 IP addresses (18 hosts up) scanned in 515.89 seconds

Open a New ssh session to the Kali server while the nmap command runs.

Metasploit uses a database to store many of the items you’ll be using as
well as the data from searches such as the one running in your nmap
session. To ensure that the database is running, run the following from
the command line:

service postgresql start

This will ensure that postgresql is running. You can also check the
status:

service postgresql status

● postgresql.service - PostgreSQL RDBMS

Loaded: loaded (/lib/systemd/system/postgresql.service; enabled)

Active: active (exited) since Tue 2017-07-04 10:59:07 EDT; 31min ago

Process: 779 ExecStart=/bin/true (code=exited, status=0/SUCCESS)

Main PID: 779 (code=exited, status=0/SUCCESS)

CGroup: /system.slice/postgresql.service

Run msfconsole

- #msfconsole

The first time you run msfconsole there can be a slight delay as indices
are updated.

Your output will vary on each run – since this is the free version – but
the final lines should look similar to the following:

=[ metasploit v4.14.5-dev ]

+ -- --=[ 1639 exploits - 945 auxiliary - 286 post ]

+ -- --=[ 473 payloads - 40 encoders - 9 nops ]

+ -- --=[ Free Metasploit Pro trial: http://r-7.co/trymsp ]

msf >

You’re now in MSFconsole and you can investigate some of the commands
available to you.

msf > help <command>

For example you can see the possible switches for the connect command:

msf > help connect

Usage: connect [options] <host> <port>

Communicate with a host, similar to interacting via netcat, taking
advantage of

any configured session pivoting.

OPTIONS:

-C Try to use CRLF for EOL sequence.

-P <opt> Specify source port.

-S <opt> Specify source address.

-c <opt> Specify which Comm to use.

-h Help banner.

-i <opt> Send the contents of a file.

-p <opt> List of proxies to use.

-s Connect with SSL.

-u Switch to a UDP socket.

-w <opt> Specify connect timeout.

-z Just try to connect, then return.

msf >

We will spend time in Metasploit investigating some of the commands
later but for now, here are some of the interesting commands. You can
type ‘help <command>’ for some information on each of these.

options
^^^^^^^

Options are like command line flags for your exploits and modules.
You’ll use this all the time. Use ‘show options’ to see what has been
set for your current exploit/module.

advanced
^^^^^^^^

I know you’re reading this and saying, “I’m just starting!” but advanced
gives you access to debugging and other helpful information while you’re
testing vulnerabilities and you’ll use this command often.

For items listed in ‘options’ and ‘advanced’ you can use:

set or unset
^^^^^^^^^^^^

These commands operation on the flags shown in options and advanced. You
can set the flags or if you want to set it back to the default/blank
value you can unset it.

info
^^^^

Like options and advanced, this displays all of your current settings.

workspace
^^^^^^^^^

You can create different areas to work in, each with their own settings
and defaults. These are known as workspaces. When you’re testing
different vulnerabilities setting each in their own workspace can be
helpful and a real time saver.

reload\_all
^^^^^^^^^^^

reload\_all is useful when you add new modules or exploits to Metasploit
and want to import them into the database.

jobs
^^^^

You can push jobs into the background within the msfconsole environment
and this will show you active running jobs and allow you to push or pull
them to the foreground or background.

Exit out of Metasploit after you have spent some time looking around.

msf > exit

You’re now a Hacker!

Importing nmap scan results
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the nmap process has completed in the first shell, you can return
to Metasploit and import the data.

Return to Metasploit

msfconsole

db\_import /tmp/nmap.xml

db\_import
^^^^^^^^^^

This command takes an XML file of a scan and will bring it into the
Metasploit database.

[\*] Importing 'Nmap XML' data

[\*] Import: Parsing with 'Nokogiri v1.7.2'

[\*] Importing host 10.1.10.14

[\*] Importing host 10.1.10.35

[\*] Importing host 10.1.10.50

[\*] Importing host 10.1.10.51

[\*] Importing host 10.1.10.55

[\*] Importing host 10.1.10.59

[\*] Importing host 10.1.10.90

[\*] Importing host 10.1.10.101

[\*] Importing host 10.1.10.102

[\*] Importing host 10.1.10.115

[\*] Importing host 10.1.10.120

[\*] Importing host 10.1.10.125

[\*] Importing host 10.1.10.131

[\*] Importing host 10.1.10.132

[\*] Importing host 10.1.10.195

[\*] Importing host 10.1.10.240

[\*] Successfully imported /tmp/nmap.xml

Now you can view the hosts where were located by nmap:

hosts -c address,name,os\_name,purpose

hosts
^^^^^

The hosts command will show the list of targets that are available for
exploiting. The XML file we have imported will also show more than just
the IP address. nmap is able to determine the kind of host that was
scanned. Here you can see that it has seen the VIPs as ‘TMOS’ and knows
that they’re an F5 virtual server based on the signature of the
connection. Where possible, it has done a reverse DNS lookup and you can
see what has been found in the local hosts file.

To see what services are available to connect to:

services

services
^^^^^^^^

This is where things get very interesting… nmap has determined the ports
and accessible items for each of the hosts. Now it’s possible to do some
investigation and access/attach to the ports of interest.

Services

========

host port proto name state info

---- ---- ----- ---- ----- ----

10.1.10.14 80 tcp http open

10.1.10.35 80 tcp http-proxy open F5 BIG-IP load balancer http proxy

10.1.10.35 443 tcp ssl/http open Apache httpd 2.4.7 (Ubuntu)
PHP/5.5.9-1ubuntu4.21 OpenSSL/1.0.1f

10.1.10.50 80 tcp http-proxy open F5 BIG-IP load balancer http proxy

10.1.10.50 443 tcp ssl/http open Apache Tomcat/Coyote JSP engine 1.1

10.1.10.51 80 tcp http-proxy open F5 BIG-IP load balancer http proxy

10.1.10.51 443 tcp ssl/https open

10.1.10.55 80 tcp http-proxy open F5 BIG-IP load balancer http proxy

10.1.10.55 443 tcp ssl/http open Apache httpd 2.4.7 (Ubuntu)
PHP/5.5.9-1ubuntu4.21 OpenSSL/1.0.1f

10.1.10.59 3389 tcp ms-wbt-server open

10.1.10.90 135 tcp msrpc open Microsoft Windows RPC

10.1.10.90 139 tcp netbios-ssn open Microsoft Windows 98 netbios-ssn

10.1.10.90 445 tcp microsoft-ds open primary domain: WORKGROUP

10.1.10.90 3389 tcp ms-wbt-server open Microsoft Terminal Service

10.1.10.90 49152 tcp msrpc open Microsoft Windows RPC

10.1.10.90 49153 tcp msrpc open Microsoft Windows RPC

10.1.10.90 49154 tcp msrpc open Microsoft Windows RPC

10.1.10.90 49155 tcp msrpc open Microsoft Windows RPC

10.1.10.90 49156 tcp msrpc open Microsoft Windows RPC

10.1.10.90 49157 tcp msrpc open Microsoft Windows RPC

10.1.10.101 81 tcp http-proxy open F5 BIG-IP load balancer http proxy

10.1.10.101 443 tcp ssl/https open

10.1.10.102 80 tcp http-proxy open F5 BIG-IP load balancer http proxy

10.1.10.102 443 tcp ssl/https open

10.1.10.115 80 tcp http-proxy open F5 BIG-IP load balancer http proxy

10.1.10.115 443 tcp ssl/https open

10.1.10.120 80 tcp http-proxy open F5 BIG-IP load balancer http proxy

10.1.10.120 443 tcp ssl/http open Apache httpd 2.4.7 (Ubuntu)
PHP/5.5.9-1ubuntu4.21 OpenSSL/1.0.1f

10.1.10.125 443 tcp ssl/http open Apache httpd 2.4.7 (Ubuntu)
PHP/5.5.9-1ubuntu4.21 OpenSSL/1.0.1f

10.1.10.131 80 tcp http open nginx 1.10.0 Ubuntu

10.1.10.132 80 tcp http open

10.1.10.195 3389 tcp ms-wbt-server open Microsoft Terminal Service

10.1.10.240 22 tcp ssh open OpenSSH 6.7p1 Debian 5 protocol 2.0

10.1.10.240 111 tcp rpcbind open 2-4 RPC #100000