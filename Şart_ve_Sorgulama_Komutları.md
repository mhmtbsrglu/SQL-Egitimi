# SQL Şart ve Sorgulama Komutları
- Where = arama filtresidir.
  - = Eşittir
  - <> Eşit Değildir
  - ( > ) Büyüktür
  - < Küçüktür
  - (>=) Büyük Eşittir
  - <= Küçük Eşittir
  - BETWEEN arasında
  - LIKE ile başlar veya biter
  - IN içinde
  - NOT LIKE başlamaz bitmez
  - NOT IN içinde değil
 
```sql
select categorY_id,category_name,description from categories where category_name != 'Beverages'
/*B% ile başlayanlar %B ile bitenler.*/
select categorY_id,category_name,description from categories where category_name LIKE 'B%'
/*
ARASINDA
3
VE
5
*/
select categorY_id,category_name,description from categories where category_id BETWEEN 3 AND 5
/*İÇERENLERİ GETİR*/
select categorY_id,category_name,description from categories where category_id IN (1,2,3,4,5)

select categorY_id,category_name,description from categories where category_name = 'Beverages' OR category_name LIKE 'Grains%'
```
