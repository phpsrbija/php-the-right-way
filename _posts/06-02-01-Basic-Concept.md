---
isChild: true
title: Osnovni koncept
anchor: basic_concept
---

## Osnovni koncept {#basic_concept_title}

Ovaj koncept se može demonstrirati jednim jednostavnim primerom.

Imamo klasu `Database` koja zahteva adapter kako bi komunicirala sa bazom podataka. Instanciranjem adaptera
direktno u konstruktoru kreiramo "čvrstu" zavisnost. Ovo znatno otežava testiranje i čini klasu `Database`
usko vezanom za konkretnu adapter implementaciju.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

Ovaj kôd možemo refaktorisati na način da koristi Dependency Injection princip, sa ciljem da "olabavimo" zavisnost.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(MySqlAdapter $adapter)
    {
        $this->adapter = $adapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

Sada klasi `Database` ubacujemo njen dependency umesto da ga ona sama kreira. Mogli smo čak da napravimo i
metod za njegovo postavljanje, ili u slučaju da je polje `$adapter` javno, mogli smo da ga postavimo direktno.
