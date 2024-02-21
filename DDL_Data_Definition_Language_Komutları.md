# Data Definition Language
Bir veritabanının yapısını ve tablolar, görünümler, dizinler ve prosedürler gibi nesnelerini tanımlamak için kullanılan SQL'in (Yapılandırılmış Sorgu Dili) bir alt kümesidir. 

## DDL ve DML Farkı
DDL (Data Definition Language), veritabanı yapısını tanımlamak için kullanılırken, DML (Data Manipulation Language), veritabanındaki verileri sorgulamak ve manipüle etmek için kullanılır.

- Create: Veritabanı nesnesi oluşturmak için kullanılır.
- Alter: Veritabanı nesnesinin özelliğini değiştirmek için kullanılır.
- Drop: Bir veritabanı nesnesini silmek için kullanılır.
- Drop, Delete ve Truncate Farkı: Truncate tablo içini boşaltır, Delete şart verdiysek verilen şartı siler, Drop tabloyu tamamen kaldırır.

```sql
create table news(
news_id varchar(255),
new_detail varchar(255),
created_date date,
updated_date date
)
/*
ALTER
NESNE TÜRÜ
NEYIN ÜZERİNDE
NE YAPMAK İSTİYORSUN (PRİMARY KEY)
ALAN ADI
*/
ALTER TABLE news ADD PRIMARY KEY (news_id)
/*
ALTER
NESNE TÜRÜ
NEYIN ÜZERİNDE
NE YAPMAK İSTİYORSUN (YENI ALAN OLUŞTURMAK)
ALAN ADI
*/
ALTER TABLE news ADD product_id INT
/*
ALTER
NESNE TÜRÜ
NEYIN ÜZERİNDE
NE YAPMAK İSTİYORSUN (MEVCUT ALANI BOŞ OLAMAZ OLARAK GÜNCELLEMEK)
ALAN ADI
*/
ALTER TABLE news
ALTER COLUMN product_id TYPE INT,
ALTER COLUMN product_id SET NOT NULL;
```
