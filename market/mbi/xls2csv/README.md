Утилита для конвертации xls в csv формат.

Используется компонентами индексатора, т.к. feedparser не умеет обрабатывать xls фиды

## Релизная машина в TSUM
[Релизная машина](https://tsum.yandex-team.ru/pipe/projects/mbi/delivery-dashboard/mbi-xls2csv)

## Пакет в кондукторе
`https://c.yandex-team.ru/packages/yandex-market-xls2csv`

## Локальный запуск из IDEA
#### Клонирование Arcadia core (если еще не сделано)
Выкачает минимальный каркас Arcadia в директорию ./arcadia
```
svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone
echo "alias ya='$(pwd)/arcadia/ya'" >> ~/.bash_profile
```
#### Чекаут проекта
Выполняется из корня репозитория Arcadia

`ya make -j0 --checkout market/mbi/xls2csv`

#### Полезные команды
Выполняются из директории arcadia/market/mbi/xls2csv

`ya make --checkout -j0` - выкачать все зависимости

`ya make` - собрать проект

`ya make -t` - собрать проект и выполнить тесты

`ya package ./package.json` - создать tar.gz пакет

`ya package --debian --key=AABBCCDD ./package.json` - создать deb пакет (будет запакован в tar.gz)

#### Генерация проекта для IDEA
`ya ide idea -r IDEA_PROJECT_PATH` - создаст проект в директории IDEA_PROJECT_PATH 
(для работы в IDEA открывать именно эту директорию)
