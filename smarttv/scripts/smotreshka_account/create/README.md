# Пример использования
```
smarttv/scripts/smotreshka_account/create/smotreshka_create_account \
--input-table='<путь до YT таблицы>' \
--output-table='<путь до YT таблицы>' \
--yt-proxy='<кластер>' \
--yt-token='<YT token>' \
--mr-account=smarttv \
--robot-name='<имя робота>' \
--tvm-client-id='<id TVM клиента>' \
--tvm-client-secret='<секрет>'
```

### input-table
Таблица с единственной колонкой - `quasar_device_id`<br/>
Пример: `'//tmp/alex-garmash/quasar_deivce_ids'`

### output-table
выходная таблица с 3мя колонками:
- `quasar_device_id` - исходный квазарный id устройства, которое регистрировали в смотрешке
- `smotreshka_device_id` - `md5` от `quasar_device_id`
- `smotreshka_account_id` - id созданного в смотрешке аккаунта

Пример: `'//tmp/alex-garmash/test'`

### yt-proxy
YT кластер(hahn, arnold, etc.)

### yt-token
Как получить YT токен: https://oauth.yt.yandex.net/
получать его нужно от имени робота

### mr-account
ну это совсем очевидно

Скорей всего мы всегда будем использовать `'smarttv'`

### robot-name
Например: https://staff.yandex-team.ru/robot-smart-tv

### tvm-client-id
один из: https://a.yandex-team.ru/arc/trunk/arcadia/smarttv/droideka/settings.py?rev=r8925401#L569-571

### tvm-client-secret
секрет для выбранного клиента
тестинг: https://yav.yandex-team.ru/secret/sec-01dz6j6bg14v8jda34h9mc4na4/explore/version/ver-01dz6j6bgyjb28atffzp892e1g
прод: https://yav.yandex-team.ru/secret/sec-01dz6j6v38esm8hz4fy8eb2q7k/explore/versions
