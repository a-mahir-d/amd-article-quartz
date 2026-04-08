---
title: Hammer
tags:
  - thm
  - medium
---

#### Author: AMD

![[static/hammer/hammer.webp]]

This is a writeup for <b>Hammer</b> room.

-----------------------------------------------------------------------------------
<b>NMAP</b>

```text
Lets start with scanning all the ports.
```

![[static/hammer/nmap.webp]]

-----------------------------------------------------------------------------------
<b>Web Page</b>

```text
Lets check out http://<MACHINE-IP>:1337
```

```text
If we check the page source we can see the developer note
```

![[static/hammer/dev_note.webp]]

-----------------------------------------------------------------------------------
<b>FFUF</b>

```text
Lets use ffuf to find other directories
```

![[static/hammer/ffuf.webp]]

-----------------------------------------------------------------------------------
<b>Directory Exploration</b>

```text
Lets check out all 4
```

```text
In hmr_logs we found error.logs

If we check that out we can find some credentials
```

![[static/hammer/error_logs.webp]]

-----------------------------------------------------------------------------------
<b>Password Reset</b>

```text
Lets try to reset the password
```

```text
First we need a payload, lets get it by catching a request
```

![[static/hammer/example_req.webp]]

```text
Next we need a file that contains all the digits
```

![[static/hammer/codes.webp]]

```text
We are ready to brute-force it with ffuf
```

![[static/hammer/ffuf_code.webp]]

```text
We got the code, lets enter it and reset the password
```

![[static/hammer/reset_password.webp]]

-----------------------------------------------------------------------------------
<b>Get flag 1</b>

```text
We can get the flag by logging in with the new credentials
```

![[static/hammer/flag1.webp]]

-----------------------------------------------------------------------------------
<b>Look around</b>

```text
We got command input area, lets try some commands
```

![[static/hammer/ls.webp]]

```text
188ade1.key looks suspicious, lets try to read it
```

![[static/hammer/cat_key.webp]]

-----------------------------------------------------------------------------------
<b>View page source</b>

```text
Lets check out the page source again
```

![[static/hammer/page_source_jwt.webp]]

```text
We found a jwt token, lets check it out with jwt.io
```

![[static/hammer/jwt_info.webp]]

```text
We found the key location --> /var/www/mykey.key

Since the key is saved on the /var/www we can access it
```

![[static/hammer/key188.webp]]

![[static/hammer/key188_content.webp]]

```text
We got the key
```

-----------------------------------------------------------------------------------
<b>View page source</b>

```text
Lets get back to jwt.io and select JWT Encoder

Add the secret --> 56058354efb3daa97ebab00fabd7a7d7
Change role to --> admin
Change kid to -> /var/www/html/188ade1.key

Now we have the admin token
```

![[static/hammer/admin_token.webp]]

-----------------------------------------------------------------------------------
<b>Get flag 2</b>

```text
Question is: What is the content of the file /home/ubuntu/flag.txt?

So the command that we need to run is cat /home/ubuntu/flag.txt

Lets catch it with burp suite
```

![[static/hammer/raw_req.webp]]

```text
If we change the tokens with admin token it should work

We got the flag
```

![[static/hammer/flag2.webp]]