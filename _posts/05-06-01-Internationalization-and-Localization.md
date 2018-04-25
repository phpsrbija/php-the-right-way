---
title:   Internacionalizacija i Lokalizacija
isChild: true
anchor:  i18n_l10n
---

## Internacionalizacija (i18n) i Lokalizacija (l10n) {#i18n_l10n_title}

_Objašnjenje za neupućene: i18n i l10n su numeromi, vrsta skraćenice kod koje se brojevi koriste da skrate reči - u našem
slučaju, internacionalizacija postaje i18n i lokalizacija postaje l10n._

Pre svega, potrebno je da definišemo ova dva slična koncepta i ostale povezane stvari:

- **Internacionalizacija** je kada organizujete vaš kôd tako da ga možete prilagoditi različitim jezicima ili regionima
bez refaktorisanja. Ovo se obično samo jednom obavi - poželjno na početku samog projekta, ili ćete u suprotnom najverovatnije
morati da obavite velike promene u izvornom kôdu!
- **Lokalizacija** se dešava kada prilagodite interfejs tako što (uglavnom) prevedete sadržaje, oslanjajući se na posao
vezan za i18n koji ste prethodno obavili. Obično se radi svaki put kada novi jezik ili region zahtevaju podršku i ažurira
se kada se dodaju novi delovi interfejsa, s' obzirom da moraju da budu dostupni u svim podržanim jezicima.
- **Pluralizacija** definiše potrebna pravila među različitim jezicima kako bi tumačili stringove koji sadrže brojeve i brojioce.
Na primer, u engleskom jeziku kada imate samo jednu stavku, to je jednina, i bilo šta drugačije od toga se zove množina; množina
u ovom jeziku se označava sa dodavanjem jednog slova S nakon nekih reči, a ponekad se menjaju neki njihovi delovi. U drugim
jezicima, kao što su ruski ili srpski, postoje dva oblika množine pored jednine - možete čak pronaći i jezike koji imaju
i četiri, pet ili šest oblika, kao što su slovenački, irski ili arapski jezik.

## Uobičajeni načini implementacije
Najlakši način da implementirate internacionalizaciju u PHP softveru jeste da koristite fajlove sa nizovima i da koristite
njihove stringove u templejtima, kao na primer `<h1><?=$TRANS['title_about_page']?></h1>`. Ovo je, međutim, nepreporučeni način
za ozbiljne projekte zato što ostavlja neke probleme za održavanje usput - neki će se pojaviti na početku, kao što je pluralizacija.
Tako da, molimo vas, ne pokušavajte ovo ako će vaš projekat sadržati više od nekolicine stranica.

Najklasičniji način koji se često uzima kao primer za i18n i l10n je [Unix alatka zvana `gettext`][gettext]. Pojavila se
1995. godine i još uvek je potpuno rešenje za prevođenje softvera. Poprilično je lako započeti da je koristite, dok još
uvek podržava moćne alate. Ovde ćemo govoriti o Gettext alatki. Takođe, kako vas ne bismo zbunjivali sa primerima sa konzolne
linije (CLI), predstavićemo odličnu grafičku (GUI) aplikaciju koja se može koristiti za jednostavno ažuriranje vaših l10n
izvornih fajlova.

### Drugi alati

Postoje opšte biblioteke koje se koriste i koje podržavanju Gettext i druge i18n implementacije. Neke od njih vam mogu
delovati jednostavnije za instalaciju ili za podržavanje dodatnih osobina ili formata i18n fajlova. U ovom dokumentu,
mi se fokusiramo na alate koji su podržani u samom PHP jeziku, ali ćemo nabrojati ostale kako bismo bili kompletni:

- [oscarotero/Gettext][oscarotero]: Podrška za Gettext sa OO interfejsom; uključuje unapređene pomoćne funkcije, moćne
ekstraktore za nekoliko formata fajlova (neki od njih nisu nativno podržani u `gettext` komandi), i takođe može da eksportuje
u druge formate pored `.mo/.po` fajlova. Može biti koristan ukoliko imate potrebu da integrišete fajlove za prevođenje u
ostale delove sistema, kao na primer JavaScript interfejs.
- [symfony/translation][symfony]: podržava dosta različitih formata, ali preporučuje da koristite opširan XLIFF format.
Ne uključuje pomoćne funkcije niti ugrađen ekstraktor, ali podržava umetanje reči (placeholder) uz pomoć funkcije `strtr()`
koju interno koristi.
- [zend/i18n][zend]: podržava nizove i INI fajlove, ili Gettext formate. Implementira keširajući sloj kako bi vas spasao
od pristupa fajlsistemu svaki put. Takođe uključuje pomoćne funkcije za poglede (view helpers), i ulazne filtere i validatore
koji su svesni mesta tj. lokala (locale). Međutim, ne poseduje ekstraktor za poruke.

