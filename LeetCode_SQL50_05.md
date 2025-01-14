# LEETCODE SQL 50

## [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/)

Table: `Tweets`

```sql
+----------------+---------+
| Column Name    | Type    |
+----------------+---------+
| tweet_id       | int     |
| content        | varchar |
+----------------+---------+
```

- tweet_id, bu tablodaki birincil anahtar (benzersiz değerlere sahip sütun) olup, tablodaki tüm tweet'leri içermektedir.
- Bu tablo, bir sosyal medya uygulamasındaki tüm tweet'leri içermektedir.

### Geçersiz tweet'lerin ID'lerini bulmak için bir çözüm yazın. Bir tweet, içerik kısmındaki karakter sayısı **15'ten** büyükse geçersiz kabul edilir.

### Sonuç tablosunu herhangi bir sırayla döndürebilirsiniz.

### Sonuç formatı aşağıdaki örneğe göre olmalıdır.

### Örnek:

```sql
**Input:**
Tweets table:
+----------+-----------------------------------+
| tweet_id | content                           |
+----------+-----------------------------------+
| 1        | Let us Code                       |
| 2        | More than fifteen chars are here! |
+----------+-----------------------------------+
**Output:**
+----------+
| tweet_id |
+----------+
| 2        |
+----------+
Tweet 1' in uzunluğu = 11 => Bu geçerli  bir tweet'tir.
Tweet 2'nin uzunluğu = 33 => Bu geçersiz bir tweet'tir.
```

## Çözüm:

```sql
SELECT tweet_id
FROM Tweets
WHERE LEN(content)>15
```

### Açıklaması:

- **SELECT tweet_id**: `Tweets` tablosundaki **tweet_id** sütunundaki verileri seçer.
- **FROM Tweets**: Verilerin **Tweets** tablosundan alınacağını belirtir.
- **WHERE LEN(content) > 15**: **content** sütunundaki metnin uzunluğu 15 karakterden büyük olan satırları seçer.
  &nbsp;

<**_[Alper BİLGİN](https://github.com/DREAXS)_**>
