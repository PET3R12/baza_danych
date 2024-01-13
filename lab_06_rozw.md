# Rozwiązania lab_06
### Zadanie 1
* 1
```sql
create table kreatura select * from wikingowie.kreatura;
create table zasob select * from wikingowie.zasob;
create table ekwipunek select * from wikingowie.ekwipunek;
```
* 2
```sql
select * from zasob;
```
* 3
```sql
select * from zasob where rodzaj = "jedzenie";
```
* 4
```sql
select z.idZasobu, z.ilosc 
from zasob z
left join ekwipunek e on z.idZasobu = e.idZasobu
left join kreatura k on k.idKreatury = e.idKreatury
where k.idKreatury in (1, 3, 5);
```
### Zadanie 2
* 1
```sql
select * from kreatura where not rodzaj = "wiedzma" and udzwig > 50;
```
* 2
```sql
select * from zasob where waga between 2 and 5;
```
* 3
```sql
select * from kreatura where nazwa like "%or%" and udzwig between 30 and 70;
```
### Zadanie 3
* 1
```sql
select nazwa, dataPozyskania from zasob where month(dataPozyskania) between 7 and 8;
```
* 2
```sql
select * from zasob where rodzaj is not null order by waga asc;
```
* 3
```sql
select * from kreatura where dataUr is not null order by dataUr asc limit 5;
```
### Zadanie 4
* 1
```sql
select distinct rodzaj from zasob;
```
* 2
```sql
select concat(nazwa," - ", rodzaj) from kreatura where rodzaj like '%wi_%';
```
* 3
```sql
select * from zasob where  waga*ilosc not like "%,%" and year(dataPozyskania) between 2000 and 2007; 
```
### Zadanie 5
* 1
```sql
select (waga*0.7) as "waga netto", (waga*0.3) as "odpady" from zasob where rodzaj = "jedzenie";
```
* 2
```sql
select * from zasob where rodzaj is null;
```
* 3
```sql
select distinct rodzaj from zasob where rodzaj like "%Ba_%" or rodzaj like "%_os%" order by rodzaj asc;
```
