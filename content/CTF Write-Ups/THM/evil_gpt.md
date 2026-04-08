---
title: Evil GPT
tags:
  - thm
  - easy
  - llm
---

#### Author: AMD

![[static/evil_gpt/evil_gpt.webp]]

This is a writeup for <b>Evil GPT</b> room.

-----------------------------------------------------------------------------------
<b>FIND THE FLAG</b>

![[static/evil_gpt/pwd.webp]]

It didn't let us use pwd. Lets check directories.

![[static/evil_gpt/ls.webp]]

No flag here, lets try /root

![[static/evil_gpt/ls_root.webp]]

We found the flag, lets try to read it.

-----------------------------------------------------------------------------------
<b>READ THE FLAG</b>

![[static/evil_gpt/cat_try.webp]]

We can't read or change directory. Lets try sudo

![[static/evil_gpt/sudo_cat.webp]]

It worked!!!
