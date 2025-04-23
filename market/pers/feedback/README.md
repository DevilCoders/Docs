# pers-feedback

### Описание

Работа с отзывами на доставку

[Памятка дежурному](https://wiki.yandex-team.ru/market/development/pers/duty/)

[Памятка разработчику](https://wiki.yandex-team.ru/users/varvara/market/development/pers/)

[API (прод)](http://pers-feedback.vs.market.yandex.net/swagger-ui.html)

[API (тестинг)](http://pers-feedback.tst.vs.market.yandex.net/swagger-ui.html)

### Выкладка (RTC)

[Релиз из транка](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-feedback)

[Выкладка в тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-feedback-branch)

Проверку доработок желательно делать до вливания в транк - через выкатку из бранчи.
Нужно указывать путь пользовательской ветки в арке `users/user_name/branch_name` или `trunk` для выкатки из транка.

При выкатке релиза из транка нужно зайти в релизную машину, и из неё запустить релиз нужной ревизии.

### Nanny

[Nanny pers-feedback](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_feedback/)

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01e7sx0n3ehz01fpfsmsymqktg/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01e7q4gj7bfy386ht8vme6fxn6/explore/versions)

После изменения секрета можно накатить его через `persec feedback test/prod`

### Графики
[nginx метрики прода](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersfeedback;ctype=production;prj=market/)

[proto метрики прода](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpersfeedback;ctype=production;prj=market/?range=21660000)

[pers-feedback](https://grafana.yandex-team.ru/d/aNKHB5rGk/pers-feedback?orgId=1)

[статистика по отзывам](https://grafana.yandex-team.ru/d/Ir13VBrMk/pers-feedback-stats?orgId=1)

### Мониторинги
[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-feedback)

### Liquibase

Liquibase накатывается в пайплайне релиза.
Также есть отдельный пайплайн по накатыванию liquibase.
В любом случае, можно использовать скрипт `liquibase.sh`

Для использования скрипта нужно настроить переменные окружения (~/.bashrc)
```
export FEEDBACK_DB_PWD_TEST=<значение из секретницы>
export FEEDBACK_DB_PWD_PROD=<значение из секретницы>
```

Формат `./liquibase.sh <env> <command>`
- `<env>` - среда: dev, test, prod
- `<command>` - команда liquibase: updateSQL, update, ...

Пример: `./liquibase.sh dev update`


### Сборка и запуск

Сборка и прогон тестов `ya make -DUSE_PREBUILT_TOOLS --host-platform-flag=USE_PREBUILT_TOOLS -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)
В каждом из проектов есть локальные проперти `src/main/resources/properties.d/local/application-local.properties`.
Обычно они настроены достаточно для локального запуска сервиса, но могут быть исключения.

Где брать данные для запуска:
1. Токены и прочие секретные данные в [секретнице](https://yav.yandex-team.ru)

#### Локальный запуск через скрипт

Запуск приложения через скрипт `local-start.sh`
```
# простой запуск
./local-start.sh

# в режиме отладки
./local-start.sh --debug-port=6666
```

#### Локальный запуск напрямую
Локальный запуск - через класс `ru.yandex.market.pers.feedback.PersFeedbackApplication`

Переменные окружения, которые нужно ввести в конфигурации idea
```
ENVIRONMENT=local
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/feedback/src/main/conf/local/log4j2-test.xml
```

