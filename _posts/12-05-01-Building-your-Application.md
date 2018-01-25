---
isChild: true
title: Izgradnja i isporučivanje vaše aplikacije
anchor: building_and_deploying_your_application
---

## Izgradnja i isporučivanje (deploy) vaše aplikacije {#building_and_deploying_your_application}

Ako zateknete sebe da ručno radite promene šeme baze podataka ili ručno pokrećete testove pre nego što ažurirate svoje
fajlove (ručno), razmislite još jednom! Svaki dodatni ručni zadatak tokom deploy-a nove verzije vaše aplikacije povećava 
šanse za fatalne greške. Bez obzira da li se bavite jednostavnim ažuriranjem, 
obimnim procesom izgradnje ili čak strategijom kontinuirane integracije, [automatska izgradnja][buildautomation] je Vaš prijatelj.

Među zadacima koje biste možda želeli da automatizujete su:

* Upravljanje zavisnostima
* Kompilacija, minifikacija Vaših asset-a
* Pokretanje testova
* Pravljenje dokumentacije
* Pakovanje
* Isporučivanje koda (Deployment)


### Deploy alati

Deploy alati se mogu opisati kao skup skripti koje se bave određenim učestalim zadacima deploy-a (isporuke) softvera. 
Alat za izgradnju nije deo vašeg softvera, on deluje na vaš softver 'spolja'.

Postoji puno alata otvorenog kôda koji vam mogu pomoći pri automatizovanoj izgradnji (build), neki su napisani u PHP-u ali 
postoje oni koji nisu. To ne treba da vas sputava da ih koristite, ako više odgovaraju za određeni posao. Evo nekoliko primera:

[Phing] može da kontroliše pakovanje, isporuku ili proces testiranja iz XML build fajla. Phing (koji se zasniva na [Apache Ant])
obezbeđuje bogat set zadataka, obično potrebnih za instalaciju ili ažuriranje web aplikacija i može se proširiti dodatnim
prilagođenim zadacima, pisanim u PHP-u. Phing je stabilan i robustan alat koji je na tržištu već duži period, međutim
može se smatrati pomalo staromodnim zbog načina na koji se konfiguriše (XML fajlovi).

[Capistrano] je sistem namenjen *srednjim-do-naprednim programerima* za izvršavanje komandi na struktuiran, ponovljiv način
na jednoj ili više udaljenih mašina. Unapred je podešen za deploy-ovanje Ruby on Rails aplikacija, međutim vi možete
uspešno deploy-ovati i PHP sisteme sa njim. Uspešno korišćenje Capistrana zavisi od radnog iskustva sa Ruby i Rake.
Blog članak Dejva Gardnera [PHP Deployment with Capistrano][phpdeploy_capistrano] je dobra polazna tačka za PHP programere zainteresovane za Capistrano.

[Rocketeer] inspiraciju i filozofiju pronalazi iz Laravel frejmvorka. Cilj mu je da bude brz, elegantan i lak za
upotrebu sa pametnim podrazumevanim vrednostima. Podržava višestruke servere, višestruke etape (stage),
atomične deploy-ove i proces deployment-a se može obaviti paralelnim izvršavanjem. Sve u alatu se može "na vruće" (hot swap) zameniti
ili proširiti, i sve je napisano u PHP-u.

[Deployer] je deploy alat napisan u PHP-u. Jednostavan je i funkcionalan. Funkcionalnosti uključuju paralelno izvršavanje zadataka,
atomično deploy-ovanje i očuvanje konzistentnosti između servera. Dostupni su recepti uobičajenih zadataka za Symfony, Laravel, Zend Framework i Yii.
Artikal [Easy Deployment of PHP Applications with Deployer][phpdeploy_deployer] od autora Younes Rafie je odličan tutorijal
kako da deploy-ujete vašu aplikaciju sa ovim alatom.

[Magallanes] je još jedan alat napisan u PHP-u sa jednostavnom konfiguracijom u YAML fajlovima. On podržava višestruke servere
i okruženja, atomičan deployment, i sadrži neke ugrađene zadatke koje možete iskoristiti za uobičajene alate i frejmvorke.

#### Za dalje čitanje:

* [Automatizujte vaš projekat sa Apache Ant][apache_ant_tutorial]
* [Expert PHP Deployments][expert_php_deployments] - besplatna knjiga o deployment-u sa Capistrano, Phing i Vagrant alatima.
* [Deploying PHP Applications][deploying_php_applications] - plaćena knjiga o najboljim praksama i alatima za PHP deployment.

