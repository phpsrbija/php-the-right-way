---
isChild: true
title: Rad sa UTF-8
anchor: php_and_utf8
---

## Rad sa UTF-8 {#php_and_utf8_title}

_Ovu sekciju je inicijalno napisao [Alex Cabal](https://alexcabal.com/) na
[PHP Best Practices](https://phpbestpractices.org/#utf-8) sajtu, što je iskorišćeno kao osnova
za naše savete na temu UTF-8.

### Nema jednostavnog rešenja. Budite pažljivi, temeljni i konzistenti.

Trenutno, PHP u osnovi ne podržava Unicode. Postoje načini da se omogući da se UTF-8 stringovi ispravno
procesiraju, ali nisu nimalo jednostavni i zahtevaju zadiranje u praktično sve nivoe web aplikacije,
počevši od HTML-a, pa do SQL-a i PHP-a. Pokušaćemo da na sažet i praktičan način predstavimo ovu problematiku.

### UTF-8 na nivou PHP-a

Osnovne operacije sa stringovima, kao što su konkatenacija dva stringa ili definisanje string varijabli,
ne zahtevaju ništa specijalno po pitanju UTF-8. S druge strane, većina string funkcija, kao što su
`strpos()` i `strlen()` zahtevaju poseban tretman. Ove funkcije obično imaju pandane prefiksovane sa `mb_*`,
npr. `mb_strpos()` i `mb_strlen()` funkcije. One su dostupne zahvaljujući [Multibyte String] ekstenziji,
i dizajnirane su upravo za rad sa Unicode stringovima.

Korišćenje `mb_*` funkcija je neophodno kada radite nad Unicode stringom. Na primer, ako koristite `substr()`
u slučaju UTF-8 stringa, velika je verovatnoća da će dobiti neke čudne karaktere u rezultatu. Funkcija koju
treba da koristite u tom slučaju je odgovarajući multibyte pandan - `mb_substr()`.

Problem je što dosta često zaboravimo da treba da koristimo `mb_*` funkcije. Dovoljno je da samo jednom
napravite taj propust pa da vaš Unicode string bude neupotrebljiv za svako dalje procesiranje.

Ali nemaju sve string funkcije svog `mb_*` dvojnika. Ako ne postoji odgovarajuća funkcija za ono što vam treba,
onda jednostavno nemate sreće.

Funkciju `mb_internal_encoding()` bi trebalo koristiti na početku svake PHP skripte koju pišete
(ili na početku nekog globalnog skripta kojeg posle učitavate), a `mb_http_output()` odmah nakon
nje u slučaju da vaša skripta radi neki ispis. Eksplicitno definisanje enkodinga će vas lišiti dosta problema.

Takođe, dosta PHP funkcija za rad sa stringovima ima opcioni parametar putem kojeg je moguće podesiti enkoding.
Preporuka je da uvek eksplicitno prosleđujete UTF-8 kao argument. Tako na primer `htmlentities()` funkcija
ima opciju za enkoding i uvek bi trebalo da kao vrednost tog parametra prosleđujete UTF-8. Pritom, od PHP verzije
5.4.0, UTF-8 će biti podrazumevani enkoding za `htmlentities()` i `htmlspecialchars()` funkcije.

Konačno, ako razvijate distribuiranu aplikaciju i ne možete biti sigurni da ćete imati omogućenu `mbstring` ekstenziju,
onda razmislite o korišćenju [patchwork/utf8] Composer biblioteke. Ona će koristiti `mbstring` ako je dostupan,
a u suprotnom, koristiće odgovarajuće ne-UTF-8 funkcije.

[Multibyte String]: http://php.net/book.mbstring
[patchwork/utf8]: https://packagist.org/packages/patchwork/utf8

### UTF-8 na nivou baze podataka

Ako vaša PHP aplikacija pristupa MySQL bazi, postoji verovatnoća da će vaši podaci biti sačuvani kao
ne-UTF-8 stringovi u bazi, čak i ako se pridržavate saveta iz prethodnog dela teksta.

Kako biste bili sigurni da se stringovi iz PHP-a u MySQL šalju UTF-8 enkodovani, vaša baza i tabele
u njoj bi trebale da imaju podešen `utf8mb4` set karaktera (character set) i kolaciju (collation),
kao i da se  `utf8mb4` set karaktera koristi za PDO konekciju. Proučite primer kôda koji sledi. Ovo
je _veoma bitno_.

Imajte u vidu da za kompletnu UTF-8 podršku morate da koristite `utf8mb4` set karaktera, a ne `utf8`!
Ako vas zanimaju razlozi, pogledajte sekciju "Za dalje čitanje".

### UTF-8 na nivou browser-a

Koristite `mb_http_output()` funkciju kako biste bili sigurni da vaša PHP skripta ispisuje UTF-8
stringove u browser-u.

Browser bi na osnovu HTTP odgovora trebalo da zna da li je neka stranica UTF-8 enkodovana. Prevaziđen
način je bio putem odgovarajućeg [charset `<meta>` taga](http://htmlpurifier.org/docs/enduser-utf8.html)
u `<head>` sekciji stranice. Ovaj pristup je u potpunosti validan, ali podešavanje seta karaktera (charset) kroz
`Content-Type` _HTTP header_ je zapravo [mnogo brže] (https://developers.google.com/speed/docs/best-practices/rendering#SpecifyCharsetEarly).

{% highlight php %}
<?php
// Saopštimo PHP-u da koristimo UTF-8 stringove u celoj skripti
mb_internal_encoding('UTF-8');

// Saopštimo PHP-u da ispisujemo UTF-8 browser-u
mb_http_output('UTF-8');

// Naš UTF-8 testni string
$string = 'Êl síla erin lû e-govaned vîn.';

// Obrada stringa putem multibyte funkcije
// Primetite da "sečemo" string baš na ne-ASCII karakteru
$string = mb_substr($string, 0, 15);

// Otvaramo konekciju sa bazom kako bismo uneli obrađeni string
// Za više informacija pogledajte PDO primer u ovom dokumentu
// Primetite `charset=utf8mb4` u okviru Data Source Name-a (DSN)
$link = new PDO(
    'mysql:host=hostname;dbname=baza;charset=utf8mb4',
    'username',
    'password',
    array(
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_PERSISTENT => false
    )
);

// Upisujemo obrađeni string kao UTF-8 u bazi
// Vaša baza and tabele su na utf8mb4 character set-u i kolaciji, jel tako?
$handle = $link->prepare('insert into ElvishSentences (Id, Body) values (?, ?)');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->bindValue(2, $string);
$handle->execute();

// Dohvatanje upravo sačuvanog stringa kako bismo proverili da li zaista dobro unet
$handle = $link->prepare('select * from ElvishSentences where Id = ?');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->execute();

// Upisujemo rezultat u objekat kojeg ćemo posle ispisati
$result = $handle->fetchAll(\PDO::FETCH_OBJ);

header('Content-Type: text/html; charset=UTF-8');
?><!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>UTF-8 test page</title>
    </head>
    <body>
        <?php
        foreach($result as $row){
            print($row->Body);  // Ovde bi trebalo da imamo ispravan ispis našeg UTF-8 stringa
        }
        ?>
    </body>
</html>
{% endhighlight %}

### Za dalje čitanje

* [PHP Manual: Operacije sa stringovima](http://php.net/language.operators.string)
* [PHP Manual: String funkcije](http://php.net/ref.strings)
    * [`strpos()`](http://php.net/function.strpos)
    * [`strlen()`](http://php.net/function.strlen)
    * [`substr()`](http://php.net/function.substr)
* [PHP Manual: Multibyte string funkcije](http://php.net/ref.mbstring)
    * [`mb_strpos()`](http://php.net/function.mb-strpos)
    * [`mb_strlen()`](http://php.net/function.mb-strlen)
    * [`mb_substr()`](http://php.net/function.mb-substr)
    * [`mb_internal_encoding()`](http://php.net/function.mb-internal-encoding)
    * [`mb_http_output()`](http://php.net/function.mb-http-output)
    * [`htmlentities()`](http://php.net/function.htmlentities)
    * [`htmlspecialchars()`](http://php.net/function.htmlspecialchars)
* [PHP UTF-8 Cheatsheet](http://blog.loftdigital.com/blog/php-utf-8-cheatsheet)
* [Handling UTF-8 with PHP](http://www.phpwact.org/php/i18n/utf-8)
* [Stack Overflow: What factors make PHP Unicode-incompatible?](http://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)
* [Stack Overflow: Best practices in PHP and MySQL with international strings](http://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)
* [How to support full Unicode in MySQL databases](http://mathiasbynens.be/notes/mysql-utf8mb4)
* [Bringing Unicode to PHP with Portable UTF-8](http://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)
* [Stack Overflow: DOMDocument loadHTML does not encode UTF-8 correctly](http://stackoverflow.com/questions/8218230/php-domdocument-loadhtml-not-encoding-utf-8-correctly)
