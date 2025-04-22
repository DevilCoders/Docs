Миграции накатываются с помощью `pgmigrate_helper` [README](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/tools/pgmigrate_helper/README.md), это обертка над `pgmigrate`.
[Туториал](https://github.com/yandex/pgmigrate/blob/master/doc/tutorial.md) по `pgmigrate`.

## Создание новой миграции
1. Добавить файл с миграцией в папку `migrations`. Название файла должно соответствовать паттерну `V<version>__<description>.sql` для транзакционных миграций и `V<version>__NONTRANSACTIONAL_<description>.sql` для нетранзационных миграций
2. Прогнать тесты `ya make -ttt`
3. Увеличить версию БД в конфиге бинарника

## Проверить текущее состояние схемы БД
```
$ ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e $ENV info

```
где `$ENV` - окружение из `config.yaml`

## Накатить миграцию
```
$ ./pgmigrate_helper/pgmigrate_helper -c config.yaml -e $ENV  -t $VERSION migrate
```
где `$VERSION` - идентификатор нужной версии или `latest`.
