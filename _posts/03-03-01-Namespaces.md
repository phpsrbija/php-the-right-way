---
isChild: true
title: Namespace-ovi
anchor:  namespaces
---

## Namespace-ovi {#namespaces_title}

Kao što je prethodno navedeno, PHP zajednica se sastoji od mnogo programera koji stvaraju gomilu kôda. To znači da kôd jedne
biblioteke može da koristi isto ime klase kao neka druga biblioteka. Kada se obe biblioteke koriste u istom namespace-u,
dolazi do kolizije i problema.

_Namespace-ovi_ rešavaju ovaj problem. Kao što je i opisano u PHP manual-u, namespace-ovi se mogu uporediti sa
direktorijumima operativnog sistema koji fajlove _dele na imenski prostor_; dva istoimena fajla mogu postojati istovremeno u
različitim direktorijumima. Isto tako, dve PHP klase istog imena mogu postojati u različitim PHP namespace-ovima. Jako jednostavno.

Veoma je važno je da koristite namespace-ove u vašem kôdu kako bi drugi programeri mogli da ga koriste
bez straha od kolizije sa drugim bibliotekama.

Jedan od preporučenih načina za korišćenje namespace-ove opisan je u okviru [PSR-4][psr4], koji ima za cilj da pruži
standardizovanu konvenciju za fajlove, klase i namespace-ove, kako bi se omogućilo jednostavnije uključivanje kôda.

U okrobru 2014. godine, PHP-FIG je prethodni autoloading standard: [PSR-0][psr0], označio kao prevaziđen (deprecated),
i zamenio ga je upravo [PSR-4][psr4]. Trenutno su oba standarda u upotrebi, pri čemu PSR-4 zahteva PHP 5.3,
dok mnogi projekti na PHP 5.2 koriste PSR-0. Ako nameravate da koristite autoloading standard za neku novu aplikaciju
ili paket, onda definitivno treba da uzmete u obzir PSR-4.

* [Pročitajte više o Namespace-ovima][namespaces]
* [Pročitajte o PSR-0][psr0]
* [Pročitajte o PSR-4][psr4]


[namespaces]: http://php.net/language.namespaces
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