Drugi frejmvorci takođe poseduju i18n module, ali nisu dostupni izvan njihovog sopstvenog kôda:
- [Laravel] podržava osnovne fajlove sa nizovima, nema automatskog ekstraktora ali podržava `@lang` pomoćnu funkciju za templejte.
- [Yii] podržava nizove, Gettext, i prevođenje uz pomoć baze podataka, i uključuje ekstraktor za poruke. Bazira se na
ekstenziji [`Intl`][intl], koja je u PHP-u dostupna od verzije 5.3, i koja je bazirana na [ICU projektu][ICU project]; ovo
Yii-u omogućava da vrši moćne zamene kao na primer sricanje brojeva, formatiranje datuma, vremena, intervala, valuta i rednih brojeva.

Ukoliko se odlučite za neku od biblioteka koja ne podržava ekstraktore, možda ćete poželeti da koristite gettext formate,
kako biste mogli da koristite originalne gettext alate (uključujući Poedit) kao što je objašnjeno u ostatku ovog poglavlja.

## Gettext

### Instalacija
Možda će biti potrebno da instalirate Gettext i njegovu PHP biblioteku uz pomoć vašeg menadžera paketa, npr. `apt-get` ili `yum`.
Nakon instalacije, potrebno je ga uključite tako što ćete dodati `extension=gettext.so` (Linux/Unix) ili `extension=php_gettext.dll` (Windows)
u vaš `php.ini` fajl.

Ovde ćemo takođe koristiti [Poedit] za pravljenje fajlova za prevođenje (translation files). Ovaj alat ćete najverovatnije
pronaći u vašem sistemskom menadžeru paketa; dostupan je za Unix, Mac, i Windows platforme, i takođe se može
[besplatno preuzeti sa njihovog sajta][poedit_download].

### Struktura

#### Tipovi fajlova
Postoje tri fajla sa kojima se obično susrećete kada radite sa gettext alatom. Glavni fajlovi su PO (Portabilni Objekat)
i MO (Mašinski Objekat), gde je prva vrsta fajla lista "prevedenih objekata" koje možete da čitate i druga vrsta pripadajući
binarni podaci koje gettext tumači u procesu lokalizacije. Takođe, postoji i POT (Templejt) fajl, koji jednostavno sadrži
sve postojeće ključeve iz vaših fajlova sa izvornim kôdom i koji se može koristiti kao priručnik za generisanje i ažuriranje
svih PO fajlova. Ovi templejt fajlovi nisu obavezni: u zavisnosti od alata koji koristite za l10n, možete sasvim fino funkcionisati
samo sa PO/MO fajlovima. Uvek ćete imati po jedan par PO/MO fajlova po jeziku i regionu, ali samo jedan POT fajl po području (domenu).

### Domeni
Postoje slučajevi, u velikim projektima, kada će vam možda biti potrebno da odvojite prevode kada identične reči imaju različito
značenje u zavisnosti od konteksta. U ovim slučajevima potrebno je da ih raspodelite po različitim _domenima_. Domeni su, u suštini,
imenovane grupe POT/PO/MO fajlova, gde se za ime fajla kaže da je od navedenog _domena prevoda_. Mali i projekti srednje veličine obično,
zbog jednostavnosti, koriste samo jedan domen; njegovo ime je obavezno ali ćemo mi ovde koristiti naziv "main" (glavni) u primerima ispod.
U [Symfony] projektima, na primer, domeni se koriste da razgraniče prevođenje validacionih poruka.

#### Kôd lokala
Lokal je jednostavno kôd koji identifikuje jednu verziju jezika. Definisan je u saglasnosti sa [ISO 639-1][639-1] i
[ISO 3166-1 alpha-2][3166-1] specifikacijama: dva mala slova za jezik, opciono sledi donja crta i dva velika slova koja označavaju zemlju ili kôd regiona.
Za [retke jezike][rare], koriste se tri slova.

