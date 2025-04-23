#AppHost источник для запросов в API Bunker'a

## Полезные ссылки
- [Документация по AppHost](https://docs.yandex-team.ru/apphost/)
- [Документация по Bunker](https://wiki.yandex-team.ru/verstka/tools/bunker/)

## Quick Start
1. Добавить в свой граф новую вершину, в качестве бэкенда заиспользовать [BUNKER_API](https://a.yandex-team.ru/arc_vcs/apphost/conf/backends/BUNKER_API.json).
2. Сформировать запрос в `BUNKER_API` в виде айтема в AppHost контексте с типом `bunker_request`. Можно реализовать в виде `embed` источника с захардкоженными параметрами. [Пример](./graphs/testing.json).
3. В AppHost контексте в айтеме с типом `bunker_response` будут лежать все значения запрошенных ключей.


### Формат запроса в `BUNKER_API`

```
{
  nodes: Array<{path: string}>;
  type: 'bunker_request';
}
```

### Формат ответа от `BUNKER_API`

```
{
  nodes: Record<string, unknown>;
  type: 'bunker_response';
}
```
