## phone_joiner
Утилита для джоина уидов по хешу телефона для типовых задач едадила.

### Пример использования
Утилита добавляет уиды через запятую во входной csv

```
$ head ~/20191115-phones-clean.tsv | ~/phone-joiner --delimiter '       ' --key 1 PASSPADMIN-2663-sh1.csv
2019-12-05 12:50:45,213 - INFO - Reading passport dataset ...
2019-12-05 12:50:45,213 - INFO - Reading file PASSPADMIN-2663-sh1.csv ...


2019-12-05 12:59:09,624 - INFO - Finished reading file PASSPADMIN-2663-sh1.csv ...
2019-12-05 12:59:09,629 - INFO - Finished reading passport datasets, 62540257 keys, 83016555 values read
Карта   Хеш (без +)
card1        phone_hash1        uid1,uid2,uid3
card2        phone_hash2        uid4
card3        phone_hash3
card4        phone_hash4        uid5,uid6
card5        phone_hash5
card6        phone_hash6        uid7
card7        phone_hash7
card8        phone_hash8        uid8
card9        phone_hash9        uid9,uid10,uid11,uid12
```
