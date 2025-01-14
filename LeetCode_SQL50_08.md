# LEETCODE SQL 50

## [1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/)

Table: `Visits`

```sql
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| visit_id    | int     |
| customer_id | int     |
+-------------+---------+
```

- visit_id, bu tablodaki benzersiz değerlere sahip sütundur.

Table: `Transactions`

```sql
+----------------+---------+
| Column Name    | Type    |
+----------------+---------+
| transaction_id | int     |
| visit_id       | int     |
| amount         | int     |
+----------------+---------+
```

- transaction_id, bu tablodaki benzersiz değerlere sahip sütundur.

### İşlem yapmadan ziyaret eden kullanıcıların ID'lerini ve bu tür ziyaretleri kaç defa yaptıklarını bulan bir çözüm yazın.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Visits
+----------+-------------+
| visit_id | customer_id |
+----------+-------------+
| 1        | 23          |
| 2        | 9           |
| 4        | 30          |
| 5        | 54          |
| 6        | 96          |
| 7        | 54          |
| 8        | 54          |
+----------+-------------+
Transactions
+----------------+----------+--------+
| transaction_id | visit_id | amount |
+----------------+----------+--------+
| 2              | 5        | 310    |
| 3              | 5        | 300    |
| 9              | 5        | 200    |
| 12             | 1        | 910    |
| 13             | 2        | 970    |
+----------------+----------+--------+
**Output:**
+-------------+----------------+
| customer_id | count_no_trans |
+-------------+----------------+
| 54          | 2              |
| 30          | 1              |
| 96          | 1              |
+-------------+----------------+

ID si 23 olan müşteri, alışveriş merkezini bir kez ziyaret etti ve visit_id = 12 de bir işlem yaptı.
ID si  9 olan müşteri, alışveriş merkezini bir kez ziyaret etti ve visit_id = 13 te bir işlem yaptı.
ID si 30 olan müşteri, alışveriş merkezini bir kez ziyaret etti ve hiçbir işlem yapmadı.
ID si 54 olan müşteri, alışveriş merkezini  üç kez ziyaret etti Bu ziyaretlerin 2 sinde işlem yapmadı, birinde ise 3 işlem yaptı.
ID si 96 olan müşteri, alışveriş merkezini bir kez ziyaret etti ve hiçbir işlem yapmadı.
```

## Çözüm:

```sql
SELECT v.customer_id, COUNT(v.visit_id) AS count_no_trans
from Visits AS v
LEFT JOIN Transactions AS t
ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```

## **Açıklaması:**

### 1. **SELECT v.customer_id, COUNT(v.visit_id) AS count_no_trans**

- **v.customer_id**: `Visits` tablosundaki **customer_id** sütununu seçer. Bu, her ziyaretin hangi müşteriye ait olduğunu gösterir.
- **COUNT(v.visit_id) AS count_no_trans**: `Visits` tablosundaki **visit_id** sütunundaki verileri sayar. Bu, her müşteri için işlem yapılmayan (yani `Transactions` tablosunda karşılık gelmeyen) ziyaretlerin sayısını verir. **AS count_no_trans** ifadesi, bu sayım sonucuna **count_no_trans** adını verir.

### 2. **FROM Visits AS v**

- Verilerin **Visits** tablosundan alınacağını belirtir.
- **AS v**: `Visits` tablosuna **v** takma adını verir, böylece sorguda bu tabloyu daha kısa bir şekilde kullanabiliriz.

### 3. **LEFT JOIN Transactions AS t**

- **LEFT JOIN**: `Visits` tablosundaki tüm satırları alır ve **Transactions** tablosundaki eşleşen verileri ekler. Eşleşmeyen satırlar için **Transactions** tablosundaki değerler **NULL** olacaktır.
- **AS t**: `Transactions` tablosuna **t** takma adını verir.

### 4. **ON v.visit_id = t.visit_id**

- **ON** koşulu, iki tabloyu birleştirmek için kullanılan eşleştirme koşuludur. Burada **Visits** tablosundaki **visit_id** ile **Transactions** tablosundaki **visit_id** değerleri karşılaştırılır ve eşleşen satırlar birleştirilir.

### 5. **WHERE t.transaction_id IS NULL**

- **WHERE** koşulu, yalnızca belirli satırları seçmek için kullanılır. Burada, **Transactions** tablosunda **transaction_id** değeri **NULL** olan satırları filtreler.
- **t.transaction_id IS NULL**: Bu koşul, **Visits** tablosundaki bir ziyarete karşılık gelen **Transactions** tablosunda işlem (transaction) kaydının olmadığını gösteren satırları seçer. Yani, bu sorgu yalnızca işlem yapılmayan ziyaretleri dikkate alır.

### 6. **GROUP BY v.customer_id**

- **GROUP BY** komutu, seçilen veriyi belirli bir sütuna göre gruplar. Burada, sonuçları **customer_id**'ye göre gruplar.
- Bu, her müşteri için işlem yapılmayan ziyaretlerin sayısını hesaplamak için gereklidir.
  &nbsp;

<**_[Alper BİLGİN](https://github.com/DREAXS)_**>
