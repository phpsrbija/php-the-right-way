---
isChild: true
title: Izgradnja i isporučivanje vaše aplikacije
anchor: building_and_deploying_your_application
---

## Izgradnja i isporučivanje vaše aplikacije {#building_and_deploying_your_application}

Ako zateknete sebe da ručno radite promene šeme baze podataka ili ručno pokrećete testove pre nego što ažurirate svoje
fajlove (ručno), razmislite još jednom! Svaki dodatni ručni zadatak tokom deploy-a nove verzije vaše aplikacije povećava 
šanse za fatalne greške. Bez obzira da li se bavite jednostavnim ažuriranjem, 
obimnim procesom izgradnje ili čak strategijom kontinuirane integracije, [automatska izgradnja](http://en.wikipedia.org/wiki/Build_automation) je Vaš prijatelj.

Među zadacima koje biste možda želeli da automatizujete su:

* Upravljanje zavisnostima
* Kompilacija, minifikacija Vaše aktive
* Pokretanje testova
* Pravljenje dokumentacije
* Pakovanje
* Isporučivanje koda (Deployment)


### Alati za automatizaciju izgradnje

Alati za izgradnju (build) mogu biti shvaćeni kao skup skripti koje se bave određnim učestalim zadacima isporuke (deploy-a) softvera. 
Alat za izgradnju nije deo vašeg softvera, on deluje na vaš softver 'spolja'.

Postoji puno alata otvorenog koda koji vam mogu pomoći pri automatizovanoj izgradnji (build), neki su napisani u PHP-u ali 
postoje oni koji nisu. To ne treba da vas sputava da ih koristite, ako više odgovaraju za određeni posao. Evo nekoliko primera:

[Phing](http://www.phing.info/) je najlakši način da počnete sa primenom automatizacije isporučivanja koda u svetu PHP-a. Pomoću Phing-a
možete da kontrolišete pakovanje, isporuku ili proces testiranja unutar jednostavnog XML fajla. Phing (koji se zasniva na [Apache Ant](http://ant.apache.org/)) obezbeđuje bogat set zadataka, obično potrebnih za instalaciju ili ažuriranje web aplikacija i može se proširiti dodatnim prilagođenim zadacima, pisanim u PHP-u.

[Capistrano](https://github.com/capistrano/capistrano/wiki) je sistem namenjen *srednjim-do-naprednim programerima* za
izvršavanje komandi na struktuiran, ponovljivi način na jednoj ili više udaljenih mašina. Prekonfigurisan je za primenu na Ruby on Rails aplikacije, međutim ljudi **uspešno isporučuju PHP sisteme** sa njim. Uspešno korišćenje Capistrana zavisi od radnog iskustva sa Ruby i Rake.

Blog članak Dejva Gardnera [PHP Deployment with Capistrano](http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/)
je dobra polazna tačka za PHP programere zainteresovane za Capistrano.

[Chef](http://www.opscode.com/chef/) je više od framework-a za deploy, to je veoma moćan Ruby baziran sistemski integracioni framework 
koji ne samo da radi deploy Vaše aplikacije već može izgraditi i celokupno serversko okruženje ili virtuelne kutije(virtual boxes).

#### Chef resursi za PHP programere:

* [Trodelna blog serija o angažovanju(deploying) LAMP applikacije sa Chef, Vagrant i EC2](http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/)
* [Chef Kuvar koji instalira i konfiguriše PHP 5.3 i PEAR sistem za upravljane paketima](https://github.com/opscode-cookbooks/php)
* [Chef video serije][Chef_tutorial] od Opscode tvorca Chef alata

#### Za dalje čitanje:

* [Automatizujte Vaš projekat sa Apache Ant](http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/)

### Kontinuirana integracija

> Kontinuirana integracija je praksa softverskog razvoja u kojoj članovi tima često integrišu svoj rad, uglavnom svaka
> osoba integriše najmanje jednom dnevno — što rezultira više integracija dnevno. Mnogi timovi nalaze da ovakav
> pristup vodi do značajnog smanjenja integracionih problema i omogućava timu da razvija kohezivni softver mnogo brže.

*-- Martin Fowler*

Postoje različiti načini za implementaciju kontinuirane integracije za PHP. [Travis CI](https://travis-ci.org/) je odradio 
odličan posao i učinio kontinuiranu integraciju olakšanom čak i u slučaju manjih projekata. Travis CI je hostovan servis 
kontinuirane integracije namenjen open source zajednici. Integrisan je sa GitHub-om i nudi prvoklasnu podršku za mnoge jezike, 
uključujući i PHP.

#### Za dalje čitanje:

* [Kontinuirana integracija sa Jenkins][Jenkins]
* [Kontinuirana integracija sa PHPCI][PHPCI]
* [Kontinuirana integracija sa Teamcity][Teamcity]


[buildautomation]: http://en.wikipedia.org/wiki/Build_automation
[Phing]: http://www.phing.info/
[Apache Ant]: http://ant.apache.org/
[Capistrano]: https://github.com/capistrano/capistrano/wiki
[phpdeploy_capistrano]: http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/
[Chef]: http://www.opscode.com/chef/
[chef_vagrant_and_ec2]: http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/
[Chef_cookbook]: https://github.com/opscode-cookbooks/php
[Chef_tutorial]: https://www.youtube.com/playlist?list=PLrmstJpucjzWKt1eWLv88ZFY4R1jW8amR
[apache_ant_tutorial]: http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/
[Travis CI]: https://travis-ci.org/
[Jenkins]: http://jenkins-ci.org/
[PHPCI]: http://www.phptesting.org/
[Teamcity]: http://www.jetbrains.com/teamcity/
[Deployer]: https://github.com/deployphp/deployer
