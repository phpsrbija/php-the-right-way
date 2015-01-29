---
isChild: true
anchor:  programming_paradigms
---

## Programerske paradigme {#programming_paradigms_title}

PHP je fleksibilan, dinamičan jezik koji podržava raznovrsne tehnike programiranja. Poslednjih godina
se značajno razvio, naročito nakon uvođenja solidnog objektno-orijentisanog modela u verziji PHP 5.0 (2004),
anonimnih (lambda) funkcija i namespace-ova u verziji PHP 5.3 (2009), kao i trait-ova u PHP 5.4 (2012).

### Objektno-orijentisano programiranje

PHP ima vrlo upotpunjen set odlika objektno-orijentisanog programiranje, uključujući podršku za klase, apstraktne
klase, interfejse, nasleđivanje, konstruktore, kloniranje, izuzetke i drugo.

* [Pročitajte o Objektno-orijentisanom PHP-u][oop]
* [Pročitajte o Trait-ovima][traits]

### Funkcionalno programiranje

PHP podržava funkcije prve klase (first-class funkcije), što znači da funkcija može biti dodeljena promenljivoj. I korisnički definisane i
ugrađene funkcije mogu biti referencirane promenljivom i pozvane dinamički. Funkcije se mogu prosleđivati kao argumenti
drugim funkcijama (odlika nazvana _Funkcije višeg reda_) i funkcija može vratiti druge funkcije.

Rekurzija, osobina koja omogućava funkciji da poziva samu sebe, je podržana u samom jeziku, ali se
većina PHP kôda fokusira na iteriranje.

Nove anonimne funkcije (sa podrškom za closures) su prisutne od verzije PHP 5.3 (2009).

PHP 5.4 je dodao mogućnost da se closure poveže sa scope-om objekta, a takođe i poboljšao podršku za callable tipove,
tako da se oni praktično u skoro svim slučajevima mogu koristiti na isti način kao anonimne funkcije.

* Nastavite sa čitanjem o [Funkcionalnom programiranju u PHP-u](/pages/Functional-Programming.html)
* [Pročitajte o anonimnim funkcijama][anonymous-functions]
* [Pročitajte o Closure klasi][closure-class]
* [Više detalja o Closures RFC-u][closures-rfc]
* [Pročitajte šta su Callables][callables]
* [Pročitajte o dinamičkim pozivima funkcija pomoću `call_user_func_array`][call-user-func-array]

### Meta programiranje

PHP podržava razne vidove meta programiranja preko mehanizama kao što su Reflection API i magičnih metoda (Magic
Methods). Postoji dosta magičnih metoda, kao što su `__get()`, `__set()`, `__clone()`, `__toString()`, `__invoke()`, itd.
koje omogućavaju programerima da se uključe u ponašanje klase. Ruby programeri često izjavljuju da PHP-u nedostaje
`method_missing`, ali on postoji kao `__call()` i `__callStatic()`.

* [Pročitajte o magičnim metodama (Magic Methods)][magic-methods]
* [Pročitajte o reflekciji (Reflection)][reflection]
* [Pročitajte o overload-ovanju (Overloading)][overloading]


[oop]: http://php.net/language.oop5
[traits]: http://php.net/language.oop5.traits
[anonymous-functions]: http://php.net/functions.anonymous
[closure-class]: http://php.net/class.closure
[closures-rfc]: https://wiki.php.net/rfc/closures
[callables]: http://php.net/language.types.callable
[call-user-func-array]: http://php.net/function.call-user-func-array
[magic-methods]: http://php.net/language.oop5.magic
[reflection]: http://php.net/intro.reflection
[overloading]: http://php.net/language.oop5.overloading
