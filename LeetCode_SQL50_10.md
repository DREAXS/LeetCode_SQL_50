# LEETCODE SQL 50

## [1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/)

Table: `Activity`

```sql
+----------------+---------+
| Column Name    | Type    |
+----------------+---------+
| machine_id     | int     |
| process_id     | int     |
| activity_type  | enum    |
| timestamp      | float   |
+----------------+---------+
```

- **(machine_id, process_id, activity_type)** bu tablonun birincil anahtarıdır.
- **'start'** bir makinenin, belirtilen zaman damgasında süreci başlattığını,
  **'end'** ise sürecin o zaman damgasında sona erdiğini belirtir.

- Her **(machine_id, process_id)** çifti için **'start'** zaman damgası, **'end'** zaman damgasından önce olacaktır.
- Her **(machine_id, process_id)** çifti için bir **'start'** ve bir **'end'** zaman damgası bulunduğu garanti edilmiştir.

### Bir süreci tamamlamak için geçen zaman, 'end' zaman damgası ile 'start' zaman damgası arasındaki farktır.

### Ortalama zaman, her bir sürecin tamamlanması için geçen toplam zamanı, o makinedeki çalıştırılan süreç sayısına bölerek hesaplanır.

### Sonuç tablosunda machine_id ve processing_time (işlem süresi) yer almalı, processing_time 3 ondalıklı basamağa yuvarlanmalıdır.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Activity table:
+------------+------------+---------------+-----------+
| machine_id | process_id | activity_type | timestamp |
+------------+------------+---------------+-----------+
| 0          | 0          | start         | 0.712     |
| 0          | 0          | end           | 1.520     |
| 0          | 1          | start         | 3.140     |
| 0          | 1          | end           | 4.120     |
| 1          | 0          | start         | 0.550     |
| 1          | 0          | end           | 1.550     |
| 1          | 1          | start         | 0.430     |
| 1          | 1          | end           | 1.420     |
| 2          | 0          | start         | 4.100     |
| 2          | 0          | end           | 4.512     |
| 2          | 1          | start         | 2.500     |
| 2          | 1          | end           | 5.000     |
+------------+------------+---------------+-----------+
**Output:**
+------------+-----------------+
| machine_id | processing_time |
+------------+-----------------+
| 0          | 0.894           |
| 1          | 0.995           |
| 2          | 1.456           |
+------------+-----------------+

3 makine, her biri 2 süreç için  çalıştırılıyor.
Makine 0  ın ortalama süresi, ((1.520 - 0.712) + (4.120 - 3.140)) / 2 = 0.894
Makine 1  in ortalama süresi, ((1.550 - 0.550) + (1.420 - 0.430)) / 2 = 0.995
Makine 2 nin ortalama süresi, ((4.512 - 4.100) + (5.000 - 2.500)) / 2 = 1.456
```

## Çözüm:

```sql
SELECT act1.machine_id,
ROUND(AVG(act2.timestamp-act1.timestamp), 3) AS processing_time
FROM Activity AS act1
JOIN Activity AS act2
ON act1.machine_id = act2.machine_id
AND act1.process_id = act2.process_id
AND act1.activity_type = 'start'
AND act2.activity_type = 'end'
GROUP BY act1.machine_id
```

## **Açıklaması:**

### 1. **SELECT act1.machine_id, ROUND(AVG(act2.timestamp - act1.timestamp), 3) AS processing_time**

- **act1.machine_id**: `Activity` tablosundaki **machine_id** sütununu seçer. Bu sütun, her makinenin benzersiz kimliğini temsil eder.
- **ROUND(AVG(act2.timestamp - act1.timestamp), 3) AS processing_time**:
  - **act2.timestamp - act1.timestamp**: İki kayıt arasındaki **timestamp** farkını hesaplar. **act1** kaydı, işlem başlangıcını (`activity_type = 'start'`), **act2** kaydı ise işlem bitişini (`activity_type = 'end'`) temsil eder. Bu fark, işlem süresini yani **işlem süresi**ni verir.
  - **AVG(...)**: Bu farkların ortalamasını alır. Yani, her makine için başlangıç ve bitiş arasındaki ortalama işlem süresini hesaplar.
  - **ROUND(..., 3)**: Ortalamayı 3 basamağa yuvarlar. Bu, işlem süresinin daha okunabilir ve hassas bir şekilde sunulmasını sağlar.
  - **AS processing_time**: Bu hesaplanan değere **processing_time** adını verir. Sonuç olarak, her makine için ortalama işlem süresi **processing_time** olarak dönecektir.

### 2. **FROM Activity AS act1**

- **FROM** komutu, verilerin **Activity** tablosundan alınacağını belirtir.
- **AS act1**: **Activity** tablosuna **act1** takma adı verir. Bu, tablonun daha kısa ve anlaşılır bir şekilde kullanılmasını sağlar.

### 3. **JOIN Activity AS act2**

- **JOIN** komutu, iki tabloyu birleştirmek için kullanılır. Burada aynı **Activity** tablosu iki kez kullanıldığı için, **act2** takma adıyla ikinci bir referans ekleniyor.
- **AS act2**: **Activity** tablosuna **act2** takma adı verir. Bu, **act2** tablosunun birinci tablodan (act1) farklı bir veri kümesi olarak kullanılmasını sağlar.

### 4. **ON act1.machine_id = act2.machine_id**

- **ON** koşulu, hangi şartlarla iki tabloyu birleştireceğimizi belirtir.
- **act1.machine_id = act2.machine_id**: Bu koşul, **act1** ve **act2** tablosundaki aynı **machine_id** değerine sahip satırları birleştirir. Yani, her iki kaydın aynı makineye ait olması gerekir.

### 5. **AND act1.process_id = act2.process_id**

- **AND act1.process_id = act2.process_id**: Bu koşul, hem **act1** hem de **act2** için aynı **process_id** değerine sahip satırların birleştirilmesini sağlar. Yani, her iki kayıt aynı işlemi (process) temsil etmelidir.

### 6. **AND act1.activity_type = 'start'**

- **AND act1.activity_type = 'start'**: **act1** tablosundaki satırların sadece **activity_type** değeri **'start'** olanları dikkate alınır. Yani, **act1** tablosundaki her satır, işlemin başlangıcı olmalıdır.

### 7. **AND act2.activity_type = 'end'**

- **AND act2.activity_type = 'end'**: **act2** tablosundaki satırların sadece **activity_type** değeri **'end'** olanları dikkate alınır. Yani, **act2** tablosundaki her satır, işlemin bitişi olmalıdır.

### 8. **GROUP BY act1.machine_id**

- **GROUP BY** komutu, sonuçları belirli bir sütuna göre gruplar. Burada, gruplama **act1.machine_id** sütununa göre yapılır.
- Bu, her makine için işlem süresi hesaplamasını sağlar ve her makine için bir satır döndürür.
