---
isChild: true
anchor:  vagrant
---

## Vagrant {#vagrant_title}


[Vagrant] pomaže u kreiranju virtuelnih kutija, oslanjaju ći se na poznata virtuelna okruženja, 
a ta okruženja konfiguriše na osnovu jednog konfiguracionog fajla.
Virtuelne kutije možete podesiti ručno ili koristeći "provisioning" softvere kao što su [Puppet] ili [Chef] koji će 
obaviti manuelni posao za vas.

Kreiranje osnovne virtuelne kutije je dobar način da se uverite da su sve ostale kutije podešene na isti način 
i otklanja potrebu da ručno izvršavate komplikovane inicijalne komande. Takođe, možete "uništiti" vašu osnovnu 
virtuelnu kutiju i ponovo je kreirati bez dodatnih koraka. Na taj način je omogućeno da na lak način kreirate svežu 
instalaciju. 

Vagrant kreira folder za deljenje vašeg koda izmedju host-a i vaše virtuene mašine, tako da možete 
kreirati i menjati fajlove na host mašini i potom ih pokretati unutar virtuelne mašine.

### Mala pomoć

Ako vam treba pomoć za prve korake u korišćenju Vagrant alata, ispod su servisi koji vam mogu pomoći:

- [Rove][Rove]: Servis omogućava generisanje osnovnog Vagrant "builds", a PHP je medju opcijama. 
Obezbeđuje se preko Chef alata.
- [Puphpet][Puphpet]: Jednostavan GUI koji podešava virtuelne mašine za PHP razvoj. **Jako orientisan ka PHP-u**. 
Pored lokalnih VMa, može se koristiti za deploy servisa u oblaku. Obezbeđuje se preko Puppet alata. 
- [Protobox][Protobox]: je sloj na vrhu vagranta i sadrži veb GUI za podešavanje virtuelnih mašina za veb razvoj. 
Jedan YAML fajl kontroliše sve što je instalirano na virtuelnoj mašini.
- [Phansible][Phansible]: Obezbeđuje jednostavan interfejs koji pomaže u generisanju Ansible Playbooks za PHP baziranu aplikaciju.



[Vagrant]: http://vagrantup.com/
[Puppet]: http://www.puppetlabs.com/
[Chef]: http://www.opscode.com/
[Rove]: http://rove.io/
[Puphpet]: https://puphpet.com/
[Protobox]: http://getprotobox.com/
[Phansible]: http://phansible.com/
