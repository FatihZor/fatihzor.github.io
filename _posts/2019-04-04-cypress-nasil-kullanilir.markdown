---
layout: post
title:  "Cypress Nasıl Kullanılır?"
categories: [ Node.js ]
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

![kurulum]({{ site.baseurl }}/assets/images/cypress1.png)

Kurulum tamamlandıktan sonra Cypress uygulamasını çalıştırmak için gerek komutu giriyoruz.

```node_modules\.bin\cypress open```

Cypress uygulaması açıldığında, testleri hangi klasörde yazmamız gerektiğini gösteriyor. Bu kısımda aşağıda gösterilen sıra ile linklere tıklıyoruz.

![klasör]({{ site.baseurl }}/assets/images/cypress2.png)

Açılan klasörde yeni bir dosya oluşturarak ismini ```my-test.js``` yapalım. Eğer Javascript dosyası doğru klasörde açılmış ise Cypress uygulamasında dosyamızı görebiliriz.

![cypress]({{ site.baseurl }}/assets/images/cypress3.png)


{% highlight javascirpt %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

[node-js]: https://nodejs.org/en/download/
