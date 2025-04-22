# stability-tms

## Данные и дашборды

Данные есть в соломоне в

- [Кластере push](https://solomon.yandex-team.ru/?project=market-mbo&cluster=push&service=mbo-stability)
- Или [кластере autoPush](https://solomon.yandex-team.ru/?project=market-mbo&cluster=autoPush&service=mbo-stability)

Какой из них актуален - непонтяно.

Графики можно посмотреть на [дашборде grafana](https://grafana.yandex-team.ru/d/TvA2gKtGk/mbo-stability)


## Документация

Актуальной документации нет.
Неактуальная документация тут: https://wiki.yandex-team.ru/market/mbo/kontur-infra/metriki-dostupnosti/metriki-dostupnosti-howto/

## Локальный старт проекта:

0. Для генерации idea-проекта наберите следующую команду:
    ```sh
    ${ARCADIA_ROOT}/junk/sulim/tools/ya-ide-idea-generator/ya_ide_idea_generator.py
    ```
    Этот скрипт сгенерирует проект для вот этой [структуры папок](https://wiki.yandex-team.ru/users/sulim/howto/arc-directory-structure/).
0. Притащите `properties.d/production/20_stability-tms-vault.properties` с прода в файлик `src/main/properties.d/90-overrides.local.properties`
0. Откройте `StabilityTms` класс и `Ctrl+Shift+F10` его
0. Упадёт. Поменяйте Working directory на папку с проектом в Аркадии.

## Конфиг

Файл конфигурации графиков [MboGraphV7.kt](src/main/java/ru/yandex/market/mbo/stability/tms/task/graph/graphs/MboGraphV7.kt)
