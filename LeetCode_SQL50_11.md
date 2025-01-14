**# LEETCODE SQL 50**

[[577. Employee Bonus](https://leetcode.com/problems/employee-bonus/)]

Table: `Employee`

```sql
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| empId       | int     |
| name        | varchar |
| supervisor  | int     |
| salary      | int     |
+-------------+---------+
```

Bu `Employee` tablosu şu sütunlardan oluşur:

1.  **empId (int)**: Çalışanın benzersiz kimliği.
2.  **name (varchar)**: Çalışanın adı.
3.  **supervisor (int)**: Çalışanın yöneticisinin `empId` değeri.
4.  **salary (int)**: Çalışanın maaşı.

Table: `Bonus`

```sql
+-------------+------+
| Column Name | Type |
+-------------+------+
| empId       | int  |
| bonus       | int  |
+-------------+------+
```

Bu `Bonus` tablosu şu sütunlardan oluşur:

1.  **empId (int)**: Çalışanın benzersiz kimliği.
2.  **bonus (int)**: Çalışanın aldığı bonus miktarı.

**Her bir çalışanın adını ve 1000'den daha az bonus alan çalışanların bonus miktarını raporlayan bir çözüm yazın.**

**Sonuç tablosunu herhangi bir sırayla döndürün.**

**Sonuç formatı aşağıdaki örneğe benzer olacaktır.**

`Örnek`

```sql
**Input:**
Employee table:
+-------+--------+------------+--------+
| empId | name   | supervisor | salary |
+-------+--------+------------+--------+
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |
+-------+--------+------------+--------+
Bonus table:
+-------+-------+
| empId | bonus |
+-------+-------+
| 2     | 500   |
| 4     | 2000  |
+-------+-------+
**Output:**
+------+-------+
| name | bonus |
+------+-------+
| Brad | null  |
| John | null  |
| Dan  | 500   |
+------+-------+
```

---

`Çözüm`

```sql
SELECT name, bonus
FROM Employee e
LEFT JOIN Bonus b
ON e.empId = b.empId
WHERE bonus < 1000
OR bonus IS NULL
```

Bu SQL sorgusunun adım adım açıklaması:

1.  **SELECT name, bonus**:

    - Çalışanların adını (`name`) ve bonus miktarını (`bonus`) seçer.

2.  **FROM Employee e**:

    - `Employee` tablosunu alias olarak `e` kullanarak sorgular.

3.  **LEFT JOIN Bonus b**:

    - `Bonus` tablosunu alias olarak `b` kullanarak `Employee` tablosuna sol dış birleşim (LEFT JOIN) yapar.
    - Sol dış birleşim, tüm çalışanları listelemeyi garanti eder ve bonusu olmayanlar için `NULL` değeri döndürür.

4.  **ON e.empId = b.empId**:

    - İki tabloyu, `empId` sütununa göre eşleştirir. Yani her çalışanın `empId`'si ile bonusun `empId`'sini bağlar.

5.  **WHERE bonus < 1000 OR bonus IS NULL**:

    - Bonus miktarı 1000'den küçük olanları veya bonusu olmayan (NULL olan) çalışanları filtreler.

&nbsp;

<**_[Alper BİLGİN](https://github.com/DREAXS)_**>
