---
isChild: true
title: MySQL ekstenzija
anchor: mysql_extension
---

# MySQL ekstenzija {#mysql_extension_title}

[mysql] ekstenzija za PHP više nije u aktivnom razvoju i [zvanično je prevaziđena od verzije PHP 5.5.0][mysql_deprecated],
što znači da će biti uklonjena u nekoj od sledećih verzija. Ako u vašim aplikacijama koristite `mysql_*` funkcije,
kao što su `mysql_connect()`, onda ćete u nekom momentu biti prinuđeni da prepravite kôd, a najbolja opcija je da
zamenite korišćenje mysql esktenzije sa [mysqli] ili [PDO] u skladu sa sopstvenim tempom razvoja.

**Ako počinjete od nule onda nikako nemojte koristiti [mysql] ekstenziju, već koristite ili
[MySQLi ekstenziju][mysqli] ili [PDO].**

* [PHP: Izbor API-a za MySQL][mysql_api]
* [PDO tutorijal za MySQL programere][pdo4mysql_devs]

[mysql]: http://php.net/mysql
[mysql_deprecated]: http://php.net/migration55.deprecated
[mysqli]: http://php.net/mysqli
[pdo]: http://php.net/pdo
[mysql_api]: http://php.net/mysqlinfo.api.choosing
[pdo4mysql_devs]: http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers
