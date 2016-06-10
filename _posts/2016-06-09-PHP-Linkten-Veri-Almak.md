---
layout: post
title:  "PHP Linkten Veri Almak"
date:   2016-05-12
excerpt: "Php ile linkten veri alıp değişkene yazdırarak bir çok sorgu çalışması yapabiliriz."
tag:
- PHP
- $_GET
- Linkten Veri Almak
comments: false
---

Örneğin bazı sitelerde şu tarz linklere denk gelmiş olabilirsiniz.

xaesitesi.com/?id=1
{: .notice}

Linkte `?id=1` kısmı sayfaya gönderilen veri oluyor. 

## Peki bunu nasıl kullanırız?

{% highlight php %}
<?php
if (empty($_GET)) {
    $link = 2;
}
elseif($_GET['id'] == null) 
$link = 1;
else
$link = ($_GET['id']);
?>

<?php echo $link ?>
{% endhighlight %}

* `$link` değişken ismidir.
* `$_GET['id']` url'de bulunan tanımdır.

* `xaesitesi.com/?id=0` linki için ekrana `0` yazdırılacaktır.
* `xaesitesi.com/?id` ve `xaesitesi.com/?id=` linkleri için ekrana `1` yazdırılacaktır.
* `xaesitesi.com` linki için ekrana `2` yazdırılacaktır.