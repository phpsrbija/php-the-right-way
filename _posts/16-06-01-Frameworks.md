---
isChild: true
title: Frejmvorci
anchor: frameworks
---

## Frejmvorci {#frameworks_title}

Umesto da "izmišljaju toplu vodu", dosta PHP programera koristi frejmvorke (frameworks) za razvoj web aplikacija.
Frejmvork apstrahuje većinu low-level pitanja i pruža koristan, jednostavan interejs za rešavanje nekih
uobičajenih zadataka.

Ne morate da koristite frejmvork za svaki projekat. Nekada je "čist" PHP bolji izbor, ali ako vam je potreban
frejmvork postoje tri glavne kategorije:

* Mikro frejmvorci (micro frameworks)
* Full-Stack frejmvorci
* Frejmvorci bazirani na komponentama (glue frameworks)

Mikro frejmvorci su u suštini maksimalno optimizovani wrapper-i za rutiranje HTTP request-a na callback,
kontroler, metod, itd. Ponekad dolaze sa dodatnim bibliotekama koje potpomažu razvoj, kao što su komponente
za komunikaciju sa bazom i slično. Najčešće se koriste za razvoj web servisa.

Mnogi frejmvorci dodaju priličan broj funkcionalnosti na ono što nude mikro frejmvorci, i takvi su poznati
kao Full-Stack frejmvorci. Oni često poseduju ugrađene ORM-ove, komponente za autentifikaciju, itd.

Frejmvorci bazirani na komponentama su zapravo kolekcije usko specijalizovanih i jednonamenskih biblioteka.
Moguće je iskombinovati komponente nekoliko frejmvorka ovog tipa i tako napraviti mikro ili full-stack frejmvork.

* [Popularni PHP frejmvorci](https://github.com/codeguy/php-the-right-way/wiki/Frameworks)