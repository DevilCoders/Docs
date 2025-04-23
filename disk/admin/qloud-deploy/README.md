# qloud-deploy

## Что это такое

Это небольшой инструментарий для деплоя приложений Диска в Qloud или Deploy

## Установка

- ubuntu: `apt-get install qloud-deploy`
- arcadia: `PATH="$ARCADIA_PATH/disk/admin/qloud-deploy:$PATH"; ya make`

## Запуск

Обновить docker образ и sandbox ресурс в Qloud
```bash
qloud-deploy qloud deploy --image latest --application 12345 disk.disk-mworker.testing
```

Обновить docker образ и sandbox ресурс в Deploy
```bash
qloud-deploy deploy update --image latest --sandbox application:12345 telemost_backend_testing
```

Вместо id ресурса можно указывать строку package=version - для поиска приложения по аттрибутам.
