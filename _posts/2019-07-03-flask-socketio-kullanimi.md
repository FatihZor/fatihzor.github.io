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

HTML dosyamıza socketio ve jquery javascirpt kütüphanelerimizi ekleyelim.
{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>INDEX</title>
</head>
<body>


<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js" integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/2.2.0/socket.io.js" integrity="sha256-yr4fRk/GU1ehYJPAs8P4JlTgu0Hdsp4ZKrx8bDEDC3I=" crossorigin="anonymous"></script>
</body>
</html>
{% endhighlight %}

İlk denememiz sokete biri bağlandığında diğer kullanıcıları uyarmak olacak.

```app.py``` dosyası
{% highlight python %}
from flask import Flask, render_template
from flask_socketio import SocketIO, send, emit
from flask_cors import CORS

app = Flask(__name__)
app.config['SECRET_KEY'] = 'secret!'
sio = SocketIO(app)
CORS(app)

@app.route('/')
def index():
    return render_template('index.html')

@sio.on('connect')
def connect_message():
    emit('new_user', {'data': 'yeni kullanici baglandi'}, broadcast=True)

if __name__ == '__main__':
    sio.run(app, host="0.0.0.0", port=8080)
{% endhighlight %}

```index.html``` dosyası
{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>INDEX</title>
</head>
<body>

<div id="soket"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js" integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/2.2.0/socket.io.js" integrity="sha256-yr4fRk/GU1ehYJPAs8P4JlTgu0Hdsp4ZKrx8bDEDC3I=" crossorigin="anonymous"></script>
<script type="text/javascript" charset="utf-8">
    var socket = io();
    socket.on('connect', function() {
    });
    socket.on('new_user', function(gelen_veri) {
        $('#soket').append("<p>" + gelen_veri['data'] + "</p>")
    });
</script>
</body>
</html>
{% endhighlight %}

### Neden Flask-CORS Kullandık?
CORS (Cross-Origin Resource Sharing) teriminin Türkçe karşılığı Kökler Arası Kaynak Paylaşımı demek. CORS hatası ile daha önce karşılaştığım için ekledim. Javascript ile uygulamama istek atarken karşılaştığım bir hatayı çözmek için bu kütüphaneyi kullanmıştım. CORS hakkında detaylı bilgiye Gökhan Şengün'ün [bu yazısından](https://medium.com/@gokhansengun/cors-nedir-ve-ne-i%C5%9Fe-yarar-27006d85bf54) ulaşabilirsiniz.

### Neden emit() Kullandık?
SocketIO da belirli bir fonksiyona veri göndermek istiyorsak ```emit()``` kullanılır. ```emit()``` fonksiyonun ilk parametresi veriyi göndermek istediğimiz fonksiyonun ismi olmalıdır.

### Neden broadcast Kullandık?
```broadcast``` sokete bağlı olan tüm kullanıcıları/istemcileri bilgilendirmek için kullanılır. ```broadcast``` seçeneği aktif ise gönderende dahil olmak üzere herkes mesajı alır. 

Bu yazımı yazarken hem soket programlama öğrenip hem de sizlere anlatmaya çalıştım. Hatalı olduğum kısımları twitter üzerinden bildirmeyi unutmayın. 