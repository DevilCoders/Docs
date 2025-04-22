# Пример использования
```
smarttv/scripts/smotreshka_account/save_to_redis/smotreshka_save_registered_accounts_to_redis \
--input-table='<путь до YT таблицы>' \
--redis-auth-key='<Ключ для подключения к редису>' \
--environment='<testing | production | prestable>' \
--yt-proxy='<кластер>' \
--yt-token='<YT token>' \
--mr-account=smarttv \
--robot-name='<имя робота>'
```

### input-table
Таблица с 3мя колонками:
- `quasar_device_id` - исходный квазарный id устройства, которое регистрировали в смотрешке
- `smotreshka_device_id` - `md5` от `quasar_device_id`
- `smotreshka_account_id` - id созданного в смотрешке аккаунта

Пример: `'//tmp/alex-garmash/quasar_deivce_ids'`

Является выхлопом скрипта для регистрации аккаунтов


### redis-auth
Ключ для подключения к редису:<br/>
testing: https://yav.yandex-team.ru/secret/sec-01eb5zqy319ps4dhnmgajqz21w/explore/versions <br/>
production: https://yav.yandex-team.ru/secret/sec-01dwcajef7802chad8b8bndjgm/explore/versions

### environment
Окружение редиса
- `production`
- `testing`

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
