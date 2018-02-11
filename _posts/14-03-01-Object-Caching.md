---
isChild: true
title: Keširanje podataka/objekata
anchor: object_caching
---

## Keširanje podataka/objekata {#object_caching_title}

Postoje situacije u kojima je isplativo keširati određene objekte, kao na primer neke podatke koji su
komplikovani za dohvatanje ili upiti ka bazi čiji se rezultat retko menja. Tada možete koristiti alate
za keširanje objekata, kako bi ti podaci bili u memoriji radi njihovog bržeg dohvatanja. Ako sačuvate
te podatke u neko skladište (storage) nakon što ih dohvatite, a zatim ih izvlačite iz keša u svakom narednom zahtevu,
dobićete znatno poboljšanje performansi, kao i smanjeno opterećenje (load) na vaše DB servere.

Dosta popularnih bajtkôd keš rešenja omogućava keširanje i nekih custom podataka, pa je to još jedan
razlog da ih koristite. APCu, XCache i WinCache na raspolaganje imaju API-je za čuvanje podataka iz
vašeg PHP kôda u njihov memorijski keš.

Najčešće korišćeni memorijski sistemi za keširanje su APCu i Memcached. APCu je odličan izbor za keširanje
objekata, koji poseduje jednostavan API za ubacivanje vaših podataka u njegov memorijski keš i veoma se
jednostavno instalira i koristi. Jedini nedostatak APCu-a je to što je vezan za server na kojem je
instaliran. S druge strane, Memcached se instalira kao zaseban servis i može mu se pristupati putem mreže,
što znači da vaše podatke možete čuvati u veoma brzom skladištu na centralizovanoj lokaciji, a više
različitih sistema može da čita podatke iz njega.

Imajte na umu da ako PHP radi kao (Fast-)CGI aplikacija na vašem web serveru, svaki PHP proces će imati svoj keš,
pa na primer APCu podaci neće biti deljeni među procesima. U tom slučaju bi trebalo razmisliti o korišćenju Memcached-a,
zato što se on ne vezuje za PHP proces.

U umreženoj konfiguraciji APCu se obično bolje pokazuje od Memcached-a u smislu brzine pristupa, ali Memcached
se brže i bolje skalira. Ukoliko ne očekujete da će se vaša aplikacija izvršavati na više servera ili vam ne trebaju dodatne mogućnosti
koje Memcached nudi, onda je APCu verovatno najbolja opcija za keširanje.

Primer korišćenja APCu-a:

{% highlight php %}
<?php
// provera da li postoji unos u kešu pod ključem 'expensive_data'
$data = apc_fetch('expensive_data');
if ($data === false) {
    // podaci nisu keširani; sačuvaj podatke "skupocenog" poziva za sledeći poziv
    apc_add('expensive_data', $data = get_expensive_data());
}

print_r($data);
{% endhighlight %}

Pre verzije PHP 5.5, APC je omogućavao keširanje i objekata i opcode-a. APCu je projekat koji omogućava APC-ovo
keširanje objekata za PHP verzije >= 5.5, pošto PHP sada ima ugrađen opcode keš (OPcache).

### Saznajte više o popularnim sistemima za keširanje:

* [APCu](https://github.com/krakjoe/apcu)
* [APC Functions](http://php.net/ref.apc)
* [Memcached](http://memcached.org/)
* [Redis](http://redis.io/)
* [XCache APIs](http://xcache.lighttpd.net/wiki/XcacheApi)
* [WinCache Functions](http://php.net/ref.wincache)
