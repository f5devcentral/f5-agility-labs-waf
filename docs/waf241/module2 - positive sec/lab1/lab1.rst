Lab 2: Intro to Positive Security - File Types and Cookie Enforcement
-------------------------------------------------------------------------

#. Navigate to **Security > Application Security > Security Policies > Policies List > Create** and configure a policy named **juiceshop_blocking**
#. Choose Policy Template: **Rapid Deployment Policy**, Enforcement Mode: **Blocking** and click **Save**. 

.. image:: images/juice_block.png
  :width: 600 px

3. Navigate to **Security > Application Security > Policy Building > Learning and Blocking Settings**. 
#. Under **Cookies** note the default settings. Uncheck **Learn** from **Modified ASM Cookie**. Generally we do not want to allow modification of the WAF cookie and therefor will disable learning suggestions for this. 
#. Under **File Types** note the default Learning Mode is set to **Never (wildcard only)** Change that to be **Selective** and enable **Learn and Alarm** for **Illegal File Types**. 

.. image:: images/cookies.png
  :width: 600 px

6. Under **Headers** check the box for both Alarm and Block for **Illegal host name** and then check the bottom box for **Learn New Hostnames**.
7. Under **URLS** enable **Compact Mode** for Learning Mode instead of **Never (wildcard only)**. Note the description of this mode: 
*Choose this option if you would like to create a list of top-level URL directories (e.g. /abc/*) and /, while enforcing all other URLs with a wildcard rule.

8. Enable Learn and Alarm for **Illegal URL**, click ** Save** and **Apply Policy**. 

.. image:: images/heads.png
  :width: 600 px

Whitelist
~~~~~~~~~~
Since we will be training the waf for positive security create a whitelist. This will create high fidelity learning suggestions. 

#. Navigate to **Security > Application Security > IP Addresses > IP Address Exceptions** and click **Create**. Configure the whitelist for a 10/8 as shown below and check the box for **Policy Builder trusted IP**. 
#. Click **Create** and **Apply Policy**. 

.. image:: images/list.png
  :width: 600 px



apply to virtual_server

create account juiceshop
Log in 
leave review for apple juice 
accept false positive request for illegal method in event viewer

traffic learning
Add URL - Accept
Add Hostname 

Select all and hit accept

jucieshop - chat / browse around go to photo wall, leave more feedback. this is how to train a waf. 

go back to l&b settings and change file-types to compact. 
browse site 

traffic learning - selct all file types and add

browse to app-sec file types and review what has been added. 


open burp - proxy - browser

change request to  https://juiceshop.f5agility.com/evilfile.exe

event logs - review 

l&b settings - enable block
even though policy is in blocking mode individual elements are not 

curl -k https://juiceshop.f5agility.com/evilfile.exe

review event log


open burp - proxy - browser
enter site
modify asm cookie

revie alert



test header enforcement

burp - change hostname to ip

event logs


















**This concludes Lab 2.**
