---
layout: page
title:  Design Patterns
sitemap: true
---

# Design Patterns

Postoje brojni načini i pristupi u izgradnji kôda za vašu web aplikaciju, samo je pitanje koliko ćete vremena posvetiti arhitekturi vašeg sistema.
Obično je dobra ideja da se vodite nekim uobičajenim šablonima i praksama, zato što će na taj način vaš kôd biti jednostavniji za održavanje i
lakši za razumevanje.

* [Arhitekturalni pattern (Wikipedia)](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Design pattern (Wikipedia)](https://en.wikipedia.org/wiki/Software_design_pattern)
* [Primeri implementacija design pattern-a](https://github.com/domnikl/DesignPatternsPHP)

## Factory

Jedan od najčešće korišćenih dizajn pattern-a je Factory. U njegovom slučaju, neka klasa jednostavno treba da kreira
objekat koji nameravate da koristite. Pogledajmo sledeći primer Factory pattern-a:

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
je ta što u slučaju da je samo kreiranje objekta kompleksna operacija, sav taj posao možete obaviti u factory
klasi, umesto da ga ponavljate svaki put kada vam treba nova instanca.

Korišćenje Factory pattern-a nije uvek neophodno (ispravno). Prethodni primer je toliko prost da bi korišćenje
factory-a bio samo nepotrebna komplikacija. Ipak, ako radite na velikom i kompleksnom projektu korišćenje
factory-a vas možete lišiti dosta problema.

* [Factory pattern (Wikipedia)](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton

Pri razvoju web aplikacija, često ima smisla konceptualno i arhitekturalno omogućiti korišćenje samo jedne
instance određene klase. Singleton pattern omogućava upravo tako nešto.

{% highlight php %}
<?php
class Singleton
{
    /**
     * @var Singleton The reference to *Singleton* instance of this class
     */
    private static $instance;
    
    /**
     * Returns the *Singleton* instance of this class.
     *
     * @return Singleton The *Singleton* instance.
     */
    public static function getInstance()
    {
        if (null === static::$instance) {
            static::$instance = new static();
        }
        
        return static::$instance;
    }

    /**
     * Konstruktor je protected kako bi izvan klase bilo onemogućeno
     * kreiranje *Singleton* instance preko `new` operatora.
     */
    protected function __construct()
    {
    }

    /**
     * Sprečavanje kloniranja *Singleton* instance.
     *
     * @return void
     */
    private function __clone()
    {
    }

    /**
     * Sprečavanje deserijalizacije *Singleton* instance.
     *
     * @return void
     */
    private function __wakeup()
    {
    }
}

class SingletonChild extends Singleton
{
}

$obj = Singleton::getInstance();
var_dump($obj === Singleton::getInstance());             // bool(true)

$anotherObj = SingletonChild::getInstance();
var_dump($anotherObj === Singleton::getInstance());      // bool(false)

var_dump($anotherObj === SingletonChild::getInstance()); // bool(true)
{% endhighlight %}

Ovaj kôd implementira singleton pattern koristeći [*statičku* promenljivu](http://php.net/language.variables.scope#language.variables.scope.static)
i statički `getInstance()` metod. Obratite pažnju i na sledeće:

* Konstruktor [`__construct()`](http://php.net/language.oop5.decon#object.construct) je deklarisan kao protected
kako bi izvan klase bilo onemogućeno kreiranje *Singleton* instance preko `new` operatora.
* Magični metod [`__clone()`](http://php.net/language.oop5.cloning#object.clone) je deklarisan kao private
kako bi bilo onemogućeno kloniranje instance preko [`clone`](http://php.net/language.oop5.cloning) operatora.
* Magični metod [`__wakeup()`](http://php.net/language.oop5.magic#object.wakeup) je deklarisan kao private
kako bi bila onemogućena deserijalizacija instance preko globalne funkcije [`unserialize()`](http://php.net/function.unserialize).
* Nova instanca se kreira prek [late static binding](http://php.net/language.oop5.late-static-bindings) mehanizma
u statičkom metodu `getInstance()` putem ključne reči `static`. Upravo ovo omogućava nasleđivanje klase `Singleton` u primeru.

Signleton pattern je koristan u situacijama kada treba da obezbedimo da imamo samo jednu instancu neke klase
u toku jednog kompletnog request ciklusa u aplikaciji. Tipičan primer su globalni objekti (kao što je neka Configuration klasa)
ili deljeni resursi (kao što je event queue).

Treba da budete oprezni pri korišćenju Singleton pattern-a, jer sama njegova priroda uvodi globalno stanje
u vašu aplikaciju, čime se smanjuje njena testabilnost. U većini slučajeva, dependency injection princip može (i treba)
da se koristi umesto Singleton klasa. Korišćenjem dependency injection-a ne uvodimo nepotrebne direktne zavisnosti u
dizajn naše aplikacije, jer objekat koji bude koristio taj neki deljen ili globalan resurs neće imati znanja o
tome o kojoj se tačno klasi radi.

* [Singleton pattern (Wikipedia)](https://en.wikipedia.org/wiki/Singleton_pattern)

## Strategy

Primenom Strategy pattern-a enkapsulirate grupu određenih algoritama, pri je klijentska klasa odgovorna za
instanciranje konkretnog algoritma, bez znanja o načinu na koji je on implementiran. Postoji nekoliko varijacija
ovog pattern-a, a najjednostavniji od njih će biti demonstriran u nastavku.

Prvi snippet prikazuje grupu algoritama za ispis nekog niza podataka: jedan vrši nativnu, drugi radi JSON
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

Ova klijentska klasa  ima privatno svojstvo koje mora da bude prosleđeno prilikom instanciranja,
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

* [Strategy pattern (Wikipedia)](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller

U slučaju Front Controller pattern postoji jedinstvena ulazna tačka u vašoj aplikaciji (npr. index.php)
koja prihvata sve zahteve. Taj deo kôda je odgovoran za učitavanje svih zavisnosti, procesiranje samog zahteva
i slanja odgovora browser-u. Ovaj pattern može biti veoma koristan iz razloga što pospešuje modularan kôd
i obezbeđuje cetralno mesto za ubacivanje nekog kôda koji treba da se izvršava na svaki zahtev (kao na primer
saniranje ulaznih podataka).

* [Front Controller pattern (Wikipedia)](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller

Model-View-Controller (MVC) pattern i srodni pattern-i kao što su HMVC i MVVM vam omogućavaju da podelite kôd
na logičke objekte pri čemu svaki ima posebnu namenu. Model predstavlja sloj business logike, i najčeće obavlja
manipulaciju podacima (dohvatanje, čuvanje) koji se koriste u okviru aplikacije. Kontroleri (Controllers)
prihvataju request, uzimaju i obrađuju podatke od modela, a zatim učitavaju View-ove kako bi poslali response.
View-ovi su templejti (markup, xml i slično) za prikaz podataka čiji se rezultujući output šalje browser-u
u okviru samog response-a.

MVC je najčešće korišćeni arhitekturalni pattern u popularnim [PHP framework-ovima](https://github.com/codeguy/php-the-right-way/wiki/Frameworks).

Naučite više o MVC-u i srodnim pattern-ima:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
