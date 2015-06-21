---
isChild: true
title: Instalacija za Windows
anchor:  windows_setup
---

## Instalacija za Windows {#windows_setup_title}

Binarnu verziju možete preuzeti na [windows.php.net/download][php-downloads]. Nakon što raspakujete PHP,
preporučuje se da podesite [PATH][windows-path] na root vašeg PHP foldera (lokacija php.exe fajla) kako biste mogli da izvršavate PHP sa bilo kog mesta.

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
[windows-path]: http://www.windows-commandline.com/set-path-command-line/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
[easyphp]: http://www.easyphp.org/
[wamp]: http://www.wampserver.com/en/
[phpmanager]: http://phpmanager.codeplex.com/
[php-iis]: http://php.iis.net/
