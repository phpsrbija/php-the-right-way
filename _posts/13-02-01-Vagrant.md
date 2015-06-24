---
isChild: true
title: Vagrant
anchor:  vagrant
---

## Vagrant {#vagrant_title}

[Vagrant] vam pomaže u kreiranju virtuelnih kutija, oslanjaju ći se na poznato virtuelno okruženje koga konfiguriše na
osnovu jednog konfiguracionog fajla. Virtuelne kutije možete podesiti ručno ili koristeći "provisioning" softvere
kao što su [Puppet] ili [Chef] koji će obaviti manuelni posao za vas.

Kreiranje **osnovne virtuelne kutije** je dobar način da se uverite da su sve ostale kutije podešene na isti način
i otklanja potrebu za ručnim izvršavanjem komplikovanih inicijalnih komandi. Takođe, možete "uništiti" vašu osnovnu
virtuelnu kutiju i ponovo je kreirati bez dodatnih koraka. Na taj način omogućeno je da lako kreirate svežu instalaciju.

Vagrant kreira folder za deljenje vašeg koda između hosta i vaše virtuene mašine, tako da možete
kreirati i menjati fajlove na host mašini i potom ih pokrenuti unutar virtuelne mašine.

### Mala pomoć

Ako vam treba pomoć za prve korake u korišćenju Vagrant alata, pogledajte sledeće linkove/servise:

- [Vagrant za početnike][Vagrant_za_pocetnike]: Članak koji detaljno opisuje upotrebu Vagranta u realnim situacijama.
- [Rove][Rove]: Servis koji omogućava generisanje osnovnog Vagrant okruženja, a PHP je među opcijama.
Obezbeđuje se preko Chef alata.
- [Puphpet][Puphpet]: Jednostavan GUI koji podešava virtuelne mašine za PHP razvoj. **Izrazito orijentisan ka PHP-u**.
Pored lokalnih VMa, može se koristiti za deploy servisa u oblaku. Obezbeđuje se preko Puppet alata.
- [Protobox][Protobox]: Predstavlja sloj na vrhu Vagranta koji sadrži web GUI za podešavanje virtuelnih mašina za web razvoj.
Jedan YAML fajl kontroliše sve što je instalirano na virtuelnoj mašini.
- [Phansible][Phansible]: Obezbeđuje jednostavan interfejs koji pomaže u generisanju Ansible Playbooks za PHP aplikacije.

[Vagrant_za_pocetnike]: http://viewsource.rs/uvod-u-vagrant-alat-za-jednostavno-podesavanje-razvojnog-okruzenja/
[Vagrant]: http://vagrantup.com/
[Puppet]: http://www.puppetlabs.com/
[Chef]: http://www.opscode.com/
[Rove]: http://rove.io/
[Puphpet]: https://puphpet.com/
[Protobox]: http://getprotobox.com/
[Phansible]: http://phansible.com/
