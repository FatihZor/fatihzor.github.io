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

* PyCharm'ı açarak yeni bir proje oluşturalım. Sunucudaki klasör ismi ile aynı olma zorunluluğu yok fakat ben buradaki projemin isminide ```projects``` yaptım. Bilgisayarımızda bulunan herhangi bir python interpreter'i seçerek devam ediyorum.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/3.png)

* Şimdi ``` File > Settings ``` menüsü veya <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>S</kbd> ile PyCharm'ın ayarlarını açalım. Bu alanda arama kısmına ```deployment``` yazıp arıyoruz. Sonra gelen ekranda ```Deployment``` menüsünü seçerek ```Add Server``` butonuna tıklıyoruz.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/4.png)

* ```Add Server``` menüsünde bir isim belirleyerek yapılacak bağlantının türünü belirliyoruz. Burada PyCharm'ın dosyaları SSH üzerinden alıp-vermesi için SFTP seçiyorum.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/5.png)

* Artık sunucu bilgilerimizi girerek ayarlarımız uygulayabiliriz.
  * SFTP host -> Sunucumuzun IP bilgisi girilmelidir.
  * Port -> Tanımlı olarak 22 geliyor.
  * Root path -> PowerShell üzerinde aktif olan SSH bağlantımızda sunucu üzerinde oluşturduğunuz projects klasörüne giderek, burada ```pwd``` komutunu yazalım. Sunucudan gelen dizin bilgisi bu alana yazılacak. ```(/home/work/projects)```
  * Username -> Sunucu için belirlediğimiz ve sunucuya bağlanırken kullandığımız kullanıcı adı.
  * Auth type -> Azure üzerinde sanal makineyi (sunucuyu) oluştururken SSH üzerinden bağlanma işleminin parola ile gerçekleşeceğini belirtmiştik. Bu yüzden ```Password``` seçiyoruz.
  * Password -> Sunucu için belirlediğimiz ve sunucuya bağlanırken kullandığımız parola
  * Save password -> Sürekli parola sormaması için ben bunu seçili hale getiriyorum. Fakat, bunun oluşturacağı güvenlik risklerini göz önüne alırsak aktif olmasını önermem.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/6.png)

* Bağlantı ayarlarımızı yaptıktan sonra ```Mappings``` sekmesine tıklayarak bu kısımda gerekli ayarları yapıp uygula diyoruz.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/u1.png)

* Deployment ayarlarımızı uyguladıktan sonra tekrar arama kısmına ```interpreter``` yazarak arıyoruz. Ayarlar butonuna tıklayarak ```Add...``` seçeneğini seçiyoruz.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/7.png)
![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/8.png)

* Artık son adımdayız. Bu kısımda sunucu üzerinde oluşturduğumuz workpy environment içerisinde yer alan Python uygulamasının yolunu yazalım ve ```Sync folders``` alanında yer alan ```/tmp/pycharm_....``` bilgisini kaldıralım ve ```Finish``` butonuna tıklayalım. Bu ekran kapandıktan sonra ayarlar ekranına geri dönecektir. Bu ekranda önce ```Apply``` sonra ```Ok``` butonlarına tıklayalım.

![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/9.png)
![pycharm ve azure]({{ site.baseurl }}/assets/images/pycharmazure/10.png)

Yukarıdaki adımlar yapıldıktan sonra PyCharm sunucu bilgilerini doğrulayacak ve birkaç dosya alışverişi yapacaktır. Bu işlemin süresi internet hızınıza bağlı olarak değişmektedir. 

## İlk Uygulama

