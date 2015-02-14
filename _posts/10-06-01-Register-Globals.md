---
isChild: true
title: Register Globals
anchor: register_globals
---

## Register Globals {#register_globals_title}

**NAPOMENA:** Od PHP verzije 5.4.0 podešavanje `register_globals` je uklonjeno i više se ne može koristiti.
Ovo poglavlje postoji samo kao upozorenje svima onima koji su u procesu upgrade-a legacy aplikacije.

Kada je uključeno, `register_globals` podešavanje omogućava da podaci iz nekoliko tipova promenljivih
(uključujući one iz `$_POST`, `$_GET` i `$_REQUEST`) bude dostupno u globalnom scope-u aplikacije.
Ovo vrlo lako može prouzrokovati bezbednosne probleme, jer aplikacija ne može sa sigurnošću znati
odakle ti podaci dolaze.

Na primer: `$_GET['foo']` bi bilo dostupno i kao `$foo`, što može override-ovati promenljive koje
još uvek nisu definisane. Ako koristite PHP < 5.4.0 __postarajte se__ da je `register_globals`
podešavanje __isključeno__.

* [Register_globals u PHP manual-u](http://php.net/security.globals)
