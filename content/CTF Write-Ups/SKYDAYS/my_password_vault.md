---
title: My Password Vault
tags:
  - skydays26
  - easy-medium
---

#### Author: AMD

Repository: [SKYDAYS26 My Password Vault]()

-----------------------------------------------------------------------------------
<b>Teknoloji Belirle</b>

```text
DIE Engine kullanarak .exe dosyasının hangi teknoloji ile yazıldığını bulalım.
```

![[static/my_password_vault/die.webp]]


-----------------------------------------------------------------------------------
<b>İçeriği Oku</b>

```text
.NET kullanıldığını öğrendik. DnSpy kullanarak içeriğie bakmayı deneyebiliriz.
```

![[static/my_password_vault/dnspy_1.webp]]

-----------------------------------------------------------------------------------
<b>Dosyayı Aç</b>

```text
DnSpy ile içeriği görüntülüyemediğimize göre .exe dosyasını açmamız lazım. Bu işlem için SingleFileExtractor'ı kullanabiliriz.
```

```sh
dotnet tool install -g sfextract
sfextract .\amd-my-password-vault.exe --output tmp
```

![[static/my_password_vault/sfe.webp]]

-----------------------------------------------------------------------------------
<b>.dll Dosyasını İncele</b>

![[static/my_password_vault/dnspy_2.webp]]

-----------------------------------------------------------------------------------
<b>Şifreyi Çöz</b>

```text
Kullanıcıdan beklenen input'un base64 ile şifrelenmiş halinin aioyS2EyUC12M20wZHcqOQ== olduğunu gördük. Şifreyi elde edelim.
```

![[static/my_password_vault/cyber_chef.webp]]

-----------------------------------------------------------------------------------
<b>Flag'i Al</b>

![[static/my_password_vault/flag.webp]]
