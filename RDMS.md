# Relational Database Management Systems
- SQL'de iki konuda zorlanıyorduk, group by aggregate ve ilişkisel veritabanı.
- RDMS modern veri tabanı sistemlerin desteklediği, hem performans hem yerden tasarruf etmek dahil veri bütünlüğünü korumak amaçlıdır.
- Tekrar eden verileri tekilleştirme sistemleridir.


# Constraint:
- SQL Constraint (kısıtlamalar), bir tablodaki veriler için kurallar belirtmek için kullandığımız yapıdır.
- Tablodaki verilerin doğruluğunu ve güvenilirliğini sağlar.
- Aşağıdaki kısıtlamalar SQL’de yaygın olarak kullanılır
  - NOT NULL boş olamaz şartıdır
  - UNIQUE tekil olmalıdır
  - PRIMARY KEY NOT NULL VE UNIQUE karışımıdır.
  - CHECK Bir sütundaki değerlerin belirli bir koşulu karşılamasını sağlar.
  - DEFAULT Varsayılan değer işlemleridir
  - CREATE-INDEX Veritabanında çok hızlı indeks oluşturma işlemidir.
 
Primary key: Birincil tekil olan temsil anahtardır.

Foreign key: 
- İki tablo arasındaki ilişkiyi tanımlayan bir veya birden fazla alan içerir.
- Yabancı anahtar, bir tablodaki bir alanın, diğer tablodaki birincil anahtar ile ilişkilendirilmesini sağlar.
```sql
CREATE TABLE customer (
	_id INT PRIMARY KEY,
	id TEXT NOT NULL,
	account_id INT,
	is_active BOOLEAN NOT NULL DEFAULT false,
	created_date DATE NOT NULL DEFAULT CURRENT_DATE,
	subscription_id INT,
	CONSTRAINT FK_SUBSCRIPTION_ID -- Yabancı kısıtlanacak anahtar adı
		FOREIGN KEY (subscription_id) -- Yabancı anahtar adı
		REFERENCES subscription (_id) -- Yabancı anahtarın referans aldığı tablo ve sütun
);

CREATE TABLE subscription (
	_id INT NOT NULL PRIMARY KEY,
	id TEXT NOT NULL,
	type TEXT NOT NULL
);
```

# Geleneksel Yöntem
- Tavsiye edilen yöntem değildir. En Eskiden kullanılan yöntemdir.
- İki tablo ile pk ve fk'lar karşılaştırılır veri elde edilirdi (select kullanarak)
- Tabloların virgül ile ayrı belirtilmesi gerekmektedir.
- ```sql
  CREATE DATABASE TCELL_RDMS

  CREATE TABLE account(
  	_id INT PRIMARY KEY ,
  	id Text not null,
  	email varchar(50) NOT NULL,
  	password varchar(50) NOT NULL,
  	is_active boolean not null default false,
  	created_date DATE not null default CURRENT_DATE
  )
  
  INSERT INTO account (_id,id,email,password) VALUES(1,'123-456-777','admin@midas.com','123456')
  
  create table customer(
  	_id INT PRIMARY KEY ,
  	id Text not null,
  	account_id INT,
  	is_active boolean not null default false,
  	created_date DATE not null default CURRENT_DATE
  )
  
  INSERT INTO customer (_id,id,account_id) VALUES(1,'777-777',1)
  
  /* GELENEKSEL YÖNTEM İLE VERİ İLİŞKİSİ 
  AS = ALİAS.
  */
  SELECT CUSTOMER._id as Musteri_id, CUSTOMER.account_id, ACCOUNT.email,ACCOUNT.password FROM ACCOUNT account, CUSTOMER customer WHERE ACCOUNT._id = CUSTOMER.account_id```

# Join Yöntemi:
- En çok kullanılan yöntemdir. Bilinmesi gerekmektedir.
- Birden fazla join edilen tablo bulunabilir. (TABLO 1 = ACCOUNT, TABLO 2 CUSTOMER, TABLO 3 = ŞEHİRLER)
- İlişkisel veritabanlarında birden fazla tabloyu birleştirmek için kullanılan bir SQL operatörüdür. İki veya daha fazla tablonun belirli bir sütundaki değerlere göre eşleştirilmesini sağlar. Bu sayede, ilişkilendirilmiş veriler bir araya getirilebilir.
- ```sql
  
	/* JOIN YÖNTEM İLE VERİ İLİŞKİSİ 
	ON = EŞLEŞME KRİTERİDİR.
	*/
	SELECT CUSTOMER._id as Musteri_id, CUSTOMER.account_id, ACCOUNT.email,ACCOUNT.password FROM ACCOUNT account JOIN CUSTOMER customer ON ACCOUNT._id = CUSTOMER.account_id
  ```
##  Join Türleri
- Inner Join:Bu, eşleşen satırları getirir. Yani, eşleşmeyen satırlar sonuç kümesine dahil edilmez.
  - ![image](https://github.com/mhmtbsrglu/SQL-Egitimi/assets/99546413/b1728882-b8b8-4f48-a046-a9588d037271)
 
- LEFT (OUTER) JOIN: Sol tablonun tüm satırlarını ve eşleşen sağ tablo satırlarını getirir. Eşleşmeyen sağ tablo satırları NULL değerleriyle doldurulur.
  - ![image](https://github.com/mhmtbsrglu/SQL-Egitimi/assets/99546413/48edf4de-c7dd-4966-8810-dc463c4b3ac6)
 
- RIGHT (OUTER) JOIN: Sağ tablonun tüm satırlarını ve eşleşen sol tablo satırlarını getirir. Eşleşmeyen sol tablo satırları NULL değerleriyle doldurulur.
  - ![image](https://github.com/mhmtbsrglu/SQL-Egitimi/assets/99546413/7407574b-ef04-4b60-88e7-dd20915931d6)
 
- FULL (OUTER) JOIN: Her iki tablonun tüm satırlarını getirir ve eşleşmeyen satırları NULL değerleriyle doldurur.

# Subquery:
- Bir sql sorgusunun parantez içerisinde başka sql sorgusunu kullanma işlemidir.

```sql
-- Ana sorgu
SELECT
    customer_id,
    (SELECT SUM(order_amount) FROM orders WHERE customer_id = customers.customer_id) AS toplam_siparis_miktari,
    (SELECT MAX(order_amount) FROM orders WHERE customer_id = customers.customer_id) AS en_yuksek_siparis_miktari
FROM
    customers;
```

# Cross Apply:
- Birden fazla tabloyu birleştirmek için kullanılan farklı yöntemdir.
```sql
SELECT
    customers.customer_id,
    orders.order_id
FROM
    customers
CROSS APPLY
    (
        SELECT
            order_id
        FROM
            orders
        WHERE
            customer_id = customers.customer_id
    ) AS orders;

```

# Select Into:  
SELECT INTO, SQL dilinde bir tabloyu oluşturup, bu tabloya bir sorgunun sonuçlarını eklemek için kullanılan bir ifadedir. Bu ifade, mevcut bir tablonun içeriğini veya bir sorgunun sonuçlarını alarak yeni bir tablo oluşturur veya mevcut bir tablonun içeriğini değiştirir.
