---
isChild: true
title: Opcode keš
anchor: opcode_cache
---

## Opcode keš {#opcode_cache_title}

Kada se PHP fajl izvršava, on se u pozadini najpre kompajlira u opcode, a zatim se taj opcode izvršava.
Ako se PHP fajl ne menja, odgovarajući opcode će biti isti. To znači da korak kompajliranja predstavlja samo
bespotrebno trošenje procesorskih resursa.

Upravo ovde opcode keširanje stupa na scenu. Ono sprečava suvišno kompajliranje, tako što se rezultujući
opcode čuva u memoriji, a zatim se koristi u narednim izvršavanjima. Instalacija opcode keša je brza i
jednostavna, a vaša aplikacija će raditi znatno brže. Zaista nema razloga da ga ne koristite.

Od verzije PHP 5.5 postoji ugrađen opcode keš nazvan [OPcache][opcache-book]. On je takođe
dostupan i za prethodne verzije.

Saznajte više o opcode keširanju:

* [OPcache][opcache-book] (ugrađen od verzije PHP 5.5)
* [APC] (PHP <= 5.4)
* [XCache]
* [Zend Optimizer+] (deo Zend Server paketa)
* [WinCache] (ekstenzija za MS Windows Server)
* [lista PHP akceleratora][PHP_accelerators]


[opcache-book]: http://php.net/book.opcache
[APC]: http://php.net/book.apc
[XCache]: http://xcache.lighttpd.net/
[Zend Optimizer+]: http://www.zend.com/products/server/
[WinCache]: http://www.iis.net/download/wincacheforphp
[PHP_accelerators]: http://en.wikipedia.org/wiki/List_of_PHP_accelerators