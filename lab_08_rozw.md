# Rozwiązania Lab_08
### Zad 1
* 1
```sql
create table kreatura select * from wikingowie.kreatura;
create table uczestnicy select * from wikingowie.uczestnicy;
create table etapy_wyprawy select * from wikingowie.etapy_wyprawy;
create table sektor select * from wikingowie.sektor;
create table wyprawa select * from wikingowie.wyprawa;
```
* 2
```sql
select k.nazwa from kreatura k left join uczestnicy u on u.id_uczestnika = k.idKreatury where u.id_uczestnika is null;
```
* 3
```sql
select w.nazwa, sum(e.ilosc)
from wyprawa w 
left join uczestnicy u on w.id_wyprawy = u.id_wyprawy 
left join ekwipunek e on u.id_uczestnika = e.idKreatury 
group by w.nazwa;
```
### Zad 2
* 1
```sql
select w.nazwa as 'nazwa_wyprawy', count(u.id_uczestnika) as 'liczba_uczestnikow', group_concat(k.nazwa order by k.nazwa separator ', ') as 'uczestnicy'
from wyprawa w 
left join uczestnicy u on w.id_wyprawy = u.id_wyprawy
left join kreatura k on u.id_uczestnika = k.idKreatury
group by w.nazwa;
```
* 2
```sql
select w.nazwa, ew.kolejnosc, s.nazwa, w.data_rozpoczecia, k.nazwa
from wyprawa w 
join etapy_wyprawy ew on w.id_wyprawy = ew.idWyprawy
join sektor s on ew.sektor = s.id_sektora
left join kreatura k on w.kierownik = k.idKreatury
order by w.data_rozpoczecia asc, ew.kolejnosc asc;
```
### Zad 3
* 1
```sql
select s.nazwa as nazwa_sektora, count(ew.sektor) as ilosc_odwiedzin
from sektor s 
left join etapy_wyprawy ew on s.id_sektora = ew.sektor
group by s.id_sektora, s.nazwa;
```
* 2
```sql
select k.nazwa,
case 
	when COUNT(u.id_uczestnika) > 0 then 'brał udział w wyprawie' 
  else 'nie brał udziału w wyprawie' 
end as udzial_w_wyprawie
from kreatura k 
left join uczestnicy u on k.idKreatury = u.id_uczestnika
group by k.nazwa;
```
### Zad 4
* 1
```sql
select w.nazwa as nazwa_wyprawy, sum(length(ew.dziennik)) as dlugosc_dziennika
from wyprawa w 
join etapy_wyprawy ew on w.id_wyprawy = ew.idWyprawy
group by w.nazwa
having dlugosc_dziennika < 400;
```
* 2
```sql
select w.nazwa, avg(z.waga * z.ilosc)
from wyprawa w 
join uczestnicy u on w.id_wyprawy = u.id_wyprawy
join kreatura k on k.idKreatury = u.id_uczestnika
join ekwipunek e on k.idKreatury = e.idKreatury
join zasob z on e.idZasobu = z.idZasobu
group by w.nazwa;
```
### Zad 5
```sql
select k.nazwa, datediff(w.data_rozpoczecia, k.dataUr) as wiek_w_dniach_w_momencie_rozpoczecia 
from kreatura k
inner join uczestnicy u on u.id_uczestnika = k.idKreatury
inner join etapy_wyprawy ew on u.id_wyprawy = ew.idWyprawy
inner join wyprawa w on w.id_wyprawy = u.id_wyprawy
where ew.sektor = '7';
```


