### Zad 1
```sql
elimiter //
create trigger kreatura_before_insert
before insert on kreatura
for each row
begin
	if new.waga <= 0
    then
		set new.waga = 1;
	end if;
end
//
delimiter ;

```
