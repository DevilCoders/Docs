# delivery-partner-api-mock
Заглушка для эмулирования ответов FF СД и СЦ

Краткое описание компонента: https://wiki.yandex-team.ru/delivery/development/Zaglushka-dlja-SD-i-SC/

Как запускать:
1. Запустить dependency-stubs (см. dependency-stubs/README.md)
2. Сконфигурировать application-local.yml (см. application-local.yml.dist)
3. Создать локальный конфиг logback из шаблона [logback.xml.dist](src/main/conf/local/logback.xml.dist)  
4. Запуск: `./gradlew run -Denvironment=local`

Через VM аргументы можно дополнительно задать: `-Dlog.path=<path> -Dhttp.port=<port>`

Миграции накатываются во время запуска приложения