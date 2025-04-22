## shopsdat_to_json

Этот небольшой скрипт для awk конвертирует shops.dat в json формат.

Формат вывода таков, что его можно обрабатывать как json процессором, как и просто grep'ом:
```
[
{объект про первый фид}
,
{объект про второй фид}
,
...
]
```

Вывод в таком формате можно зачитать целиком и получить список объектов, либо отгрепать что надо и парсить как однострочные json'ы.


Найти все фиды, где хоть как-то упоминания lamoda:
```
cat shops-utf8.dat | ./shopsdat_to_json.awk | grep lamoda | jq .
```

Найти все фиды, у которых в datasource_name находится "lamoda"
```
cat shops-utf8.dat | ./shopsdat_to_json.awk | jq '[.[] | select(.datasource_name | contains("lamoda"))]'
```
