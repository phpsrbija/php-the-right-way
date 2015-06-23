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
svi korisnički nalozi biće kompromitovani. Neki korisnici (nažalost) koriste istu lozinku i za druge sajtove i servise.
Zbog toga je neophodno da bezbednosne aspekte tretirate ozbiljno.

**Hešovanje lozinki pomoću `password_hash`**

U verziji PHP 5.5 je uvedena `password_hash()` funkcija. Ona trenutno koristi BCrypt, najjači algoritam koji PHP trenutno
podržava. U budućnosti će biti ažurirana da bi podržala više algoritama ako bude neophodno. Biblioteka The
`password_compat` je napravljena kako bi pružila kompatibilnost za starije verzije (PHP >= 5.3.7).

U primeru koji sledi hešujemo string, a onda proveravamo heš sa novim stringom. Pošto se naša dva izvorna stringa razlikuju
('secret-password' vs. 'bad-password') ovo logovanje će biti neuspešno.

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


* [Naučite više o `password_hash()`] [1]
* [`password_compat` za PHP >= 5.3.7 && < 5.5] [2]
* [Naučite o hešovanju s aspekta kriptografije] [3]
* [PHP `password_hash()` RFC] [4]

[1]: http://php.net/function.password-hash
[2]: https://github.com/ircmaxell/password_compat
[3]: http://en.wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash
