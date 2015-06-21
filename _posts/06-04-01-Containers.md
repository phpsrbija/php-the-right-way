---
isChild: true
title: Kontejneri
anchor: containers
---

## Kontejneri (Containers) {#containers_title}

Prva stvar koju treba razumeti u vezi Dependency Injection kontejnera jeste da oni nisu isto što i Dependency Injection.
Kontejner je praktičan alat koji nam pomaže u implementaciji Dependency Injection pristupa, pri čemu oni mogu biti i loše
iskorišćeni za implementaciju anti-paterna - Servis lokacije (Service Location). Korišćenje DI kontejnera kao lokatora servisa
obično proizvodi jaču zavisnost na sâm kontejner nego na stvaran dependency kojeg vaša klasa treba da koristi. To takođe čini vaš kôd
nepreglednim, manje transparentnim i u krajnjem slučaju težim za testiranje.

Većina modernih frejmvorka ima svoj Dependency Injection kontejner koji omogućava da definišete vaše zavisnosti putem
konfiguracije. Ovo zapravo znači da možete pisati kôd aplikacije koji je čist i razdvojen, baš kao i sâm frejmvork nad kojim je izgrađen.
