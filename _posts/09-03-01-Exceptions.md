---
isChild: true
title: Izuzeci (exceptions)
anchor:  exceptions
---

## Izuzeci (exceptions) {#exceptions_title}

Izuzeci su sastavni deo većine popularnih programskih jezika, ali ih PHP programeri često previđaju.
Jezici kao što je Ruby su izuzetno "exception-intenzivnim", tako da kad god nešto pođe po zlu, kao
na primer neuspeo HTTP request ili upit ka bazi podataka, ili čak u slučaju nepostojeće slike, Ruby
(odnosno gem-ovi koji se koriste) će ispisati izuzetak na ekranu tako da odmah znate u čemu je problem.

PHP je sam po sebi tolerantan što se ovoga tiče, tako da će poziv `file_get_contents()` funkcije
može rezultovati samo sa vraćenim `FALSE` i warning-om.
Mnogi stariji PHP framework-ovi kao što je CodeIgniter će samo vratiti false, logovati poruku u
njihove logove i eventualno će vam omogućiti da koristite metod kao što je `$this->upload->get_error()`
kako biste videli šta se zapravo desilo. Problem s tim je što mora da tražite grešku i čitate dokumentaciju
kako biste našli odgovarajući error metod, umesto da to bude veoma očigledno.

Još jedan problem postoji u slučaju kada klase automatski ispisuju grešku i prekidaju izvršavanje.
Kada uradite tako nešto, sprečavate drugog programera da dinamički obradi tu grešku. Izuzetke treba
bacati sa svrhom obaveštavanja programera o grešci, a oni onda mogu da odluče šta da rade sa njim. Na primer:

{% highlight php %}
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // Neuspela validacija
}
catch(Fuel\Email\SendingFailedException $e)
{
    // Nuspelo slanje email poruke
}
finally
{
    // Deo koji se izvršava uvek, bez obzira da li je izuzetak bačen i pre nego što se nastavi dalje izvršavanje
}
{% endhighlight %}

### SPL izuzeci

Generička `Exception` klasa pruža vrlo malo debug prostora za programera. Ipak, u cilju bolje situacije po tom pitanju,
moguće je kreirati specijalizovanu `Exception` klasu, izvođenjem iz generičke:

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

Ovo zapravo znači da možete imati nekoliko catch blokova i ponaosob obrađivati različite izuzetke. Ovo može dovesti
do toga da imate _mnogo_ custom Exception klasa, a pritom su umesto nekih od njih mogli biti korišćene
SPL Exception klase, dostupne kroz [SPL ekstenziju][splext].

Ako na primer koristite `__call()` magični metod i zatražen je neki nepostojeći metod, onda umesto bacanja
standardnog izuzetka, što bi bilo nejasno, ili kreiranja custom Exception klase samo u te svrhe, možete baciti
`BadMethodCallException`.

* [Pročitajte još o izuzecima][exceptions]
* [Pročitajte još o SPL izuzecima][splexe]
* [Ugnježdeni izuzeci u PHP-u][nesting-exceptions-in-php]
* [Najbolja praksa za izuzetke u PHP 5.3][exception-best-practices53]


[splext]: /#standard_php_library
[exceptions]: http://php.net/language.exceptions
[splexe]: http://php.net/spl.exceptions
[nesting-exceptions-in-php]: http://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
[exception-best-practices53]: http://ralphschindler.com/2010/09/15/exception-best-practices-in-php-5-3
