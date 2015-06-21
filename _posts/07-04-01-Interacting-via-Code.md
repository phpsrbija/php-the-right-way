---
isChild: true
title: Interakcija sa bazom podataka
anchor: databases_interacting
---

## Interakcija sa bazom podataka {#databases_interacting_title}

Kada programeri počnu da uče PHP, obično dođu u situaciju da mešaju logiku interakcije sa bazom i
prezentacione logike, kao na primer u ovom slučaju:

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
?>
</ul>
{% endhighlight %}

Ovo je loša praksa iz više razloga, a ponajviše zbog toga što je ovakav kôd teško debug-ovati,
testirati i uopšte čitati i prikazaće previše polja ukoliko ne postavite limit.

Iako postoji dosta načina da se interakcija ostvari, u zavisnosti da li preferirate
[OOP](#object_oriented_programming) ili [proceduralno programiranje](#functional_programming),
mora postojati taj aspekt razdvajanja logike.

Razmotrimo ovaj osnovni korak:

{% highlight php %}
<?php
function getAllFoos($db) {
    return $db->query('SELECT * FROM table');
}

foreach (getAllFoos($db) as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // LOŠE!!
}
{% endhighlight %}

Ovo je dobar početak. Ako stavite ova dva segmenta u dva zasebna fajla imaćete čisto razdvajanje.

Napravite klasu sa ovim metodama i imate "Model". Napravite jednostavan `.php` fajl sa
prezentacionom logikom i imate "View", što je dosta blizu [MVC-a] &mdash; najčešćeg koncepta u
većini [framework-ova](#frameworks_title).

**foo.php**

{% highlight php %}
<?php
$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8', 'username', 'password');

// Učitajte klasu modela
include 'models/FooModel.php';

// Kreirajte instancu
$fooModel = new FooModel($db);
// Dohvatite listu svih entiteta
$fooList = $fooModel->getAllFoos();

// Prikažite view
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class FooModel
{
    protected $db;

    public function __construct(PDO $db)
    {
        $this->db = $db;
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<?php foreach ($fooList as $row): ?>
    <?= $row['field1'] ?> - <?= $row['field1'] ?>
<?php endforeach ?>
{% endhighlight %}

Ovo u suštini radi i većina modernih framework-ova. Možda nećete imati stalnu potrebu za ovim, ali
mešanje logike interakcije sa bazom i prezentacione logike može biti ozbiljan problem ako ikada
budete želeli da pišete [unit testove](#unit-testing) za vašu aplikaciju.

[PHPBridge] ima sjajan članak na sličnu temu nazvan [Kreiranje Data klase], koji je odličan za
programere koji se tek uhodavaju sa konceptom interakcije sa bazom podataka.

[MVC]: http://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488
[PHPBridge]: http://phpbridge.org/
[Kreiranje Data klase]: http://phpbridge.org/intro-to-php/creating_a_data_class
