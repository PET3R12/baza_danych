# Rozwiązania lab_05
### Zadanie 1
* a)
```sql
delete * from postac where nazwa != 'Bjorn' and rodzaj = 'wiking' and data_ur is not null order by data_ur asc limit 2;
```
* b)
```sql
alter table walizka drop foreign key walizka_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_2;

alter table postac modify id_postaci int;

alter table postac drop primary key;
#set fereign_key_checks = 1;
```
### Zadanie 2
*   a)
```sql
alter table postac add pesel char(11) first;

update postac set pesel='12345678910' where id_postaci=1;

update postac set pesel='12345678910' + id_postaci;

alter table postac add primary key(pesel);
```
* b)
```sql
alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena')
```
* c)
```sql
insert into postac values("13245678910","11","Gertruda Nieszczera", "syrena","1678-05-17",21)
```
### Zadanie 3
* a)
```sql
update postac set statek= "Santa Maria" where nazwa like "%a%";
```
* b)
```sql
update statek set max_ladownosc = 0.7 * max_ladownosc where year(data_wodowania) between 1901 and 2000;
```
* c)
```sql
alter table postac add check (wiek < 1000);
```
### Zadanie 4
* a)
```sql
alter table postac modify column rodzaj enum('wiking','ptak','kobieta','waz');
insert into postac(nazwa, rodzaj) values('Loko', 'waz');
```
* b)
```sql
create table marynaz like postac;

insert into marynaz select * from postac where statek is not null ;
```
* c)
```sql
alter table marynarz add foreign key(statek) references statek(nazwa_statku) ON DELETE SET NULL;
```
### Zadanie 5
* a)
```sql
update marynarz set statek=null;
```
* b)
```sql
delete from postac where id_postaci = 8;
```
* c)
```sql
delete from statek where rodzaj_statku;
```
* d)
```sql
drop table statek;
```
* e)
```sql
create table zwierz(id int auto_increment primary key, nazwa varchar(120), wiek int unsigned);
```
* f)
```sql
insert into zwierz select * from postac where rodzaj="ptak" or rodzaj="wąż";
```
