# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

# Proje Kurulumu
Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

## Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.
* src -> main -> resources altında `test.sql` adında bir doya bulacaksınız.
* `test.sql` dosyasını projeye başlamadan önce kendi veritabanınızda MUTLAKA ÇALIŞTIRMALISINIZ.
* `application.properties` dosyasında `spring.datasource.username` karşısına veritabanını bağlanmak için kullandığınız kullanıcı ismini MUTLAKA GİRİNİZ.
* `application.properties` dosyasında `spring.datasource.password` karşısına veritabanını bağlanmak için kullandığınız şifreyi MUTLAKA GİRİNİZ.


#Tablolar
`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/] (update, delete, drop sorguları iptal edilmiştir).

### Görevler
* Öncelikle aşağıdaki sorguların tümünü yazdıktan sonra veritabanınızda çalıştırınız. Projenin içerisine yazdığınız sorguları eklemenize gerek yoktur.
* Uygulamadaki testler yazdığınız sorguların tümünün veritabanında çalıştırıldığını varsayarak test edeceklerdir. Bu yüzden aşağıdaki 10 sorgu için yazdığınız queryleri mutlaka veritabanında çalıştırdıktan sonra test kısmına geliniz.

# SQL DML Procedures

Bu proje PostgreSQL üzerinde SQL DML, Function ve Procedure konularını içeren alıştırmaları kapsamaktadır.

## Görevler ve Çözümler

### 1. Biyografi türünü ekleyin

```sql
INSERT INTO tur (ad)
VALUES ('Biyografi');
```

---

### 2. Nurettin Belek isimli yazarı ekleyin

```sql
INSERT INTO yazar (ad, soyad)
VALUES ('Nurettin', 'Belek');
```

---

### 3. 10B sınıfındaki öğrencileri 10C sınıfına geçirin

```sql
UPDATE ogrenci
SET sinif = '10C'
WHERE sinif = '10B';
```

...

### 8. ogrencilistesi fonksiyonu

```sql
CREATE OR REPLACE FUNCTION ogrencilistesi()
RETURNS SETOF ogrenci
LANGUAGE sql
AS $BODY$
    SELECT * FROM ogrenci;
$BODY$;
```

### 9. ekle prosedürü

```sql
CREATE OR REPLACE PROCEDURE public.ekle(
    p_ad VARCHAR,
    p_puan INTEGER,
    p_yazarno BIGINT,
    p_turno BIGINT
)
LANGUAGE plpgsql
AS $BODY$
BEGIN
    INSERT INTO kitap(ad, puan, yazarno, turno)
    VALUES (p_ad, p_puan, p_yazarno, p_turno);
END;
$BODY$;
```

### 10. sil prosedürü

```sql
CREATE OR REPLACE PROCEDURE public.sil(
    p_ogrno BIGINT
)
LANGUAGE plpgsql
AS $BODY$
BEGIN
    DELETE FROM ogrenci
    WHERE ogrno = p_ogrno;
END;
$BODY$;
```


### ⚠️ Skorun NextGen'e Kaydedilmediyse

Eğer testleri çalıştırdığın halde skorun NextGen'e kaydedilmediyse, önce fork'unun güncel olup olmadığını kontrol et:

1. GitHub reponu aç.
2. Repo **X commit ahead** ve **X commits behind** şeklinde bir uyarı gösteriyorsa, branch'in güncel değildir.
3. **Sync fork → Update branch** adımlarını uygula.
4. Ardından localinde şu komutu çalıştır:

```bash
   git pull
```

5. Testleri tekrar çalıştır. Bu adımdan sonra skorun güncellenmiş olacaktır.

> **Not:** Bu kontrolü yapmadan tekrar tekrar test çalıştırmak sorunu çözmez; sorunun kaynağı genellikle fork'un upstream repository ile senkron olmamasıdır.
