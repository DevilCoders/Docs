## Компонент Fulfillment Wrap Marschroute (Прослойка между FFSM и FF Marschroute)


Как запускать:
1. Запустить fulfillment-dependency-stubs (см. readme)
2. Сконфигурировать application-local.properties (см. application-local.properties.dist)
3. Сконфигурировать wrap-secrets.properties (см. wrap-secrets.properties.dist)
4. Создать локальный конфиг logback из шаблона [logback.xml.dist](src/main/conf/local/logback.xml.dist)  
5. Запускать через runLocal/run таску в gradle со следующими VM аргументами:
-Dlog.dir=<log_dir> -Denvironment=local
