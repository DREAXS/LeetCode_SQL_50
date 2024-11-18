# LEETCODE SQL 50

## [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/)

Table: `Employees`

```sql
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| name          | varchar |
+---------------+---------+
```

- id, bu tablodaki birincil anahtar (benzersiz değerlere sahip sütun) olup, her satırda bir çalışanla ilgili **id** ve **isim** bilgileri bulunmaktadır

Table: `EmployeeUNI`

```sql
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| unique_id     | int     |
+---------------+---------+
```

- (id, unique_id) bu tablonun birincil anahtarıdır.
- Her satır, bir çalışanın **id** ve ona karşılık gelen **unique_id** bilgisini içermektedir.

### Her kullanıcı için benzersiz kimliğini (unique ID) gösteren bir çözüm yazın. Eğer bir kullanıcının benzersiz kimliği yoksa, bunun yerine **null** gösterilsin.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Employees table:
+----+----------+
| id | name     |
+----+----------+
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |
+----+----------+
EmployeeUNI table:
+----+-----------+
| id | unique_id |
+----+-----------+
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |
+----+-----------+
**Output:**
+-----------+----------+
| unique_id | name     |
+-----------+----------+
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |
+-----------+----------+
Alice ve Bob'un benzersiz kimliği (unique ID) yok, bu yüzden **null** gösterilecektir.
Meir'in benzersiz kimliği 2'dir.
Winston'ın benzersiz kimliği 3'tür.
Jonathan'ın benzersiz kimliği 1'dir.
```

## Çözüm:

```sql
SELECT EmployeeUNI.unique_id, Employees.name
FROM Employees
LEFT JOIN EmployeeUNI
ON Employees.id = EmployeeUNI.id
```

## **Açıklaması:**

### 1. **SELECT EmployeeUNI.unique_id, Employees.name**

- **EmployeeUNI.unique_id**: `EmployeeUNI` tablosundaki **unique_id** sütununu seçer.
- **Employees.name**: `Employees` tablosundaki **name** (isim) sütununu seçer.

### 2. **FROM Employees**

- Verilerin **Employees** tablosundan alınacağını belirtir.

### 3. **LEFT JOIN EmployeeUNI**

- **LEFT JOIN**: `Employees` tablosundaki tüm verileri alır ve **EmployeeUNI** tablosundaki eşleşen verileri ekler.
- Eğer **EmployeeUNI** tablosunda eşleşen veri yoksa, **NULL** değeri döner.

### 4. **ON Employees.id = EmployeeUNI.id**

- **Employees.id** ile **EmployeeUNI.id** değerleri eşleşen satırları birleştirir.
