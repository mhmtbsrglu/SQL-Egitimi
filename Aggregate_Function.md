# Aggregate Fonksiyon
SQL'deki AGGREGATE fonksiyonu, bir veri kümesinin özet istatistiklerini veya toplu sonuçlarını döndüren bir fonksiyondur. Genellikle bir sorgu içinde kullanılarak, belirli bir sütun veya sütunlardaki verileri işleyerek sonuçları toplar, gruplar veya hesaplar.
- SUM(): Belirli bir sütundaki değerlerin toplamını hesaplar.
  - ```sql
    SELECT SUM(satis_miktari) AS toplam_satis
    FROM urunler;
    ```
- COUNT(*): Belirli bir sütundaki değerlerin satır sayısını hesaplar.
  - ```sql
    SELECT COUNT(*) AS toplam_satis
    FROM urunler;
    ```
- AVG(): Belirli bir sütundaki değerlerin ortalamasını hesaplar.
  - ```sql
    SELECT AVG(satis_miktari) AS toplam_satis
    FROM urunler;
    ```
- MIN VE MAX(): Belirli bir sütundaki değerlerin minimum ve maksimum değerlerini hesaplar.
  - ```sql
    SELECT MIN(fiyat) AS en_dusuk_fiyat,
    MAX(fiyat) AS en_yuksek_fiyat
    FROM urunler;
    ```
- GROUP BY: Verileri belirli bir sütuna göre gruplayarak, grup bazlı toplu işlemler yapmayı sağlar.
  - ```sql
    SELECT kategori, COUNT(*) AS urun_sayisi
    FROM urunler
    GROUP BY kategori;

    ```
