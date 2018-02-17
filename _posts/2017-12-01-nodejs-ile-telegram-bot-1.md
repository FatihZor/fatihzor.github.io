---
layout: post
title:  "NodeJS ile Telegram Botu Ilk Uygulama"
feature-img: 'assets/img/bot.jpg'
date:   2017-12-02 00:06:31
tags:
- nodejs
- telegram bot
description: 'İlk olarak kullanacağımız NodeJS paketimizi sunucumuza kurmamız gerekiyor. Paketimiz kurulduktan sonra dizinimizin içerisine herhangi bir javascript dosyası oluşturup kodlarımızı bu javascript dosyasının içerisine yazacağız.'
categories:
- NodeJS
- ChatBots
---


<img src="http://stackresolve.com/assets/uploads/files/1497713671749-nodejs-telegram-bot.jpg" alt="NodeJS ile Telegram Botu - Fatih Zor">


- Kullanılacak npm ```https://github.com/yagop/node-telegram-bot-api```

İlk olarak kullanacağımız NodeJS paketimizi sunucumuza kurmamız gerekiyor. Paketimiz kurulduktan sonra dizinimizin içerisine herhangi bir javascript dosyası oluşturup kodlarımızı bu javascript dosyasının içerisine yazacağız.

{% highlight bash %}
mkdir telegramBOT
cd telegramBOT
npm install --save node-telegram-bot-api
touch myApp.js
nano myApp.js
{% endhighlight %}

Javascript dosyamızı oluşturduktan sonra ```nano myApp.js``` komutu ile dosyamızı düzenlemeye başlıyoruz. Dosyamızın en üst satırına oluşturacağımız bot için sabit değişkenleri yazıyoruz.


{% highlight javascript %}
const TelegramBot = require('node-telegram-bot-api');
const token = 'bot-father-token-bilgisi';
{% endhighlight %}

Bu bilgileri girdikten sonra botumuzu oluşturmak için npm paketimiz ve token bilgimizi kullanıyoruz. Ayrıca güncellemeleri kontrol etmesi için botumuzu oluştururken ```polling``` değişkeninin değerini ```true``` olarak belirtiyoruz. 

{% highlight javascript %}
const bot = new TelegramBot(token, {
    polling: true
});
{% endhighlight %}

Ön hazırlıkları tamamladık ve artık botumuzun kullanıcıdan gelecek mesajlara tepki vermesi için son olarak basit bir kod daha ekliyoruz bu aşamada botumuz gelen her mesaja aynı tepkiyi verecektir. 

{% highlight javascript %}
bot.on('message', (msg) => {
    const chatId = msg.chat.id;
  
    bot.sendMessage(chatId, 'mesaj alındı');
}); 
{% endhighlight %}

Dosyamıza eklediğimiz son kod parçası ile dosyamızın içeriği aşağıdaki şekilde olacaktır. 

{% highlight javascript %}
const TelegramBot = require('node-telegram-bot-api');
const token = 'bot-father-token-bilgisi';

const bot = new TelegramBot(token, {
    polling: true
});

bot.on('message', (msg) => {
    const chatId = msg.chat.id;
  
    bot.sendMessage(chatId, 'mesaj alındı');
}); 
{% endhighlight %}
