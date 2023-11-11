# Odpowiedzi do lab_03

### Zadanie 1:
  1. Stworzenie tabeli postac:
```sql
CREATE TABLE postac(id_postaci INT AUTO_INCREMENT PRIMARY KEY, nazwa VARCHAR(40), rodzaj ENUM("wiking","ptak","kobieta"), data_ur DATE, wiek INT UNSIGNED);
```
2. Stworzenie wierszy dla Bjorn, Drozd, Tesciowa: 
```sql
INSERT INTO postac VALUES(default, 'Bjorn', 'wiking', '1990-01-01', 30), (default, 'Drozd', 'ptak', '2010-05-15', 3), (default, 'Tesciowa', 'kobieta', '1965-08-20', 56);
```
3. Zmaina wieku teściowej na 88:
```sql
UPDATE postac SET wiek = 88 WHERE id_postaci = 3;
```
### Zadanie 2:
1. Stworzenie tabeli walizka:
 ```sql
CREATE TABLE walizka (id_walizki INT AUTO_INCREMENT PRIMARY KEY, pojemnosc INT UNSIGNED, kolor ENUM('różowy', 'czerwony', 'tęczowy', 'żółty'), id_wlasciciela INT, FOREIGN KEY (id_wlasciciela) REFERENCES postac(id_postaci) ON DELETE CASCADE);
```
2. Ustawienie defaultowego koloru na rozowy:
```sql
ALTER TABLE walizka MODIFY COLUMN kolor ENUM('różowy', 'czerwony', 'tęczowy', 'żółty') DEFAULT 'różowy';
```
3. Dodanie walizki dla Bjorna i tesciowej:
```sql
INSERT INTO walizka (pojemnosc, kolor, id_wlasciciela) VALUES (30, 'czerwony', 1);
```
```sql
INSERT INTO walizka (pojemnosc, kolor, id_wlasciciela) VALUES (25, 'różowy', 3);
```
### Zadanie 3:
1. Tabela izba:
```sql
CREATE TABLE izba (adres_budynku VARCHAR(255),nazwa_izby VARCHAR(255),metraz INT UNSIGNED,wlasciciel INT,PRIMARY KEY (adres_budynku, nazwa_izby),FOREIGN KEY (wlasciciel) REFERENCES postac(id_postaci) ON DELETE SET NULL);
```
2. Dodanie do izba pola kolor po polu metraz:
```sql
ALTER TABLE izba ADD COLUMN kolor VARCHAR(50) DEFAULT 'czarny' AFTER metraz;
```
3. Izba spiżarnia:
```sql
INSERT INTO izba VALUES("Bjornowska 1", "spiżarnia", 50, default, 1);
```
### Zadanie 4:
1. Tabela Przetwory:
```sql
CREATE TABLE przetwory (id_przetworu INT AUTO_INCREMENT PRIMARY KEY, rok_produkcji INT DEFAULT 1654, id_wykonawcy INT, zawartosc VARCHAR(255),dodatek VARCHAR(255) DEFAULT 'papryczka chilli',id_konsumenta INT, FOREIGN KEY (id_wykonawcy) REFERENCES postac(id_postaci), FOREIGN KEY (id_konsumenta) REFERENCES postac(id_postaci));
```
2. Bigos z papryczką chili
```sql
INSERT INTO przetwory VALUES (default, default, 1, 'bigos', default, 2);
```

Kod umieszczamy liniowo, Polecenie ```SELECT``` oznacza wybranie danych

BazY_23_**A
