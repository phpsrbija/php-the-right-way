---
isChild: true
title: Prednosti
anchor: templating_benefits
---

## Prednosti {#templating_benefits_title}

Glavna korist od korišćenja templejta je jasno razdvajanje prezentacione logike od ostatka aplikacije.
Templejti imaju odgovornost isključivo za formatiranje i prikazivanje podataka. Oni nisu zaduženi za
dohvatanje i čuvanje podataka, niti za neke druge kompleksnije poslove. To za rezultat ima
čistiji, čitljiviji kôd, što je posebno korisno u timovima gde programeri rade na server-side kôdu
(kontroleri, modeli), a dizajneri na client-side delu (markup).

Takođe, templejti unapređuju organizaciju prezentacione logike. Oni su najčešće smešteni u "views"
folderu, svaki u posebnom fajlu. Ovo doprinosi praktičnijem iskorišćenju kôda, jer su veći blokovi
podeljeni na manje, višekratne (reusable) delove, takozvane parcele (partials). Na primer, header i
footer sekije vašeg sajta mogu biti definisane kao templejti, koji se onda učitavaju pre i posle
templejta za svaku pojedinačnu stranicu.

Konačno, u zavisnosti od biblioteke koju koristite, templejti obično brinu o bezbednosti, tako što automatski
_escape-uju_ sadržaj koji potiče od korisnika. Neke biblioteke čak omogućavaju sandbox-ovanje, pri čemu
je dizajnerima omogućen pristup isključivo određenim, proverenim promenljivama i funkcijama.
