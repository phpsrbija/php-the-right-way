---
isChild: true
title: Vagrant
anchor: vagrant
---

## Vagrant {#vagrant_title}

Izvršavanjem vaše aplikacije u okruženju koje se razlikuje tokom razvoja od
produkcije, može dovesti do pojave čudnih bagova kada postane dostupan
korisnicima. Prilično je zahtevno ažurirati različita okruženja za razvoj
sa istim verzijama svih biblioteka kada radite u timu.

Ako razvijate na Windows-u a koristite servere na Linux-u (ili bilo čemu sto
nije Windows), ili radite u timu, trebalo bi da razmotrite korišćenje virtualne
mašine. Ovo zvuči zahtevno, ali korišćenjem [Vagrant][vagrant]-a možete podesiti
jednostavnu virtuelnu mašinu u samo nekoliko koraka. Ove virtualne
mašine se onda mogu podešavati ručno, ili možete koristiti softver za
"konfigurisanje okruženja" kao što je [Puppet][puppet] ili [Chef][chef] da to
obavi za vas. Konfigurisanje okruženja virtualnih mašina je odličan
način da osigurate da je više virtualnih mašina konfigurisano na identičan način
i uklanja potrebu da imate komplikovane liste komandi za "konfigurisanje".
Takodje možete "uništiti" vašu virtualnu mašinu i rekreirati je u par komandi,
što čini pravljenje "nove" instalacije jednostavno i lako.

Vagrant pravi direktorijume koji vaš kod čini dostupan na vašoj i virtualnoj
mašini, što znači da možete praviti i menjati vaše fajlove na vašoj mašini a
onda ih izvršiti unutar virtualne mašine.

### Pomoć za početak korišćenja

Ako vam je potrebna pomoć da počete da koristite Vagrant, ova tri servisa vam
u tome mogu pomoći:

- [Rove][rove]: servis koji vam omogućava da generišete tipične Vagrant
konfiguracije, PHP je medju opcijama, konfiguriasnje se vrši pomoću Chef-a.
- [Puphpet][puphpet]: jednostavan interfejs koji ce vam pomoći da konfigurišete
virtualne mašine za PHP razvoj. **Vrlo fokusiran na PHP**. Pored lokalnih VM-a,
može se koristiti i za puštanje koda u produkciju na cloud servisima.
Konfigurisanje se vrši pomoću Puppet-a.
- [Protobox][protobox]: je aplikacija koja koristi Vagrant i web interfejs da bi
podesila lokalne virtualne mašine za razvoj. Jedan YAML dokument kontroliše sve
što je instalirano na virtualnoj mašini.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
