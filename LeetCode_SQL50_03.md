# LEETCODE SQL 50

## [595. Big Countries](https://leetcode.com/problems/big-countries/)

Table: `World`

```sql
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| name        | varchar |
| continent   | varchar |
| area        | int     |
| population  | int     |
| gdp         | bigint  |
+-------------+---------+
```

- **name**, bu tablonun birincil anahtarıdır (benzersiz değerlere sahip olan sütun).
- Bu tablonun her satırı, bir ülkenin **adını**, ait olduğu **kıtayı**, **yüzölçümünü**, **nüfusunu** ve **gdp** değerini içerir.

### Yüzölçümü en az üç milyon (yani, 3.000.000 km²) ise, veya

### Nüfusu en az yirmi beş milyon (25.000.000) ise.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
World table:
+-------------+-----------+---------+------------+--------------+
| name        | continent | area    | population | gdp          |
+-------------+-----------+---------+------------+--------------+
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |
+-------------+-----------+---------+------------+--------------+
**Output:**
+-------------+------------+---------+
| name        | population | area    |
+-------------+------------+---------+
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |
+-------------+------------+---------+
```

## Çözüm:

```sql
SELECT name, population, area
FROM world
WHERE area >= 3000000 OR population >=25000000
```

### Açıklaması:

- **SELECT name, population, area**: **name**, **population** ve **area** sütunlarını seçer.
- **FROM world**: Veriler **world** tablosundan alınır.
- **WHERE area >= 3000000 OR population >= 25000000**: Yüzölçümü en az 3 milyon km² veya nüfusu en az 25 milyon olan ülkeleri seçer.
  Bu sorgu, **yüzölçümü 3 milyon km²** veya **nüfusu 25 milyon** olan ülkelerin **adını**, **nüfusunu** ve **yüzölçümünü** döndürür.
  &nbsp;

<**_[Alper BİLGİN](https://github.com/DREAXS)_**>
