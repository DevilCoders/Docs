# Workflow склейки графов 

Здесь храним конфиги для pipeline реакций. Довозятся до Реактора [Ламой](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama).
Пока что тут конфигурируются только артефакты, которые приезжают в проект [reactor:crypta/graph](https://reactor.yandex-team.ru/browse?selected=7841506).

```
# Собираем бинарник 
cd maps/analytics/tools/lama/bin
ya make --checkout
# Готовим окружение
ln -snf ~/arc/arcadia/maps/analytics/tools/lama/bin/lama  /usr/local/bin/lama
export NIRVANA_TOKEN='<token>'
export YT_TOKEN='<token>'
export SOLOMON_TOKEN='<token>'
export JUGGLER_TOKEN='<token>'
# Синхронизируем конфиг с Реактором Ламой
cd crypta/graph/orchestration/reactor/configs
lama sync -c artefacts.yaml --force
```
