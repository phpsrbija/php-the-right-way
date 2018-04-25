---
isChild: true
title: MySQL ekstenzija
anchor: mysql_extension
---

# MySQL ekstenzija {#mysql_extension_title}

[mysql] ekstenzija za PHP je neverovatno stara i prevaziđena sa druge dve ekstenzije:

- [mysqli]
- [pdo]

[mysql] ekstenzija za PHP ne samo da više nije u aktivnom razvoju, već je [prevaziđena od verzije PHP 5.5.0][mysql_deprecated] i
**[zvanično uklonjena u verziji PHP 7.0][mysql_removed]**.

Da biste se sačuvali od _kopanja_ po podešavanjima u vašem `php.ini` fajlu da biste videli koji modul koristite, jedna
od opcija jeste da u vašem tekst editoru izvršite pretragu za `mysql_*` termin. Ukoliko pronađete bilo koju od funkcija kao što su
`mysql_connect()` i `mysql_query()` to znači da je `mysql` ekstenzija u upotrebi.

Čak ukoliko još uvek ne koristite PHP verziju 7.x, nerazmatranje da izvršite ovu nadogradnju što pre je moguće će vam samo
otežati nadogradnju kada se zaista odlučite za PHP 7.x. Najbolja opcija je da zamenite korišćenje mysql esktenzije sa [mysqli] ili [PDO] u skladu sa sopstvenim tempom razvoja.

**Ukoliko vršite nadogradnju sa [mysql] na [mysqli] čuvajte se lenjog uputstva za nadogradnju koji predlaže da je samo dovoljno da
pretražite i zamenite `mysql_*` sa `mysqli_*`. Ne samo da je to preveliko uprošćavanje, već se i ne spominju prednosti
koje mysqli pruža, kao što su vezivanje parametara (parameter binding), koje [PDO][pdo] takođe nudi.**

* [PHP: Izbor API-a za MySQL][mysql_api]
* [PDO tutorijal za MySQL programere][pdo4mysql_devs]

[mysql]: http://php.net/mysql
[mysql_deprecated]: http://php.net/migration55.deprecated
[mysql_removed]: http://php.net/manual/en/migration70.removed-exts-sapis.php
[mysqli]: http://php.net/mysqli
[pdo]: http://php.net/pdo
[mysql_api]: http://php.net/mysqlinfo.api.choosing
[pdo4mysql_devs]: http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers
