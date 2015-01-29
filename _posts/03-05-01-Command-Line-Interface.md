---
isChild: true
anchor:  command_line_interface
---

## Interfejs sa komandne linije (Command Line Interface - CLI) {#command_line_interface_title}

PHP je napravljen prvenstveno radi pisanja web aplikacija, ali je takođe koristan za skriptne programe koji se
izvršavaju sa komandne linije. PHP programi sa komandne linije mogu vam pomoći da automatizujete uobičajene zadatke
kao što su testiranje, razvoj i administracija aplikacije.

CLI PHP programi su moćni jer možete da koristite kôd vaše aplikacije direktno, bez potrebe da napravite i obezbedite
web GUI (grafički interfejs) za nju. Samo nikako **nemojte** smeštati vaše CLI PHP skripte u javni root direktorijum!

Pokušajte da pokrenete PHP sa komandne linije:

{% highlight console %}
> php -i
{% endhighlight %}

Opcija `-i` će ispisati vašu PHP konfiguraciju isto kao i [`phpinfo`][phpinfo] funkcija.

Opcija `-a` omogućava interaktivni shell, sličan Ruby-jevom IRB ili Python-ovom interaktivnom shell-u. Postoji još dosta
korisnih [CLI opcija][cli-options].

Hajde da napišemo jednostavan "Hello, $name" CLI program. Najpre napravite fajl sa imenom `hello.php`,
sa sledećim sadržajem:

{% highlight php %}
<?php
if ($argc !== 2) {
    echo "Usage: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
{% endhighlight %}

PHP postavlja dve specijalne promenljive na osnovu argumenata koje se prosleđuju pri pokretanju vaše skripte. [`$argc`][argc] je
integer koji sadrži *broj* argumenata, a [`$argv`][argv] je niz koji sadrži *vrednost* svakog argumenta.
Prvi argument je uvek naziv fajla vaše PHP skripte, u ovom slučaju to je `hello.php`.

Komandi `exit()` se prosleđuje broj različit od nule kako bi se shell-u skrenula pažnja da komanda nije uspela. Najčešće
korišćeni izlazni kodovi su dostupni [ovde][exit-codes].

Pokretanje prethodne skripte iz komandne linije:

{% highlight console %}
> php hello.php
Usage: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}

 * [Naučite o izvršavanju PHP-a sa komandne linije][php-cli]
 * [Naučite o podešavanju Windows-a sa ciljem izvršavanja PHP-a sa komandne linije][php-cli-windows]


[phpinfo]: http://php.net/function.phpinfo
[cli-options]: http://php.net/features.commandline.options
[argc]: http://php.net/reserved.variables.argc
[argv]: http://php.net/reserved.variables.argv
[exit-codes]: http://www.gsp.com/cgi-bin/man.cgi?section=3&amp;topic=sysexits
[php-cli]: http://php.net/features.commandline
[php-cli-windows]: http://php.net/install.windows.commandline
