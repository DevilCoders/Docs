# Приостановка деплоя

При необходимости деплой [Pod](../concepts/pod/pod.md) можно приостановить. При этом  также останавливается [эвакуация](../reference/internals/architecture/rsc.md#eviction) Pod.

## Веб-интерфейс
1. Откройте Stage в режиме редактирования.
1. В настройках соответствующего [Deploy Unit](../concepts/deploy-unit/deploy-unit.md) в поле `Disruption budget` укажите 0.
1. Нажмите **Update** внизу страницы.
1. Убедитесь, что спецификация изменилась требуемым образом, добавьте комментарий и нажмите **Deploy**.

## dctl
1. Скачайте спецификацию Stage в формате `yaml`. Для этого перейдите в каталог с `ya` и выполните: `./ya tool dctl get stage <stage-id> > stage-spec.yaml`

* `stage-id` - это `Stage Name`, который был задан при создании Stage.

1. Задайте в спецификации `stage-spec.yaml`:

```yaml
deployment_strategy: 
  max_unavailable: 0
```

1. Выкатите новую версию спецификации: `./ya tool dctl put stage stage-spec.yaml`
