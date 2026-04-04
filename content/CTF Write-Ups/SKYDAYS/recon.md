---
title: Recon
tags:
  - skydays26
  - easy
---

#### Author: AMD

Repository: [SKYDAYS26 Recon]()

-----------------------------------------------------------------------------------
<b>What is the secret route?</b>

```text
Gizli yolu bulmak için ffuf kullanabiliriz.
```

![[static/recon/ffuf.png]]


-----------------------------------------------------------------------------------
<b>What is the secret url?</b>

```text
https://recon.skydays.ctf/hitcount sayfasını ziyaret ederek url'e ulaşabiliriz.
```

![[static/recon/secret_url.png]]

-----------------------------------------------------------------------------------
<b>What is the secret minecraft players name?</b>

```text
Secret url'in bir docker image olduğunu görüyoruz. /hitcount sayfasında da her zaman enviroment'da bir şey kalır diye ipucu var.
```

```sh
docker pull amahird/reckon-mock-backend:latest
docker inspect amahird/reckon-mock-backend --format='{{json .Config.Env}}' | ConvertFrom-Json
```

![[static/recon/player.png]]

-----------------------------------------------------------------------------------
<b>The player has a Youtube channel, when was the channel started?</b>

![[static/recon/search.png]]

![[static/recon/channel.png]]

-----------------------------------------------------------------------------------
<b>Flag'i Al</b>

![[static/recon/flag.png]]
