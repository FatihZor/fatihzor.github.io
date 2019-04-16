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

Sunucuya SSH ile bağlan

{% highlight bash %}
work@python:~$ sudo apt update
work@python:~$ sudo apt upgrade
work@python:~$ sudo apt install virtualenv
{% endhighlight %}
