# Факторы (Features)

Для хранения факторов используется KV-хранилище SaaS. Сервис называется `drive_features`. С недавних пор все ключи объединены в отдельные группы, называемые `Namespace` (или `sgkps`)

## Документы

### `Namespace=0` (`sgkps=0`)

#### Ключ `user_id:{USER_ID}:features`

Содержит общие пользовательские факторы.

### `Namespace=1` (`sgkps=1`)

#### Ключ `area_id:{AREA_ID}:hour_ts:{HOUR_TS}`

Содержит факторы для полигона `{AREA_ID}` для заданного времени `{HOUR_TS}` округленного до часов по формуле:

`{HOUR_TS} = {UNIX_TS} / 3600 * 3600` (используется целочисленное деление).

### `Namespace=2` (`sgkps=2`)

TODO.