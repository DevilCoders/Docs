## **generate_normal_requests.py**

Генерирует заданное число реквестов для ручек **/find_template**, **/force_detemple** и **/route**.

### Ручки **/force_detemple** и **/route**

Имеют на данный момент одинаковый формат запроса:

```json
{
    "from":    "<email>",
    "html":    "<html>",
    "queueId": "<string>",
    "subject": "<string>",
    "uids":    ["<string>"]
}
```

Все парамерты, кроме `html`, генерируются либо случайно, либо захардкожены. Параметр `html` генерируется так:

1. Выбираем `n` случайных строк из таблички `sherlockdb_pg.template_bodies`
2. Из каждой строки получаем по одному реквесту: конкатенируем в случайном порядке токены, лежащие в колонке `chunks`

### Ручка **/find_template**

Ей требуется только параметр `stable_sign` в query-string.

1. Выбираем `n` случайных строк из таблички `sherlockdb_pg.template_bodies`
2. Из каждой строки получаем по одному реквесту: берем значение из колонки `stable_sign`

### Запуск:

Из директории `arcadia/mail/template_master/load_testing/scripts` запускается так:

```
$ ya make
$ ./generate_normal_requests --ammo-count <n> --case-tag <str> --out-path <file name> --req-type <type> --url <schema://host/path>
```

_Актуальная информация о параметрах доступна по `--help`._

Заливаем в сандбокс:

```
ya upload --sandbox --do-not-remove --owner=MAIL <file name>
```

_Подробнее про Sandbox-джобу см. README в корне проекта._

**Использует [секрет](https://yav.yandex-team.ru/secret/sec-01e14z2jy8nc4r92kgmrvvzycd/explore/versions)**
