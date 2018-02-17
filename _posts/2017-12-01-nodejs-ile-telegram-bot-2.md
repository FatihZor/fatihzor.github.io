---
layout: post
title:  "NodeJS ile Telegram Botu Zaafiyet Sorgulama"
image: 'http://stackresolve.com/assets/uploads/files/1497713671749-nodejs-telegram-bot.jpg'
date:   2017-12-07 00:06:31
tags:
- nodejs
- telegram bot
description: 'Bir önceki yazımızda gönderilen her mesaja mesaj alındı şeklinde cevap veren bir bot yapmıştık. Bu sefer ise API kullanan bir bot yapacağız. Amacımız tanımlı bir liste içerisinde bulunan wordpress eklentilerinden seçim yapan kullanıcıya o eklentinin zaafiyetlerini bildirmek.'
categories:
- NodeJS
- ChatBots
---


<img src="http://stackresolve.com/assets/uploads/files/1497713671749-nodejs-telegram-bot.jpg" alt="NodeJS ile Telegram Botu - Fatih Zor">


- Kullanılacak npm ```https://github.com/yagop/node-telegram-bot-api```
- Kullanılacak npm ```https://nodejs.org/api/https.html```

Bir önceki yazımızda gönderilen her mesaja "mesaj alındı" şeklinde cevap veren bir bot yapmıştık. Bu sefer ise API kullanan bir bot yapacağız. Amacımız tanımlı bir liste içerisinde bulunan wordpress eklentilerinden seçim yapan kullanıcıya o eklentinin zaafiyetlerini bildirmek. Önceki yazımızda oluşturduğumuz ```telegramBOT``` klasörüne giriyoruz. Daha önce ```node-telegram-bot-api``` paketini indirdiğimiz için bu klasöre artık indirmemize gerek yok. ```GET``` isteği göndereceğimiz site ```SSL``` kullandığı için ```npm install https``` komutu ile ```https``` NodeJS paketini sunucumuza kuruyoruz. Son olarak ```touch wpvuln.js``` komutu ile sunucumuzda javascript dosyamızı oluşturuyoruz.

{% highlight bash %}
cd telegramBOT
npm install https
touch myApp.js
nano myApp.js
{% endhighlight %}

Javascript dosyamızı oluşturduktan sonra ```nano wpvuln.js``` komutu ile dosyamızı düzenlemeye başlıyoruz. Dosyamızın en üst satırına oluşturacağımız bot için sabit değişkenleri yazıyoruz.


{% highlight javascript %}
const TelegramBot = require('node-telegram-bot-api');
const https = require('https');
const token = 'bot-father-token-bilgisi';
{% endhighlight %}

Bu bilgileri girdikten sonra botumuzu oluşturmak için npm paketimiz ve token bilgimizi kullanıyoruz. Ayrıca güncellemeleri kontrol etmesi için botumuzu oluştururken ```polling``` değişkeninin değerini ```true``` olarak belirtiyoruz. 

{% highlight javascript %}
const bot = new TelegramBot(token, {
    polling: true
});
{% endhighlight %}

Şimdi bir liste oluşturup içerisin bir kaç wordpress eklentisi ismi yazalım. Fakat, bunu kullanıcı bota erişip ```/start``` butonuna tıkladığında alt alta butonlar olacak şekilde yapalım. Kullanıcı botu ilk başlattığında kullanıcıya ismi ve kullanıcı adı ile hitap edeceğiz. Bunun için ```msg.from.first_name``` ve ```msg.from.username``` komutlarını, göndereceğimiz cevap string'ine ekleyeceğiz. 

{% highlight javascript %}
bot.onText(/\/start/, (msg) => {

    bot.sendMessage(msg.chat.id, "Hoşgeldin " + msg.from.first_name + (" @" + msg.from.username), {
        "reply_markup": {
            "keyboard": [
                ["userpro"],
                ["eshop"],
                ["qards"],
                ["wphrm"],
                ["formcraft3"],
                ["examapp"],
                ["AffiliateWP"],
                ["directdownload"]
            ]
        }
    });

});
{% endhighlight %}

Şimdi gelen eklenti ismini ```https://wpvulndb.com/api/v2/plugins/``` adresine ```GET``` isteği olarak göndereceğiz. Gönderdiğimiz ```GET``` isteği sonucu bize ```JSON``` veri olarak dönecektir. İlk olarak bir dizi oluşturuyoruz ve bu diziye butonlar için girdiğimiz eklenti listesinde bulunan eklenti isimlerini gireceğiz. 
{% highlight javascript %}const yourArray = ["userpro", "eshop", "qards", "wphrm", "formcraft3", "examapp", "AffiliateWP", "directdownload"]{% endhighlight %} 

