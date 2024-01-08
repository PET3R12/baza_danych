# Rozwaiązania zti1 cz.1:
### Zad1
```sql
select imie, nazwisko, data_urodzenia from pracownik;
```
### Zad2
```sql
select imie, nazwisko, (year(curdate()) - year(data_urodzenia)) as wiek from pracownik;
```
### Zad3
```sql
select d.nazwa as 'nazwa dzialu', count(p.id_pracownika) as 'ilosc pracownikow'
from dzial d
left join pracownik p on p.dzial = d.id_dzialu
group by d.nazwa;
```
### Zad 4
```sql
select k.nazwa_kategori, count(sm.ilosc) as ilosc
from towar t 
left join kategoria k on k.id_kategori = t.kategoria
left join stan_magazynowy sm on sm.towar = t.id_towaru
group by t.kategoria;
```
### Zad 5
```sql
select k.nazwa_kategori, group_concat(t.nazwa_towaru) as 'towary w tej kategorii'
from kategoria k 
left join towar t on t.kategoria = k.id_kategori
group by k.nazwa_kategori;
```
### Zad 6
```sql
select round(avg(pensja), 2) as 'srednia pensja pracownikow' from pracownik;
```
### Zad 7 
```sql
select round(avg(pensja)) as 'srednia pensja' from pracownik where year(curdate() - data_zatrudnienia) > 5;
```
### Zad 8
```sql
select t.nazwa_towaru, sum(pz.ilosc)
from towar t 
inner join pozycja_zamowienia pz on t.id_towaru = pz.towar
group by t.nazwa_towaru
order by 2 desc limit 10;
```

### Zad 9 
```sql
select z.numer_zamowienia, sum(pz.ilosc * pz.cena) as wartosc_zamowienia
from zamowienie z
inner join pozycja_zamowienia pz on pz.zamowienie = z.id_zamowienia
where year(z.data_zamowienia) = 2017
and quarter(z.data_zamowienia) = 1
group by z.id_zamowienia;
```

### Zad 10
```sql
select imie, nazwisko, sum(pz.ilosc * pz.cena) as wartosc
from zamowienie z
inner join pozycja_zamowienia pz on pz.zamowienie = z.id_zamowienia
inner join pracownik p on p.id_pracownika = z.pracownik_id_pracownika
group by p.id_pracownika
order by wartosc desc;
```

