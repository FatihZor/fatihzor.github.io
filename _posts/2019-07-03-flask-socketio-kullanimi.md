---
layout: post
title:  "Flask-SocketIO Kullanımı"
categories: [ Python, Flask ]
author: fatih
image: assets/images/flasksocket.png
---

SocketIO hız ve güvenilirliğe odaklanan gerçek zamanlı, çift yönlü (bidirectional) ve olaya dayalı (event-based) iletişimi sağlar. Her platformda, tarayıcıda veya cihazda çalışabilir. Flask-SocketIO ise Flask tabanlı web uygulamalarında kullanabileceğimiz soketler için oluşturulmuş bir kütüphanedir. Herhangi bir SocketIO istemcisi ile erişilebilir ve kullanılabilir. 

İşletim Sistemi
* Ubuntu 18.04

Uygulama Sürümleri
* Python 3.6.7
* pip 19.0.3 from (python 3.6)

Kütüphane Sürümleri
* Flask==1.0.3
* Flask-Cors==3.0.8
* Flask-SocketIO==4.1.0

İlk olarak kütüphanemizin kurulumunu gerçekleştirelim.
{% highlight bash %}
pip3 install flask-socketio
{% endhighlight %}