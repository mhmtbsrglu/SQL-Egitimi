# Data Manipulation Language
Data Manipulation Language veya kısaca DML, ilişkisel bir veritabanındaki verileri yönetmenize ve değiştirmenize izin veren güçlü bir araçtır. 
- Select : Veriyi seçer
- Insert: Veri Ekler
- Update: Veriyi Günceller
- Delete: Veriyi Siler
- Truncate: Tablo'nun içini boşaltır.

```sql
select categorY_id,category_name,description from categories 
/*
YENİ KAYIT EKLE
NEREYE = CATEGORIES
ALANLAR
DEĞERLER
*/
insert into categories (category_id,category_name,description) values (9,'Electronics','Apple, Samsung Products')

update categories SET description='phone,computer, iot'  where category_name = 'Electronics'

/*delete from categories */

/*tabloyu tamamen boşaltır. truncate categories */
```

- Distinct: Sorgu sonucunun tekil olmasını sağlar.
- Order By: Sıralama sorgusudur
- TOP: Sorgu sonucu verilerin bir kısmının gelmesini sağlar.
- AS: (Alias) istediğimiz şekilde kolon adlarını görme imkanı sunar.

```sql
select DISTINCT categorY_id,category_name,description from categories where category_name != 'Beverages'

/*
order by = Sırala
DESC = Sondan Başa doğru
ASC = Baştan Sona Doğru
*/
select DISTINCT categorY_id,category_name,description from categories ORDER BY category_id DESC

SELECT product_id AS Ürün_No, * FROM public.products
ORDER BY product_id ASC 

```
