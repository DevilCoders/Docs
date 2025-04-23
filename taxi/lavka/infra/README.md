-   [abc](https://abc.yandex-team.ru/services/lavkainfra/)
-   [staff](https://staff.yandex-team.ru/persons/yandex_rkub_taxi_5151_8501_dep41202_dep48321_dep64819)
-   [arcanum](https://a.yandex-team.ru/projects/lavkainfra)
-   [monitoring (juggler/solomon/etc)](https://monitoring.yandex-team.ru/projects/lavka-frontend-infra)

## Базовые docker образы

Простая обертка над внешними docker hub образами, чтобы не ходить во внешнюю сеть.

Образы сохраняются в `registry.yandex.net/lavka-infra/` префикс.

Пример публикации:

```bash
baseimages/publish.sh --package postgres --tag 12-buster
```

**Важно:** при добавлении нового пакета необходимо обновить переменную `PACKAGES_LIST` в файле `baseimages/publish.sh`
