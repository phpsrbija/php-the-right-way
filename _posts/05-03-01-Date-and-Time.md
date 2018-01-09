---
isChild: true
title: Datum i vreme
anchor: date_and_time
---

## Datum i vreme {#date_and_time_title}

PHP poseduje DateTime klasu za potrebe čitanja, pisanja, poređenja i računanja datuma i vremena.
Postoji i dosta drugih funkcija za rad sa datumom/vremenom u PHP-u pored DateTime klase, ali ona
pruža dobar objektno-orijentisani interfejs za najčešće slučajeve korišćenja. Ova klasa može da
manipuliše i vremenskim zonama, ali to je van okvira ovog kratkog uvoda.

Da biste započeli sa radom sa DateTime klasom, konvertujte string koji sadrži datum i vreme u objekat pomoću
`createFromFormat()` proizvodne (factory) metode ili pozovite `new \DateTime` kako biste dobili trenutni datum/vreme.
Koristite `format()` metodu za konvertovanje DateTime instance u string.

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = DateTime::createFromFormat('d. m. Y', $raw);

echo 'Početni datum: ' . $start->format('Y-m-d') . "\n";
{% endhighlight %}

Računanje sa klasom DateTime je moguće korišćenjem DateInterval klase. DateTime ima metode kao što su `add()` and `sub()` koji prihvataju
DateInterval instancu kao argument. Nemojte pisati kôd koji očekuje isti broj sekundi svakog dana, jer će letnje i zimsko
računanje vremena i promene vremenske zone oboriti tu pretpostavku. Umesto toga koristite vremenske intervale. Za
računanje razlike između datuma koristite metodu `diff()`. Ona vraća DateInterval instancu, koja u sebi sadrži sve
potrebne informacije.

{% highlight php %}
<?php
// kloniraj $start i dodaj 1 mesec i 6 dana
$end = clone $start;
$end->add(new DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Razlika: ' . $diff->format('%m mesec, %d dana (ukupno: %a dana)') . "\n";
// Razlika: 1 mesec, 6 dana (ukupno: 37 dana)
{% endhighlight %}

Nad DateTime objektima je moguće raditi standardno poređenje:

{% highlight php %}
<?php
if ($start < $end) {
    echo "Početni je pre kranjeg datuma!\n";
}
{% endhighlight %}

Poslednji primer demonstrira korišćenje DatePeriod klase. Ona se koristi za iteraciju nad periodičnim događajima.
Može da primi dva DateTime objekta, početni i krajni datum, kao i interval po kojem treba da vraća rezultujuće datume.

{% highlight php %}
<?php
// ispisuj svaki četvrtak između $start i $end
$periodInterval = DateInterval::createFromDateString('first thursday');
$periodIterator = new DatePeriod($start, $periodInterval, $end, DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // ispisuj svaki datum u periodu
    echo $date->format('Y-m-d') . ' ';
}
{% endhighlight %}

[Carbon](http://carbon.nesbot.com) je popularna ekstenzija (produžetak) PHP API-ja za DateTime. Ona nasleđuje sve osobine
od DateTime klase tako da zahteva minimalne izmene postojećeg kôda dok donosi dodatne osobine kao što su podrška za lokalizaciju (Localization),
dodatni načini za dodavanje, oduzimanje i formatiranje objekata tipa DateTime, i dodatno sredstva za testiranje vašeg kôda
tako da možete da simulirate datum/vreme po vašem izboru.

* [Pročitajte više o DateTime klasi][datetime]
* [Pročitajte više o formatiranju datuma][dateformat] (prihvaćene opcije za formatiranje datuma)

[datetime]: http://php.net/book.datetime
[dateformat]: http://php.net/function.date