Bu kodumuzdan sonra ```msg.chat.id``` değişkenini daha rahat kullanabilmek için bu değişkeni ```chatId``` isminde sabit bir değişkene aktarıyoruz. Değişkenleri oluşturduktan sonra bir koşul oluşturacağız. Bu koşul ile kullanıcının gönderdiği eklenti ismi bizim tanımladığımız dizi içerisinde bulunuyorsa zaafiyet sorgulama işlemi gerçekleşecek. Bu koşulu gerçekleştirebilmek için yazacağımız kod aşağıdaki gibidir. 
{% highlight javascript %}if (yourArray.indexOf(msg.text.toString()) > -1){% endhighlight %} 

Artık ```https://wpvulndb.com/api/v2/plugins/``` adresine ```GET``` isteği göndermeye hazırız. ```GET``` isteği gönderebilmek için ```https``` NodeJS paketini kullanacağız. ```GET``` isteği göndereceğimiz adresi ```url``` isminde bir değişken olarak oluşturuyoruz. 
{% highlight javascript %}
if (yourArray.indexOf(msg.text.toString()) > -1) {
        var url = 'https://wpvulndb.com/api/v2/plugins/' + msg.text.toString();
{% endhighlight %}

```GET``` isteği gönderdik ve artık gelen ```JSON``` veriyi işleyip kullanıcıya zaafiyetleri sıra sıra göndereceğiz. Bunu yaparken kullanıcının uygulamamıza sorduğu eklenti isimlerini görmek için ```console.log(chatId + " || " + msg.text.toString() + " || " + msg.from.first_name + " || " + msg.from.username);``` kodunu kullanacağız. 
{% highlight javascript %}
            res.on('end', function () {
                var data = JSON.parse(body);
                for (var item of data[msg.text.toString()]['vulnerabilities']) {
                    bot.sendMessage(chatId, "https:\/\/wpvulndb.com\/vulnerabilities\/" + item.id + "\n" + item.title);
                    console.log(chatId + " || " + msg.text.toString() + " || " + msg.from.first_name + " || " + msg.from.username);
                }
            });
{% endhighlight %}

<img src="https://i.hizliresim.com/a1ZPDR.png" alt="NodeJS ile Telegram Botu - Fatih Zor">

{% highlight javascript %}
const TelegramBot = require('node-telegram-bot-api');
const https = require('https');
const token = 'bot-father-token-bilgisi';

const bot = new TelegramBot(token, {
    polling: true
});

bot.onText(/\/start/, (msg) => {
    bot.sendMessage(msg.chat.id, "Hoşgeldin " + msg.from.first_name + (" @" + msg.from.username), {
        "reply_markup": {
            "keyboard": [
                ["userpro"],
                ["eshop"],
                ["qards"],
                ["wphrm"],
                ["formcraft3"],
                ["examapp"],
                ["AffiliateWP"],
                ["directdownload"]
            ]
        }
    });
});


bot.on('message', (msg) => {
    const yourArray = ["userpro", "eshop", "qards", "wphrm", "formcraft3", "examapp", "AffiliateWP", "directdownload"]
    const chatId = msg.chat.id;
    if (yourArray.indexOf(msg.text.toString()) > -1) {
        var url = 'https://wpvulndb.com/api/v2/plugins/' + msg.text.toString();
        https.get(url, function (res) {
            var body = '';

            res.on('data', function (chunk) {
                body += chunk;
            });

            res.on('end', function () {
                var data = JSON.parse(body);
                for (var item of data[msg.text.toString()]['vulnerabilities']) {
                    bot.sendMessage(chatId, "https:\/\/wpvulndb.com\/vulnerabilities\/" + item.id + "\n" + item.title);
                    console.log(chatId + " || " + msg.text.toString() + " || " + msg.from.first_name + " || " + msg.from.username);
                }
            });

        }).on('error', function (e) {
            console.log("Bir hata oldu: ", e);
            bot.sendMessage(chatId, msg.text.toString() + ' Bir şeyler ters gitti :) Gönderdiğiniz kayıt incelenecektir.');
        });
    }
});
{% endhighlight %}
