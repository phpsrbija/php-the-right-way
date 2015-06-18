---
isChild: true
title: Instalacija za Mac
anchor: mac_setup
---

## Instalacija za Mac {#mac_setup_title}

OS X dolazi za preinstaliraom PHP verzijom koja je obično malo starija u odnosu na poslednju stabilnu verziju.
Mountain Lion dolazi sa verzijom 5.3.10, Mavericks sa 5.4.17, Yosemite sa 5.5.9, ali to nije dovoljno dobro
pošto je dostupna novija verzija PHP 5.6.

Postoji nekoliko načina za instalaciju PHP-a na OS X-u.

### Instalacija PHP-a preko Homebrew-a

[Homebrew] je moćan paket manadžer za OS X, pomoću kojeg vrlo lako možete da instalirate PHP i njegove ekstenzije.
[Homebrew PHP] je repozitorijum koji sadrži različite PHP "formule" za Homebrew, putem kojeg možete instalirati sâm PHP.

Trenutno, moguće je instalirati verzije `php53`, `php54`, `php55` ili `php56` pomoću `brew install` komande, a zatim ih menjati
izmenom `PATH` varijable. Alternativa ovome je korišćenje [brew-php-switcher][brew-php-switcher] alata, koji omogućava automatsku promenu verzije.

### Instalacija PHP-a preko Macports-a

[MacPorts] projekat je open-source inicijativa za dizajniranje jednostavnog sistema za kompajliranje, instalaciju i ažuriranje
bilo command-line, X11 ili Aqua baziranih open-source programa na OS X operativnom sistemu.

MacPorts podržava pre-kompajlirane fajlove, tako da ne morate ponovo da kompajlirate svaki dependency
iz izvornih tarball fajlova, i olakšava vam život ako nemate nijedan instaliran paket na vašem sistemu.

Trenutno, moguće je instalirati verzije `php53`, `php54`, `php55` ili `php56` pomoću `port install` komande, na primer:

    sudo port install php54
    sudo port install php55

Nakon toga možete izvršavati `select` komandu za promenu aktivne verzije PHP-a:

    sudo port select --set php php55

### Instalacija PHP-a preko phpbrew-a

[phpbrew] je alat za instalaciju i upravljanje sa više verzija PHP-a. Ovo može biti veoma korisno ako
dve različite aplikacije/projekta zahtevaju različite verzije PHP-a, pritom ne koristite virtuelne mašine.

### Instalacija PHP-a putem Liip's installer-a

Još jedna popularna opcija je [php-osx.liip.ch] koje omogućava jednostavnu instalaciju verzija 5.3 do 5.6.
On ne prepisuje PHP fajlove instalirane od strane Apple-a, već instalaciju vrši na zasebnoj lokaciji (/usr/local/php5).

### Ručno kompajliranje source-a

Još jedna opcija koja vam daje kontrolu nad verzijom PHP-a koju instalirate je [ručno kompajliranje][mac-compile].
U tom slučaju vodite računa da instalirate bilo [Xcode][xcode-gcc-substitution] ili Apple-ov ["Command Line Tools za XCode"]
dostupnu na Apple-ovom Mac Developer centru.

### "Sve u jednom" instaleri

Prethodna rešenja će vam obezbediti sâm PHP, ali ne i stvari kao što su Apache, Nginx ili SQL server.
"Sve u jednom" rešenja kao što su [MAMP][mamp-downloads] ili [XAMPP][xampp] će instalirati i sve te
druge programe, ali ta jednostavnost instalacije kao kompromis ima manjak fleksibilnosti.


[Homebrew]: http://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: http://php-osx.liip.ch/
[mac-compile]: http://php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools za XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/
[xampp]: http://www.apachefriends.org/en/xampp.html
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
