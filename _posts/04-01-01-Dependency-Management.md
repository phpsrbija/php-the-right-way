---
title: Upravljanje zavisnostima (dependencies)
anchor: dependency_management
---

# Upravljanje zavisnostima (dependencies) {#dependency_management_title}

Na raspolaganju imate ogroman broj PHP biblioteka, frejmvorka i komponenti. Vaš projekat će verovatno koristiti
njih nekoliko, a sve te stvari su zapravo _zavisnosti projekta_. Do nedavno, PHP nije imao adekvatan način za upravljanje ovim
zavisnostima. Čak i ako ste njima upravljali ručno, i dalje ste morali da brinete o autoloading-u. Ali to više nije slučaj.

Trenutno postoje dva glavna sistema za upravljanja paketima (package managers) za PHP - [Composer] i [PEAR].
Composer je trenutno izbor broj jedan, ali treba pomenuti da je PEAR dosta dugo bio na toj poziciji.
Poznavanje PEAR-a može biti korisno, jer i dalje možete naći reference za njega, čak iako ga ne koristite.

[Composer]: #composer_and_packagist
[PEAR]: #pear
