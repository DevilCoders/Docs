## Локальный запуск из IDEA
### Use classpath of module
`report-generator`

### Main class
`ru.yandex.common.util.application.XmlAppContextMain`

### Working directory
`$MODULE_WORKING_DIR$`

### VM-options
```
-Djava.library.path=<каталог проекта ya idea>/dlls
-Djna.library.path=<каталог проекта ya idea>/dlls
-Dspring.profiles.active=development,transparent_security_filter
-Dservant.home.dir=src/main/properties.d
-Dspring.context.initializers=ru.yandex.market.core.initializer.LocalStartContextInitializer
-Dsimple.host.name="$(/bin/hostname -f)"
-Dlog.dir=../logs/
-Dtmp.dir=tmp/
```

### Отладка
Требуется
1. Выполнить действия из `README.md` проекта mbi-partner,
2. Создать файл `reports-generator/src/main/properties.d/local/x-servant-local-secrets.properties`
3. Добавить значение переменной `market.mbi.business_migration.tvm.secret`, взяв нужное с тестового стенда (например, в няне по пути `/market/mbi/report-generator testing_market_report_generator_sas`) или из секрета https://yav.yandex-team.ru/secret/sec-01d7kp1kt0074hfqcnqps7v8xp/explore/versions.
4. Добавить значение переменной `mbi.robot.yt.token`, взяв свой токен

