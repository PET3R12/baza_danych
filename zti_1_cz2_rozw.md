# Rozwiązania zti 1 cz.2
### Zad 1
```sql
select d.nazwa, min(p.pensja), max(p.pensja), avg(p.pensja) as srednia_pensja
from pracownik p
inner join dzial d on p.dzial = d.id_dzialu
group by d.id_dzialu;
```
### Zad 2
```sql
select k.pelna_nazwa,z.numer_zamowienia,  sum(pz.ilosc * pz.cena) as wartosc
from zamowienie z
inner join pozycja_zamowienia pz on pz.zamowienie = z.id_zamowienia
inner join klient k on k.id_klienta = z.klient
group by z.id_zamowienia
order by wartosc desc limit 10;
```
### Zad 7
```sql
select year(z.data_zamowienia), sum(sm.ilosc * pz.cena) - sum(t.cena_zakupu * pz.ilosc) as dochod
from pozycja_zamowienia pz
inner join zamowienie z on z.id_zamowienia = pz.zamowienie
inner join towar t on t.id_towaru = pz.towar
inner join stan_magazynowy sm on sm.towar = t.id_towaru
group by year(z.data_zamowienia);
```
