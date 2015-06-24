---
isChild: true
title: Razvoj vođen ponašanjanjem (Behavior Driven Development - BDD)
anchor:  behavior_driven_development
---

## Razvoj vođen ponašanjanjem (Behavior Driven Development - BDD) {#behavior_driven_development_title}

Postoje dva različita tipa BDD-a: SpecBDD i StoryBDD. SpecBDD se fokusira na tehničko ponašanje kôda,
dok je StoryBDD fokusiran na proizvod, ponašanje određene funkcionalnosti i interakciju. PHP ima
frejmvorke za oba tipa BDD-a.

U slučaju StoryBDD-a, pišu se čitljive "priče" koje opisuje ponašanje aplikacije. One se zatim mogu
pokrenuti kao testovi nad vašom aplikacijom. Frejmvork koji se koristi u PHP aplikacijama za StoryBDD
je [Behat], koji je inspirisan Ruby [Cucumber] projektom i koji implementira Gherkin DSL za opis
ponašanja funkcionalnosti.

U slučaju SpecBDD-a, pišu se specifikacije koje opisuju kako sâm kôd treba da se ponaša. Umesto testiranja
funkcije ili metode, vi opisujete kako ta funkcija ili metod treba da se ponaša. PHP nudi [PHPSpec]
frejmvork u te svrhe. Ovaj frejmvork je inspirisan [RSpec projektom][Rspec] za Ruby.

### BDD linkovi

* [Behat] - StoryBDD frejmvork za PHP, inspirisan Ruby [Cucumber] projektom
* [PHPSpec] - SpecBDD frejmvork za PHP, inspirisan Ruby [Rspec] projektom
* [Codeception] - full-stack frejmvork za testiranje koji koristi BDD principe

[Behat]: http://behat.org/
[Cucumber]: http://cukes.info/
[PHPSpec]: http://www.phpspec.net/
[RSpec]: http://rspec.info/
[Codeception]: http://codeception.com/