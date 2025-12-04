---
title: How To Execute DoS Attack With Burp Suite
tags:
  - burpsuite
  - dos
---

<div align="right">
  <a href="#tr">🇹🇷 Türkçe</a> | <a href="#en">English</a>
</div>

---

## <span id="tr">🇹🇷 Türkçe</span>

-----------------------------------------------------------------------------------
<b>Uyarı</b>

```text
Bu makale yalnızca eğitim amaçlıdır. Sahibi olmadığınız veya test etmek için açık izniniz olmayan herhangi bir sistemde bu saldırıyı denememelisiniz.
```

-----------------------------------------------------------------------------------
<b>DoS saldırısının ne olduğuyla başlayalım?</b>

```text
Hizmet Engelleme (DoS) saldırısı, hedef sistem, servis veya ağı aşırı trafik veya kaynak tüketen istekler ile bunaltma yöntemidir.
Amaç, hedefin kapasitesini tüketerek meşru kullanıcıların servise erişememesini sağlamaktır. DoS saldırıları genellikle sistemde yavaşlamaya veya tamamen erişilemez hale gelmeye neden olmak için istek limitlerini, protokol zayıflıklarını veya uygulama seviyesindeki darboğazları kullanır.
```

```text
Bu makalede sistemi kilitlemek için istek limiti zafiyetini kullanacağız.
```

-----------------------------------------------------------------------------------
<b>Test senaryomuz nedir?</b>

```text
Giriş ekranı olan özel bir backend üzerinde DoS saldırısı gerçekleştireceğiz. Sadece DoS saldırısının nasıl yapıldığını göstermek istediğimiz için backend ile Swagger üzerinden iletişim kuracağız.
```

-----------------------------------------------------------------------------------
<b>Hangi API endpoint’ine sahibiz bakalım?</b>

```text
Giriş endpoint’inin nickname ve password kabul ettiğini biliyoruz.
Diyelim ki bu servisi kilitlemek ve hiçbir kullanıcının giriş yapamamasını istiyorum.
```

![[static/dos_burp_suite/endpoint.png]]

-----------------------------------------------------------------------------------
<b>Saldırıyı Gerçekleştirme</b>

```text
1. Burp Suite’i açmamız ve intercept’i aktif etmemiz gerekiyor.
```

![[static/dos_burp_suite/enable_intercept.png]]

```text
2. Tarayıcımızı proxy ile Burp Suite’e bağlamamız gerekiyor.
```

![[static/dos_burp_suite/enable_proxy.png]]

```text
3. İsteği gönderelim ve yakalayalım.
```

![[static/dos_burp_suite/send_request.png]]

![[static/dos_burp_suite/catch_request.png]]

```text
4. Şimdi bu isteği repeater’a göndermemiz gerekiyor.
```

![[static/dos_burp_suite/send_to_repeater.png]]

```text
5. İsteği bir sekme grubuna ekleyin.
```

![[static/dos_burp_suite/req_to_tab_group.png]]

```text
6. İsteği çoğaltın. Toplam 20 tane bizim işimizi görür.
```

![[static/dos_burp_suite/duplicate_tab.png]]

```text
7. Gönderim türünü değiştirin.
```

![[static/dos_burp_suite/change_send_type.png]]

```text
8. Saldırıyı başlatın.
```

![[static/dos_burp_suite/start_attack.png]]

```text
9. Login endpoint’ini hâlâ kullanabiliyor muyuz bakalım.
```

![[static/dos_burp_suite/service_error.png]]


```text
10. İşe yaradı, artık diğer kullanıcılar bir süre endpoint’i kullanamıyor ve ben aynı isteği tekrar tekrar göndererek istediğim süre boyunca herkesi engelelyebilirim.
```

-----------------------------------------------------------------------------------
<b>Bu saldırının neden çalıştığına bakalım</b>

```text
Backend koduna bakarsak hız sınırlayıcısı olduğunu görebiliriz. Ancak sorun şu ki hız sınırlayıcıda IP gibi herhangi bir filtre yok. Bu nedenle tek bir kullanıcı diğer kullanıcılar için de sistemi kilitleyebiliyor.
```

![[static/dos_burp_suite/rate_limiter.png]]

-----------------------------------------------------------------------------------
<b>Peki… Bu kadar kolay mı?</b>

```text
Elbette hayır. 
Kaliteli tüm sistemlerde hataya dayanıklı hız sınırlama kuralları vardır. Çok fazla istek göndermek engellenmenize veya sadece sizi etkileyen bir hizmet engelleme yanıtı almanıza yol açar. Yani reddedilme yalnızca ağınıza uygulanır ve başkalarını etkilemez.
```

---

## <span id="en">English</span>

-----------------------------------------------------------------------------------
<b>Disclaimer</b>

```text
This article is for educational purposes only. You should not attempt this attack on any system you do not own or have explicit permission to test.
```

-----------------------------------------------------------------------------------
<b>Lets start with what is DoS attack?</b>

```text
A Denial of Service (DoS) attack is a method of overwhelming a target system, service, or network with excessive traffic or resource-consuming requests. 

The goal is to exhaust the target’s capacity so that legitimate users cannot access the service. DoS attacks typically exploit rate limits, protocol weaknesses, or application-level bottlenecks to force the system into slowdown or complete unavailability.
```

```text
In this article we will use rate limit vulnerability to lock the system.
```

-----------------------------------------------------------------------------------
<b>What is our test case?</b>

```text
We will execute DoS attack on a custom backend that has login. Since we are trying to only showcase how to execute DoS attack we will interact the backend by Swagger.
```

-----------------------------------------------------------------------------------
<b>Lets see what we got as api endpoint?</b>

```text
We know that login endpoint accepts nickname and password.
Lets say I want to lock this service so no user can be able to login.
```

![[static/dos_burp_suite/endpoint.png]]

-----------------------------------------------------------------------------------
<b>Executing The Attack</b>

```text
1. We need to open our Burp Suite and activate intercept.
```

![[static/dos_burp_suite/enable_intercept.png]]

```text
2. We need to connect our browser to Burp Suite by proxy.
```

![[static/dos_burp_suite/enable_proxy.png]]

```text
3. Lets send and catch the request.
```

![[static/dos_burp_suite/send_request.png]]

![[static/dos_burp_suite/catch_request.png]]

```text
4. Now we need to send this request to repeater.
```

![[static/dos_burp_suite/send_to_repeater.png]]

```text
5. Add request to a tab group
```

![[static/dos_burp_suite/req_to_tab_group.png]]

```text
6. Duplicate the request. Total of 20 will do for us.
```

![[static/dos_burp_suite/duplicate_tab.png]]

```text
7. Change send type
```

![[static/dos_burp_suite/change_send_type.png]]

```text
8. Start the attack
```

![[static/dos_burp_suite/start_attack.png]]

```text
9. Lets see if we can still use login endpoint.
```

![[static/dos_burp_suite/service_error.png]]


```text
10. It worked, now other users can't use the endpoint for some time and I can just send the same request again and again locking everyone out as long as I want.
```

-----------------------------------------------------------------------------------
<b>Lets look at why this attack worked</b>

```text
If we look at the backend code we can see that it has a rate limiter.
But the problem is rate limiter doesn't have any filters like IP.
Because of this one user can lock the system for other users too.
```

![[static/dos_burp_suite/rate_limiter.png]]

-----------------------------------------------------------------------------------
<b>So... Is it that easy?</b>

```text
Of course not.
Since all quality systems have error-proof rate limiting sending a lot of request will only get you banned or affect you meaning that you will get denial of service answer but the denial will be only for your network and won't affect the others. 
```
