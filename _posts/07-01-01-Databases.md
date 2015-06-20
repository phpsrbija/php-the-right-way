---
title: Baze podataka
anchor: databases
---

# Baze podataka {#databases_title}

Vaš PHP kôd će često koristiti bazu podataka za čuvanje informacija. Na raspolaganju je nekoliko opcija za
povezivanje i interakciju sa bazom. Preporučena opcija **do verzije PHP 5.1.0** je bila korišćenje nativnih
drajvera kao što su [mysqli], [pgsql], [mssql], itd.

Nativni drajveri su odličan izbor ako koristite samo jednu bazu u aplikaciji, ali ako na primer koristite MySQL i malo MSSQL,
ili se povezujete i na Oracle bazu, onda nećete moći da koristite iste drajvere. Moraćete da naučite
potpuno nov API za svaki tip baze podataka &mdash; a to je apsurdno.

[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
[mssql]: http://php.net/mssql