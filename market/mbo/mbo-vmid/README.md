## Создание проекта для idea
```shell
ya ide idea --directory-based --group-modules=tree --no-local-executor --iml-in-project-root --with-content-root-modules --yt-store -lr ~/projects/idea-project/mbo-vmid market/mbo/mbo-vmid/
```

## Локальный запуск

Через скрипты:
```shell
ya make & ./bin/mbo-vmid-local-start.sh
```

Через идею:
1. Открываем `MboVmid` и запускаем проект
2. Заполнить данные для подключения к тестовой бд. Взять отсюда: https://st.yandex-team.ru/MBO-29713
3. В настройках конфигурации указать VM options: `-Dlog4j.configurationFile=${ARCADIA_ROOT}/market/mbo/mbo-vmid/src/main/conf/local/log4j2-test.xml -Dconfigs.path=${ARCADIA_ROOT}/market/mbo/mbo-vmid/src/main/properties.d -Denvironment=test
   -ea`

## Тесты

Запуск тестов:
в корне проекта выполнить одну из команд
```shell
ya make -t  # unit
ya make -tt # integration
```


## Изменения в БД

Добавить новый changeset в liquibase/migration, добавить новый файл в changelog при необходимости.
Данный скрипт автоматически добавиться к интеграционным тестам и при запуске раскатается на Embedded Postgre.

## Запуск интеграционных тестов из идеи

На данный момент (22.01.2021) плагин неудачно генерит проект для идеи, поэтому нужна пара манипуляций:
1. Удалить из File -> Project Structure -> Library библиотеку org/apache/logging/log4j/log4j-slf4j-impl
2. При запуске теста нужно ему передать параметры jvm (в Edit Configuration):
`-Dlog4j.configurationFile=${ARCADIA_ROOT}/market/mbo/mbo-vmi/home/marbok/arc/arcadiad/src/main/conf/local/log4j2-test.xml
   -Dconfigs.path=${ARCADIA_ROOT}/market/mbo/mbo-vmid/src/integration-test/properties.d
   -Denvironment=test
   -ea`


## Дополнительное описание

wiki: https://wiki.yandex-team.ru/users/marbok/servis-generacii-id-virtualnyx-modelejj/
