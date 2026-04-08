---
title: Boiler CTF
tags:
  - thm
  - medium
---

#### Author: AMD

![[static/boiler_ctf/boiler_ctf.webp]]

This is a writeup for <b>Boiler CTF</b> room.

-----------------------------------------------------------------------------------
<b>NMAP</b>

Lets scan the target ip.

![[static/boiler_ctf/nmap.webp]]

-----------------------------------------------------------------------------------
<b>File extension after anon login?</b>

![[static/boiler_ctf/q1.webp]]

-----------------------------------------------------------------------------------
<b>What is on the highest port?</b>

![[static/boiler_ctf/q2.webp]]

It is ssh.

-----------------------------------------------------------------------------------
<b>What's running on port 10000?</b>

![[static/boiler_ctf/q3_research.webp]]

![[static/boiler_ctf/q3.webp]]

It is webmin

-----------------------------------------------------------------------------------
<b>Can you exploit the service running on that port?</b>

The version is not on the login page or on the page source. Lets try curl.

![[static/boiler_ctf/q4_version.webp]]

Lets go to https://www.exploit-db.com/ and search webmin.

![[static/boiler_ctf/q4_research.webp]]

No public unauthenticated RCE, LFI, or CSRF exists for Webmin 1.930. So answer is nay.

-----------------------------------------------------------------------------------
<b>What's CMS can you access?</b>

Lets use gobustor to look.

![[static/boiler_ctf/q5_gobuster.webp]]

The answer is joomla.

-----------------------------------------------------------------------------------
<b>Keep enumerating, you'll know when you find it.</b>

![[static/boiler_ctf/q6_gobuster.webp]]

_files look weird, lets check it out. After decoding the message it comes to "Whopsie daisy". 

Lets try it with bigger data.

![[static/boiler_ctf/q6_gobuster_2.webp]]

Perfect, we got new ones. _database and _test is weird too.

-----------------------------------------------------------------------------------
<b>The interesting file name in the folder?</b>

_database gives us "Lwuv oguukpi ctqwpf. " which is "J u s t   m e s s i n g   a r o u n d ." with Caesar cipher.

![[static/boiler_ctf/q7_test_page.webp]]

We can see that if we change the plot on the url it reflect to page. So lets try running a command.

I tried ls, it didn't worked but ;ls works.

![[static/boiler_ctf/q7.webp]]

I guess log.txt is weird.

-----------------------------------------------------------------------------------
<b>PREPERATION</b>

Lets get in.

![[static/boiler_ctf/prep_cat.webp]]

We found username and password.

![[static/boiler_ctf/prep_ssh.webp]]

-----------------------------------------------------------------------------------
<b>Where was the other users pass stored(no extension, just the name)?</b>

![[static/boiler_ctf/q8.webp]]

It is in backup.sh

-----------------------------------------------------------------------------------
<b>user.txt</b>

Lets ssh stoner.

![[static/boiler_ctf/q9_ssh.webp]]

I looked for user.txt, it wasn't there but we have .secret

![[static/boiler_ctf/q9.webp]]

-----------------------------------------------------------------------------------
<b>What did you exploit to get the privileged user?</b>

Lets search the system for regular files with the setuid bit set.

![[static/boiler_ctf/q10_research.webp]]

/find looks weird. (Note: You can use GPT to locate whats unusual)

Lets visit https://gtfobins.github.io/ to look for find.

![[static/boiler_ctf/q10_find.webp]]

![[static/boiler_ctf/q10_exploit.webp]]

We used find to become root.

-----------------------------------------------------------------------------------
<b>root.txt</b>

![[static/boiler_ctf/q11.webp]]