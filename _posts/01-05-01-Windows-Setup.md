---
isChild: true
title: Instalacija za Windows
anchor: windows_setup
---

## Instalacija za Windows {#windows_setup_title}

PHP je dostupan na nekoliko načina na Windows-u. Možete [preuzeti binarnu verziju][php-downloads],
a do skora ste mogli da koristite i '.msi' fajl za instalaciju. Podrška za ovaj instalacioni fajl je
prestala sa PHP verzijom 5.3.0.

Za učenje i razvoj u lokalu, možete koristiti ugrađeni web server sa PHP 5.4+ tako da se ne morate
brinuti o njegovoj konfiguraciji. Ako preferirate "sve-u-jednom" rešenja koja sadrže kompletan web server
sa sve MySQL bazom podataka, onda ce Vam alati kao što su [Web Platform Installer][wpi],
[XAMPP][xampp], [EasyPHP][easyphp] i [WAMP][wamp] pomoći da veoma brzo imate radno okruženje pod Windows-om.
Treba napomenuti da će se okruženje koje ovi alati naprave verovatno malo razlikovati od onoga u produkciji,
tako da morate obratiti pažnju na te razlike ako razvijate na Windows-u, a produkcija vam je na Linux-u.

Ako je potrebno da vam produkcija bude na Windows-u, onda će IIS7 pružiti najveću stabilnost i najbolje performanse.
Možete koristiti [phpmanager][phpmanager] (GUI dodatak za IIS7) za pojednostavljenje konfiguracije i upravljanja PHP-om.
IIS7 dolazi sa ugrađenim FastCGI-om, spremnim za upotrebu, i sve što je potrebno je konfigurisati PHP kao handler.
Za podršku i dodatne informacije pogledajte [deo posvećen PHP-u na iis.net][php-iis].


[php-downloads]: http://windows.php.net
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
[easyphp]: http://www.easyphp.org/
[wamp]: http://www.wampserver.com/en/
[phpmanager]: http://phpmanager.codeplex.com/
[php-iis]: http://php.iis.net/
