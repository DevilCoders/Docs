# mbo-lite

Сервис с которым взаимодействует x-script фронт.
XScript часть отпиливается и переписывается на реакт.
В целом сервис используется для получения различной информации из сервиса, типа запроса глобального лога категорий и другой информации.

## запуск на aida
Для запуска используйте скрипт scripts/dev/run-mbo-lite.py

## Локальный запуск интеграционных тестов
Для запуска интеграционных тестов используется команда:
```bash
ya make -ttt
```
Для запуска тестов необходима предварительная настройка etcd, описание лежит в корневом [README.md](../README.md#локальный-запуск-автотестов-через-ya-make)

## Devops

### Дашборды

#### Прод
- [NGINX](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-lite-production)

#### Тестинг
- [NGINX](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-lite-testing)


## Разработка

### Локальный запуск из IDEA

Если ты смелый, ловкий, умелый, то можно запустить локально. 

Профит: 
- не надо заливать вёрстку, 
- проще дебажить (не надо никуда подключаться), 
- проще запуск - просто в идее запуск и все логи, всё тут
- по ?_xml=1 можно получить xml-выдачу до xsl стилизации

Минусы:
- рендерится через Java - в проде - через C++, могут быть минорные разницы, лучше перепроверить в большом варианте
- похоже, что не работает `disable-output-escaping="yes"`

Что нужно делать:
1. Создай файл `src/main/properties.d/local/99.oeverrides.local.properties` с содержимым `mbo-lite.local-user-uid=111111`, где `111111` - твой uid (можно посмотреть [тут](https://mbo.market.yandex.ru/admin/users.xml))
2. Создаё конфигурацию запуска в IDEA:
  - Main class: `MboLiteMain`
  - VM options: `-Dconfigs.path=mbo-lite/src/main/properties.d -Dlog4j.configurationFile=mbo-lite/src/main/conf/log4j2-local.xml -Djava.net.preferIPv6Stack=true -Djava.net.preferIPv6Addresses=true -Xverify:none -Denvironment=local -Doracle.net.tns_admin=/etc/oracle -Dspring.profiles.active=no-auth -Djava.awt.headless=true`
3. Если ещё нет - скопируй с дева `tnsnames.ora`: `scp aida.market.yandex.net:/etc/oracle/tnsnames.ora /etc/oracle`
