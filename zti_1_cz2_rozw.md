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
### Zad 3
```sql
select year(z.data_zamowienia) as rok, sum(pz.ilosc * pz.cena) as przychod
from zamowienie z 
inner join pozycja_zamowienia pz on z.id_zamowienia = pz.zamowienie
group by rok;
```
### Zad 4
```sql
select sum(pz.ilosc* pz.cena) as wartosc_anulowanych_zamowien
from status_zamowienia sz
inner join zamowienie z on z.status_zamowienia = sz.id_statusu_zamowienia
inner join pozycja_zamowienia pz on z.id_zamowienia = pz.id_pozycji
where nazwa_statusu_zamowienia = 'anulowane';
```
### Zad 5
```sql
select ak.miejscowosc, count(z.id_zamowienia) as liczba_zamowien_z_danej_miejscowosci, sum(pz.ilosc*pz.cena) as suma_watrosci_zamowien
from adres_klienta ak
inner join klient k on k.id_klienta = ak.klient
inner join zamowienie z on z.klient = k.id_klienta
inner join typ_adresu ta on ta.id_typu = ak.typ_adresu
inner join pozycja_zamowienia pz on pz.zamowienie = z.id_zamowienia
where ta.nazwa = 'podstawowy'
group by ak.miejscowosc;
```
### Zad 6
```sql
select ((sum(t.cena_zakupu * sm.ilosc)) - (sum(pz.ilosc *  pz.cena))) as Dochod
from towar t 
inner join stan_magazynowy sm on t.id_towaru = sm.towar
inner join pozycja_zamowienia pz on t.id_towaru = pz.towar
inner join zamowienie z on z.id_zamowienia = pz.zamowienie
inner join status_zamowienia sz on sz.id_statusu_zamowienia = z.status_zamowienia
where sz.nazwa_statusu_zamowienia = 'zrealizowane';
```
### Zad 7
```sql
select year(z.data_zamowienia) as rok ,sum((t.cena_zakupu * sm.ilosc) - (pz.ilosc *  pz.cena)) as przychod
from towar t 
inner join stan_magazynowy sm on t.id_towaru = sm.towar
inner join pozycja_zamowienia pz on t.id_towaru = pz.towar
inner join zamowienie z on z.id_zamowienia = pz.zamowienie
inner join status_zamowienia sz on sz.id_statusu_zamowienia = z.status_zamowienia
where sz.nazwa_statusu_zamowienia = 'zrealizowane'
group by year(z.data_zamowienia);
```
### Zad 8
```sql
select k.nazwa_kategori, round(sum(sm.ilosc), 0) as ilosc_rzeczy_w_tej_kategori
from kategoria k 
inner join towar t on t.kategoria = k.id_kategori
inner join stan_magazynowy sm on t.id_towaru = sm.towar
group by t.kategoria;
```
### Zad 9
```sql
select monthname(data_urodzenia) as Miesiac, count(month(data_urodzenia)) as 'Liczba pracownikow'
from pracownik p
group by Miesiac
order by field(Miesiac, 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December');
```
### Zad 10
```sql
select imie, nazwisko, ((timestampdiff(month, data_zatrudnienia, curdate())) * pensja) as koszty_pracodawcy
from pracownik;
```
