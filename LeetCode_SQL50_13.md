**# LEETCODE SQL 50**

[[570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/)]

Table: `Employee`

```sql
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| name        | varchar |
| department  | varchar |
| managerId   | int     |
+-------------+---------+
```

Bu `Employee` tablosu:

1.  **id (int)**: Çalışanın benzersiz kimlik numarası (birincil anahtar).
2.  **name (varchar)**: Çalışanın adı.
3.  **department (varchar)**: Çalışanın ait olduğu departman.
4.  **managerId (int)**: Çalışanın yöneticisinin `id` numarası. Eğer `NULL` ise yöneticisi yok demektir.

Bir çalışan kendi yöneticisi olamaz.

---

**En az beş doğrudan raporlama yapan yöneticileri bulan bir çözüm yazın.**

**Sonuç tablosunu herhangi bir sırayla döndürün.**

**Sonuç formatı aşağıdaki örneğe benzer olacaktır.**

`ÖRNEK`

```sql
**Input:**
Employee table:
+-----+-------+------------+-----------+
| id  | name  | department | managerId |
+-----+-------+------------+-----------+
| 101 | John  | A          | null      |
| 102 | Dan   | A          | 101       |
| 103 | James | A          | 101       |
| 104 | Amy   | A          | 101       |
| 105 | Anne  | A          | 101       |
| 106 | Ron   | B          | 101       |
+-----+-------+------------+-----------+
**Output:**
+------+
| name |
+------+
| John |
+------+
```

Bu SQL sorgusunun kısa açıklaması:

1.  **Ana Sorgu:**

    - **`SELECT name`**: Çalışanların adlarını seçer.
    - **`WHERE id IN`**: Yalnızca, alt sorgudan dönen yöneticilerin kimlik numaralarına sahip çalışanları seçer.

2.  **Alt Sorgu:**

    - **`SELECT managerId`**: Yöneticilerin kimlik numaralarını alır.
    - **`GROUP BY managerId`**: Yöneticilere göre gruplar.
    - **`HAVING count(*) >= 5`**: En az 5 çalışanı olan yöneticileri seçer.

**Sonuç:** En az 5 çalışanı olan yöneticilerin altında çalışanların adları döndürülür.

&nbsp;

<**_[Alper BİLGİN](https://github.com/DREAXS)_**>