### Server Provisioning

Upravljanje serverima i njihovo podešavanje može biti zastrašujuć posao kada se suočite sa mnogo servera. Postoje alati
koji se bave ovim problemom tako da možete da automatizujete vašu infrastrukturu kako biste bili sigurni da imate prave servere
i da su oni ispravno konfigurisani. Ovi alati se često integrišu sa većim cloud hosting provajderima (Amazon Web Services, Heroku, DigitalOcean itd)
u cilju upravljanja instancama, što skaliranje aplikacije čini dosta lakšim.

[Ansible] je alat koji upravlja vašom infrastrukturom kroz YAML fajlove. Lako je početi i može upravljati sa
kompleksnim i aplikacijama velikih razmera. Postoji API za upravljanje sa cloud instancama i on može upravljati sa njima
kroz dinamički inventar koristeći određene alate.

[Puppet] je alat koji ima sopstveni jezik i tipove fajlova za upravljanje serverima i konfiguracijama. Može se koristiti
u gospodar/mušterija (master/client) podešavanju ili se može koristiti u modu "bez gospodara" ("master-less"). U master/client modu
u određenim zakazanim intervalima mušterije (client) će upitati centralne gospodare (master) ukoliko postoji nova konfiguracija
i sami se ažurirati ukoliko je to potrebno. U "master-less" modu možete poslati konfiguraciju vašim čvorovima (node).

[Chef] je moćni frejmvork za integraciju sistema, baziran na Ruby-ju, uz pomoć kojeg možete izgraditi kompletno serversko
okruženje ili virtuelne kutije. Dobro se integriše sa Amazon Web Servisima kroz njihov servis OpsWorks.

#### Za dalje čitanje:

* [Ansible tutorijal][an_ansible_tutorial]
* [Ansible za DevOps][ansible_for_devops] - plaćena knjig o svemu za Ansible
* [Ansible za AWS][ansible_for_aws] - plaćena knjiga o integrisanju Ansible i Amazon Web Servisa
* [Trodelna blog serija o isporučivanju (deploying) LAMP applikacije sa Chef, Vagrant i EC2][chef_vagrant_and_ec2]
* [Chef Kuvar koji instalira i konfiguriše PHP i PEAR sistem za upravljane paketima][Chef_cookbook]
* [Chef serijal video tutorijala][Chef_tutorial]

### Kontinuirana integracija

> Kontinuirana integracija je praksa softverskog razvoja u kojoj članovi tima često integrišu svoj rad, uglavnom svaka
> osoba integriše najmanje jednom dnevno — što rezultira više integracija dnevno. Mnogi timovi nalaze da ovakav
> pristup vodi do značajnog smanjenja integracionih problema i omogućava timu da razvija kohezivni softver mnogo brže.

*-- Martin Fowler*

Postoje različiti načini za implementaciju kontinuirane integracije za PHP. [Travis CI] je odradio 
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
[phpdeploy_deployer]: http://www.sitepoint.com/deploying-php-applications-with-deployer/
[Chef]: https://www.chef.io/
[chef_vagrant_and_ec2]: http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/
[Chef_cookbook]: https://github.com/chef-cookbooks/php
[Chef_tutorial]: https://www.youtube.com/playlist?list=PL11cZfNdwNyPnZA9D1MbVqldGuOWqbumZ
[apache_ant_tutorial]: http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/
[Travis CI]: https://travis-ci.org/
[Jenkins]: http://jenkins-ci.org/
[PHPCI]: http://www.phptesting.org/
[Teamcity]: http://www.jetbrains.com/teamcity/
[Deployer]: http://deployer.org/
[Rocketeer]: http://rocketeer.autopergamene.eu/
[Magallanes]: http://magephp.com/
[expert_php_deployments]: http://viccherubini.com/assets/Expert-PHP-Deployments.pdf
[deploying_php_applications]: http://www.deployingphpapplications.com
[Ansible]: https://www.ansible.com/
[Puppet]: https://puppet.com/
[ansible_for_devops]: https://leanpub.com/ansible-for-devops
[ansible_for_aws]: https://leanpub.com/ansible-for-aws
[an_ansible_tutorial]: https://serversforhackers.com/an-ansible-tutorial
