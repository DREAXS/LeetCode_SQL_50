# LEETCODE SQL 50

## [1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)

Table: `Products`

```sql
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| product_id  | int     |
| low_fats    | enum    |
| recyclable  | enum    |
+-------------+---------+
```

- **product_id**, bu tablonun **birincil anahtarı**dır (benzersiz değerlere sahip olan sütun).
- **low_fats**, **ENUM** (kategori) türünde bir alandır ve türleri ('Y', 'N')'dir. Burada 'Y', bu ürünün **düşük yağlı** olduğunu, 'N' ise **düşük yağlı** olmadığını belirtir.
- **recyclable**, **ENUM** (kategori) türünde bir alandır ve türleri ('Y', 'N')'dir. Burada 'Y', bu ürünün **geri dönüştürülebilir** olduğunu, 'N' ise **geri dönüştürülebilir** olmadığını belirtir.

### Düşük yağlı ve geri dönüştürülebilir olan ürünlerin **id**'lerini bulun.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Products table:
+-------------+----------+------------+
| product_id  | low_fats | recyclable |
+-------------+----------+------------+
| 0           | Y        | N          |
| 1           | Y        | Y          |
| 2           | N        | Y          |
| 3           | Y        | Y          |
| 4           | N        | N          |
+-------------+----------+------------+
**Output:**
+-------------+
| product_id  |
+-------------+
| 1           |
| 3           |
+-------------+
Sadece ürün 1 ve ürün 3 hem düşük yağlı hem de geri dönüştürülebilirdir
```

## Çözüm:

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y'
```

### Açıklaması:

- **SELECT product_id**: Bu kısım, sorgu sonucunda yalnızca **product_id** sütununu döndürür.

- **FROM Products**: Verilerin **Products** tablosundan alınacağını belirtir.

- **WHERE low_fats = 'Y' AND recyclable = 'Y'**: Ürünlerin hem **düşük yağlı** (`low_fats = 'Y'`) hem de **geri dönüştürülebilir** (`recyclable = 'Y'`) olmasını filtreler. Bu koşul sağlanan ürünlerin **product_id**'lerini döndürür.
