# Утилита для удаления офферов по результатам yql-запроса

Утилита находится в [market/idx/datacamp/dev/delete_offers](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/delete_offers).

**Внимание!** Не рекомендуется использовать для маркетных офферов, т.к. их удаление необходимо транслировать подписчикам.

```
export YT_TOKEN_PATH=/etc/datasources/yt-market-indexer
export YT_META_PROXY=markov
export YT_PROXY=hahn
export DATACAMP_ENV=testing
./delete_offers //tmp/yql/mlevkov/aa38a952-14f114b7-1f6f79a7-fc41f53f
```
[Пример yql запроса для получения таблицы](https://yql.yandex-team.ru/Operations/YcNDedJwbFW0JFyiq4XH2uM496j46T0euesdVj4uN0U=)
