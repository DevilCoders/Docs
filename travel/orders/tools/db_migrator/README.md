## Использование

### Сборка
```
# optional
rm -rf ./db-migrator.*
ya package --raw-package package.json
```

### Запуск
`db-migrator.<revision>/db_migrator/bin/flyway.py -X -password=<database_password> <command>`
<revision> - автоматически возьмется при сборке
<database_password> - взять в [секретнице](https://yav.yandex-team.ru/secret/sec-01datq0myrd0zv6bfzfgvgbf8x/explore/version/ver-01datq0mz15fzbr8nc8w3ewnyh)
<command> - `info`, `validate`, `migrate`

Можно использовать и в таком виде (внимательно следим за тем, чтобы не было нескольких собранных пакетов):
```
./db-migrator.*/db_migrator/bin/flyway.py -X -password=`ya vault get version -n ver-01datq0mz15fzbr8nc8w3ewnyh -o value` info
```

Для тяжёлых обновлений таблиц заказов, услуг и счетов могут возникать timeoit-ы в миграционных скриптах. В этом случае мы пытаемся променить их многократно, но не увеличивая время на взятие блокировки:
```
until ./db-migrator.*/db_migrator/bin/flyway.py -X -password=`ya vault get version -n ver-01datq0mz15fzbr8nc8w3ewnyh -o value` migrate; do echo "trying again in 5 sec"; sleep 5; done
```
