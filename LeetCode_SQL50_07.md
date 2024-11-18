# LEETCODE SQL 50

## [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/)

Table: `Sales`

```sql
+-------------+-------+
| Column Name | Type  |
+-------------+-------+
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |
+-------------+-------+
```

- (sale_id, year) bu tablonun birincil anahtarıdır.
- product_id, **Product** tablosuna referans veren bir yabancı anahtardır.
- Her satır, belirli bir yıl içinde **product_id**'li bir ürünün satışını gösterir.

Table: `Product`

```sql
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| product_id   | int     |
| product_name | varchar |
+--------------+---------+
```

- product_id, bu tablonun birincil anahtarıdır

### **Sales** tablosundaki her bir **sale_id** için **product_name**, **year** ve **price** bilgilerini raporlayan bir çözüm yazın.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Sales table:
+---------+------------+------+----------+-------+
| sale_id | product_id | year | quantity | price |
+---------+------------+------+----------+-------+
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |
+---------+------------+------+----------+-------+
Product table:
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |
+------------+--------------+
**Output:**
+--------------+-------+-------+
| product_name | year  | price |
+--------------+-------+-------+
| Nokia        | 2008  | 5000  |
| Nokia        | 2009  | 5000  |
| Apple        | 2011  | 9000  |
+--------------+-------+-------+

Sale_id = 1=> Nokia'nın 2008 yılında 5000'ücrete satıldığını anlayabiliriz.
Sale_id = 2=> Nokia'nın 2009 yılında 5000'ücrete satıldığını anlayabiliriz.
Sale_id = 7=> Apple' ın 2011 yılında 9000'ücrete satıldığını anlayabiliriz.
```

## Çözüm:

```sql
SELECT p.product_name, s.year, s.price
FROM Sales AS s
LEFT JOIN Product AS p
ON s.product_id = p.product_id
```

## **Açıklaması:**

### 1. **SELECT p.product_name, s.year, s.price**

- **p.product_name**: `Product` tablosundaki **product_name** (ürün adı) sütununu seçer.
- **s.year**: `Sales` tablosundaki **year** (yıl) sütununu seçer.
- **s.price**: `Sales` tablosundaki **price** (fiyat) sütununu seçer.
- Bu sorgu, her ürünün adını, satış yılını ve fiyatını döndürecektir.

### 2. **FROM Sales AS s**

- Verilerin **Sales** tablosundan alınacağını belirtir.
- **AS s**: `Sales` tablosuna **s** takma adını verir. Bu takma ad, tablonun daha kısa bir şekilde kullanılmasını sağlar.

### 3. **LEFT JOIN Product AS p**

- **LEFT JOIN**: `Sales` tablosundaki tüm satırları alır ve **Product** tablosundaki eşleşen verileri ekler.
- Eğer **Product** tablosunda eşleşen veri yoksa, **NULL** değeri döner.
- **AS p**: `Product` tablosuna **p** takma adını verir.

### 4. **ON s.product_id = p.product_id**

- **s.product_id** ile **p.product_id** değerleri eşleşen satırları birleştirir. Yani, **Sales** tablosundaki her satışın hangi ürüne ait olduğunu belirler.
