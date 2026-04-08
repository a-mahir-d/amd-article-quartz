---
title: Disgruntled
tags:
  - thm
  - easy
---

#### Author: AMD

![[static/disgruntled/disgruntled.webp]]

This is a writeup for <b>Disgruntled</b> room.

-----------------------------------------------------------------------------------
<b>Nothing suspicious... So far</b>

```text
Lets start with looking into sudoers list:
```

![[static/disgruntled/sudoers.webp]]

```text
Lets look at the bash history for each user
```

![[static/disgruntled/installed_package.webp]]

```text
We found the installed package, now lets find the command by looking to authentication logs
```

![[static/disgruntled/command.webp]]

-----------------------------------------------------------------------------------
<b>Let’s see if you did anything bad</b>

```text
Lets search adduser command
```

![[static/disgruntled/adduser.webp]]

```text
Lets search visudo command
```

![[static/disgruntled/visudo.webp]]

```text
Lets search vi command
```

![[static/disgruntled/vi.webp]]

-----------------------------------------------------------------------------------
<b>Bomb has been planted. But when and where?</b>

```text
Lets checkout bash history of it-admin
```

![[static/disgruntled/bomb_create.webp]]

```text
We can see that vi text editor is used. Vi text editor can edit and save files to a different location. Lets check out .viminfo with "cat /home/it-admin/.viminfo"
```

![[static/disgruntled/bomb_renamed.webp]]

```text
Lets use ls -la with full-time for the answer
```

![[static/disgruntled/modification_date.webp]]

```text
Lets read the os-update.sh
```

![[static/disgruntled/os_update_content.webp]]

-----------------------------------------------------------------------------------
<b>Following the fuse</b>

```text
To find the trigger time we need to check cronjobs
```

![[static/disgruntled/cron_expression.webp]]

```text
We need to turn this into time. We can use "https://crontab.cronhub.io/"
```

![[static/disgruntled/cron_time.webp]]
