---
layout: page
title:  Funkcionalno programiranje u PHP-u
sitemap: true
---

# Funkcionalno programiranje u PHP-u

PHP podržava funkcije prve klase (first-class funkcije), što znači da funkcija može biti dodeljena promenljivoj. I korisnički definisane i
ugrađene funkcije mogu biti referencirane promenljivom i pozvane dinamički. Funkcije se mogu prosleđivati kao argumenti
drugim funkcijama (odlika nazvana _Funkcije višeg reda_) i funkcija može vratiti druge funkcije.

Rekurzija, osobina koja omogućava funkciji da poziva samu sebe, je podržana u samom jeziku, ali se
većina PHP kôda fokusira na iteriranje.

Anonimne (anonymous) funkcije (sa podrškom za closures) su prisutne od verzije PHP 5.3 (2009).

PHP 5.4 je dodao mogućnost da se closure poveže sa _scope-om_ objekta, a takođe i poboljšao podršku za _callable_ tipove,
tako da se oni praktično u skoro svim slučajevima mogu koristiti na isti način kao anonimne funkcije.

Najčešći slučaj korišćenja funkcija višeg reda pri implementaciji Strategy paterna. Ugrađena `array_filter()`
funkcija od parametara zahteva niz (data) i funkciju (strategiju ili callback) koja će biti korišćena kao filter nad
svakim elementom prosleđenog niza.

{% highlight php %}
<?php
$input = array(1, 2, 3, 4, 5, 6);

// Definisanje anonimne funkcije u promenljivu
$filter_even = function($item) {
    return ($item % 2) == 0;
};

// Ugrađena array_filter funkcija prihvata niz i callback funkciju
$output = array_filter($input, $filter_even);

// Callback funkcija ne mora da bude assign-ovana nekoj promenljivoj. Ovo je takođe ispravno:
$output = array_filter($input, function($item) {
    return ($item % 2) == 0;
});

print_r($output);
{% endhighlight %}

Closure je anonimna funkcija koja može da pristupi promenljivama izvan svog scope-a bez korišćenja globalnih
promenljivih. U teoriji, closure je funkcija sa određenim argumentima koji su zatvoreni njenom definicijom.
Closure funkcije mogu da prevaziđu ograničenja po pitanju scope-a na dosta čist način.

U sledećem primeru je closure u vidu funkcije koja vraća jednu filter funkciju za potrebe `array_filter()` iz
grupe filter funkcija.

{% highlight php %}
<?php
/**
 * Kreira anonimnu filter funkciju koja prihvata item-e > $min.
 *
 * Vraća funkciju iz grupe "veće od n" filtera
 */
function criteria_greater_than($min)
{
    return function($item) use ($min) {
        return $item > $min;
    };
}

$input = array(1, 2, 3, 4, 5, 6);

// Poziv array_filter nad nizom i određenom filter funkcijom
$output = array_filter($input, criteria_greater_than(3));

print_r($output); // items > 3
{% endhighlight %}

Svaka filter funkcija iz grupe prihvata samo elemente koji su veći od određene minimalne vrednosti. Filter kojeg vraća
`criteria_greater_than` je closure sa `$min` argumentom čija je vrednost zatvorena u scope-u (prosleđuje se kao argument pri
pozivu `criteria_greater_than` funkcije).

Rano bind-ovanje se podrazumevano koristi za import `$min` promenljive u kreiranu funkciju. Za prave closure-e sa kasnim
bind-ovanje je potrebno koristiti referencu prilikom import-a. Zamislite neku template biblioteku ili biblioteku za validaciju
input-a, gde se definiše closure koji zatvara promenljive u scope, a pristupa im se kasnije pri izvršavanju anonimne funkcije.

* [Pročitajte o anonimnim funkcijama][anonymous-functions]
* [Više detalja o Closures RFC-u][closures-rfc]
* [Pročitajte o dinamičkim pozivima funkcija pomoću `call_user_func_array()`][call-user-func-array]


[anonymous-functions]: http://php.net/functions.anonymous
[closures-rfc]: https://wiki.php.net/rfc/closures
[call-user-func-array]: http://php.net/function.call-user-func-array