Za neka govorna područja, deo sa zemljom možda može izgledati suvišno. U suštini, neki jezici imaju dijalekte u različitim
zemljama, kao na primer austrijski nemački (`de_AT`) ili brazilski portugalski (`pt_BR`). Drugi deo se koristi za razlikovanje
između ovih dijalekata - ukoliko nije prisutan smatra se da se koristi "generička" ili "hibridna" verzija jezika.

### Struktura direktorijuma
Ukoliko želite da koristite Gettext, moraćete da se pridržavate određene strukture foldera. Prvo, u vašem repozitorijumu
biće potrebno da izaberete proizvoljnu korenu (root) lokaciju za vaše l10n fajlove. Unutar tog direktorijuma, imaćete
po jedan direktorijum za svaki lokal koji podržavate, i fiksirani `LC_MESSAGES` direktorijum koji će čuvati sve vaše
PO/MO parove: Na primer:

{% highlight console %}
<project root>
 ├─ src/
 ├─ templates/
 └─ locales/
    ├─ forum.pot
    ├─ site.pot
    ├─ de/
    │  └─ LC_MESSAGES/
    │     ├─ forum.mo
    │     ├─ forum.po
    │     ├─ site.mo
    │     └─ site.po
    ├─ es_ES/
    │  └─ LC_MESSAGES/
    │     └─ ...
    ├─ fr/
    │  └─ ...
    ├─ pt_BR/
    │  └─ ...
    └─ pt_PT/
       └─ ...
{% endhighlight %}

### Oblici množine
Kao što smo napomenuli u uvodu, različiti jezici mogu drugačije da upotrebljavaju pravila množine. Međutim, gettext nas lišava
ovih muka još jedanput. Kada pravite novi `.po` fajl, potrebno je da deklarišete [pravila množine][plural] za taj jezik,
i delovi prevoda koji se menjaju u množini će imati drugačije oblike za svako od ovih pravila. Kada pozivate Gettext u kôdu,
moraćete da navedete broj koji se odnosi na rečenicu, i on će izabrati pravilan oblik koji će se koristiti - čak će zameniti string ukoliko je to potrebno.

Pravila množine uključuju broj dostupnih oblika množine i bulov (boolean) test sa `n` koji definiše za koje pravilo zadati broj
odgovara (odbrojavanje kreće od 0). Na primer:

- Japanski: `nplurals=1; plural=0` - samo jedno pravilo
- Engleski: `nplurals=2; plural=(n != 1);` - dva pravila, prvo ako je N jednako jedan, u suprotnom drugo pravilo
- Brazilski portugalski: `nplurals=2; plural=(n > 1);` - dva pravila, drugo ukoliko je N veće od jedan, prvo u suprotnom

Sada kada ste razumeli osnove kako pravila množine funkcionišu - a ukoliko niste, molimo vas da pogledate detaljnije objašnjenje
u [LingoHub tutorijalu][lingohub_plurals] -, možda ćete poželeti da prekopirate neka pravila sa [liste][plural] umesto
da ih ručno pišete.

Kada pozivate Gettext da uradi lokalizaciju u rečenicama sa brojiocima, biće potrebno da mu takođe obezbedite relevantan broj.
Gettext će sam shvatiti koje pravilo da upotrebi i iskoristiti ispravnu lokalizovanu verziju. U `.po` fajlu moraćete da unesete
različitu rečenicu za svako definisano pravilo množine.

### Primer implementacije
Nakon sve te teorije, hajde da uradimo nešto praktično. Pred nama je jedan izvod `.po` fajla - ne obazirite se na njegov
format, već na njegov sadržaj, kasnije ćete naučiti kako da ga jednostavno modifikujete:

{% highlight po %}
msgid ""
msgstr ""
"Language: pt_BR\n"
"Content-Type: text/plain; charset=UTF-8\n"
"Plural-Forms: nplurals=2; plural=(n > 1);\n"

msgid "We're now translating some strings"
msgstr "Nós estamos traduzindo algumas strings agora"

msgid "Hello %1$s! Your last visit was on %2$s"
msgstr "Olá %1$s! Sua última visita foi em %2$s"

msgid "Only one unread message"
msgid_plural "%d unread messages"
msgstr[0] "Só uma mensagem não lida"
msgstr[1] "%d mensagens não lidas"
{% endhighlight %}

