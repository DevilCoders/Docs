# Как почистить временные папки после неудачного бекапа

Если бекап не завершился успешно, то в корне базы данных остается временная папка `~backup_XXX` которая занимает место и есть немного ресурсов.

Чтобы их почистить нет готовой утилиты, но можно воспользоваться следующими однострочниками:

```bash
# найти все таблицы внутри папки с названием ~backup_*
# и удалить их по одной, с предварительным подтверждением каждой команды
ya ydb -e ydb-ru.yandex.net:2135 -d /ru/verticals/production/general scheme ls -lR   | grep 'table' | grep -Eo '~backup_[^ ]*' | xargs -pL1 ya ydb -e ydb-ru.yandex.net:2135 -d /ru/verticals/production/general table drop
```

```bash
# найти все папки внутри папки ~backup_*
# и удалить их одна за другой с подтверждением
ya ydb -e ydb-ru.yandex.net:2135 -d /ru/verticals/production/general scheme ls -lR   | grep 'dir' | grep -Eo '~backup_[^ ]*' | tail -r | xargs -pL1 ya ydb -e ydb-ru.yandex.net:2135 -d /ru/verticals/production/general scheme rmdir
```
