---
isChild: true
anchor:  windows_setup
---

## Windows Setup {#windows_setup_title}

You can download the binaries from [windows.php.net/download][php-downloads]. After the extraction of PHP, it is recommended to set the [PATH][windows-path] to the root of your PHP folder (where php.exe is located) so you can execute PHP from anywhere.

For learning and local development you can use the built in webserver with PHP 5.4+ so you don't need to worry about
configuring it. If you would like an "all-in-one" which includes a full-blown webserver and MySQL too then tools such
as the [Web Platform Installer][wpi], [XAMPP][xampp], [EasyPHP][easyphp] and [WAMP][wamp] will
help get a Windows development environment up and running fast. That said, these tools will be a little different from
production so be careful of environment differences if you are working on Windows and deploying to Linux.

If you need to run your production system on Windows then IIS7 will give you the most stable and best performance. You
can use [phpmanager][phpmanager] (a GUI plugin for IIS7) to make configuring and managing PHP simple. IIS7 comes with
FastCGI built in and ready to go, you just need to configure PHP as a handler. For support and additional resources
there is a [dedicated area on iis.net][php-iis] for PHP.


[php-downloads]: http://windows.php.net/download/
[windows-path]: http://www.windows-commandline.com/set-path-command-line/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
[easyphp]: http://www.easyphp.org/
[wamp]: http://www.wampserver.com/en/
[phpmanager]: http://phpmanager.codeplex.com/
[php-iis]: http://php.iis.net/
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