Prva sekcija služi kao zaglavlje, gde su `msgid` i `msgstr` posebno prazni. Ono opisuje koji enkoding fajl koristi,
pravila množine i ostale stvari koje su manje važne.
Druga sekcija prevodi jednostavan string iz engleskog u brazilski portugalski, i treća takođe, ali upotrebljava zamenu
stringova uz pomoć funkcije [`sprintf`][sprintf] tako da prevod može da sadrži korisnikovo ime i datum posete.
Poslednja sekcija je primer oblika množine, koja prikazuje oblike jednine i množine kao `msgid` u engleskom i njihove
odgovarajuće prevode kao `msgstr` 0 i 1 (prateći broj za zadato pravilo množine). Tu se takođe koristi zamena stringova,
tako da se broj može direktno videti u rečenici ukoliko upotrebite `%d`. Oblik množine uvek ima dve verzije `msgid` (jednina i množina),
tako da se ne preporučuje da koristite kompleksan jezik za izvor prevođenja.

### Diskusija o l10n ključevima
Kao što ste verovatno primetili, mi koristimo stvarnu rečenicu u engleskom za ID izvora. To polje `msgid` je isto koje se
koristi u svim vašim `.po` fajlovaima, što znači da će ostali jezici imati isti format i ista `msgid` polja ali prevedene
`msgstr` linije.

Dok govorimo o ključevima za prevode, postoje dve glavne "škole":

1. _`msgid` kao stvarna rečenica_.  
    Glavne prednosti su:
    - ukoliko postoji neki deo softvera koji još uvek nije preveden u bilo kom jeziku, prikazani ključ će i dalje imati neko značenje. Na primer
    ako se potrudite iz sveg srca da prevedete engleski u španski, ali vam je potrebna pomoć da prevedete u francuski,
    možete da objavite novu stranicu sa francuskim prevodom kome nedostaju rečenice, i delovi websajta će se prikazati na engleskom;
    - prevodicu je mnogo lakše da razume o čemu se radi i da pravilno prevede oslanjajući se na `msgid`;
    - dobijate "besplatno" jedan l10n za jedan jezik - izvorni;
    - jedina mana: ukoliko je potrebno da promenite stvarni tekst, moraćete da zamenite isti `msgid` u više jezičkih fajlova.

2. _`msgid` kao jedinstveni, struktuirani ključ_.  
Opisala bi ulogu rečenice u aplikaciji u struktuiranom smislu, uključujući šablon ili deo gde je string lociran umesto njegov sadržaj.
    - odlično je dobro organizovati kôd, tako da se razdvoji tekstualni sadržaj od logike templejta.
    - međutim, to može doneti probleme prevodiocu kojem bi nedostajao kontekst. Izvorni jezički fajl bi bio potreban kao osnova
    za ostale prevode. Na primer: idealno, developer bi mogao da ima jedan `en.po` fajl koji bi prevodioci pročitali kako bi
    znali šta da napišu u `fr.po` fajlu.
    - prevodi koji nedostaju bi se prikazali kao nerazumni ključevi na ekranu (`top_menu.welcome` umesto `Hello there, User!`
    na, recimo, nepotpuno prevedenoj stranici na francuskom jeziku). To je dobro jer bi se na taj način forsiralo potpuno
    prevođenje pre objave - ali je zato loše zato što bi se problemi sa prevodima prikazali zaista odvratno na ekranu.
    Neke biblioteke, međutim, imaju jednu opciju da navedete jedan "fallback" jezik, koji vam pruža slično ponašanje kao prethodni pristup.

[Gettext priručnik][manual] favorizuje prvi pristup jer je, generalno, lakši za prevodioce i korisnike u slučaju nevolje.
Taj pristup ćemo i mi ovde koristiti. Međutim, [Symfony dokumentacija][symfony-keys] favorizuje prevode koji se baziraju
na ključnim rečima, da bi omogućili nezavisne promene svih prevoda bez efekata na templejte.

### Svakodnevna upotreba
Za uobičajene aplikacije, normalno biste koristili neke Gettext funkcije dok pišete statičan tekst u vašim stranicama.
Te rečenice bi se onda pojavile u `.po` fajlovima, pa bi se prevele, pa kompajlirale u `.mo` fajlove i onda bi ih koristio
Gettext prilikom prikazivanja sadržaja. Prema tome, hajde da ovo što smo diskutovali do sada povežemo u celinu u korak-po-korak primeru:

