---
isChild: true
title: Virtuelni ili namenski serveri
anchor: virtual_or_dedicated_servers
---

## Virtuelni ili namenski serveri {#virtual_or_dedicated_servers_title}

Ako ste upućeni u administraciju sistema ili želite da je naučite, virtuelni ili namenski serveri daju potpunu kontrolu
nad produkcionim okruženjem Vaše aplikacije.

### nginx i PHP-FPM

PHP, preko ugrađenog PHP-ovog FastCGI proces menadžera (FPM) je lepo uparen sa [nginx](http://nginx.org), laganim web
serverom visokih performansi. Koristi manje memorije od Apache-a i bolje rukuje sa više istovremenih zahteva. Ovo je
naročito važno na virtuelnim serverima koji nemaju mnogo memorije za trošenje.

* [Pročitajte više o nginx][nginx]
* [Pročitajte više o PHP-FPM][phpfpm]
* [Pročitajte više o bezbednom podešavanju nginx and PHP-FPM][secure-nginx-phpfpm]

### Apache i PHP

PHP i Apache imaju dugu zajedničku istoriju. Apache je izuzetno konfigurabilan i ima mnogo dostupnih [modula][apache-modules] za
proširenje funkcionalnosti. To je popularan izbor na deljenim serverima koji se lako podešava za PHP frejmvorke i
aplikacije otvorenog koda kao što je WordPress. Nažalost, Apache koristi više resursa nego što ih koristi nginx po
default-u i ne može da rukuje sa toliko posetilaca istovremeno.

Apache ima nekoliko mogućih konfiguracija za pokretanje PHP-a. Najčešća i najlakša za podešavanje je [prefork MPM] sa mod_php5. Iako nije najefikasnija po pitanju memorije, najjednostavnija je za početak rada i za
korišćenje. Ovo je verovatno najbolji izbor ukoliko ne želite da se previše upuštate u aspekte serverske administracije.
Imajte na umu da ako koristite mod_php5 MORATE koristiti prefork MPM.

Alternativno, ukoliko želite da iz Apache-a izvučete bolje performanse i stabilnost, možete koristiti prednost istog FPM
sistema kao nginx i pokrenuti [worker MPM] ili [event MPM] sa mod_fastcgi ili mod_fcgid. Ova konfiguracija je po pitanju korišćenja memorije značajno efikasnija i mnogo brža, ali
zahteva i više posla oko podešavanja.

Ukoliko koristite Apache verziju 2.4 ili noviju, možete koristiti [mod_proxy_fcgi] kako biste dobili odlične performanse koje se lako podešavaju.

* [Pročitajte više o Apache][apache]
* [Pročitajte više o Multi-Processing modulima][apache-MPM]
* [Pročitajte više o mod_fastcgi][mod_fastcgi]
* [Pročitajte više o mod_fcgid][mod_fcgid]
* [Pročitajte više o mod_proxy_fcgi][mod_proxy_fcgi]
* [Pročitajte više o podešavanju Apache i PHP-FPM sa mod_proxy_fcgi][tutorial-mod_proxy_fcgi]


[nginx]: http://nginx.org/
[phpfpm]: http://php.net/install.fpm
[secure-nginx-phpfpm]: https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/
[apache-modules]: http://httpd.apache.org/docs/2.4/mod/
[prefork MPM]: http://httpd.apache.org/docs/2.4/mod/prefork.html
[worker MPM]: http://httpd.apache.org/docs/2.4/mod/worker.html
[event MPM]: http://httpd.apache.org/docs/2.4/mod/event.html
[apache]: http://httpd.apache.org/
[apache-MPM]: http://httpd.apache.org/docs/2.4/mod/mpm_common.html
[mod_fastcgi]: https://blogs.oracle.com/opal/entry/php_fpm_fastcgi_process_manager
[mod_fcgid]: http://httpd.apache.org/mod_fcgid/
[mod_proxy_fcgi]: https://httpd.apache.org/docs/current/mod/mod_proxy_fcgi.html
[tutorial-mod_proxy_fcgi]: https://serversforhackers.com/video/apache-and-php-fpm
