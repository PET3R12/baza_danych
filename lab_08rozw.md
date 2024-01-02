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
### Zad 5
```sql
select k.nazwa, datediff(w.data_rozpoczecia, k.dataUr) as wiek_w_dniach_w_momencie_rozpoczecia 
from kreatura k
inner join uczestnicy u on u.id_uczestnika = k.idKreatury
inner join etapy_wyprawy ew on u.id_wyprawy = ew.idWyprawy
inner join wyprawa w on w.id_wyprawy = u.id_wyprawy
where ew.sektor = '7';
```


