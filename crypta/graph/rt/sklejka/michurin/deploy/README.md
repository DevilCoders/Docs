Дамп YAML'ов окружения Y.Deploy
===============================

**michurin_stage.yaml**: Окружение crypta-rtsklejka-michurin
**michurin_rule.yaml**: Релизное правило, чтобы окружение обновлялось по релизу докреного образа

Чтобы завести в Y.Deploy
```bash
$ ya tool dctl put stage michurin_stage.yaml
$ ya tool dctl put release_rule michurin_rule.yaml
```
