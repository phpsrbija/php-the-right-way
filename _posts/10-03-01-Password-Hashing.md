---
isChild: true
title: Hešovanje lozinki
anchor: password_hashing
---

## Hešovanje (Hashing) lozinki {#password_hashing_title}

Većina PHP aplikacija ima funkcionalnost koja podrazumeva prijavu korisnika (login). Korisnička imena
i lozinke se čuvaju u bazi podataka i kasnije se koriste za autentifikaciju korisnika pri prijavi.

Veoma je važno da pravilno [_hešujete_][3] lozinke pre nego što ih sačuvate. Hešovanje lozinki je nepovratan,
jednosmeran proces, koji se vrši nad korisničkom lozinikom. Pritom se kreira string fiksne dužine koji se ne može lako
rekonstruisati. Ovo znači da možete da uporedite dva heša da biste utvrdili da li potiču od istog stringa, ali ne možete
saznati vrednost izvornog stringa. Ako lozinke nisu hešovane, a vašoj bazi pristupa neovlašćena osoba,
svi korisnički nalozi biće kompromitovani.

Lozinke takođe trebaju biti pojedinačno [_posoljene (salted)_][5] tako što ćete dodati proizvoljni string svakoj lozinci pre nego što je hešujete.
Ovo sprečava napade uz pomoć rečnika i upotreba "rainbow tabela" (obrnuta lista kriptografskih heševa za uobičajene lozinke).

Hešovanje i soljenje (salting) su od vitalnog značaja jer korisnici često koriste iste lozinke za više servisa i kvalitet same lozinke može biti niskog nivoa.

Srećom, u današnje vreme PHP sve ovo rešava na lak način.

**Hešovanje lozinki pomoću `password_hash`**

U verziji PHP 5.5 je uvedena `password_hash()` funkcija. Ona trenutno koristi BCrypt, najjači algoritam koji PHP trenutno
podržava. U budućnosti će biti ažurirana da bi podržala više algoritama ako bude neophodno. Biblioteka The
`password_compat` je napravljena kako bi pružila kompatibilnost za starije verzije (PHP >= 5.3.7).

U primeru koji sledi hešujemo string, a onda proveravamo heš sa novim stringom. Pošto se naša dva izvorna stringa razlikuju
('secret-password' u poređenju sa 'bad-password') ovo logovanje će biti neuspešno.

{% highlight php %}
<?php
require 'password.php';

$passwordHash = password_hash('secret-password', PASSWORD_DEFAULT);

if (password_verify('bad-password', $passwordHash)) {
    // Ispravna lozinka
} else {
    // Pogrešna lozinka
}
{% endhighlight %}

`password_hash()` funkcija će se za vas pobrinuti za "soljenje (salting)". So (salt) je sačuvana zajedno sa algoritmom
i "cenom" (cost) kao jedan deo heša. Funkcija `password_verify()` se koristi da izdvoji ovu informaciju kako bi proverila
lozinku tako da vama nije potrebno odvojeno polje u bazi podataka da biste sačuvali vaše soli (salts).

* [Naučite više o `password_hash()`] [1]
* [`password_compat` za PHP >= 5.3.7 && < 5.5] [2]
* [Naučite o hešovanju s aspekta kriptografije] [3]
* [Naučite o solima (salts)] [5]
* [PHP `password_hash()` RFC] [4]

[1]: http://php.net/function.password-hash
[2]: https://github.com/ircmaxell/password_compat
[3]: http://en.wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash
[5]: https://en.wikipedia.org/wiki/Salt_(cryptography)
