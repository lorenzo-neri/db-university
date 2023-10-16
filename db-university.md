<!-- 
Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);

ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)

ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);

ogni Corso può essere tenuto da diversi Insegnanti;

ogni Corso prevede più appelli d’Esame;

ogni Studente è iscritto ad un solo Corso di Laurea;

ogni Studente può iscriversi a più appelli di Esame;

per ogni appello d’Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.
-->

# Requisiti Università

## Table Dipartimenti
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL 
- Nome | VARCHAR (50), NOTNULL
- Indirizzo | VARCHAR (50), NOTNULL
- Email | VARCHAR (50), NOTNULL
- Telefono | VARCHAR (20), NOTNULL
- Numero corsi di laurea | SMALLINT, NOTNULL

## Table Corsi di Laurea
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL 
- Nome | VARCHAR (50), NOTNULL
- Numero corsi | SMALLINT, NOTNULL
- Codice corso di laurea | VARCHAR (20), NOTNULL 
- Tipo | VARCHAR (20), NOTNULL
- Requisiti | VARCHAR (255), DEFAULT (Nessun requisito richiesto)
- Note | TEXT, NULL
- Durata | SMALLINT, NULL
- Lingua | VARCHAR (50), DEFAULT(Italiano)

## Table Corsi
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL 
- Nome | VARCHAR (50), NOTNULL
- Durata | SMALLINT, NULL
- Esami | SMALLINT, NULL
- Insegnanti | VARCHAR (50), NOTNULL
- Studenti | SMALLINT, NOTNULL
- Note | TEXT, NULL



## Table Insegnanti
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL 
- Nome | VARCHAR (50), NOTNULL
- Cognome | VARCHAR (50), NOTNULL
- Anno di nascita | YEAR, NOTNULL
- Email | VARCHAR (50), NOTNULL
- Note | TEXT, NULL
- Lingua | VARCHAR (50), DEFAULT(Italiano)



## Table Esami
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL 
- Nome | VARCHAR (50), NOTNULL
- Tipo | VARCHAR (50), NOTNULL
- Codice | VARCHAR (10), NOTNULL
- Durata | SMALLINT, NULL
- obbligatorio | BOOLEAN, DEFAULT (true)
- CFU | SMALLINT, NOTNULL
- Data | DATE, NULL


## Table Studenti
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL 
- Nome | VARCHAR (50), NOTNULL
- Cognome | VARCHAR (50), NOTNULL
- Matricola | VARCHAR (10), NOTNULL
- Email | VARCHAR (50), NOTNULL
- Anno di nascita | YEAR, NULL
- Media voti | FLOAT (4,2)
- Fascia reddituale
- Occupazione
- Voto diploma
- Note | TEXT, NULL


## Relationships 

Dipartimento <oneToMany> Corsi di laurea 
Corso di Laurea <manyToMany> Corsi 
Corso <manyToMany> Insegnanti 
Corso <oneToMany> Esami
Corso <manyToMany> Studenti
Studente <manyToMany> Esami
Insegnante <manyToMany> Esami