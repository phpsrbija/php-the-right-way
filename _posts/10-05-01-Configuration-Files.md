---
isChild: true
title: Konfiguracioni fajlovi
anchor: configuration_files
---

## Konfiguracioni fajlovi {#configuration_files_title}

Pri kreiranju konfiguracionih fajlova vaše aplikacije, preporuka je da to bude u skladu sa jednom od sledećih metoda:

- Vaše konfiguracije treba da čuvate na mestu odakle im se ne može direktno pristupiti.
- Ako ipak morate da čuvate konfiguracione fajlove u document root-u, neka to budu fajlovi sa `.php` ekstenzijom.
Na taj način ćete obezbediti da, čak iako im se pristupi direktno, kroz browser, neće biti prikazani u tekstualnom formatu.
- Informacije u konfiguracionim fajlovima bi trebalo da se adekvatno zaštite, bilo enkripcijom ili sistemskim
dozvolama za prava pristupa
