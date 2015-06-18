---
layout: page
title:  Osnove
sitemap: true
---

# Osnove

## Operatori za poređenje

Operatori za poređenje su aspekt PHP-a koji je često zanemaren, što može dovesti do nekih neočekivanih rezultata.
Jedan takav problem proističe iz striktnog poređenja (poređenje bool vrednosti u vidu integer-a).

{% highlight php %}
<?php
$a = 5;   // 5 kao integer

var_dump($a == 5);       // poređenje vrednosti; vraća true
var_dump($a == '5');     // poređenje vrednosti (bez tipa); vraća true
var_dump($a === 5);      // poređenja tipa/vrednosti (integer sa integer-om); vraća true
var_dump($a === '5');    // compare tipa/vrednosti (integer sa string-om); vraća false

/**
 * Striktno poređenje
 */
if (strpos('testing', 'test')) {    // 'test' je pronađen na poziciji 0, a to se u ovom slučaju interpretira kao 'false'
    // ...
}

// nasuprot

if (strpos('testing', 'test') !== false) {    // true, zahvaljujući striktnom poređenju (0 !== false)
    // ...
}
{% endhighlight %}

* [Operatori za poređenje](http://php.net/language.operators.comparison)
* [Tabela tipova i operatora za poređenje](http://php.net/types.comparisons)
* [Cheat-sheet o poređenju](http://phpcheatsheets.com/index.php?page=compare)

## Uslovni izrazi

### If izrazi

Prilikom korišćenja 'if/else' izraza u nekoj funkciji ili klasa, postoji zabluda da 'else' uvek mora biti
napisan kako bi se pokrili svi potencijalni slučajevi. Ako je ishod zapravo definisanje povratne vrednosti,
'else' nije neophodan, jer će 'return' izaći iz funkcije, što bi 'else' učinilo suvišnim.

{% highlight php %}
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

// nasuprot

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else je nepotreban
}
{% endhighlight %}

* [If izrazi](http://php.net/control-structures.if)

### Switch izrazi

Switch izrazi predstavljaju odličnu alternativu za beskonačne if-ove i elseif-ove, ali treba biti svestan nekoliko stvari:

- Switch izrazi porede samo vrednosti, ne i tipove (ekvivalentno '==' poređenju)
- Prolaze svaki 'case' sve dok ne pronađu poklapanje. Ako ga nema, koristi se 'default' slučaj (ako je definisan)
- Bez 'break'-a, nastaviće da izvršavaju svaki 'case' sve dok se ne stigne do nekog break-a ili return-a
- U sklopu funkcije, korišćenjem 'return'-a se gubi potreba za 'break'-ovima, pošto on prekida funkciju

{% highlight php %}
<?php
$answer = test(2);    // i 'case 2' i 'case 3' će biti izvršeni

function test($a)
{
    switch ($a) {
        case 1:
            // ...
            break;             // break prekida switch izraz
        case 2:
            // ...             // bez break-a, poređenje se nastavlja na 'case 3'
        case 3:
            // ...
            return $result;    // u sklopu funkcije, 'return' će završiti (prekinuti) tu funkciju
        default:
            // ...
            return $error;
    }
}
{% endhighlight %}

* [Switch izrazi](http://php.net/control-structures.switch)
* [PHP switch](http://phpswitch.com/)

## Globalni namespace

Pri korišćenju namespace-ova, možda ste naišli na situaciju da su neke interne funkcije "pregažene" funkcijama koje ste vi napisali.
Kako biste to rešili, globalnu funkciju pozivajte sa backslash-om (\) pre njenog imena.

{% highlight php %}
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // Naša funkcija nosi isti naziv kao ugrađena.
                         // Izvršavanje funkcije iz globalnog namespace-a prefiksovanjem sa '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator je interna klasa. Njeno pozivanje bez backslash-a
                                         // će pokušati da je resolve-uje na osnovu vašeg trenutnog namespace-a.
}
{% endhighlight %}

* [Globalni namespace](http://php.net/language.namespaces.global)
* [Globalna pravila](http://php.net/userlandnaming.rules)

## Stringovi

### Konkatenacija (nadovezivanje)

- Ako je dužina neke vaše linije kôda veća od preporučene 120 karaktera, razmislite o konkatenaciji te linije
- Radi bolje preglednosti, najbolje je koristiti operatore za konkatenaciju umesto konkatenacije operatora za dodelu vrednosti
- Unutar originalnog scope-a neke promenljive, koristite indentaciju (uvlačenje teksta) kada konkatenacija prelazi u sledeći red


{% highlight php %}
<?php
$a  = 'Multi-line example';    // operator konkatenacije dodele vrednosti (.=)
$a .= "\n";
$a .= 'of what not to do';

// nasuprot

$a = 'Multi-line example'      // operator za konkatenaciju (.)
    . "\n"                     // uvlačenje linije
    . 'of what to do';
{% endhighlight %}

* [String operatori](http://php.net/language.operators.string)

### Tipovi stringova

Stringovi su zapravo serija karaktera, što zvuči dosta jednostavno. Pritom, postoji nekolicina različitih tipova
stringova, koji imaju vrlo male razlike u sintaksi, ali i male razlike u ponašanju.

#### Jednostruki navodnici

Jednostruki navodnici se koriste za "bukvalne/literalne stringove". Ovi stringovi ne rade parsiranje specijalnih
znakova i promenljivih.

Ako prilikom korišćenja jednostrukih navodnika unesete ime promenljive u sâm string, na primer: `'neka $stvar'`,
dobili biste isti takav output: `neka $stvar`. U slučaju dvostrukih navodnika, parser bi pokušao da evaluira
promenljivu `$stvar` i prikazao greške ako ona ne postoji.


{% highlight php %}
<?php
echo 'This is my string, look at how pretty it is.';    // nema potrebe za parsiranjem ovog jednostavnog stringa

/**
 * Ispis:
 *
 * This is my string, look at how pretty it is.
 */
{% endhighlight %}

* [Jednostruki navodnici](http://php.net/language.types.string#language.types.string.syntax.single)

#### Dvostruki navodnici

Dvostruki navodnici predstavljaju pravi "švajcarski vojnički nož" u kontekstu stringova. Oni ne samo da će da parsiraju
promenljive pomenute u prethodnom delu, ali i mnoge druge specijalne znakove, kao što su `\n` za novi red, `\t` za tab, itd.

{% highlight php %}
<?php
echo 'phptherightway is ' . $adjective . '.'     // primer sa jednostrukim navodnicima koji koristi konkatenaciju
    . "\n"                                       // za umetanje promenljivih
    . 'I love learning' . $code . '!';

// vs

echo "phptherightway is $adjective.\n I love learning $code!"  // Umesto konkatenacije, dvostruki navodnici nam omogućavaju
                                                               // korišćenje stringova koji se mogu parsirati
{% endhighlight %}

Dvostruki navodnici mogu da sadrže promenljive, a to se naziva "interpolacija".

{% highlight php %}
<?php
$juice = 'plum';
echo "I like $juice juice";    // Ispis: I like plum juice
{% endhighlight %}

Pri korišćenju interpolacije, često se dešava da promenljiva "dodiruje" neki drugi karakter u stringu. Ovo će
za rezultat imati konflikt u smislu razlikovanja imena promenljive od samog karaktera.

U cilju prevazilaženja ovog problema, potrebno je uokviriti promenljivu sa vitičastim zagradama.

{% highlight php %}
<?php
$juice = 'plum';
echo "I drank some juice made of $juices";    // $juice ne može biti parsirano

// nasuprot

$juice = 'plum';
echo "I drank some juice made of {$juice}s";    // $juice će biti parsirano

/**
 * Složenije promenljive takođe mogu biti parsirane unutar vitičastih zagrada.
 */

$juice = array('apple', 'orange', 'plum');
echo "I drank some juice made of {$juice[1]}s";   // $juice[1] će biti parsirano
{% endhighlight %}

* [Dvostruki navodnici](http://php.net/language.types.string#language.types.string.syntax.double)

#### Nowdoc sintaksa

Nowdoc sintaksa je predstavljena u verziji 5.3 i interno radi na isti način kao jednostruki navodnici, pri čemu je
prevashodno namenjena za pisanje stringova u više redova bez potrebe za konkatenacijom.

{% highlight php %}
<?php
$str = <<<'EOD'             // počinje sa <<<
Example of string
spanning multiple lines
using nowdoc syntax.
$a does not parse.
EOD;                        // završni 'EOD' mora biti u novom redu i kranje ulevo

/**
 * Ispis:
 *
 * Example of string
 * spanning multiple lines
 * using nowdoc syntax.
 * $a does not parse.
 */
{% endhighlight %}

* [Nowdoc sintaksa](http://php.net/language.types.string#language.types.string.syntax.nowdoc)

#### Heredoc sintaksa

Heredoc sintaksa interno radi na isti način kao dvostruki navodnici, pri čemu je prevashodno namenjena
za pisanje stringova u više redova bez potrebe za konkatenacijom.

{% highlight php %}
<?php
$a = 'Variables';

$str = <<<EOD               // počinje sa <<<
Example of string
spanning multiple lines
using heredoc syntax.
$a are parsed.
EOD;                        // završni 'EOD' mora biti u novom redu i kranje ulevo

/**
 * Ispis:
 *
 * Example of string
 * spanning multiple lines
 * using heredoc syntax.
 * Variables are parsed.
 */
{% endhighlight %}

* [Heredoc sintaksa](http://php.net/language.types.string#language.types.string.syntax.heredoc)

### Šta je brže?

Postoji mit o tome da su jednostruki navodnici nešto brži od dvostrukih, a to u osnovi nije tačno.

Ako definišete string i pritom nemate konkatenaciju vrednosti, onda će stringovi sa jednostrukim i dvostrukim
navodnicima biti u potpunosti ista. Oba rešenja će biti podjednako brza.

Ako vršite konkatenaciju više stringova ili vršite interpolaciju promenljivih u string sa dvostrukim navodnicima,
onda se rezultati mogu razlikovati. Ako radite sa malim brojem promenljivih, konkatenacija će biti neznatno brža.
A u slučaju dosta promenljivih, interpolacija će biti nešto brža.

Nezavisno od toga šta radite sa stringovima, nijedan od ova dva tipa neće imati značajan uticaj na vašu aplikaciju.
Pokušaj prepravke kôda sa ciljem korišćenja jednog ili drugog tipa je uzaludan posao, tako da izbegavajte te
mikro-optimizacije osim ako zaista razumete značenje i uticaj njihov razlika.

* [Razbijanje mita o performansama jednostrukih navodnika](http://nikic.github.io/2012/01/09/Disproving-the-Single-Quotes-Performance-Myth.html)


## Ternarni operatori

Ternarni operatori predstavljaju odličan način za uštedu kôda, ali programeri često preteruju u njihovom korišćenju.
Iako ternarni operatori mogu biti ugnježdeni, preporuka je da se pišu u istoj liniji zbog preglednosti.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? 'yay' : 'nay';
{% endhighlight %}

Nasuprot ovome, sledi primer koji kompromituje sve vidove preglednosti u cilju smanjenja broja linija kôda:

{% highlight php %}
<?php
echo ($a) ? ($a == 5) ? 'yay' : 'nay' : ($b == 10) ? 'excessive' : ':(';
{% endhighlight %}

Za povratnu vrednost u slučaju ternarnih operatora koristite ispravnu sintaksu:

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // ovo će prouzrokovati grešku

// nasuprot

$a = 5;
return ($a == 5) ? 'yay' : 'nope';    // ovaj primer će vratiti 'yay'

{% endhighlight %}

Treba pomenuti i to da nema potrebe da koristite ternarni operator u slučaju vraćanja bool vrednosti.
Na primer:

{% highlight php %}
<?php
$a = 3;
return ($a == 3) ? true : false; // vraća true ili false ako je $a == 3

// nasuprot

$a = 3;
return $a == 3; // vraća true ili false ako je $a == 3

{% endhighlight %}

Ovo važi i za sve druge operacije (===, !==, !=, ==, itd.).

#### Korišćenje zagrada sa ternarnim operatorima za formatiranje i funkcionalnost

Pri korišćenju ternarnog operatora, zagrade mogu biti značajnte u cilju poboljšanja preglednosti, ali i
stvaranja unija u okviru blokova izraza. Primer u kojem zagrade nisu neophodne:

{% highlight php %}
<?php
$a = 3;
return ($a == 3) ? "yay" : "nope"; // vraća 'yay' ili 'nope' ako je $a == 3

// nasuprot

$a = 3;
return $a == 3 ? "yay" : "nope"; // vraća 'yay' ili 'nope' ako je $a == 3
{% endhighlight %}

Zagrade takođe nude mogućnost stvaranja unija u okviru blokova izraza, pri čemu se blok proverava u celosti.
To možemo videti u sledećem primeru koji će vratit true ako su oba uslova ($a == 3 i $b == 4) ispunjena i
ako je $c == 5 takođe tačno.

{% highlight php %}
<?php
return ($a == 3 && $b == 4) && $c == 5;
{% endhighlight %}

Još jedan primer je sledeći kôd koji vraća true ako je ($a != 3 i $b != 4) ili je $c == 5:

{% highlight php %}
<?php
return ($a != 3 && $b != 4) || $c == 5;
{% endhighlight %}

* [Ternarni operatori](http://php.net/language.operators.comparison)

## Definisanje/deklarisanje promenljivih

Programeri ponekad pokušavaju da učine kôd "čistijim" tako što će deklarisati neke promenljive određenim imenima.
To rezultuje povećanjem memorije koje će potrošiti neka skripta. Primera radi, ako imamo neki string veličine
1MB, upisivanjem istog u neku promenljivu biste povećali korišćenje memorije na 2MB:

{% highlight php %}
<?php
$about = 'A very long string of text';    // koristi 2MB memorije
echo $about;

// nasuprot

echo 'A very long string of text';        // koristi 1MB memorije
{% endhighlight %}

* [Saveti po pitanju performansi](http://web.archive.org/web/20140625191431/https://developers.google.com/speed/articles/optimizing-php)
