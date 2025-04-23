# Market Back Office
**Переехал в tier-0**.

## Генерация проекта в IDEA

Базовый скрипт, который должен сделать всё нормально: `scripts/create-idea-project-with-libs.sh`. Можно, при желании, дополнять по вкусу.

## Модули
// TODO переместить в README.md инструкции для модулей из https://wiki.yandex-team.ru/market/mbo/newbie/
_Фронт_
- React фронтенд MBO: [/mbo-react-ui](./mbo-react-ui/src/frontend/README.md)
- Устаревший сервис работающий для фронта на базе GWT: [/mbo-gwt](./mbo-gwt). Канет в лету, как только все gwt странички будут переписаны на React.
- XScript фронтенд MBO: [/verstka](./verstka). XScript в процессе переписывания на React или закапывания.
- UI-тесты: [/autotests](./autotests)

_Бэкенд - код_
- Основная библиотека mbo: [/mbo-core](./mbo-core). В ней хранятся общие сервисы, которые используют различные модули.
- Библиотека общих классов для различных сервисов mbo: [/mbo-common](./mbo-common)
- Библиотека с кучей экспортеров, которые позволяют дампить различные данные из mbo: [/mbo-dump](./mbo-dump)
- Liquibase скрипты: [/mbo-db](./mbo-db)
- Зависимости jooq для последующей генерации и использования в других модулях: [/mbo-jooq](./mbo-jooq)
- Хранилище контентных знаний, аналогично выгрузке, позволяет получать штучные данные, как в выгрузке, по http запросам: [/mbo-http-exporter](./mbo-http-exporter)
- Сервис, занимающийся отображением, сбором и обработкой журналируемых данных действий пользователей на mbo:  [/mbo-audit](./mbo-audit)
- Http сервис, хранящий в себе модели, позволяющий добавлять, удалять и изменять карточки на mbo, которые впоследствии появятся 
в выгрузке: [/mbo-card-api](./mbo-card-api)
- Сервис  для обработки запросов и получения информации об оферах из Yt: [/mbo-offers-api](./mbo-offers-api)
- Сервис с которым взаимодействует XScript фронт: [/mbo-lite](./mbo-lite) Сейчас XScript отпиливается и переписывается на React.
- Сервис на Quartz2, который крутит регулярные таски mbo по шедулеру:[/mbo-tms](./mbo-tms)

_Бэкенд - тесты_
- Юнит-тесты - во всех модулях. Настроены как `SMALL` и `MEDIUM` тесты в для `ya` и `CI`. 
- Интеграционные тесты - во многих модулях в `/src/integration-test`. Настроены как `LARGE` тесты в для `ya` и `CI`.
- Функциональные тесты - интеграционные тесты в `/src/integration-test`, которые запускаются на реальной БД: [/mbo-functional-tests-oaas](/mbo-functional-tests-oaas). 
Настроены как `LARGE` тесты в для `ya` и `CI`.

