# LEETCODE SQL 50

## [1148. Article Views I](https://leetcode.com/problems/article-views-i/)

Table: `Views`

```sql
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| article_id    | int     |
| author_id     | int     |
| viewer_id     | int     |
| view_date     | date    |
+---------------+---------+
```

- Bu tablonun birincil anahtarı (benzersiz değerlere sahip sütun) yoktur, bu nedenle tablo tekrarlanan satırlara sahip olabilir.
- Her satır, bir **viewer_id**'nin bir **article_id**'yi (yazarı belirten **author_id**) belirli bir **view_date**'de görüntülediğini belirtir.
- **Not:** **author_id** ve **viewer_id** eşit olduğunda, bu durum aynı kişiyi ifade eder.

### Kendi yazdığı en az bir makaleyi görüntüleyen tüm yazarları bulun.

### Sonuç tablosunu **id**'ye göre artan sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Views table:
+------------+-----------+-----------+------------+
| article_id | author_id | viewer_id | view_date  |
+------------+-----------+-----------+------------+
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |
+------------+-----------+-----------+------------+
**Output:**
+------+
| id   |
+------+
| 4    |
| 7    |
+------+
```

## Çözüm:

```sql
SELECT DISTINCT author_id as id
FROM Views
WHERE author_id = viewer_id
ORDER BY id
```

### Açıklaması:

- **SELECT DISTINCT author_id as id**: **author_id** sütunundaki benzersiz değerleri seçer ve **author_id**'yi **id** olarak adlandırır.
- **FROM Views**: Verilerin **Views** tablosundan alınacağını belirtir.
- **WHERE author_id = viewer_id**: **author_id** ve **viewer_id** değerlerinin eşit olduğu satırları seçer, yani kendi yazdığı makaleyi görüntüleyen yazarları filtreler.
- **ORDER BY id**: Sonuçları **id** sütununa göre artan sırayla sıralar. Bu sorgu, **kendi yazdığı makaleyi görüntüleyen yazarların** **author_id** değerlerini **id** olarak döndürür.
