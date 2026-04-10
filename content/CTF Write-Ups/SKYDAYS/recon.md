---
title: Recon
tags:
  - skydays26
  - easy
---

#### Author: AMD

Repository: [SKYDAYS26 Recon](https://github.com/skylab-kulubu/SKYDAYS-CTF-26/tree/main/web/amd-recon-ctf)

-----------------------------------------------------------------------------------
<b>What is the secret route?</b>

```text
Gizli yolu bulmak için ffuf kullanabiliriz.
```

![[static/recon/ffuf.webp]]


-----------------------------------------------------------------------------------
<b>What is the secret url?</b>

```text
https://recon.skydays.ctf/hitcount sayfasını ziyaret ederek url'e ulaşabiliriz.
```

![[static/recon/secret_url.webp]]

-----------------------------------------------------------------------------------
<b>What is the secret minecraft players name?</b>

```text
Secret url'in bir docker image olduğunu görüyoruz. /hitcount sayfasında da her zaman enviroment'da bir şey kalır diye ipucu var.
```

```sh
docker pull amahird/reckon-mock-backend:latest
docker inspect amahird/reckon-mock-backend --format='{{json .Config.Env}}' | ConvertFrom-Json
```

![[static/recon/player.webp]]

-----------------------------------------------------------------------------------
<b>The player has a Youtube channel, when was the channel started?</b>

![[static/recon/search.webp]]

![[static/recon/channel.webp]]

-----------------------------------------------------------------------------------
<b>Flag'i Al</b>

![[static/recon/flag.webp]]
