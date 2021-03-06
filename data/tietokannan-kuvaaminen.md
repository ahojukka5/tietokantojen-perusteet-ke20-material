---
path: '/tietokannan-kuvaaminen'
title: 'Tietokannan kuvaaminen'
hidden: false
---

## Tietokantakaavio

Tietokantakaavio on tietokannan graafinen esitys,
jossa jokainen tietokannan taulu on laatikko,
joka sisältää taulun nimen ja sarakkeet listana.
Rivien viittaukset toisiinsa esitetään
laatikoiden välisinä yhteyksinä.

Tietokantakaavion piirtämiseen on monia vähän erilaisia tapoja.
Seuraava kaavio on luotu netissä olevalla
työkalulla [dbdiagram.io](https://dbdiagram.io/):

<img src="/kaavio.png">

Tässä merkki `1` tarkoittaa,
että sarakkeessa on eri arvo joka rivillä,
ja merkki `*` puolestaan tarkoittaa,
että sarakkeessa voi olla sama arvo usealla rivillä.
Esimerkiksi taulussa `Tuotteet` joka rivillä on eri `id`,
mutta taulussa `Ostokset` monella rivillä voi olla sama `tuote_id`.

## SQL-skeema

SQL-skeema on tietokannan rakenteen tekstimuotoinen esitys,
jossa annetaan tietokannan luomiseen tarvittavat SQL-komennot.
Tämän esitystavan etuna on, että se on varmasti täsmällinen
ja voimme halutessamme luoda suoraan tietokannan sen perusteella.

Esimerkiksi tässä on äskeistä tietokantaa vastaava SQL-skeema:

```sql
CREATE TABLE Tuotteet (id INTEGER PRIMARY KEY, nimi TEXT, hinta INTEGER);
CREATE TABLE Asiakkaat (id INTEGER PRIMARY KEY, nimi TEXT);
CREATE TABLE Ostokset (tuote_id INTEGER REFERENCES Tuotteet, asiakas_id INTEGER REFERENCES Asiakkaat);
```

Jos oletamme, että tämä skeema on tiedostossa `kuvaus.sql`,
voimme luoda tietokannan SQLite-tulkissa seuraavasti
komennolla `.read`:

```x
sqlite> .read kuvaus.sql
sqlite> .tables
Asiakkaat  Ostokset   Tuotteet
```

Toisaalta voimme myös käyttää SQLite-tulkissa komentoa `.schema`,
joka antaa nykyisen tietokannan skeeman:

```x
sqlite> .schema
CREATE TABLE Tuotteet (id INTEGER PRIMARY KEY, nimi TEXT, hinta INTEGER);
CREATE TABLE Asiakkaat (id INTEGER PRIMARY KEY, nimi TEXT);
CREATE TABLE Ostokset (tuote_id INTEGER REFERENCES Tuotteet, asiakas_id INTEGER REFERENCES Asiakkaat);
```
