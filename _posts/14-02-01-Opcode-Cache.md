---
isChild: true
title: Opcode keš
anchor: opcode_cache
---

## Opcode keš {#opcode_cache_title}

Kada se PHP fajl izvršava, on se prvo mora iskompajlirati u opkodove ([opcodes](http://php.net/manual/en/internals2.opcodes.php)),
mašinske instrukcije za procesor. Ukoliko izvorni kôd nije modifikovan, opkodovi će biti isti, tako da ovaj korak kompilacije
predstavlja samo trošenje procesorskih resursa.

Opcode keš sprečava suvišno kompajliranje, tako što se rezultujući opcode čuva u memoriji, a zatim se koristi u narednim izvršavanjima.
Obično će prvo proveriti potpis ili vreme poslednje izmene fajla, u slučaju ako je bilo bilo kakvih izmena.

Opcode keš će vašoj aplikaciji najverovatnije doneti značajno poboljšanje u brzini. Od verzije PHP 5.5 postoji ugrađen opcode keš nazvan [Zend OPcache][opcache-book].
U zavisnosti od vašeg PHP paketa/distribucije, uglavnom je uključen kao podrazumevana vrednost - proverite [opcache.enable](http://php.net/manual/en/opcache.configuration.php#ini.opcache.enable)
kao i rezultat poziva funkcije `phpinfo()` kako biste bili sigurni. Za prethodne verzije postoji PECL ekstenzija.

Saznajte više o opcode keširanju:

* [Zend OPcache][opcache-book] (ugrađen od verzije PHP 5.5)
* Zend OPcache (ranije poznat kao Zend Optimizer+) je sada [otvorenog kôda][Zend Optimizer+]
* [APC] (PHP <= 5.4)
* [XCache]
* [WinCache] (ekstenzija za MS Windows Server)
* [lista PHP akceleratora na Wikipediji][PHP_accelerators]


[opcache-book]: http://php.net/book.opcache
[APC]: http://php.net/book.apc
[XCache]: http://xcache.lighttpd.net/
[Zend Optimizer+]: https://github.com/zendtech/ZendOptimizerPlus
[WinCache]: http://www.iis.net/download/wincacheforphp
[PHP_accelerators]: http://en.wikipedia.org/wiki/List_of_PHP_accelerators
