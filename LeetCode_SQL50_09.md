# LEETCODE SQL 50

## [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/)

Table: `Weather`

```sql
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
```

- id, bu tablodaki benzersiz değerlere sahip sütundur.
- Aynı **recordDate**'e sahip farklı satırlar bulunmamaktadır.

### Herhangi bir tarihteki sıcaklık, bir önceki gün (dünkü) sıcaklığından daha yüksek olan tüm tarihlerin **id**'lerini bulun.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Weather table:
+----+------------+-------------+
| id | recordDate | temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+
**Output:**
+----+
| id |
+----+
| 2  |
| 4  |
+----+

-   2015-01-02 de, sıcaklık bir önceki günden (10 -> 25) daha yüksektir.
-   2015-01-04 te, sıcaklık bir önceki günden (20 -> 30) daha yüksektir.
```

## Çözüm:

```sql
SELECT w2.Id AS id
FROM Weather AS w1
INNER JOIN Weather AS w2
ON DATEDIFF(day, w1.recordDate, w2.recordDate)=1
AND w2.temperature > w1.temperature
```

## **Açıklaması:**

### 1. **SELECT w2.Id AS id**

- **w2.Id**: `Weather` tablosundaki **Id** sütununu seçer. Burada, `w2` olarak adlandırdığımız ikinci `Weather` tablosundaki **Id** değerini alıyoruz.
- **AS id**: **w2.Id** sütununa **id** adını verir. Yani, bu sorgu sonucunda dönen sütunun adı **id** olacaktır.

### 2. **FROM Weather AS w1**

- **FROM** komutu, verilerin hangi tablodan alınacağını belirtir. Burada, veriler **Weather** tablosundan alınmaktadır.
- **AS w1**: `Weather` tablosuna **w1** takma adını verir. Bu, sorgu içerisinde tablonun kısa bir şekilde kullanılmasını sağlar.

### 3. **INNER JOIN Weather AS w2**

- **INNER JOIN**: Bu, iki tabloyu birleştiren bir tür bağlantıdır. **INNER JOIN**, yalnızca her iki tablodaki eşleşen satırları döndürür.
- Burada, **Weather** tablosu bir kez daha **w2** takma adıyla sorguya ekleniyor. Bu, aynı tablonun iki kez kullanıldığı bir sorgudur.
- **w2** tablosu, **w1** tablosu ile birleştirilecektir.

### 4. **ON DATEDIFF(day, w1.recordDate, w2.recordDate) = 1**

- **ON**: İki tabloyu birleştirmek için kullanılan koşulu belirtir.
- **DATEDIFF(day, w1.recordDate, w2.recordDate) = 1**:
  - **DATEDIFF** fonksiyonu, iki tarih arasındaki farkı hesaplar. Burada, `w1.recordDate` ile `w2.recordDate` arasındaki fark **1 gün** olmalıdır.
  - Yani, `w1` ve `w2` tablolarındaki tarihler arasındaki fark 1 gün olmalıdır. Örneğin, bir tarih **2024-10-01** ise diğer tarih **2024-10-02** olmalıdır.

### 5. **AND w2.temperature > w1.temperature**

- Bu ek koşul, **w2** tablosundaki sıcaklığın (**temperature**) **w1** tablosundaki sıcaklıktan (**temperature**) daha yüksek olmasını zorunlu kılar.
- Yani, sadece bir gün arayla kaydedilen ve **w2** tarihindeki sıcaklığın, **w1** tarihindeki sıcaklıktan daha yüksek olduğu durumlar seçilir.
