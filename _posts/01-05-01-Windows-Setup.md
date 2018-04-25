---
isChild: true
title: Instalacija za Windows
anchor:  windows_setup
---

## Instalacija za Windows {#windows_setup_title}

Binarnu verziju možete preuzeti na [windows.php.net/download][php-downloads]. Nakon što raspakujete PHP,
preporučuje se da podesite [PATH][windows-path] na vaš PHP folder (lokacija php.exe fajla) kako
biste mogli da izvršavate PHP sa bilo kog mesta.

Za učenje i razvoj u lokalu, možete koristiti ugrađeni web server sa PHP 5.4+ tako da se ne morate
brinuti o njegovoj konfiguraciji. Ako preferirate "sve u jednom" rešenja koja sadrže kompletan web server
sa sve MySQL bazom podataka, onda će vam alati kao što su [Web Platform Installer][wpi],
[XAMPP][xampp], [EasyPHP][easyphp], [OpenServer][openserver] i [WAMP][wamp] pomoći da veoma brzo imate radno okruženje pod Windows-om.
Treba napomenuti da će se okruženje koje ovi alati naprave verovatno razlikovati od onoga u produkciji,
tako da morate obratiti pažnju na te razlike ako razvijate na Windows-u, a produkcijsko okruženje vam je na Linux-u.

Ako je potrebno da vam produkcijsko okruženje bude na Windows-u, onda će IIS7 pružiti najveću stabilnost i najbolje performanse.
Možete koristiti [phpmanager][phpmanager] (GUI dodatak za IIS7) za pojednostavljenje konfiguracije i upravljanja PHP-om.
IIS7 dolazi sa ugrađenim FastCGI-om, spremnim za upotrebu, i sve što je potrebno je konfigurisati PHP kao _handler_.
Za podršku i dodatne informacije pogledajte [deo posvećen PHP-u na iis.net][php-iis].

Generalno izvršavanje vaše aplikacije u drugačijim okruženjima u development i produkcionom modu može dovesti do čudnih grešaka koje će početi da iskaču kada odete uživo. Ako razvijate na Windows-u i deploy-ujete na Linux-u (ili bilo šta drugo osim Windows-a) onda biste trebali da razmislite da koristite [Virtuelnu Mašinu](/#virtualization_title).

Chris Tankersley ima veoma koristan blog post o alatima koje on koristi da bi [razvijao uz pomoć PHP-a na Windows-u][windows-tools].

[windows-path]: http://www.windows-commandline.com/set-path-command-line/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
[easyphp]: http://www.easyphp.org/
[openserver]: http://open-server.ru/
[wamp]: http://www.wampserver.com/en/
[php-downloads]: http://windows.php.net/download/
[phpmanager]: http://phpmanager.codeplex.com/
[php-iis]: http://php.iis.net/
[windows-tools]: http://ctankersley.com/2016/11/13/developing-on-windows-2016/
