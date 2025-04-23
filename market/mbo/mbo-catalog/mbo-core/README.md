## mbo-core
Основная библиотека mbo, в ней хранятся общие сервисы, которые используют различные модули.
По-хорошему очень большой и крупный модуль, его бы подразбить на кучу мелких и уменьшить лапшу, чтобы было проще ориентироваться в проекте.

## Локальный запуск интеграционных тестов
Для запуска интеграционных тестов используется команда:
```bash
ya make -ttt
```

## Релиз в артифактори
~~В нормальной ситуации релиз библиотеки происходит вместе с релизами в релизной машине [mbo-cd](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-cd). [Вот](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-cd/release/613b9604b3a3b77d3c5a4e4a?selectedJob=publish&launchNumber=1) пример запуска кубика, который сделал релиз библиотеки в артифактори.~~

~~Но в случае, если по каким-то причинам библиотеку надо опубликовать срочно, не дожидаясь очередного релиза в [mbo-cd](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-cd), её можно собрать и зарелизить локально с помощью команд вида:~~
```
export LATEST_VERSION=$(date +"%Y%m%d-%H%M%S")
./gradlew -Pversion=5.0-${LATEST_VERSION}.master  -Prelease.useAutomaticVersion=true --no-daemon --console plain --info --refresh-dependencies --rerun-tasks --recompile-scripts -s -b build.gradle clean :mbo-core:release
```

~~Релиз нужно выполять из мастера при отсутствии локальных изменений.~~

## Импорт в Аркадию
~~Для того чтобы иметь возможность использовать обновлённую опубликованную библиотеку в проектах в Аркадии, нужно выполнить команду для импорта библиотеки из артифактори в Аркадию:~~
```
ya maven-import ru.yandex.market:mbo-core:5.0-${LATEST_VERSION}.master
```
~~(здесь предполагается, что определена переменная `LATEST_VERSION` - см. описание релиза в артифактори выше)~~

~~После этого создать pr с изменениями в `contrib/java/ru/yandex/market/mbo-core` и вмерджить его в транк.~~

~~Подробнее о `maven-import` см. в [документации](https://docs.yandex-team.ru/ya-make/manual/java/commands#ya-maven-import).~~
