---
isChild: true
title: Filtriranje podataka
anchor: data_filtering
---

## Filtriranje podataka {#data_filtering_title}

Apsolutno nikada ne verujte "stranom" (korisnikovom) ulaznom podatku (input) koji se šalje u vaš PHP kôd. Uvek filtrirajte i validirajte
strani input pre nego što ga upotrebite u kôdu. Funkcije `filter_var()` i `filter_input()` se koriste za filtriranje
nekog teksta, kao i za njegovu validiciju (npr. email adrese).

Strani input može biti bilo šta: `$_GET` i `$_POST` podaci iz forme, neke vrednosti u superglobalnoj promenljivoj
`$_SERVER` ili body HTTP zahteva dobijen putem `fopen('php://input', 'r')`. Zapamtite, strani input nije ograničen
samo na podatke iz forme koje je poslao korisnik. Uploadovani i preuzeti fajlovi, vrednosti iz sesije, podaci iz cookie-a
i podaci iz 3rd party web servisa su takođe strani input.

Iako se ti podaci mogu čuvati, kombinovati i može im se pristupiti kasnije, oni su ipak strani input. Svaki put
kad obradite, prikažete, spojite ili uključite podatke u vaš kôd, zapitajte se da li su podaci pravilno filtrirani i da
li su bezbedni.

Podaci se mogu različito _filtrirati_ u zavisnosti od njihove namene. Na primer, nefiltrirani strani input prosleđen
HTML stranici za prikaz može izvršiti HTML i JavaScript na vašem sajtu! Ovo se naziva Cross-Site Scripting (XSS) i predstavlja
vrlo opasan vid napada. Jedan od načina da sprečite XSS napade je da filtrirate sve podatke koje je korisnik generisao pre
nego što ih ispišete, tako što ćete ukloniti HTML tagove pomoću `strip_tags()` funkcije ili escape-ovati karaktere koji imaju
specijalno značenje u odgovarajuće HTML entitete pomoću `htmlentities()` ili `htmlspecialchars()` funkcija.

Još jedan primer je prosleđivanje opcija putem komandne linije. Ovo može biti vrlo opasno (i najčešće je
loša ideja), ali možete da upotrebite ugrađenu `escapeshellarg()` funkciju da prečistite argumente komande.

Poslednji primer je prihvatanje stranog input-a sa ciljem učitavanja određenog fajla. Ovo se može
zloupotrebiti promenom imena fajla u putanju fajla. Na vama je da uklonite `"/"`, `"../"`, [null bajtove][6]
i druge karaktere iz putanje fajla kako biste sprečili učitavanje skrivenih, privatnih i sistemskih fajlova.

* [Naučite više o filtriranju podataka][1]
* [Naučite više o `filter_var`][4]
* [Naučite više o `filter_input`][5]
* [Naučite više o rukovanju sa null bajtovima][6]

### Filtriranje / sanacija (sanitization)

Filtriranje uklanja (ili escape-uje) ilegalne ili nebezbedne karaktere iz stranog input-a.

Na primer, trebalo bi da filtrirate strane podatake pre njihovog uključivanja u HTML ili ubacivanja u SQL
upit. Ako koristite [PDO](#databases) bound parametre, oni će biti automatski sanirani.

Ponekad je neophodno da namerno dozvolite unos određenih HTML tagova u input-u prilikom ispisa. Ovo je donekle
teško za implementirati i mnogi pribegavaju korišćenju striktnijeg formatiranja kao što je Markdown ili BBCode,
iako biblioteke kao što je [HTML Purifier][html-purifier] postoje baš iz ovog razloga.

[Pogledaj filtere za prečišćavanje][2]

### Validacija

Validacija obezbeđuje da strani input bude u skladu sa onim što vaša aplikacija očekujete. Na primer, možda će
biti potrebno da validirate email adresu, broj telefona ili godište prilikom procesiranja registracione forme.

[Pogledaj validacione filtere][3]

[1]: http://php.net/book.filter
[2]: http://php.net/filter.filters.sanitize
[3]: http://php.net/filter.filters.validate
[4]: http://php.net/function.filter-var
[5]: http://php.net/function.filter-input
[6]: http://php.net/security.filesystem.nullbytes
[html-purifier]: http://htmlpurifier.org/
