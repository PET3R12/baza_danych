# Rozwiązania LAB_07
### Zadanie 1
* 1
```sql
select avg(waga) from kreatura where rodzaj = 'wiking';
```
* 2
```sql
select rodzaj, avg(waga), count(*) as liczba_kreatur from kreatura group by rodzaj;
```
* 3
```sql
select rodzaj, avg((year(curdate()) - year(dataUr))) as sredni_wiek from kreatura group by rodzaj;
```
### Zadanie 2
* 1
```sql
select rodzaj, sum(waga*ilosc) as suma_wag from zasob group by rodzaj;
```
* 2
```sql
select nazwa, avg(waga*ilosc) as srednia_waga from zasob
where ilosc >= 4 group by nazwa having sum(waga*ilosc)>10;
```
* 3
```sql
select rodzaj, count(distinct(nazwa)) as ilosc_nazw from zasob
group by rodzaj having count(*)>1;
```
### Zadanie 3
* 1
```sql
select k.nazwa, e.ilosc from kreatura k inner join ekwipunek e on k.idKreatury = e.idKreatury; 
```
* 2
```sql
select k.nazwa, z. nazwa from kreatura k inner join ekwipunek e on e.idKreatury = k.idKreatury
inner join zasob z on z.idZasobu = e.idZasobu; 
```
* 3
```sql
select k.nazwa from kreatura k left join ekwipunek e on k.idKreatury = e.idKreatury where e.idKreatury is null;
```
### Zadanie 4
* 1
```sql
select k.nazwa, z.nazwa from kreatura k join ekwipunek e on k.idKreatury = e.idKreatury
join zasob z on e.idZasobu = z.idZasobu
where dataUr between 1600-01-01 and 1699-12-30 and k.rodzaj = 'wiking';
```
* 2
```sql
select k.nazwa from kreatura k join ekwipunek e on k.idKreatury = e.idKreatury join zasob z on e.idZasobu = z.idZasobu
where z.rodzaj = 'jedzenie' order by k.dataUr desc limit 5;
```
* 3
```sql
select concat(k1.nazwa,' - ' ,k2.nazwa) as nazwy_kreatur from kreatura k1
join kreatura k2 on k1.idKreatury = k2.idKreatury - 5;
```
### Zadanie 5
* 1
```sql
select k.rodzaj, (avg(z.waga*z.ilosc))as srednia_waga_zasobow from kreatura k
join ekwipunek e on k.idKreatury = e.idKreatury 
join zasob z on z.idZasobu = e.idZasobu
where k.rodzaj not in ('waz', 'malpa') and e.ilosc < 30 group by k.rodzaj;
```
* 2
```sql

```
