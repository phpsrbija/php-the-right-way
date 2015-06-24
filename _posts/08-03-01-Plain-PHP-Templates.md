---
isChild: true
title: Nativni PHP templejti
anchor: plain_php_templates
---

## Nativni PHP templejti {#plain_php_templates_title}

Nativni PHP templejti u osnovi koriste standardnu PHP sintaksu. Oni predstavljaju logičan izbor
pošto je PHP sam po sebi templejt jezik. Ovo znači da je moguće kombinovati PHP kôd u okviru nečeg
drugog, kao što je HTML. Ovo dosta znači PHP programerima, jer nije neophodno učiti novi sintaksu,
znaju koje su im funkcije dostupne, a njihovi editori omogućavaju isticanje (highlighting) sintakse,
kao i auto-complete. Takođe, nativni PHP templejti su veoma brzi imajući u vidu da u njihovom slučaju
nije potrebno kompajliranje.

Svaki moderan PHP frejmvork poseduje neku vrstu templejt sitema, pri čemu većina podrazumevano
koristi nativan PHP. Pored frejmvorka, biblioteke kao [Plates][plates] i [Aura.View][aura]
omogućavaju jednostavniji rad sa nativnim PHP templejetima, putem funkcionalnosti kao što su
nasleđivanje, _layout-i_ i ekstenzije.

### Jednostavan primer nativnog PHP templejta

Primer baziran na [Plates][plates] biblioteci.

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->insert('header', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>

<?php $this->insert('footer') ?>
{% endhighlight %}

### Primer nativnog PHP templejta koji koristi nasleđivanje

Primer baziran na [Plates][plates] biblioteci.

{% highlight php %}
<?php // template.php ?>

<html>
<head>
    <title><?=$title?></title>
</head>
<body>

<main>
    <?=$this->section('content')?>
</main>

</body>
</html>
{% endhighlight %}

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->layout('template', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>
{% endhighlight %}


[plates]: http://platesphp.com/
[aura]: https://github.com/auraphp/Aura.View
