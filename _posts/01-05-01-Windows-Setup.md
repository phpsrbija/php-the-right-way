---
isChild: true
title: Instalacija za Windows
anchor: windows_setup
---

## Instalacija za Windows {#windows_setup_title}

PHP je dostupan na nekoliko načina na Windows-u. Možete [skinuti binarnu verziju](php-downloads)(php-downloads)
a do skora ste mogli da koristite i '.msi' alat za instalaciju. Podrška za alat za instalaciju prestaje sa
PHP verzijom 5.3.0.

Za učenje i razvoj u lokalu, možete koristiti ugrađeni web server sa PHP 5.4+
tako da se ne morate brinuti o konfiguraciji. Ako preferirate kompletne "Sve-u-jednom" pakete koji potpuni web server
sa MySQL bazom podataka, onda ce Vam alati kao [Web Platform Installer][wpi], [Zend Server CE][zsce], [XAMPP][xampp] i
[WAMP][wamp] pomoći da brzo podesite i pokrenete okruženje pod Windowsom. Treba napomenuti da se ovi alati razlikuju od
verzija u produkciji, tako da morate paziti na razlike u okrućenju ako razvijate na Windows-u
a produkcija Vam je na Linux-u.

Ako je potrebno da Vam produkcija bude na Windows-u, onda će Vam IIS7 pružiti najveću stabilnost i najbolje performanse.
Možete koristiti [phpmanager][phpmanager] (GUI dodatak za IIS7) za pojednostavljenje konfiguracije i upravljanje PHP-om.
IIS7 dolazi sa FastCGI ugradjenim i spremnim za upotrebu, samo je podtreno konfigurisati PHP kao handler.
Za podrsku i dodatne resurse pogledajte [deo posvecen PHP na iis.net][php-iis]

[php-downloads]: http://windows.php.net
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
[easyphp]: http://www.easyphp.org/
[wamp]: http://www.wampserver.com/en/
[phpmanager]: http://phpmanager.codeplex.com/
[php-iis]: http://php.iis.net/
