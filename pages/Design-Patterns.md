---
layout: page
title: Dizajn paterni (Design patterns)
sitemap: true
---

# Dizajn paterni (Design patterns)

Postoje brojni pristupi i različiti načini za izgradnju kôda vaše web aplikacije, samo je pitanje koliko ćete vremena posvetiti arhitekturi vašeg sistema.
Obično je dobra ideja da se vodite nekim uobičajenim šablonima i praksama, zato što će na taj način vaš kôd biti jednostavniji za održavanje i
lakši za razumevanje.

* [Arhitekturalni patern (Wikipedia)](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Dizajn patern (Wikipedia)](https://en.wikipedia.org/wiki/Software_design_pattern)
* [Primeri implementacija dizajn paterna](http://designpatternsphp.readthedocs.io/en/latest/)

## Factory (fabrika)

Jedan od najčešće korišćenih dizajn paterna je Factory. U njegovom slučaju, sve što neka klasa radi jeste kreiranje
objekta kojeg nameravate da koristite. Pogledajmo sledeći primer Factory paterna:

{% highlight php %}
<?php
class Automobile
{
    private $vehicleMake;
    private $vehicleModel;

    public function __construct($make, $model)
    {
        $this->vehicleMake = $make;
        $this->vehicleModel = $model;
    }

    public function getMakeAndModel()
    {
        return $this->vehicleMake . ' ' . $this->vehicleModel;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// Factory kreira Automobile objekat
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->getMakeAndModel()); //ispisuje "Bugatti Veyron"
{% endhighlight %}

Ovaj kôd koristi Factory za kreiranje instance Automobile klase. Postoje dva moguća benefita pisanja kôda
na ovaj način. Prvi je to što ćete u slučaju izmene, preimenovanja ili zamene Automobile klase, morati da
menjate jedino kôd u njenom factory-u, umesto na svakom mestu gde se koristi klasa Automobile. Druga prednost
je ta što u slučaju da je sâmo kreiranje objekta kompleksna operacija, sav taj posao možete obaviti u factory
klasi, umesto da ga ponavljate svaki put kada vam treba nova instanca.

Korišćenje Factory paterna nije uvek neophodno (ispravno). Prethodni primer je toliko prost da bi korišćenje
factory-a bio samo nepotrebna komplikacija. Ipak, ako radite na velikom i kompleksnom projektu, korišćenje
factory-a vas možete lišiti dosta problema.

* [Factory patern (Wikipedia)](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton (unikat)

Pri razvoju web aplikacija, često ima smisla konceptualno i arhitekturalno omogućiti korišćenje samo jedne
instance određene klase. Singleton patern omogućava upravo tako nešto.

**TODO: NEED NEW SINGLETON CODE EXAMPLE**

Ovaj kôd implementira singleton patern koristeći [*statičku* promenljivu](http://php.net/language.variables.scope#language.variables.scope.static)
i statički `getInstance()` metod. Obratite pažnju i na sledeće:

* Konstruktor [`__construct()`](http://php.net/language.oop5.decon#object.construct) je deklarisan kao protected
kako bi izvan klase bilo onemogućeno kreiranje *Singleton* instance preko `new` operatora.
* Magični metod [`__clone()`](http://php.net/language.oop5.cloning#object.clone) je deklarisan kao private
kako bi bilo onemogućeno kloniranje instance preko [`clone`](http://php.net/language.oop5.cloning) operatora.
* Magični metod [`__wakeup()`](http://php.net/language.oop5.magic#object.wakeup) je deklarisan kao private
kako bi bila onemogućena deserijalizacija instance preko globalne funkcije [`unserialize()`](http://php.net/function.unserialize).
* Nova instanca se kreira preko [late static binding](http://php.net/language.oop5.late-static-bindings) mehanizma
u statičkom metodu `getInstance()` putem ključne reči `static`. Upravo ovo omogućava nasleđivanje klase `Singleton` u primeru.

Signleton patern je koristan u situacijama kada treba da obezbedimo da imamo samo jednu instancu neke klase
u toku jednog kompletnog ciklusa u web aplikaciji. Tipičan primer su globalni objekti (kao što je neka Configuration klasa)
ili deljeni resursi (kao što je event queue).

Treba da budete oprezni pri korišćenju Singleton paterna, jer sama njegova priroda uvodi globalno stanje
u vašu aplikaciju, čime se smanjuje njena testabilnost. U većini slučajeva, dependency injection princip može (i treba)
da se koristi umesto Singleton klasa. Korišćenjem dependency injection-a ne uvodimo nepotrebne direktne zavisnosti u
dizajn naše aplikacije, jer objekat koji bude koristio taj neki deljeni ili globalni resurs neće imati znanja o
tome o kojoj se tačno klasi radi.

* [Singleton patern (Wikipedia)](https://en.wikipedia.org/wiki/Singleton_pattern)

## Strategy

Primenom Strategy paterna enkapsulirate grupu određenih algoritama, pri čemu je klijentska klasa odgovorna za
instanciranje konkretnog algoritma, bez znanja o načinu na koji je on implementiran. Postoji nekoliko varijacija
ovog paterna, a najjednostavniji od njih će biti demonstriran u nastavku.

Prvi deo prikazuje grupu algoritama za ispis nekog niza podataka: jedan vrši nativnu, drugi radi JSON
serijalizaciju, a treći ga ostavlja netaknutim:

{% highlight php %}
<?php

interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
{% endhighlight %}

Enkapsuliranjem ovih algoritama u zasebne klase, na elegantan i čist način stavljate do znanja drugim programerima
da lako mogu da dodaju novu output strategiju, bez uticaja na klijenstki kôd.

Primetićete da svaka 'output' klasa implementira određeni OutputInterface. Ovaj interfejs ima za cilj ima da
definiše jednostavan "ugovor" koji svaka nova implementacija mora da ispoštuje. Takođe, implementiranjem jednog
zajedničkog interfejsa, kao što ćete i videti u nastavku, biće omogućena primena [Type Hinting-a](http://php.net/language.oop5.typehinting),
kako bi se obezbedilo to da kôd koji koristi ovu funkcionalnost radi sa ispravnim tipovima klasa, u ovom slučaju 'OutputInterface' implementacijama.

Sledeći primer kôda demonstrira kako poziv klijentske klase može da koristi neki od ovih algoritama
tako što će ga zahtevati prilikom izvršavanja:

{% highlight php %}
<?php
class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}
{% endhighlight %}

Ova klijentska klasa ima privatno svojstvo koje mora da bude prosleđeno prilikom instanciranja,
pri čemu to mora da bude 'OutputInterface' implementacija. Nakon što je ovo svojstvo postavljeno,
poziv loadOutput() metoda će pozvati load() metod neke konkretne Output klase.

{% highlight php %}
<?php
$client = new SomeClient();

// Želite niz?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Želite JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [Strategy patern (Wikipedia)](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller

U slučaju Front Controller paterna postoji jedinstvena ulazna tačka u vašoj aplikaciji (npr. index.php)
koja prihvata sve zahteve. Taj deo kôda je odgovoran za učitavanje svih zavisnosti, procesiranje samog zahteva
i slanja odgovora browser-u. Ovaj patern može biti veoma koristan iz razloga što pospešuje modularan kôd
i obezbeđuje cetralno mesto za ubacivanje nekog kôda koji treba da se izvršava na svaki zahtev (kao na primer
saniranje ulaznih podataka).

* [Front Controller patern (Wikipedia)](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller

Model-View-Controller (MVC) patern i srodni paterni kao što su HMVC i MVVM vam omogućavaju da podelite kôd
na logičke objekte pri čemu svaki ima posebnu namenu. Model predstavlja sloj business logike i najčeće obavlja
manipulaciju podacima (dohvatanje, čuvanje) koji se koriste u okviru aplikacije. Kontroleri (Controllers)
prihvataju zahtev (request), uzimaju i obrađuju podatke od modela, a zatim učitavaju View-ove kako bi poslali odgovor (response).
View-ovi su templejti (markup, xml i slično) za prikaz podataka čiji se rezultujući output šalje browser-u
u okviru samog odgovora.

MVC je najčešće korišćeni arhitekturalni patern u popularnim [PHP frejmvorcima](https://github.com/codeguy/php-the-right-way/wiki/Frameworks).

Naučite više o MVC-u i srodnim paternima:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
