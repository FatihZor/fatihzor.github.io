---
layout: post
title:  "PyCharm ve Azure"
author: fatih
categories: [ Python, Azure ]
image: assets/images/python.jpg
tags: [python]
---

Bu yazımda PyCharm ile Microsoft Azure üzerinde Python uygulamalarının SSH üzerinden nasıl geliştirileceğine değinmek istiyorum. Eğer öğrenci iseniz ve Microsoft Azure hesabınız yoksa, bu yazıya başlamadan önce aşağıdaki iki yazıyı okumanız faydalı olacaktır. Ek olarak öğrenciler için PyCharm uygulamasını indirirek PyCharm uygulamasının ```Professional``` sürümüne sahip olabilirsiniz.

* [Öğrenciler İçin Azure](https://fatihzor.github.io/ogrenciler-icin-azure/){:target="_blank"}
* [Azure Sanal Makine Oluşturma](https://fatihzor.github.io/azure-sanal-makine-olusturma/){:target="_blank"}
* [Öğrenciler İçin PyCharm](https://www.jetbrains.com/student/){:target="_blank"}

## Sanal Makinede Python Environment Oluşturma

[Python Virtual Environment nedir?](https://yazilimportal.com/python-virtual-environment-8d50f5bae0d7){:target="_blank"}

Sunucuya SSH ile bağlanıp güncellemeleri yaparak ```virtualenv``` paketini yüklüyoruz ve ```virtualenv -p python3 workpy``` komutu ile ```workpy``` isimli bir Pyton 3 Environment oluşturuyoruz.

{% highlight bash %}
work@python:~$ sudo apt update
work@python:~$ sudo apt upgrade
work@python:~$ sudo apt install virtualenv
work@python:~$ virtualenv -p python3 workpy
{% endhighlight %}

Environment oluşturulduktan sonra ```source workpy/bin/activate``` ile aktif hale getirelim. Şimdi ```python -V``` komutu ile python sürümünü kontrol edelim. Son olarak proje dosyaları için ```mkdir projects``` komutu ile sunucuda ```projects``` isimli bir klasör oluşturalım.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/2.png)

## PyCharm Ayarlarının Yapılması

1) PyCharm'ı açarak yeni bir proje oluşturalım. Sunucudaki klasör ismi ile aynı olma zorunluluğu yok fakat ben buradaki projemin isminide ```projects``` yaptım. Bilgisayarımızda bulunan herhangi bir python interpreter'i seçerek devam ediyorum.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/3.png)

2) Şimdi ``` File > Settings ``` menüsü veya <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>S</kbd> ile PyCharm'ın ayarlarını açalım. Bu alanda arama kısmına ```deployment``` yazıp arıyoruz. Sonra gelen ekranda ```Deployment``` menüsünü seçerek ```Add Server``` butonuna tıklıyoruz.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/4.png)

3) ```Add Server``` menüsünde bir isim belirleyerek yapılacak bağlantının türünü belirliyoruz. Burada PyCharm'ın dosyaları SSH üzerinden alıp-vermesi için SFTP seçiyorum.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/5.png)