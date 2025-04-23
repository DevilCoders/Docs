# Про локальную разработку

## Раньше трава была зеленее
В проектах на первом хорадрике была локальная прокся на Flask'е и дергать http-ручки можно было тривиально.

В horadric2 нет локальной прокси, вместо нее в проде используется [Zephyr](https://z.yandex-team.ru).
Поднять Zephyr локально - задача нетривиальная. Поэтому чтобы подергать http-ручки в проекте на horadric2 Zephyr поднимать не надо.

## Как ходить в gRPC-ручки по HTTP в условиях локальной разработки
1. Добавляем в [inifuss.scroll](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/scroll.md) камушек [chronicler](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/cairn_stones/chronicler):
```yaml
# inifuss.scroll
...

cairnStones:
    ...
    - name: chronicler
```

2. Перезапускаем `horadric` внутри проекта. В результате видим новую директорию `serval_configs`.

3. Выкачиваем и собираем `search/serval`:
```bash
cd $ARCADIA_ROOT
ya make --checkout balancer/serval
```

4. Запускаем `serval`:
```bash
$ARCADIA_ROOT/balancer/serval/serval -c <project>/serval_configs/serval_config.yaml
```

5. Радуемся!
```
curl -X POST 'http://localhost:8888/api/zephyr.Storage/listInstances'
{"objects":[...]}
```

## Но есть нюанс...
Chronicler считает, что проект поднимается на порту `50051`. Если это почему-то не подходит конкретному проекту - пишем roboslone@.