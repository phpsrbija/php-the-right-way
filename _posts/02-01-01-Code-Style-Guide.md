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
Ove preporuke su zapravo setovi pravila koje neki projekti kao što su Drupal, Zend, Symfony, CakePHP, phpBB,
AWS SDK, FuelPHP, Lithium, itd. počinju da usvajaju. I vi ih možete primenjivati u vašim ličnim projektima,
ili nastaviti sa korišćenjem nekog vašeg ličnog stila.

Bilo bi idealno da pišete PHP kôd koji je u skladu sa poznatim standardima. Ovo može biti bilo koja kombinacija PSR-ova
ili jedan od standarda kodiranja koje je definisao PEAR ili Zend. Ovo znači da će drugi programeri moći lako da čitaju
i rade sa vašim kôdom, a da će aplikacije koje koriste komponente biti konzistentne čak i pri radu sa dosta 3rd party kôda.

* [Pročitajte o PSR-0][psr0]
* [Pročitajte o PSR-1][psr1]
* [Pročitajte o PSR-2][psr2]
* [Pročitajte o PEAR standardima kodiranja][pear-cs]
* [Pročitajte o Symfony standardima kodiranja][symfony-cs]

Možete da koristite [PHP_CodeSniffer][phpcs] kako biste proverili da li je vaš kôd u skladu sa nekom od ovih preporuka,
ali i dodatke za tekst editore kao što je [Sublime Text 2][st-cs] u cilju dobijanja rezultata provera u realnom vremenu.

Automatksu korekciju izgleda kôda možete obaviti korišćenjem jednog od sledeća dva alata. Prvi je [PHP Coding Standards Fixer][phpcsfixer]
kojeg je napravio Fabien Potencier, a koji je veoma dobro testiran. Veći je i sporiji, ali isto tako
veoma stabilan i koriste ga veliki projekti kao što su Magento i Symfony. Druga opcija je [php.tools][phptools],
koji je postao popularan zahvaljujući [sublime-phpfmt][sublime-phpfmt] dodatku. Iako je noviji, postiže značajne
rezultate po pitanju performansi, pa je samim tim korekcija kôda u realnom vremenu dosta tečnija.

Korišćenje engleskog jezika se preporučuje u slučaju svih imenovanja u kôdu i njegovoj infrastrukturi.
Komentari mogu biti pisani u bilo kom jeziku poznatom svim trenutnim i budućim učesnicima u razvoju kôda.


[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
[phptools]: https://github.com/dericofilho/php.tools
[sublime-phpfmt]: https://github.com/dericofilho/sublime-phpfmt