#### 1. Primer templejt fajla koji sadrži različite pozive gettext alata
{% highlight php %}
<?php include 'i18n_setup.php' ?>
<div id="header">
    <h1><?=sprintf(gettext('Welcome, %s!'), $name)?></h1>
    <!-- code indented this way only for legibility -->
    <?php if ($unread): ?>
        <h2><?=sprintf(
            ngettext('Only one unread message',
                     '%d unread messages',
                     $unread),
            $unread)?>
        </h2>
    <?php endif ?>
</div>

<h1><?=gettext('Introduction')?></h1>
<p><?=gettext('We\'re now translating some strings')?></p>
{% endhighlight %}

- [`gettext()`][func] jednostavno prevodi `msgid` u njegov odgovarajući `msgstr` za zadati jezik. Takođe, postoji i skraćenica
funkcija `_()` koja radi na isti način;
- [`ngettext()`][n_func] radi isto to samo sa pravilima množine;
- takođe, postoje [`dgettext()`][d_func] i [`dngettext()`][dn_func], koje vam omogućavaju da redefinišete domen za jedan poziv.
Više o konfiguraciji domena u sledećem primeru.

#### 2. Primer konfiguracionog fajla (`i18n_setup.php` kao što je gore korišćen), koji bira pravilan lokal i konfiguriše Gettext
{% highlight php %}
<?php
/**
 * Verifikuje da li je zadati $locale podržan u projektu
 *
 * @param string $locale
 * @return bool
 */
