---
layout: post
title:  "Cypress Nedir, Nasıl Kullanılır?"
categories: [ Node.js, Cypress ]
author: fatih
image: assets/images/cypress-io-logo-social-share.png
---
Cypress, modern web uygulamaları için tasarlanmış açık kaynak bir front-end test aracıdır.

### Kurulum

Kurulum için [Node.js][node-js] gerekmektedir.
Node.js kurulumunu tamamladıktan sonra, proje dizinine ilerliyoruz.

```cd proje/dizini```

Örnek kullanım: ```cd C:\Users\work\Desktop\myproject```

Proje dizinimizde kurulumu gerçekleştirmek için npm paket yöneticisini kullanacağız.

```npm install cypress --save-dev```

![cypress kurulum]({{ site.baseurl }}/assets/images/cypress1.png)

Kurulum tamamlandıktan sonra Cypress uygulamasını çalıştırmak için gerek komutu giriyoruz.

```node_modules\.bin\cypress open```

Cypress uygulaması açıldığında, testleri hangi klasörde yazmamız gerektiğini gösteriyor. Bu kısımda aşağıda gösterilen sıra ile linklere tıklıyoruz.

![cypress ilk ekran]({{ site.baseurl }}/assets/images/cypress2.png)

Açılan klasörde yeni bir dosya oluşturarak ismini ```my-test.js``` yapalım. Eğer Javascript dosyası doğru klasörde açılmış ise Cypress uygulamasında dosyamızı görebiliriz.

![cypress ilk test dosyası]({{ site.baseurl }}/assets/images/cypress3.PNG)

Şimdi bir metin editörü ile ```my-test.js``` dosyamızı açalım. Metin editörleri arasında benim tercihim [Visual Studio Code][vs-code]. Testimizi Twitter üzerinde yapacağız. İlk olarak twitter giriş sayfasını açmalıyız.

{% highlight javascirpt %}
describe('Twitter Test', function () {
    it('Twitter ziyaret et', function () {
        cy.visit('https://twitter.com/login')
    })
})
{% endhighlight %}

Kodumuzu yazdıktan sonra ```my-test.js``` dosyamızı kaydediyoruz. Daha sonra Cypress uygulamasına dönerek ```my-test.js``` dosyasına tıklıyoruz. Test çalışmaya başlayarak ```https://twitter.com/login``` linkini ziyaret edecektir.

![cypress ilk test]({{ site.baseurl }}/assets/images/cypress4.PNG)

Yazının devamı için [Cypress Nasıl Kullanılır? - 2][sonra]

[node-js]: https://nodejs.org/en/download/
[vs-code]: https://code.visualstudio.com/docs/setup/setup-overview
[sonra]: https://fatihzor.github.io/cypress-nasil-kullanilir-2/