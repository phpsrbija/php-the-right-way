---
isChild: true
title: Slojevi za apstrakciju (Database Abstraction Layers - DAL)
anchor: databases_abstraction_layers
---

## Slojevi za apstrakciju (Database Abstraction Layers - DAL) {#databases_abstraction_layers_title}

Mnogi frejmvorci imaju sopstveni DAL koji može, a ne mora da bude "nad" [PDO-om][1].
Oni najčešće emuliraju mogućnosti jednog sistema baze podataka koje nedostaju u drugom, tako što
pretvaraju upite u PHP metode, dajući nam apstrakciju same baze, a ne samo konekcije na bazu kao
što je to slučaj sa PDO-om. Ovo će naravno uneti i malo overhead-a, ali ako pravite portabilnu aplikaciju
koja treba da radi sa MySQL, PostgreSQL i SQLite bazama, onda se malo overhead-a isplati u korist čistote kôda.

Neki slojevi za apstrakciju su napravljeni u skladu sa [PSR-0][psr0] i [PSR-4][psr4] namespace
standardima, tako da mogu da se integrišu u bilo koju aplikaciju:

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]

[1]: http://www.php.net/manual/en/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[4]: http://packages.zendframework.com/docs/latest/manual/en/index.html#zend-db
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/Propel/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
