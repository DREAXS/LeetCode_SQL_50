**# LEETCODE SQL 50**

[[1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/)]

Table: `Signups`

```sql
+----------------+----------+
| Column Name    | Type     |
+----------------+----------+
| user_id        | int      |
| time_stamp     | datetime |
+----------------+----------+
```

`Signups` tablosu:

1.  **user_id (int)**: Kullanıcının benzersiz kimlik numarası.
2.  **time_stamp (datetime)**: Kullanıcının kaydolma tarihi ve saati.

Table: `Confirmations`

```sql
+----------------+----------+
| Column Name    | Type     |
+----------------+----------+
| user_id        | int      |
| time_stamp     | datetime |
| action         | ENUM     |
+----------------+----------+
```

`Confirmations` tablosu:

1.  **user_id (int)**: Kullanıcının benzersiz kimlik numarası, **`Signups`** tablosuna dış anahtar.
2.  **time_stamp (datetime)**: Onay mesajı talep edilen tarih ve saat.
3.  **action (ENUM)**: Onay durumu; `'confirmed'` (onaylandı) veya `'timeout'` (süresi dolmuş).

**Bir kullanıcının onay oranı, 'confirmed' mesajlarının sayısının, istenen toplam onay mesajlarına bölünmesiyle hesaplanır. Onay mesajı talep etmeyen bir kullanıcının onay oranı 0'dır. Onay oranını iki ondalık basamağa yuvarlayın.**

**Her bir kullanıcının onay oranını bulan bir çözüm yazın.**

**Sonuç tablosunu herhangi bir sırayla döndürün.**

**Sonuç formatı aşağıdaki örneğe benzer olacaktır.**

`ÖRNEK`

```sql
**Input:**
Signups table:
+---------+---------------------+
| user_id | time_stamp          |
+---------+---------------------+
| 3       | 2020-03-21 10:16:13 |
| 7       | 2020-01-04 13:57:59 |
| 2       | 2020-07-29 23:09:44 |
| 6       | 2020-12-09 10:39:37 |
+---------+---------------------+
Confirmations table:
+---------+---------------------+-----------+
| user_id | time_stamp          | action    |
+---------+---------------------+-----------+
| 3       | 2021-01-06 03:30:46 | timeout   |
| 3       | 2021-07-14 14:00:00 | timeout   |
| 7       | 2021-06-12 11:57:29 | confirmed |
| 7       | 2021-06-13 12:58:28 | confirmed |
| 7       | 2021-06-14 13:59:27 | confirmed |
| 2       | 2021-01-22 00:00:00 | confirmed |
| 2       | 2021-02-28 23:59:59 | timeout   |
+---------+---------------------+-----------+
**Output:**
+---------+-------------------+
| user_id | confirmation_rate |
+---------+-------------------+
| 6       | 0.00              |
| 3       | 0.00              |
| 7       | 1.00              |
| 2       | 0.50              |
+---------+-------------------+
```

**Kullanıcı 6, herhangi bir onay mesajı talep etmedi. Onay oranı 0'dır.**
**Kullanıcı 3, 2 talep yaptı ve her ikisi de zaman aşımına uğradı. Onay oranı 0'dır.**
**Kullanıcı 7, 3 talep yaptı ve tamamı onaylandı. Onay oranı 1'dir.**
**Kullanıcı 2, 2 talep yaptı; bir tanesi onaylandı, diğeri ise zaman aşımına uğradı. Onay oranı 1 / 2 = 0.5'dir.**

`ÇÖZÜM`

```sql
SELECT s.user_id,
       ROUND(SUM(CASE WHEN c.action = 'confirmed' THEN 1 ELSE 0 END) * 1.0 / COUNT(*), 2) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c ON s.user_id = c.user_id
GROUP BY s.user_id;
```

Bu SQL sorgusunun kısa açıklaması:

1.  **`SELECT s.user_id,`**: Kullanıcı kimliklerini seçer.
2.  **`ROUND(SUM(CASE WHEN c.action = 'confirmed' THEN 1 ELSE 0 END) * 1.0 / COUNT(*), 2) AS confirmation_rate`**:
    - Kullanıcının onaylanan mesajlarının sayısını toplar, toplam mesaj sayısına böler ve sonucu 2 ondalıklı basamağa yuvarlar.
    - Bu değeri **`confirmation_rate`** olarak adlandırır.
3.  **`FROM Signups s`**: `Signups` tablosu seçilir.
4.  **`LEFT JOIN Confirmations c ON s.user_id = c.user_id`**: `Signups` ve `Confirmations` tabloları `user_id` ile birleştirilir.
5.  **`GROUP BY s.user_id`**: Kullanıcı bazında gruplama yapılır.
    &nbsp;

<**_[Alper BİLGİN](https://github.com/DREAXS)_**>
