Коллекция утилит для скачивания и парсинга серпов
====

Утилита для скачивания серпов через scraper
---

### Запуск группового скачивания
```bash
./download_serp.py -v -b queries.txt -n "test api" -c "some comment" -u "augolubtsov" -m raw -r tr
```
можно с помощью параметров -e и -r можно выбирать поисковую систему и регион, -m задаёт режим скачивания:

- raw - сырой html
- html - распарсенный html
- jpg - скриншот и сырой html

### Проверка результата скачивания
```bash
./download_serp.py -i 1429547576654 -s
```

### Скачивание результата
```bash
./download_serp.py -i 1429546143905 -d jpg.dump -j
```

Утилита для нарезки результата скачивания на файлы и парсинга результатов
---

### Нарезка результатов скачивания
```bash
./parse_serp.py -d img-jpg.dump -s htmls/
ls htmls
машины_3.html                       мультики_983.json
машины_3.jpg                        картинки_для_срисовки_3.html
машины_983.json                     картинки_для_срисовки_3.jpg
мадонна_3.html                      картинки_для_срисовки_983.json
рисунки_3.html                      чернобыль_3.html
мадонна_3.jpg                       чернобыль_3.jpg
```

При нарезке в выходном каталоге сладываются файлы у которых в качестве имени запрос, утилита сама вытаскивает из дампа всё, что возможно: html, parsed-data, jpg

### Дамп позиций колдунщиков
```bash
./parse_serp.py -d html_g.dump -w -
augolubtsov-os2:serp augolubtsov$ ./parse_serp.py -d html_g.dump -w -
чернобыль   3   RIGHT   WIZARD_MAPS 1   UNK
чернобыль   3   LEFT    WIZARD_IMAGE    3   STD 4
чернобыль   3   LEFT    WIZARD_NEWS 6   UNK
новогодние картинки 3   LEFT    WIZARD_IMAGE    1   BIG 9
картинки для срисовки   3   LEFT    WIZARD_IMAGE    1   BIG 15
животные    3   RIGHT   WIZARD_IMAGE    1   STD 3
животные    3   LEFT    WIZARD_NEWS 6   UNK
животные    3   LEFT    WIZARD_UNKNOWN_SERVICE  11  UNK
интерстеллар    3   RIGHT   WIZARD_IMAGE    1   STD 3
интерстеллар    3   RIGHT   WIZARD_KG_OBJECTS   2   UNK
интерстеллар    3   RIGHT   WIZARD_KG_OBJECTS   3   UNK
интерстеллар    3   LEFT    WIZARD_AFISHA   1   UNK
интерстеллар    3   LEFT    WIZARD_NEWS 7   UNK
интерстеллар    3   LEFT    WIZARD_UNKNOWN_SERVICE  12  UNK
рисунки 3   LEFT    WIZARD_IMAGE    1   STD 7
рисунки 3   LEFT    WIZARD_NEWS 6   UNK
машины  3   RIGHT   WIZARD_MAPS 1   UNK
машины  3   LEFT    WIZARD_IMAGE    1   STD 4
машины  3   LEFT    WIZARD_ADRESA   4   UNK
мультики    3   LEFT    WIZARD_IMAGE    4   STD 5
мадонна 3   RIGHT   WIZARD_IMAGE    1   STD 3
мадонна 3   RIGHT   WIZARD_KG_OBJECTS   2   UNK
мадонна 3   LEFT    WIZARD_UNKNOWN_SERVICE  11  UNK
```
Формат вывода такой `запрос<tab>регион<tab>колонка серпа<tab>тип колдунщика<tab>позиция<tab>дизайн` дизайн работает только для WIZARD_IMAGE: STD-однорядный колдунщик, BIG - 2-3х рядный, чиселка на конце это сколько картинок попало в колдунщик.

Опция -w задаёт выходной файл **-** это вывод на stdout

### HTML отчёт о распределении колдунщиков

```
python serp wizards_report -h
usage: serp [-h] -d filename [-p pools list] [-s systems list]
            [-w wizards list] [-e sides list] [-i]

Parser SERP

optional arguments:
  -h, --help            show this help message and exit
  -d filename, --file_with_dump filename
                        name of file with scraper results
  -p pools list, --pools pools list
                        commaseparated list of pools for report (default: all)
  -s systems list, --systems systems list
                        commaseparated list of systems for report (default:
                        all)
  -w wizards list, --wizards wizards list
                        commaseparated list of wizards for report (default:
                        all)
  -e sides list, --sides sides list
                        commaseparated list of sides for report (default: all)
  -i, --info            dump names of pools, systems, wizards, sides
```

#### Получение списка колдунщиков и пулов

```
python serp wizards_report -d wizards3.json -w WIZARD_IMAGE -i
Pools: ya.img.2000, ya.web.2000, g.touch.2000, ya.touch.2000, g.web.1210, ya.porno_tr.4574, ya.porno_ru.7056
Systems: y, b, g
Wizards: WIZARD_IMAGE
Sides: RIGHT, LEFT
```

#### Генерация отчёта

```python serp wizards_report -d wizards3.json -w WIZARD_IMAGE > report.html```

