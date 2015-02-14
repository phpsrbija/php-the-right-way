---
isChild: true
title: Izveštaji o greškama (Error Reporting)
anchor: error_reporting
---

## Izveštaji o greškama (Error Reporting) {#error_reporting_title}

Logovanje grešaka može biti korisno prilikom traženja problematičnih mesta u vašoj aplikaciji, ali istovremeno može
javno otkriti informacije o strukturi aplikacije. Da biste na pravi način zaštitili vašu aplikaciju od problema koje
može izazvati javno prikazivanje poruka o greškama, morate posebno podesiti server u slučaju razvojnog (development)
i produkcionog (live) okruženja aplikacije.

### Razvojno okruženje

Da biste prikazali svaku moguću grešku prilikom razvoja, postavite sledeće vrednosti u vašem `php.ini` fajlu:

{% highlight ini %}
display_errors = On
display_startup_errors = On
error_reporting = -1
log_errors = On
{% endhighlight %}

> Prosleđivanje vrednosti `-1` će prikazati svaku grešku, čak i nakon što budu dodati novi nivoi i konstante u budućim
> verzijama PHP-a. Konstanta `E_ALL` takođe ima isti efekat od verzije 5.4 - [php.net](http://php.net/function.error-reporting).

`E_STRICT` nivo je uveden u verziji 5.3.0 i nije bio deo `E_ALL` sve do verzije 5.4.0. Šta to tačno znači?
Apropo prikazivanja svih grešaka u verziji 5.3, to znači da morate da koristite ili `-1` ili `E_ALL | E_STRICT`.

**Prijavljivanje svih grešaka po verzijama PHP-a**

* &lt; 5.3 `-1` or `E_ALL`
* &nbsp; 5.3 `-1` or `E_ALL | E_STRICT`
* &gt; 5.3 `-1` or `E_ALL`

### Produkciono (live) okruženje

Da biste sakrili greške u vašem produkcionom okruženju, podesite `php.ini` na sledeći način:

{% highlight ini %}
display_errors = Off
display_startup_errors = Off
error_reporting = E_ALL
log_errors = On
{% endhighlight %}

Sa ovim podešavanjima, greške će se i dalje upisivati u error log, ali se neće prikazivati korisniku.
Za više informacija o ovim podešavanjima, proučite PHP manual:

* [error_reporting](http://php.net/errorfunc.configuration#ini.error-reporting)
* [display_errors](http://php.net/errorfunc.configuration#ini.display-errors)
* [display_startup_errors](http://php.net/errorfunc.configuration#ini.display-startup-errors)
* [log_errors](http://php.net/errorfunc.configuration#ini.log-errors)
