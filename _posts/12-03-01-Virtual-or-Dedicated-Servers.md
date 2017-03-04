---
title:   Virtual or Dedicated Servers
isChild: true
title: Virtuelni ili namenski serveri
anchor: virtual_or_dedicated_servers
---

## Virtuelni ili namenski serveri {#virtual_or_dedicated_servers_title}

Ako ste upućeni u administraciju sistema ili želite da je naučite, virtuelni ili namenski serveri daju potpunu kontrolu
nad produkcionim okruženjem Vaše aplikacije.

### nginx i PHP-FPM

PHP, preko ugrađenih PHP-ovih FastCGI proces menadžera (FPM) je lepo uparen sa [nginx](http://nginx.org), laganim web
serverom visokih performansi. Koristi manje memorije od Apache-a i bolje rukuje sa više istovremenih zahteva. Ovo je
naročito važno na virtuelnim serverima koji nemaju mnogo memorije za trošenje.

* [Pročitajte više o nginx](http://nginx.org)
* [Pročitajte više o PHP-FPM](http://php.net/manual/en/install.fpm.php)
* [Pročitajte više o bezbednom podešavanju nginx and PHP-FPM](https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/)

### Apache i PHP

PHP i Apache imaju dugu zajedničku istoriju. Apache je izuzetno konfigurabilan i ima mnogo dostupnih [modula](http://httpd.apache.org/docs/2.4/mod/) za
proširenje funkcionalnosti. To je popularan izbor na deljenim serverima koji se lako podešava za PHP frejmvorke i
aplikacije otvorenog koda kao što je WordPress. Nažalost, Apache koristi više resursa nego što ih koristi nginx po
default-u i ne može da rukuje sa toliko posetilaca istovremeno.

Apache ima nekoliko mogućih konfiguracija za pokretanje PHP-a. Najčešća i najlakša za podešavanje je [prefork MPM](http://httpd.apache.org/docs/2.4/mod/prefork.html) sa mod_php5. Iako nije najefikasnija po pitanju memorije, najjednostavnija je za početak rada i za
korišćenje. Ovo je verovatno najbolji izbor ukoliko ne želite da se previše upuštate u aspekte serverske administracije.
Imajte na umu da ako koristite mod_php5 MORATE koristiti prefork MPM.

Alternativno, ukoliko želite da iz Apache-a izvučete bolje performanse i stabilnost, možete koristiti prednost istog FPM
sistema kao nginx i pokrenuti [worker MPM](http://httpd.apache.org/docs/2.4/mod/worker.html) ili [event MPM](http://httpd.apache.org/docs/2.4/mod/event.html) sa mod_fastcgi ili mod_fcgid. Ova konfiguracija je po pitanju korišćenja memorije značajno efikasnija i mnogo brža, ali
zahteva i više posla oko podešavanja.

* [Pročitajte više o Apache](http://httpd.apache.org/)
* [Pročitajte više o Multi-Processing modulima](http://httpd.apache.org/docs/2.4/mod/mpm_common.html)
* [Pročitajte više o mod_fastcgi](http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html)
* [Pročitajte više o mod_fcgid](http://httpd.apache.org/mod_fcgid/)
