## Использование

### Сборка
```
# removal is optional
rm -rf ./db-migrator.*
ya package --raw-package package.json
```

### Запуск
```
db-migrator.<revision>/db_migrator/bin/flyway.py -X -password=<database_password> <command>
```  
&lt;revision> - автоматически возьмется при сборке  
&lt;database_password> - взять в [секретнице](https://yav.yandex-team.ru/secret/sec-01e4dye05vk4qwg02ar5cc6mhy/explore/versions)  
&lt;command> - `info`, `validate` или `migrate`

Можно использовать и в таком виде (внимательно следим за тем, чтобы не было нескольких собранных пакетов):
```
./db-migrator.*/db_migrator/bin/flyway.py -X -password=`ya vault get version -n ver-01e4dye0638p6zc6k0w6we19t6 -o prod-db-password` info
```