function valid($locale) {
   return in_array($locale, ['en_US', 'en', 'pt_BR', 'pt', 'es_ES', 'es');
}

// postavlja izvorni/podrazumevani lokal, za informativne potrebne
$lang = 'en_US';

if (isset($_GET['lang']) && valid($_GET['lang'])) {
    // lokal se može promeniti kroz query-string
    $lang = $_GET['lang'];    // ovo biste trebali sanirati!
    setcookie('lang', $lang); // sačuvan je u kolačiću kako bi se ponovo mogao koristiti
} elseif (isset($_COOKIE['lang']) && valid($_COOKIE['lang'])) {
    // ako kolačić postoji, hajde da ga zadržimo
    $lang = $_COOKIE['lang']; // ovo biste trebali sanirati!
} elseif (isset($_SERVER['HTTP_ACCEPT_LANGUAGE'])) {
    // podrazumevano: proverite koje jezike korisnik prihvata na osnovu informacije iz pregledača (browser)
    $langs = explode(',', $_SERVER['HTTP_ACCEPT_LANGUAGE']);
    array_walk($langs, function (&$lang) { $lang = strtr(strtok($lang, ';'), ['-' => '_']); });
    foreach ($langs as $browser_lang) {
        if (valid($browser_lang)) {
            $lang = $browser_lang;
            break;
        }
    }
}

// ovde definišemo globalni sistemski lokal na osnovu pronađenog jezika
putenv("LANG=$lang");

// ovo na primer može biti korisno za funkcije za rad sa datumima (LC_TIME) ili za formatiranje novca (LC_MONETARY)
setlocale(LC_ALL, $lang);

// ovo ukazuje Gettext-u da traži ../locales/<lang>/LC_MESSAGES/main.mo
bindtextdomain('main', '../locales');

// naglasiti koje šifrovanje (encoding) se treba koristiti prilikom čitanja datoteke (fajla)
bind_textdomain_codeset('main', 'UTF-8');

// ukoliko vaša aplikacija ima više domena, kao što je pomenuto iznad, ovde biste ih trebali vezati
bindtextdomain('forum', '../locales');
bind_textdomain_codeset('forum', 'UTF-8');

// ovde naglašavamo na koji podrazumevani domen će gettext() pozivi da se odnose
textdomain('main');

// ovo bi trebalo da traži string u forum.mo umesto main.mo
// echo dgettext('forum', 'Welcome back!');
?>
{% endhighlight %}

#### 3. Pripremanje prevoda za prvu upotrebu
Da bi stvari bile jednostavnije - i jedna od moćnih prednosti koje Gettext nudi u odnosu na custom i18n pakete - 
je njegov lični tip fajla. "Čoveče, to je poprilično teško razumeti i izmeniti ručno, jednostavan niz bi bio lakši!" ne greši,
aplikacije kao što je [Poedit] su ovde da bi pomogle - _poprilično_. Možete preuzeti program sa [njihovog websajta][poedit_download]
i on je besplatan i dostupan za sve platforme. Veoma je lako navići se da koristite ovaj alat, ali je istovremeno veoma moćan - 
dok on koristi sve moćne osobine koje Gettext nudi.

Prilikom prvog pokretanja, potrebno je da iz menija izaberete "File > New Catalog". Tu ćete imati mali ekran gde ćemo postaviti
teren tako da sve ostalo radi lagodno. Kasnije, bićete u mogućnosti da pronađete ova podešavanja kroz "Catalog > Properties":

- Ime projekta i verzija, tim prevodioca i email adresa: korisna informacija koja ide u zaglavlje `.po` fajla;
- Jezik: ovde biste trebali da koristite format koji smo ranije spomenuli, kao npr. `en_US` ili `pt_BR`;
- Charset-ovi (skupovi znakova): UTF-8, preferirano;
- Charset izvora: ovde postavite charset koji vaši PHP fajlovi koriste - verovatno UTF-8 takođe, zar ne?
- pravila množine: ovde idu ona pravila koja smo ranije spomenuli - ovde postoji i veza sa primerima takođe;
- Putanje do izvora: ovde morate uključiti sve foldere iz projekta gde će se pojaviti `gettext()` (i rođaci) - ovo su obično vaši templejt folder(i)
- Ključne reči izvora: ovaj poslednji deo je podrazumevano popunjen, ali ćete naknadno možda morati da ga izmenite - 
i takođe je jedan od moćnijih aspekata Gettext alata. Softver koji u pozadini koristi Gettext zna kako `gettext()` pozivi
izgledaju u više programskih jezika, ali vi takođe možete napraviti vaše vlastite oblike za prevođenje. Ovo će biti obrađeno
kasnije u sekciji "Saveti".

Nakon podešavanja ovih tačaka bićete upitani da sačuvate fajl - koristeći strukturu direktorijuma koju smo spomenuli,
i onda će se pokrenuti skeniranje vaših izvornih fajlova kako bi se pronašli pozivi za lokalizaciju. Oni će biti kreirani
kao prazni redovi u vašoj tabeli sa prevodima, i vi ćete početi da unosite lokalizovane verzije ovih stringova. Sačuvajte
je i `.mo` fajl će se (re)kompajlirati u istom folderu i na kraju: vaš projekat je internacionalizovan.

#### 4. Prevođenje stringova
Kao što ste verovatno ranije primetili, postoje dva glavna tipa lokalizovanih stringova: jednostavni i oni sa oblicima množine.
Prva grupa ima jednostavno dva polja: izvorni i lokalizovani string. Izvorni string se ne može modifikovati jer Gettext/Poedit
nemaju tu mogućnost da menjate izvorne fajlove - potrebno je da sami izmenite izvor i ponovo skenirate fajlove. Savet: možete
pritisnuti desni klik na liniju za prevođenje i on će vam prikazati izvorne fajlove i linije gde se taj string koristi.
Na drugu stranu, stringovi sa oblicima množine sadrže dva polja da prikažu dva izvorna stringa, i tabove kako biste mogli da konfigurišete
različite konačne oblike.

Svaki put kada izmenite vaše izvore i kada je potrebno da ažurirate prevode, samo pritisnite Osveži (Refresh) i Poedit će
ponovo skenirati kôd, ukloniti nepostojeće zapise, i spojiti one koji su promenjeni i dodati nove. Možda će čak pokušati da
pogodi neke prevode, oslanjajući se na one koje ste vi već uneli. Ova nagađanja i izmenjeni zapisi će dobiti obeleživač "Fuzzy"
što ukazuje da im je potrebna revizija, i biće naglašeni u listi. Takođe je korisno ukoliko imate tim prevodioca i neko
pokuša da napiše nešto u šta nije sasvim siguran: samo obeležite sa Fuzzy i neko drugi će revidirati kasnije.

Konačno, proporučljivo je da ostavite "View > Untranslated entries first" aktivirano, jer će vam _mnogo_ pomoći da ne zaboravite
nijedan zapis. Iz tog menija, takođe možete otvoriti delove UI-ja koji vam omogućavaju da ostavite informacije o kontekstu
za prevodioce, ukoliko je potrebno.

### Saveti i Trikovi

#### Mogući problemi sa keširanjem
Ukoliko koristite PHP kao modul na Apache-u (`mod_php`), možda ćete imati problema sa keširanim `.mo` fajlom.
To se dešava kada se prvi put pročita, i onda, da biste ga ažurirali, možda ćete morati da restartujete server. Na Nginx i
PHP verziji 5 obično je potrebno da nekoliko puta osvežite stranicu da biste osvežili keš prevoda, i u PHP verziji 7 retko
da je i potrebno.

#### Dodatne pomoćne funkcije
Većina ljudi preferira da koristi lakši način `_()` umesto `gettext()`. Mnoge proizvoljne i18n biblioteke u frejmvorcima
koriste nešto slično kao `t()`, kako bi kôd za prevođenje učinili kraćim. Međutim, to je jedina funkcija koja nudi skraćenicu.
Možda ćete poželeti u vašem projektu da dodate neke druge, kao na primer `__()` ili `_n()` za `ngettext()`, ili možda
simpatičnu `_r()` koja bi spojila pozive ka `gettext()` i `sprintf()`. Druge biblioteke, kao što je [Gettext od oscarotero][oscarotero]
takođe obezbeđuju pomoćne funkcije kao što su ove.

U tim slučajevima, biće potrebno da date instrukcije pomoćnom Gettext alatu kako da izvuče stringove iz ovih novih funkcija.
Ne plašite se, veoma je jednostavno. U pitanju je samo jedno polje u `.po` fajlu, ili ekran za podešavanje u Poedit-u.
U editoru, ta opcija je u "Catalog > Properties > Source keywords". Tu ćete uključiti specifikaciju za ove nove funkcije,
pri čemu ćete poštovati [specifičan format][func_format]:

- ukoliko napravite nešto nalik `t()` što jednostavno vraća prevod za zadati string, možete ga definisati sa `t`.
Gettext će znati da je jedini argument funkcije string koji treba prevesti.
- ukoliko funkcija ima više od jednog argumenta, možete naglasiti u kojem se nalazi prvi string - i ukoliko je potrebno,
oblik množine takođe. Na primer, ukoliko pozivamo našu funkciju ovako: `__('one user', '%d users', $number)`, specifikacija
bi bila `__:1,2`, što znači da je prvi oblik prvi argument, i da je drugi oblik drugi argument. Ukoliko se umesto toga vaš broj nađe
na mestu prvog argumenta, specifikacija bi bila `__:2,3`, ukazujući da je prvi oblik drugi argument, i tako dalje.

Nakon što uključite ova nova pravila u `.po` fajl, novo skeniranje će doneti vaše nove stringove isto onako lako kao pre.

### Reference

* [Wikipedia: i18n and l10n](https://en.wikipedia.org/wiki/Internationalization_and_localization)
* [Wikipedia: Gettext](https://en.wikipedia.org/wiki/Gettext)
* [LingoHub: Tutorijal za PHP internacionalizaciju sa gettext-om][lingohub]
* [PHP priručnik: Gettext](http://php.net/manual/en/book.gettext.php)
* [Gettext priručnik][manual]

[Poedit]: https://poedit.net
[poedit_download]: https://poedit.net/download
[lingohub]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/
[lingohub_plurals]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/#Plurals
[plural]: http://docs.translatehouse.org/projects/localization-guide/en/latest/l10n/pluralforms.html
[gettext]: https://en.wikipedia.org/wiki/Gettext
[manual]: http://www.gnu.org/software/gettext/manual/gettext.html
[639-1]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
[3166-1]: http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
[rare]: http://www.gnu.org/software/gettext/manual/gettext.html#Rare-Language-Codes
[func_format]: https://www.gnu.org/software/gettext/manual/gettext.html#Language-specific-options
[oscarotero]: https://github.com/oscarotero/Gettext
[symfony]: https://symfony.com/doc/current/components/translation.html
[zend]: https://docs.zendframework.com/zend-i18n/translation
[laravel]: https://laravel.com/docs/master/localization
[yii]: http://www.yiiframework.com/doc-2.0/guide-tutorial-i18n.html
[intl]: http://br2.php.net/manual/en/intro.intl.php
[ICU project]: http://www.icu-project.org
[symfony-keys]: https://symfony.com/doc/current/components/translation/usage.html#creating-translations

[sprintf]: http://php.net/manual/en/function.sprintf.php
[func]: http://php.net/manual/en/function.gettext.php
[n_func]: http://php.net/manual/en/function.ngettext.php
[d_func]: http://php.net/manual/en/function.dgettext.php
[dn_func]: http://php.net/manual/en/function.dngettext.php
