# LEETCODE SQL 50

## [584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/)

Table: `Customer`

```sql
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| name        | varchar |
| referee_id  | int     |
+-------------+---------+
```

- SQL'de, **id** bu tablonun birincil anahtar sütunudur.
- Bu tablonun her satırı, bir müşterinin **id**'sini, adını ve onları referans gösteren müşterinin **referee_id**'sini belirtir.

### Müşteri id'si 2 olan müşteri tarafından referans gösterilmeyen müşterilerin isimlerini bulun.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Customer table:
+----+------+------------+
| id | name | referee_id |
+----+------+------------+
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |
+----+------+------------+
**Output:**
+------+
| name |
+------+
| Will |
| Jane |
| Bill |
| Zack |
+------+
```

## Çözüm:

```sql
SELECT name
FROM Customer
WHERE referee_id IS NULL OR referee_id != 2
```

### Açıklaması:

- **SELECT name**: Müşterilerin isimlerini seçer.

- **FROM Customer**: Veriler **Customer** tablosundan alınır.

- **WHERE referee_id IS NULL OR referee_id != 2**:

  - **referee_id IS NULL**: Referans gösteren müşteri olmayan (referee_id değeri NULL olan) müşterileri seçer.
  - **OR referee_id != 2**: Ya da **referee_id** değeri 2 olmayan (yani müşteri id'si 2 tarafından referans gösterilmeyen) müşterileri seçer.
    &nbsp;

<**_[Alper BİLGİN](https://github.com/DREAXS)_**>