_Бэкенд - тулы и скрипты_
- Скрипты для запуска и остановки приложений на aida [/scripts/dev](./scripts/dev). Предпочтительно использовать `.py` скрипты вида `run-mbo-lite.py` и `stop-mbo-lite.py`, 
работающие через [dev_uploader](https://a.yandex-team.ru/arcadia/market/mbo/devops/tools/dev_uploader). `.sh` скрипты будут скоро закопаны.
- Java-программы для запуска на машинках в тестинге и проде [/mbo-tool](./mbo-tool). Подробную справку смотри в [отдельном README](./mbo-tool/README.md).
- Скрипты для чтения логов с дев машинок: [/scripts/logs](./scripts/logs)

## Сборка
Для локальной сборки и запуска тестов используйте `ya` вместо `gradle`. 
// TODO - gradle файлы и упоминания в README.md будут удалены в ближайшее время

## Локальный запуск интеграционных тестов через ya make
Настраиваем всякие etcd и прочее как описано в базовой [инструкции](https://wiki.yandex-team.ru/market/mbo/development/howto/lokalnyjj-zapusk-s-etcd-datasorsami/?from=%2Fusers%2Fs-ermakov%2FLokalnyjj-zapusk-s-etcd-datasorsami%2F#kakzapustit).
Добавляем к себе токен robot-mbo-dev [yql.token отсюда](https://yav.yandex-team.ru/secret/sec-01dwza7xnn691qkw39qjvr4dey/explore/versions)
```bash
export MBO_YQL_JDBC_TOKEN="<yql.token>"
```
Обычно запуск производится командой:
```bash
ya make -ttt
```
Если он производится какой-то кастомной командой, то внутри README.md модуля будет это описано.

## Правила ревью в ПР
Правила ревью в `CI` определяются в секциях `review:` внутри файлов a.yaml в корне проекта и в отдельных модулях:
- [/a.yaml](./a.yaml)
- [/mbo-gwt/a.yaml](./mbo-gwt/a.yaml)
- [/verstka/a.yaml](./verstka/a.yaml)
- [/mbo-react-ui/src/frontentd/a.yaml](./mbo-react-ui/src/frontentd/a.yaml)

Настроены следующие merge-правила на ревью ПР:
1. Работает автоназначение ревьюверов в блоке `rules:`. Учитывается модуль, где правится код и группа `ABC` автора. 
В `CI` выбирается только одно первое правило в блоке `rules:`, удовлетворяющее условиям снизу вверх. Правила выше не применяются.
2. Ревьюверы автоназначаются в порядке приоритета в блоке `roles:` (если используется) сверху вниз. 
При этом шипнуть ПР, удовлетворив merge-требование по ревью, может любой из `roles:`. 
Пример приоритетов:
    ```
    - mbo_catalog:developer
    - mbo_oracle_migration:developer
    - mbo:developer
    - mbo:@scope=services_management
    ```
3. В общем случае требуется по 1 ревьюверу от бекенда и фронта.
4. Для правок `/mbo-react-ui/src/frontentd ` требуется 1 assign и 1 ship. Приоритет при автоназначении для `mbo:frontend_developer`. 
5. Для правок `/mbo-gwt, /mbo-reat-ui, /verstka ` требуется  по 1 assign и 1 ship от фронта и бекенда. 
Приоритет при автоназначении для фронтов`mbo:frontend_developer`, для бекенда: либо `mbo_oracle_migration_:frontend_developer`, либо `mbo_catalog:developer` - в зависимости от автора правок.
6. Для остальных правок требуется  1 assign и 1 ship от бекенда. Приоритет при автоназначении для `mbo_oracle_migration_:frontend_developer` или `mbo_catalog:developer` в зависимости от автора правок.
7. Назначить других ревьюверов или увеличить их число можно вручную. При этом merge-правило по assign и ship должно выполняться.
8. Если после ручных правок ревьюверов недостаточно assign для выполнения merge-правила, то при публикации новой версии в ПР, ревьюверы будут автоназначены вновь.
9. Самошип - неразрешен. Чтобы вмерджить ПР самостоятельно, необходимо отключить `review` проверки целиком в merge-требованиях. Может применяться только в исключительных случаях


## Run troubleshooting

MacOS, попытка залить на aida скриптом ./gradlew clean && ./scripts/dev/run-mbo-react-ui.sh падает с ошибкой

```
Execution failed for task ':mbo-react-ui:uploadToDev'.
 > com.jcraft.jsch.JSchException: Auth cancel
```

выполняем
`ssh-add`
и убиваем все фоновые процессы _gradle_

```
gradle --status
pkill -f '.*GradleDaemon.*'
```

## FAQ

# Если приложение стартует и сразу отрубается без логов 
Если приложение на аиде/или где-то на инстансе не запускается, есть только лог GC, добавляем следующие флаги к запуску приложения:
```
  -XX:+PrintClassHistogram
  -XX:+TraceClassLoading
  -Xlog:::time,level,tags
```
Так вы будете получать вывод логов от jvm даже с exception, которые могут вылететь ещё до того, как сгенерируется логгер

