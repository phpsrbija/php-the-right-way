---
isChild: true
title: Razvoj vođen ponašanjanjem (Behavior Driven Development - BDD)
anchor:  behavior_driven_development
---

## Razvoj vođen ponašanjanjem (Behavior Driven Development - BDD) {#behavior_driven_development_title}

Postoje dva različita tipa BDD-a: SpecBDD i StoryBDD. SpecBDD se fokusira na tehničko ponašanje kôda,
dok je StoryBDD fokusiran na proizvod, ponašanje određene funkcionalnosti i interakciju. PHP ima
framework-ove za oba tipa BDD-a.

U slučaju StoryBDD-a, pišu se čitljive "priče" koje opisuje ponašanje aplikacije. One se zatim mogu
pokrenuti kao testovi nad vašom aplikacijom. Framework koji se koristi u PHP aplikacijama za StoryBDD
je [Behat], koji je inspirisan Ruby [Cucumber] projektom i koji implementira Gherkin DSL za opis
ponašanja funkcionalnosti.

U slučaju SpecBDD-a, pišu se specifikacije koje opisuju kako sâm kôd treba da se ponaša. Umesto testiranja
funkcije ili metode, vi opisujete kako ta funkcija ili metod treba da se ponaša. PHP nudi [PHPSpec]
framework u te svrhe. Ovaj framework je inspirisan [RSpec projektom][Rspec] za Ruby.

### BDD linkovi

* [Behat] - StoryBDD framework za PHP, inspirisan Ruby [Cucumber] projektom
* [PHPSpec] - SpecBDD framework za PHP, inspirisan Ruby [Rspec] projektom
* [Codeception] - full-stack framework za testiranje koji koristi BDD principe

[Behat]: http://behat.org/
[Cucumber]: http://cukes.info/
[PHPSpec]: http://www.phpspec.net/
[RSpec]: http://rspec.info/
[Codeception]: http://codeception.com/