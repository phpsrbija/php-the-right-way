---
isChild: true
title: Composer i Packagist
anchor:  composer_and_packagist
---

## Composer i Packagist {#composer_and_packagist_title}

Composer je **sjajan** menadžer zavisnosti za PHP. Navedite zavisnosti vašeg projekta u `composer.json` fajlu i sa par
jednostavnih komandi, Composer će automatski preuzeti zavisnosti i podesiti autoloading umesto vas. Composer je analogan
NPM-u u node.js svetu, ili Bundler-u u Ruby svetu.

Postoji dosta PHP biblioteka koje su kompatibilne sa Composer-om, spremne za korišćenje u vašem projektu. Ovi
"paketi" su dostupni na [Packagist]-u, zvaničnom repozitorijumu za PHP biblioteke kompatibilne sa Composer-om.

### Instalacija Composer-a

Najbezbedniji način da preuzmete Composer jeste da [pratite zvanične instrukcije](https://getcomposer.org/download/).
Ovo će proveriti ispravnost instalacione datoteke tako da ona nije oštećena ili kompromitovana.
Instalaciona datoteka instalira Composer *lokalno* u vaš trenutni radni direktorijum.

Mi preporučujemo da ga instalirate globalno (npr. jedina kopija u /usr/local/bin) - da biste to uradili izvšite sledeću komandu:

{% highlight console %}
mv composer.phar /usr/local/bin/composer
{% endhighlight %}

**Napomena:** Ukoliko zbog nedovoljnih ovlašćenja komanda iznad ne uspe, samo dodajte `sudo` ispred nje i ponovo je izvršite.

#### Instalacija na Windows-u

U slučaju Windows korisnika, najjednostavniji način za instalaciju je putem [ComposerSetup] instalera,
koji radi globalnu instalaciju i podešava vaš `$PATH`, tako da možete pozivati `composer` komandu iz
bilo kog foldera.

### Ručna instalacija Composer-a

Ručna instalacija Composer-a je napredna tehnika. Međutim, postoje razlozi zbog kojih bi se programer radije
odlučio za ovu opciju nego za interaktivnu proceduru instalacije. Interaktivna instalacija proverava vašu PHP
instalaciju kako bi se obezbedilo sledeće:

- dovoljno visoka verzija PHP-a
- `.phar` fajlovi mogu da se ispravno izvrše
- dovoljna ovlašćenja nad određenim direktorijumima
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

Kada u dokumentaciji naiđete na objašnjenje u kojem stoji da Composer pokrećete preko `php composer.phar install`,
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
`composer install` komandu. Ako na projektu radite sa drugim programerima, osigurajte da je fajl `composer.lock` distribuiran (verzionisan),
tako da nakon što oni pokrenu `composer install`, dobiće iste verzije kao i vi. Da biste ažurirali zavisnosti aplikacije, koristite `composer update` komandu.
Ne koristite `composer update` komandu prilikom deploy-a, već samo `composer install`, ili u suprotnom možete završiti sa drugačijim verzijama paketa na produkciji.

Ovo je korisno u situacijama kada fleksibilno definišete zahteve za verzije. Tako na primer zahtev verzije `~1.8` znači "sve što je novije
od verzije `1.8.0`, ali manje od `2.0.x-dev`". Takođe možete koristiti i `*` wildcard kao u slučaju `1.8.*`. Sada će
`composer update` komanda ažurirati sve vaše zavisnosti na najnoviju verziju koja odgovara ograničenjima koja ste definisali.

### Obaveštenja o novim verzijama

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
