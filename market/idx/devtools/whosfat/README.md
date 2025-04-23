# whosfat

Часто колонка таблицы в YT хранит в себе большой блоб - сериализованный протобуф. Эта тула подсчитывает, какие поля занимают сколько байт в этом блобе.

## Использование

```
./whosfat \
    --yt-proxy arnold \
    --yt-token-path ~/.yt/token \
    --yt-input-table=//home/market/production/indexer/gibson/mi3/main/last_complete/genlog/{0000..0015} \
    --column value \
    --message genlog \
    --no-squash-unknowns
```

https://paste.yandex-team.ru/676942

## Параметры командной строки

- `--yt-proxy`
- `--yt-token-path`
- `--yt-pool`
- `--yt-input-table` - можно передавать несколько
- `--column` - имя интересующей колонки
- `--message` - тип сообщения, можно указать `none`, что полезно в сочетании с `--no-squash-unknowns`
- `--sort-by` - `size` (по убыванию) или `name` (по возрастанию)
- `--no-squash-unknowns` - учитывать каждое неизвестное поле по-отдельности
- `--no-human-readable` - писать число байт в выхлопе просто как число (по умолчанию используются человеко-читаемый вывод: KiB, MiB, GiB и т. д.)

## Расширение

Достаточно добавить поддержку интересующего вас протобуфа в `enum EMessage` в `proto/options.pb` и в функцию, резолвящую дескриптор, в `main.cpp`.
