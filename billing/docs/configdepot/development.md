# Разработка

Работа с конфигуратором описана в доках
- [про интеграции](../configshop/integrations.md)
- [про создание конфигурации](https://wiki.yandex-team.ru/users/olgalyubimova/configurator/developers/)
- [порядок действий](https://wiki.yandex-team.ru/users/olgalyubimova/configurator/developers/#konfiguracii)

### Полезные ссылки

swagger для тестового Конфигуратора: https://configshop.test.billing.yandex.net/docs#

Полезные методы:
- PUT /v1/template, чтобы обновить шаблон
- GET /v1/template, чтобы получить шаблон нужной версии

Остальные ручки удобнее через Insomnia дергать.

[Коллекция ручек для Insomnia](https://sandbox.yandex-team.ru/resource/3340346139/view)

### Алгоритм работы

Фаас работает с настройками следующего формата
```yaml
namespace: "taxi-light"
endpoints:
  dope:
    faas:
      function: "...."
      peerdir: "..."
      revision: "...."
      settings:
          foo: bar

faas:
  tenants: [common, taxi-light]
```
Это настройка 1 неймспейса.

Распиливая это на шаблон я получил в тестовом шопе конфигурацию try_faas. Она позволяет собирать такую структуру для неймспейса.
В нее нужно передать namespace, tenants и endpoints и они соберутся в структуру выше.

Чтобы конфигурить множество компонентов нужно их объединить в массив и положить в поле manifests.
Получается вот так:
```yaml

manifests:
    - namespace: taxi-light
      endpoints: {}
      faas: {}
    - namespace: bnpl
      endpoints: {}
      faas: {}
```

Для того чтобы добавить настройки тенантов, нужно добавить глобальное поле faas

```yaml
manifests:
    - namespace: taxi-light
      endpoints: {}
      faas: {}
    - namespace: bnpl
      endpoints: {}
      faas: {}

faas:
  tenants:
    common:
      dcs:
          - name: vla
            amount: 1
```

Вот эта финальная структура лежит в шаблоне faas.yaml.tpl и в нее подставляется массив манифестов, который сериализуется в YAML.

### Sandbox таски

Таска BILLING_FAAS_DEPOT_TASK запускает BILLING_FAAS_BUILD_TASK, а потом TASKLET_EXECUTOR с TASKLET_BILLING_FAAS_DEPLOY.
Можно смотреть в CI какие куда параметры передавать нужно, там по-сути все тоже самое кроме места, откуда билдящая таска берет манифесты.

Таска BILLING_FAAS_BUILD_TASK просто собирает бинари, обычно она берет манифесты из Манифисенты, но если передать параметры
`override_manifests: true` и `manifests: <YAML serialized manifests>`, то она будет использовать манифесты из параметров.

Далее запускается тасклет. НУЖНО указывать awacs_prefix, чтобы в одном неймспейсе в аваксе сожительствовали апстримы для разных стейджей.

ЛУЧШЕ запускать сначала с `dry_run: true`, чтобы не поломать ничего, далее смотреть в логи.
Логи там оч подробные, что где упало и тд.

В таске BILLING_FAAS_BUILD_TASK и BILLING_FAAS_DEPOT_TASK логи по этапам в разные файлы льются для удобства.

Все таски тут являются PY3/tasklet, поэтому если в них нужно что-то поменять, то после этого запускаем sb-upload, релизим, добавляем в аттрибут `task_type: ...` (кроме тасклета, там не нужно)
и полученный ресурс меняем в components. (абсолютно также как делали в CI, но теперь ресурс меняем в своих файлах, а не в ci/registry.)


