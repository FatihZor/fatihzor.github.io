---
layout: post
title:  "Cypress Nasıl Kullanılır? - 2"
categories: [ Node.js, Cypress ]
image: assets/images/cypress-io-logo-social-share.png
---

[Bir önceki yazımızda][ilk] Cypress'in nasıl kurulduğunu ve test ortamının nasıl oluşturulduğunu anlatmıştık. Bu yazımızda ise ilk testimizi tamamlayarak Twitter uygulamasına giriş yapacağız.

```https://twitter.com/login``` adresini ziyaret ettikten sonra sayfada bulunan ```input``` elementlerlerine gerekli bilgileri yazmalıyız. Öncelikle kaynağı görüntüle diyerek form elementlerini nasıl seçebiliriz ona bakalım.

{% highlight html %}
<form action="https://twitter.com/sessions" class="t1-form clearfix signin js-signin" method="post">
    <fieldset>

        <legend class="visuallyhidden">Giriş yap</legend>

        <div class="clearfix field">
            <input
            class="js-username-field email-input js-initial-focus"
            type="text"
            name="session[username_or_email]"
            autocomplete="on" value=""
            placeholder="Telefon, e-posta veya kullanıcı adı"
            />
        </div>
        <div class="clearfix field">
            <input class="js-password-field" type="password" name="session[password]" placeholder="Şifre">
        </div>

        <input type="hidden" value="e112cb319ade0c0c538bc87c2b6a7c802f02e910" name="authenticity_token"/>

        <input type="hidden" name="ui_metrics" autocomplete="off">
        <script src="/i/js_inst?c_name=ui_metrics" async></script>

    </fieldset>

    <div class="captcha js-captcha">
    </div>
    <div class="clearfix">

    <input type="hidden" name="scribe_log">
    <input type="hidden" name="redirect_after_login" value="">
    <input type="hidden" value="e112cb319ade0c0c538bc87c2b6a7c802f02e910" name="authenticity_token"/>
    <button type="submit" class="submit EdgeButton EdgeButton--primary EdgeButtom--medium">Giriş yap</button>
{% endhighlight %}

Formda doldurmamız gereken 2 ```input``` elementi ve tıklamamız gereken 1 ```button``` elementi var. Elementleri seçmek için ```class``` özellikleri kullanılabilir. Şimdi kodumuzu düzenleyerek Twitter uygulamasına giriş yapalım.

{% highlight javascript %}
describe('Twitter Test', function () {
    it('Twitter ziyaret et', function () {
        cy.visit('https://twitter.com/login')

        cy.get('.js-username-field')
          .type('fatihhzor')
        
        cy.get('.js-password-field')
          .type('şifre')

        cy.get('[class = "submit EdgeButton EdgeButton--primary EdgeButtom--medium"]').click()
    })
})
{% endhighlight %}

![cypress twitter giriş yap]({{ site.baseurl }}/assets/images/cypress5.png)

Böylece Cypress ile ilk testimizi tamamladık.

[ilk]: https://fatihzor.github.io/cypress-nasil-kullanilir/