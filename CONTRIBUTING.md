# Doprinos

Ovaj dokument sadrži opšta uputstva za doprinos ovom projektu.

## Pull request-ovi

Poštujte ovu proceduru kako bi vaš rad i predlozi bili usvojeni i prihvaćeni u ovom projektu:

1. [Fork-ujte](http://help.github.com/fork-a-repo/) ovaj project, klonirajte vaš fork i podesite `remote` za vaš repo:

   ```bash
   # Kloniraj repo u trenutni folder
   git clone https://github.com/<tvoj-username>/php-the-right-way.git
   # Uđi u folder kreiranog klona
   cd php-the-right-way
   # Podesi izvorni repo kao remote pod nazivom "upstream"
   git remote add upstream https://github.com/phpsrbija/php-the-right-way
   ```

2. Sinhronizacija sa izvornim repozitorijumom:

   ```bash
   git checkout gh-pages
   git pull upstream gh-pages
   ```

3. Commit-ujte/push-ujte u logičnim celinama. Preporučujemo da squash-ujte commit-e pomoću
   [interaktivnog rebase-a](https://help.github.com/articles/interactive-rebase).

4. [Otvorite pull request](https://help.github.com/articles/using-pull-requests/) sa jasnim naslovom i opisom.


## Pravila za pisanje prevoda

1. Koristite četiri (4) razmaka za uvlačenje teksta; nemojte koristiti tabove
2. 120 karaktera po liniji
3. Koristite [GitHub Flavored Markdown](http://github.github.com/github-flavored-markdown/) za sav sadržaj
4. Izbegavajte _bukvalno_ ("od reči do reči") prevođenje

### Konvencija za prevod učestalih stranih reči i izraza

* *web* - **web**, **webu**
* *framework/frameworks* - **frejmvork**
* *deploy/deployed/deploying* - **deploy**, **deploy-ovan**, **deploy-ovanje**
* *document root* - ***document root***
* *design pattern* - **dizajn patern**
* *development environment* - **razvojno okruženje**
* *production environment* - **produkcijsko okruzenje**, **produkcija**
* *download* - **preuzimanje**
* *upload* - ***upload***
* *code* - **kôd**
* *run, run app* - **pokrenuti**, **pokretanje**, **izvršavanje**
* *apache, docker i sl*. **Apache**, **Docker**
* *host/hosts/hosting* - **host**, **hostovi**, **hosting**, **hostovanje**
* *dedicated servers* - **namenski serveri** 
* *shared servers*  **deljeni serveri**
* *virtual servers* - **virtuelni serveri**
* *remote servers* - **udaljeni serveri**
* *open source* - ***open source***
* *default* - **podrazumevano**, ponekad može i **default**
* *building application* - **izgradnja (build) aplikacije**
* *build automation* - **automatizovana izgradnja (build)** / **automatizacija izgradnje**
* *build process* - **proces izgradnje (build)**
* *continuous integration* - **kontinuirana integracija** (pri prvoj upotrebi bih u zagradi stavio ***continuous integration - CI***)
* *assets* - ***asset***, ***asset-i***
* *cloud* - **u oblaku**, **cloud rešenje**
* *blog post* - **članak**, **blog članak**, **blog post**
* *developer/php developer* - **programer**
* *debug* - ***debug-ovanje***, ***debug-ovati***
* *browser* - **browser**, **browser-u**
* *template* - **templejt**
* *escape* - ***escape-ovanje***, ***escape-ovati***
* *scope* - **opseg**, **obim**, **scope** u zagradi
* *plugin* - **dodatak (plugin)**
* *notice* - **obaveštenje**
* *fatal error* - **fatalna greška**
* *warning* - **upozorenje**
* *run-time* - **tokom izvršavanja (runtime)**
* *request* - **zahtev (request)**
* *response* - **odgovor (response)**
* *header (http header)* - **HTTP header**, ***header-i***
* *string* - **string**, **stringu**, **stringom**
* *log in* - **prijava korisnika**, može po potrebi i **login**
* *log out* - **odjava korisnika**, može po potrebi i **logout**
* *input* - prvi pomen: **ulazni podaci (input)**, svaki sledeći **input**, **input-i**
* *full-stack* - ***full-stack***, ***full-stack-u***
* *mock* - ***mock***, ***mock-ovanje***, ***mock-uje***
* *custom* - **prilagođen**, ***custom***
