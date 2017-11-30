---
title: Vodič za stil kodiranja
anchor: code_style_guide
---

# Vodič za stil kodiranja {#code_style_guide_title}

PHP zajednica je velika i raznolika, sastavljena od bezbroj biblioteka, frejmvorka i komponenti.
PHP programeri se često odluče za njih nekoliko i kombinuju ih u okviru jednog projekta. Bitno je da
PHP kôd bude u skladu sa (što je više moguće) opštim stilom kodiranja kako bi se programerima
olakšalo kombinovanje i integrisanje različitih biblioteka u svoje projekte.

[Framework Interop grupa][fig] je predložila i odobrila niz preporuka za stilove kodiranja. Pritom nisu sve
vezane za stil pisanja kôda, a one koje jesu su sledeće: [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] i [PSR-4][psr4].
Ove preporuke su zapravo setovi pravila koje neki projekti kao što su Drupal, Zend, Symfony, Laravel, CakePHP, phpBB,
AWS SDK, FuelPHP, Lithium, itd. počinju da usvajaju. I vi ih možete primenjivati u vašim ličnim projektima,
ili nastaviti sa korišćenjem nekog vašeg ličnog stila.

Bilo bi idealno da pišete PHP kôd koji je u skladu sa poznatim standardima. Ovo može biti bilo koja kombinacija PSR-ova
ili jedan od standarda kodiranja koje je definisao PEAR ili Zend. Ovo znači da će drugi programeri moći lako da čitaju
i rade sa vašim kôdom, a da će aplikacije koje koriste komponente biti konzistentne čak i pri radu sa dosta 3rd party kôda.

* [Pročitajte o PSR-0][psr0]
* [Pročitajte o PSR-1][psr1]
* [Pročitajte o PSR-2][psr2]
* [Pročitajte o PSR-4][psr4]
* [Pročitajte o PEAR standardima kodiranja][pear-cs]
* [Pročitajte o Symfony standardima kodiranja][symfony-cs]

Možete da koristite [PHP_CodeSniffer][phpcs] kako biste proverili da li je vaš kôd u skladu sa nekom od ovih preporuka,
ali i dodatke za tekst editore kao što je [Sublime Text][st-cs] u cilju dobijanja rezultata provera u realnom vremenu.

Automatksu korekciju izgleda kôda možete obaviti korišćenjem jednog od sledećih alata:

- Jedan je [PHP Coding Standards Fixer][phpcsfixer] koji je veoma dobro testiran.
- Takođe, može se koristiti alat [PHP Code Beautifier and Fixer][phpcbf] koji je uključen sa PHP_CodeSniffer-om da biste skladno podesili vaš kôd.

phpcs možete pokrenuti ručno iz konzole:

    phpcs -sw --standard=PSR2 file.php

Prikaziće greške kao i predloge za njihovo rešavanje. Ova komanda može biti od koristi ako je uključite u neki git hook.
Na taj način grane koje sadrže kôd koji nije u skladu sa određenim standardom neće moći da uđu u repozitorijum dok se ne poprave.

Ukoliko imate PHP_CodeSniffer onda probleme sa izgledom kôda koje on prijavljuje možete automatski popraviti uz pomoć alata [PHP Code Beautifier and Fixer][phpcbf].

    phpcbf -w --standard=PSR2 file.php

Druga opcija je da koristite [PHP Coding Standards Fixer][phpcsfixer]. Ovaj alat će vam prikazati koje vrste grešaka je vaš izgled kôda imao, pre nego što ga je on popravio.

    php-cs-fixer fix -v --level=psr2 file.php

Korišćenje engleskog jezika se preporučuje u slučaju svih imenovanja u kôdu i njegovoj infrastrukturi.
Komentari mogu biti pisani u bilo kom jeziku poznatom svim trenutnim i budućim učesnicima u razvoju kôda.


[fig]: http://www.php-fig.org/
[psr0]: http://www.php-fig.org/psr/psr-0/
[psr1]: http://www.php-fig.org/psr/psr-1/
[psr2]: http://www.php-fig.org/psr/psr-2/
[psr4]: http://www.php-fig.org/psr/psr-4/
[pear-cs]: http://pear.php.net/manual/en/standards.php
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[phpcbf]: https://github.com/squizlabs/PHP_CodeSniffer/wiki/Fixing-Errors-Automatically
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
