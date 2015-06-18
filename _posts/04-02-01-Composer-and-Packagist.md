---
isChild: true
anchor:  composer_and_packagist
---

## Composer i Packagist {#composer_and_packagist_title}

Composer je **sjajan** menadžer zavisnosti za PHP. Navedite zavisnosti vašeg projekta u `composer.json` fajlu i sa par
jednostavnih komandi, Composer će automatski preuzeti zavisnosti i podesiti autoloading umesto vas.

Postoji dosta PHP biblioteka koje su kompatibilne sa Composer-om, spremne da se koriste u vašem projektu. Ovi
"paketi" su dostupni na [Packagist]-u, zvaničnom repozitorijumu za PHP biblioteke kompatibilne sa Composer-om.

### Instalacija Composer-a

Composer možete da instalirate lokalno (u vašem radnom direktorijumu; mada se to više ne preporučuje) ili
globalno (npr. u /usr/local/bin). Ako pretpostavimo da želite da instalirate Composer lokalno, iz root
direktorijuma vašeg projekta izvršite:

{% highlight console %}
curl -s https://getcomposer.org/installer | php
{% endhighlight %}

This will download `composer.phar` (a PHP binary archive). You can run this with `php` to manage your project
dependencies.
<strong>Please Note:</strong> If you pipe downloaded code directly into an interpreter, please read the
code online first to confirm it is safe.

#### Instalacija na Windows-u

U slučaju Windows korisnika, najjednostavniji način za instalaciju je putem [ComposerSetup] installer-a,
koji radi globalnu instalaciju i podešava vaš `$PATH`, tako da možete pozivati `composer` komandu iz
bilo kog foldera.

### Ručna instalacija Composer-a

Ručna instalacija Composer-a je napredna tehnika. Međutim, postoje razlozi zbog kojih bi se programer radije
odlučio za ovu opciju nego za interaktivnu proceduru instalacije. Interaktivna instalacija proverava vašu PHP
instalaciju kako bi obezbedila da:

- se koristi dovoljno visoka verzija PHP-a
- `.phar` fajlovi mogu da se ispravno izvrše
- postoje dovoljna ovlašćenja nad određenim direktorijumima
- određene problematične ekstenzije nisu učitane
- određene `php.ini` opcije su podešene

S obzirom da ručna instalacija ne vrši nijednu od ovih provera, morate razmisliti da li vam se ovaj kompromis isplati.
Imajući to u vidu, evo uputstva kako da ručno dođete do Composer-a:

{% highlight console %}
curl -s https://getcomposer.org/composer.phar -o $HOME/local/bin/composer
chmod +x $HOME/local/bin/composer
{% endhighlight %}

Putanja `$HOME/local/bin` (ili direktorijum po vašem izboru) bi trebalo da se nalazi u vašoj promenljivoj okruženja
`$PATH`. Na taj način će komanda `composer` postati dostupna.

Kada u dokumentaciji naiđete na objašnjenje u kojem stoji da Composer pokreće preko `php composer.phar install`,
to sada možete zameniti sa:

{% highlight console %}
composer install
{% endhighlight %}

Ovo poglavlje podrazumeva da je Composer instaliran globalno.

### Kako definisati i instalirati zavisnosti

Composer čuva zavisnosti vašeg projekta u fajlu sa nazivom `composer.json`. Možete ga održavati ručno ako želite, ili
možete koristiti sâm Composer. Komanda `composer require` dodaje neku zavisnost čak i ako ne postoji
`composer.json` fajl, jer će on u tom slučaju biti napravljen. Sledeći primer dodaje [Twig] kao dependency vašeg projekta:

{% highlight console %}
composer require twig/twig:~1.8
{% endhighlight %}

Nasuprot ovome, komanda `composer init` će vas voditi kroz pravljenje kompletnog `composer.json` fajla za vaš
projekat. U svakom slučaju, nakon što jednom kada kreirate `composer.json`, možete dati instrukciju Composer-u da
preuzme i instalira vaše zavisnosti u `vendor/` direktorijum. Ovo važi i za projekte koje ste preuzeli, a koji već sadrže
`composer.json` fajl:

{% highlight console %}
composer install
{% endhighlight %}

Zatim, dodajte sledeću liniju u primarni PHP fajl vaše aplikacije. To će reći PHP-u da koristi Composer-ov autoloader za
zavisnosti vašeg projekta:

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Sada možete koristiti zavisnosti i one će se po zahtevu automatski učitavati.

### Ažuriranje vaših zavisnosti

Composer kreira fajl `composer.lock` koji čuva tačnu verziju svakog paketa kojeg je preuzeo kada ste prvi put izvršili
`composer install` komandu. Ako na vašem projektu radite sa drugim programerima, a fajl `composer.lock` je distribuiran (verzionisan),
kada i oni pokrenu `composer install` dobiće iste verzije kao i vi. Da biste ažurirali vaše zavisnosti, koristite `composer update` komandu.

Ovo je korisno u situacijama kada fleksibilno definišete zahteve za verzije. Tako na primer zahtev verzije `~1.8` znači "sve što je novije
od verzije `1.8.0`, ali manje od `2.0.x-dev`". Takođe možete koristiti i `*` wildcard kao u slučaju `1.8.*`. Sada će
`composer update` komanda ažurirati sve vaše zavisnosti na najnoviju verziju koja odgovara ograničenjima koja ste definisali.

### Obaveštenja o update-ima

Da biste dobijali obaveštenja o novim verzijama paketa možete se prijaviti na [VersionEye] web servisu
koji može da prati `composer.json` fajlove na vašim GitHub ili BitBucket nalozima i da vam šalje mejlove sa
novim verzijama paketa.

### Proveravanje vaših zavisnosti sa aspekta bezbednosti

[Security Advisories Checker] je web servis i alat koji se izvršava sa komandne linije. Oba načina će pregledati vaš
`composer.lock` fajl i ako je neophodno obavestiti vas da ažurirate neku od vaših zavisnosti.

### Upravljanje globalnim zavisnostima sa Composer-om

Composer takođe može da upravlja globalnim zavisnostima. Korišćenje je jednostavno, i sve što treba
da uradite jeste da dodate `global` prefiks na vaše komande. Ako na primer hoćete da instalirate PHPUnit globalno
izvršili biste sledeću komandu:

{% highlight console %}
composer global require phpunit/phpunit
{% endhighlight %}

Ovo će kreirati `~/.composer` folder gde će se nalaziti vaše globalne zavisnosti. Kako biste instalirane
pakete imali dostupne sa bilo kog mesta, dodajte `~/.composer/vendor/bin` folder u vašu `$PATH` varijablu.

* [Naučite više o Composer-u][Learn about Composer]

[Packagist]: http://packagist.org/
[Twig]: http://twig.sensiolabs.org
[VersionEye]: https://www.versioneye.com/
[Security Advisories Checker]: https://security.sensiolabs.org/
[Learn about Composer]: http://getcomposer.org/doc/00-intro.md
[ComposerSetup]: https://getcomposer.org/Composer-Setup.exe
