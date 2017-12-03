---
layout: post
title:  "NodeJS ile Telegram Botu İlk Uygulama - Fatih Zor"
image: ''
date:   2017-12-01 00:06:31
tags:
- nodejs
- telegram bot
description: ''
categories:
- NodeJS
- ChatBots
---


- Kullanılacak npm ```https://github.com/yagop/node-telegram-bot-api```

İlk olarak kullanacağımız NodeJS paketimizi sunucumuza kurmamız gerekiyor. Paketimiz kurulduktan sonra dizinimizin içerisine herhangi bir javascript dosyası oluşturup kodlarımızı bu javascript dosyasının içerisine yazacağız.

{% highlight bash %}
mkdir telegramBOT
cd telegramBOT
npm install --save node-telegram-bot-api
touch myApp.js
{% endhighlight %}



