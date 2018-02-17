---
layout: post
title:  "NodeJS ile Telegram Botu"
feature-img: 'http://stackresolve.com/assets/uploads/files/1497713671749-nodejs-telegram-bot.jpg'
date:   2017-12-01 00:06:31
tags:
- nodejs
- telegram bot
description: 'ChatBot, kullanıcılarından gelen mesajları analiz edip bu mesajlara en uygun cevapları veren server-side uygulamalardır. Yapay zekanın gelişmesi ile ortaya çıkan bu uygulamalar firmalar için büyük kolaylıklar yaratabilecek nitelikte. '
categories:
- NodeJS
- ChatBots
---

<img src="http://stackresolve.com/assets/uploads/files/1497713671749-nodejs-telegram-bot.jpg" alt="NodeJS ile Telegram Botu - Fatih Zor">


## ChatBot nedir?

ChatBot, kullanıcılarından gelen mesajları analiz edip bu mesajlara en uygun cevapları veren server-side uygulamalardır. Yapay zekanın gelişmesi ile ortaya çıkan bu uygulamalar firmalar için büyük kolaylıklar yaratabilecek nitelikte. 


## ChatBot ile neler yapılabilir?

- Skype uygulamasından bir uçak bileti alınılabilir ```https://join.skype.com/bot/57bfbc6f-1556-46fc-b4fa-41ea57b26df```
- Telegram uygulamasında oyun oynanabilir ```https://storebot.me/bot/telehackerobot```
- Facebook Messenger platformundan pizza siparişi verilebilir ```https://www.facebook.com/messages/t/Dominos```

## Başlarken

ChatBot yapımı için en çok kullanılan program dillerinden biri NodeJS programlama dilidir. Bende bu programlama dilini kullanarak basit bir telegram botu yapmaya çalışacağım.

Uygulama aşamasına geçmeden önce [Microsoft Azure](https://azure.microsoft.com/tr-tr/services/virtual-machines/) üzerinde Ubuntu işletim sistemine sahip sanal bir sunucu kuruyorum. Bu sunucunun 80 numaralı http portunun güvenlik ayarlarını gelen ve giden tüm bağlantılara izin verecek şekilde ayarlıyorum. 

Sunucumuzda gereken ayarları yaptıktan sonra Telegram uygulamasına giderek [BotFather](https://telegram.me/BotFather) botu ile yeni bir bot oluşturup token bilgisini alıyorum. 

<img src="https://i.hizliresim.com/4Gy6p7.png" alt="NodeJS ile Telegram Botu - Fatih Zor">