---
isChild: true
anchor:  test_driven_development
---

## Razvoj vođen testiranjem (Test Driven Development - TDD) {#test_driven_development_title}

Sa [Wikipedia-je](http://en.wikipedia.org/wiki/Test-driven_development):

> Razvoj vođen testiranjem (TDD) je proces razvoja softvera koji se bazira na ponavljanju kratkih razvojnih
> krugova: programer najpre piše neispravan automatizovan testni slučaj koji definiše željeno poboljšanje ili
> novu funkcionalnost, a onda piše kôd koji će zadovoljiti test i na kraju refaktoriše novi kôd u skladu sa standardima.
> Kent Beck, koji je zaslužan za razvoj ili 'ponovno otkrivanje' ove tehnike, izjavio je 2003. godine da TDD
> podstiče jednostavan dizajn i podiže samopouzdanje.

Postoji nekoliko različitih tipova testiranja koje možete koristiti za testiranje vaše aplikacije:

### Unit testiranje

Unit testiranje je pristup koji obezbeđuje da funkcije, klase i metode rade onako kako se očekuje, od momenta
kada ste ih napravili i tokom celokupnog razvojnog ciklusa. Proverom ulaznih i izlaznih vrednosti različitih
funkcija i metoda, možete biti sigurni da je njihova interna logika ispravna. Korišćenjem dependency
injection-a i kreiranjem mock ("lažnih") klasa i stub-ova možete utvrditi da li se zavisnosti ispravno
koriste u cilju još bolje pokrivenosti kôda testovima.

Kada kreirate klasu ili funkciju, treba da kreirate i odgovarajući unit test za različite slučajeve njenog
korišćenja. Osnova stvar koju treba obezbediti jeste prijava grešaka u slučaju loših argumenata, odnosno
ispravan rad u slučaju dobrih argumenata koji joj se proslede. Na taj način ćete biti sigurni da ako kasnije
napravite određene izmene u toj klasi ili funkciji, da će prethodne funkcionalnosti nastaviti da rade ispravno.
Jedina alternativa ovome je `var_dump()` u test.php, što naravno nikako nije način za izradu aplikacije,
bila ona mala ili velika.

Još jedna primena unit testova je contribute-ovanje open source projektima. Ako umeta da napišete test koji
prikazuje neispravnu funkcionalnost, a onda je popravite tako da test prolazi, mnogo su veće šanse da će
vaši patch-evi biti prihvaćeni. Ako imate projekat koji prihvata pull request-ove, onda bi ovo trebalo da
bude uslov za njihovo slanje.

[PHPUnit](http://phpunit.de) framework je de-facto standard za pisanje unit testova za PHP aplikacije, ali
postoji i nekoliko alternativa:

* [SimpleTest](http://simpletest.org)
* [Enhance PHP](http://www.enhance-php.com/)
* [PUnit](http://punit.smf.me.uk/)
* [atoum](https://github.com/atoum/atoum)

### Intergraciono testiranje

Sa [Wikipedia-je](http://en.wikipedia.org/wiki/Integration_testing):

> Integraciono testiranje (poznato i kao Integracija i testiranje, skraćeno "I&T") je faza u testiranju softvera u kojoj
> se individualni moduli kombinuju i testiraju grupno. Obavlja se nakon unit testova, a pre validacionog testiranja.
> Integraciono testiranje kao ulaz prima module koji su bili predmet unit testova, grupiše ih u veće celine, na njih primenjuje
> testove definisane u planu integracionog testa i zatim kao izlaz dostavlja integrisani sistem spreman za sistemsko testiranje.

Mnogi od alata koji se koriste za unit testove mogu biti korišćeni i za integraciono testiranje, jer se baziraju
na istim principima.

### Funkcionalno testiranje

Ponekad poznato i kao tkz. acceptance testiranje, funkcionalno testiranje se svodi na korišćenja alata za kreiranje
automatizovanih testova koji zapravo koriste vašu aplikaciju umesto da samo proveravaju da pojedinačni delovi kôda
rade i komuniciraju ispravno. Ovi alati obično rade na način da koriste realne podatke i simuliraju prave korisnike
aplikacije.

#### Alati za funkcionalno testiranje

* [Selenium](http://seleniumhq.com)
* [Mink](http://mink.behat.org)
* [Codeception](http://codeception.com) - full-stack framework za testiranje koji poseduje alate za acceptance testove
* [Storyplayer](http://datasift.github.io/storyplayer) - full-stack framework za testiranje koji ima podršku za kreiranje i brisanje test okruženja po zahtevu
