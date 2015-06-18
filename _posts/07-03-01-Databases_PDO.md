---
isChild: true
title: PDO ekstenzija
anchor: pdo_extension
---

# PDO ekstenzija {#pdo_extension_title}

[PDO] je biblioteka za apstrakciju povezivanja sa bazom podataka &mdash; dostupna od verzije PHP
5.1.0 &mdash; koja obezbeđuje zajednički interfejs za komunikaciju sa više različitih tipova baza podataka.
Tako na primer možete imati praktično identičan kôd koji radi sa MySQL i SQLite bazom:

{% highlight php %}
<?php
// PDO + MySQL
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');
$statement = $pdo->query("SELECT some_field FROM some_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);

// PDO + SQLite
$pdo = new PDO('sqlite:/path/db/foo.sqlite');
$statement = $pdo->query("SELECT some_field FROM some_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);
{% endhighlight %}

PDO neće prevoditi vaše SQL upite ili emulirati nedostajuće opcije; on služi isključivo za povezivanje
sa različitim tipovima baza podataka pomoću istog API-ja.

Ono što je još bitnije, `PDO` omogućava da bezbedno ubacite podatke koji potiču iz nekog stranog izvora (npr. ID-eve)
u vaš SQL upit bez bojazni od SQL Injection napada. Ovo je moguće korišćenjem PDO naredbi (statements) i bound parametara.

Pretpostavimo da PHP skripta prima numerički ID kao parametar upita. Ovaj ID se koristi da vrati korisnički podatak iz
baze. Ovo je `pogrešan` način da se to uradi:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NE!
{% endhighlight %}

Ovo je katastrofalan kôd. Ubacujete "sirov" parametar u SQL upit. Bićete hakovani u trenutku putem [SQL Injection] napada. Zamislite da haker
prosledi maliciozan `id` parametar putem URL-a kao što je `http://domain.com/?id=1%3BDELETE+FROM+users`. Ovo će postaviti
promenljivu `$_GET['id']` na `1;DELETE FROM users` što će obrisati sve vaše korisnike! Umesto toga, trebalo bi da sanirate ID
input korišćenjem PDO bound parametara:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$id = filter_input(INPUT_GET, 'id', FILTER_SANITIZE_NUMBER_INT); // <-- najpre filtrirajte podatke (vidi [Filtriranje podataka](#data_filtering)), posebno bitno za upite kao što su INSERT, UPDATE, itd.
$stmt->bindParam(':id', $id, PDO::PARAM_INT); // <-- automatski sanirano
$stmt->execute();
{% endhighlight %}

Ovo je ispravan kôd koji radi bind-ovanje parametra u PDO naredbu. Na taj način se sanira strani ID podatak pre nego što se
uopšte pošalje bazi, čime se sprečava potencijalni SQL injection napad.

U slučaju upita kao što su INSERT ili UPDATE, svejedno morate sami [filtrirati podatke](#data_filtering)
zbog drugih stvari (uklanjanje HTML tagova, JavaScript-a i slično). PDO će sanirati podatke samo u
slučaju SQL upita, a ne za potrebe vaše aplikacije.

* [Naučite o PDO-u][1]

Trebate imati svest o tome da konekcije sa bazom podataka troše sistemske resurse i neretko se dešava
da dođe do trošenja resursa ako se konekcije ne zatvaraju implicitno. Ipak, to se dosta češće dešava
u slučaju drugih programskih jezika. Pomoću PDO-a možete implicitno zatvoriti konekciju uništavanjem
samog PDO objekta, na primer postavljanjem njegove vrednosti na NULL. Ako ne uradite ovo eksplicitno,
PHP će automatski zatvoriti konekciju po završetku izvršavanja vaše skripte, osim ako naravno ne
koristite perzistentne konekcije.

* [Naučite o PDO konekcijama][1]

[pdo]: http://php.net/pdo
[SQL Injection]: http://wiki.hashphp.org/Validation
[Naučite o PDO-u]: http://php.net/book.pdo
[Naučite o PDO konekcijama]: http://php.net/pdo.connections
