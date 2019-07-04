---
layout: post
title:  "Flask-SocketIO Kullanımı"
categories: [ Python, Flask ]
author: fatih
image: assets/images/flasksocket.png
---

SocketIO hız ve güvenilirliğe odaklanan gerçek zamanlı, çift yönlü (bidirectional) ve olaya dayalı (event-based) iletişimi sağlar. Her platformda, tarayıcıda veya cihazda çalışabilir. Flask-SocketIO ise Flask tabanlı web uygulamalarında kullanabileceğimiz soketler için oluşturulmuş bir kütüphanedir. Herhangi bir SocketIO istemcisi ile erişilebilir ve kullanılabilir. 

### İşletim Sistemi
* Ubuntu 18.04

### Uygulama Sürümleri
* Python 3.6.7
* pip 19.0.3 from (python 3.6)

### Kütüphane Sürümleri
* Flask==1.0.3
* Flask-Cors==3.0.8
* Flask-SocketIO==4.1.0

İlk olarak kütüphanemizin kurulumunu gerçekleştirelim.
{% highlight bash %}
pip3 install flask-socketio
{% endhighlight %}

Aşağıdaki gibi bir klasör düzeni oluşturalım.

- soket
  - templates
  - static
  - app.py

```app.py``` dosyamıza ilk olarak kütüphaneleri ekleyelim.
{% highlight python %}
from flask import Flask, render_template
from flask_socketio import SocketIO, send, emit
from flask_cors import CORS
{% endhighlight %}

Kütüphaneleri ekledikten sonra soket ve web uygulamamızın çalışabilmesi için gerekli kodları ekleyelim.
{% highlight python %}
app = Flask(__name__)
app.config['SECRET_KEY'] = 'secret!'
sio = SocketIO(app)
CORS(app)

#flask ve soket kodları buraya gelecek

if __name__ == '__main__':
    sio.run(app, host="0.0.0.0", port=8080)
{% endhighlight %}

Şimdi ```templates``` klasörünün içerisine ```index.html``` dosyası oluşturalım. Bu html dosyasına erişebilmek için gereken flask yönlendirmesini ```app.py``` dosyasına ekleyelim. 
{% highlight python %}
@app.route('/')
def index():
    return render_template('index.html')
{% endhighlight %}