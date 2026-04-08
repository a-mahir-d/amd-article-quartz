---
title: Nocturnal
tags:
  - htb
  - easy
---

#### Author: AMD

![[static/nocturnal/nocturnal.webp]]

This is a writeup for <b>Nocturnal</b> machine.

My target IP: 10.10.11.64

-----------------------------------------------------------------------------------
<b>NMAP</b>

Lets scan out target.

![[static/nocturnal/nmap.webp]]

-----------------------------------------------------------------------------------
<b>CURL</b>

![[static/nocturnal/curl.webp]]

Add "10.10.11.64   nocturnal.htb" to /etc/hosts

-----------------------------------------------------------------------------------
<b>GOBUSTER</b>

![[static/nocturnal/gobuster.webp]]

we can not access these urls

-----------------------------------------------------------------------------------
<b>WEBSITE INSPECTION</b>

![[static/nocturnal/website.webp]]

First register then login

-----------------------------------------------------------------------------------
<b>TEST FILE UPLOAD</b>

Test file upload with .php file

See the valid file types

Upload valid file and see the link

![[static/nocturnal/file_link.webp]]

-----------------------------------------------------------------------------------
<b>FIND OTHER USERS</b>

Lets try to find the other users and use the file link to access other users files.

use https://github.com/C0euss/Nocturnal-Username-Enumeration/tree/main to find other usernames

![[static/nocturnal/enumeration.webp]]

-----------------------------------------------------------------------------------
<b>GUESS FILE NAMES</b>

![[static/nocturnal/amandas_file.webp]]

http://nocturnal.htb/view.php?username=amanda&file=privacy.odt

-----------------------------------------------------------------------------------
<b>VIEW FILE</b>

![[static/nocturnal/amanda_password.webp]]

login with amanda and password

-----------------------------------------------------------------------------------
<b>VIEW PAGES</b>

![[static/nocturnal/amandas_page.webp]]

go to admin panel

![[static/nocturnal/admin_panel.webp]]

-----------------------------------------------------------------------------------
<b>VIEW LOGIN.PHP</b>

![[static/nocturnal/login_php.webp]]

Get db information

-----------------------------------------------------------------------------------
<b>RCE</b>

Enter "dummy" to create backup password field, catch the request with burpsuite and send it to repeater.

url CyberChef to url encode

![[static/nocturnal/cyber_chef.webp]]

send with repeater

![[static/nocturnal/burp.webp]]

-----------------------------------------------------------------------------------
<b>SSH</b>

Crack tobias's password using https://crackstation.net/

![[static/nocturnal/crackstation.webp]]

connect with ssh

![[static/nocturnal/ssh.webp]]

-----------------------------------------------------------------------------------
<b>GET USER FLAG</b>

![[static/nocturnal/user_txt.webp]]

-----------------------------------------------------------------------------------
<b>NETSTAT</b>

Use netstat to use what is working on the machine

![[static/nocturnal/netstat.webp]]

-----------------------------------------------------------------------------------
<b>PF</b>

We cannot visit http://127.0.0.1:8080 so lets try port forwarding

![[static/nocturnal/pf1.webp]]

![[static/nocturnal/pf2.webp]]

Lets visit http://127.0.0.1:8080

![[static/nocturnal/isp_login.webp]]

-----------------------------------------------------------------------------------
<b>LOGIN</b>

Lets try to login with tobias's credentials --> doesnt work

Lets try other usernames we found (amanda, admin)  --> admin works

![[static/nocturnal/isp_home.webp]]

-----------------------------------------------------------------------------------
<b>EXEMINE SITE</b>

![[static/nocturnal/isp.webp]]

Lets find vulnerability for this version ISPConfig 

![[static/nocturnal/isp_volnurability_search.webp]]

![[static/nocturnal/code.webp]]

-----------------------------------------------------------------------------------
<b>EXPLOIT VULNURABILITY</b>

run "nano CVE-2023-46818.py"  --> paste the code  --> save and exit

![[static/nocturnal/run_exploit.webp]]

-----------------------------------------------------------------------------------
<b>GET ROOT FLAG</b>

![[static/nocturnal/flag.webp]]
