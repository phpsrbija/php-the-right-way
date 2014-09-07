---
isChild: false
title: Vodič za stil kodiranja
anchor: code_style_guide
---

# Vodič za stil kodiranja {#code_style_guide_title}

PHP zajednica je velika i raznolika, sastoji se od bezbroj biblioteka,
framework-a i komponenti. Uobičajeno je za PHP programere da id odaberu nekoliko
i kombinuju ih u jedan projekat. Važno je da PHP kod prati (što je bliže
moguće) opšteg stila kodiranja koji olakšava programerima da kombinuju razne
biblioteke u svoje projekte.

[Framework Interop Group][fig] je predložila i odobrila seriju preporuka, koje
se ne odnose samo na stil kodiranja. One koje se odnose na stil kodiranja
su [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] i [PSR-4][psr4]. Ove preporuke
su samo skup pravila koje neki projekti kao što su Drupal, Zend, Symfony,
CakePHP, phpBB, AWS SDK, FuelPHP, Lithium itd, počinju da usvajaju. Možete ih
koristiti u svojim projektima, ili nastaviti da koristitie vaš lični stil.

Idealno bi bilo da pišete PHP kod koji se pridržava poznatih standarda. To može
biti bilo koja kombinacija PSR preporuka, ili neki od standarda koje je napravio
PEAR ili Zend. Kao rezultat drugi programeri ce moći lakše da čitaju vaš kod,
da rade sa njim, a aplikacije koje implementiraju komponente će biti
konzistentne cak i kad rade sa kodom koji je napisao neko drugi.

* [Pročitajte više o PSR-0][psr0]
* [Pročitajte više o PSR-1][psr1]
* [Pročitajte više o PSR-2][psr2]
* [Pročitajte više o PSR-4][psr4]
* [Pročitajte više o PEAR Standardima Kodiranja][pear-cs]
* [Pročitajte više o Zend Standardima Kodiranja][zend-cs]
* [Pročitajte više o Symfony Standardima Kodiranja][symfony-cs]

Možete koristiti [PHP_CodeSniffer][phpcs] da proverite da li je vaš kod u skladu
sa bilo kojom od ovih preporuka, i plugine za tekst editore kao što je
[Sublime Text 2][st-cs] da dobijete povratnu informaciju u toku rada.

Možete koristiti [PHP Coding Standards Fixer][phpcsfixer] koji je napisao
Fabien Potencier da automatski izmeni vaš kod tako da je u skladu sa ovim
standardima, što će vam uštedeti vreme od ispravljanja ovih problema ručno.

Preferirajte Engleski za imena simbola i infrastrukturu koda. Komentari mogu
biti pisani na bilo kojem jeziku koji je lako razumljiv svim trenutnim i budućim
učesnicima u razvoju koda.

[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
