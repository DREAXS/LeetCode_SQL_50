**# LEETCODE SQL 50**

[[1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/)]

Table: `Students`

```sql
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| student_id    | int     |
| student_name  | varchar |
+---------------+---------+
```

Bu `Students` tablosunun açıklaması:

1.  **student_id (int)**: Öğrencinin benzersiz kimlik numarası (birincil anahtar).
2.  **student_name (varchar)**: Öğrencinin adı.

Tablo, her öğrencinin kimlik numarasını ve adını saklar. `student_id` her öğrenci için benzersizdir.

Table: `Subjects`

```sql
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| subject_name | varchar |
+--------------+---------+
```

Bu `Subjects` tablosunun açıklaması:

1.  **subject_name (varchar)**:
    - Bu sütun, okulda verilen dersin adını tutar.
    - `subject_name` sütunu, metin (string) veri tipindedir ve ders adı içerir.
    - **Birincil anahtar (primary key)** olarak tanımlanmıştır, yani her ders adı benzersiz olmalıdır. Aynı ders adı tabloya birden fazla kez eklenemez.

Table: `Examinations`

```sql
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| student_id   | int     |
| subject_name | varchar |
+--------------+---------+
```

Bu `Examinations` tablosunun açıklamasıı:

1.  **student_id (int)**: Öğrencinin kimlik numarası.
2.  **subject_name (varchar)**: Öğrencinin sınavına girdiği dersin adı.

Tablo, her öğrencinin her dersten sınav olduğunu gösterir. Birincil anahtar yoktur, bu yüzden tekrarlar olabilir.

---

**Her bir öğrencinin her bir sınava katılma sayısını bulan bir çözüm yazın.**

**Sonuç tablosunu student_id ve subject_name'e göre sıralayarak döndürün.**

**Sonuç formatı aşağıdaki örneğe benzer olacaktır.**

`ÖRNEK`

```sql
**Input:**
Students table:
+------------+--------------+
| student_id | student_name |
+------------+--------------+
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |
+------------+--------------+
Subjects table:
+--------------+
| subject_name |
+--------------+
| Math         |
| Physics      |
| Programming  |
+--------------+
Examinations table:
+------------+--------------+
| student_id | subject_name |
+------------+--------------+
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Programming  |
| 1          | Physics      |
| 1          | Math         |
| 13         | Math         |
| 13         | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |
+------------+--------------+
**Output:**
+------------+--------------+--------------+----------------+
| student_id | student_name | subject_name | attended_exams |
+------------+--------------+--------------+----------------+
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |
+------------+--------------+--------------+----------------+
```

`ÇÖZÜM`

```sql
SELECT s.student_id,
       s.student_name,
       sub.subject_name,
       COUNT(e.student_id) AS attended_exams
FROM Students AS s
INNER JOIN Subjects AS sub ON 1 = 1
LEFT JOIN Examinations AS e ON s.student_id = e.student_id AND sub.subject_name = e.subject_name
GROUP BY s.student_id, s.student_name, sub.subject_name
ORDER BY s.student_id, sub.subject_name;

```

Bu SQL sorgusunun açıklaması:

1.  **`SELECT s.student_id, s.student_name, sub.subject_name, COUNT(e.student_id) AS attended_exams`**:

    - Öğrencinin ID'si, adı, dersin adı ve katılım sayısı seçilir.

2.  **`FROM Students AS s`**:

    - `Students` tablosu alias olarak `s` ile seçilir.

3.  **`INNER JOIN Subjects AS sub ON 1 = 1`**:

    - `Subjects` tablosu, her öğrenci ile her dersi eşleştirir (tüm öğrencilere tüm dersler atanır).

4.  **`LEFT JOIN Examinations AS e ON s.student_id = e.student_id AND sub.subject_name = e.subject_name`**:

    - `Examinations` tablosu, öğrenci ve ders adı eşleşmesine göre birleştirilir ve katılım sayısı hesaplanır.

5.  **`GROUP BY s.student_id, s.student_name, sub.subject_name`**:

    - Öğrenciler ve dersler bazında gruplama yapılır.

6.  **`ORDER BY s.student_id, sub.subject_name`**:

    - Sonuçlar öğrenci ID'si ve ders adına göre sıralanır.

&nbsp;

<**_[Alper BİLGİN](https://github.com/DREAXS)_**>
