---
layout: post
title:  "C# IsMdiContainer Özelliği"
date:   2016-05-12
excerpt: "C# dili ile bir form içerisinde birden fazla form ve döküman üzerinde çalışmayı anlamaya çalışalım."
tag:
- C#
- IsMdiContainer
comments: false
---

## C# IsMdiContainer Özelliği

Bu özellik büyük boyutlu ve/veya birden çok form ile çalıştığımız uygulamalar için önem arz ediyor. 

#### Nasıl kullanacağız?

* Öncelikle Visual Studio'da yeni bir form uygulaması oluşturalım.
* Daha sonra bu uygulamamıza bir adet daha form ekleyeleim.
* Ana form View Code özelliğinde açalım. (VS2015 Kısayolu : <kbd>F7</kbd>)

İki adet formumuz var. Ana formun ismi : mainform | Diğer form childform olsun. 
{: .notice}



{% highlight c# %}
IsMdiContainer = true;
	childform cf = new childform();
	cf.Show();
	cf.FormBorderStyle = FormBorderStyle.None;
	cf.MdiParent = this;
{% endhighlight %}

