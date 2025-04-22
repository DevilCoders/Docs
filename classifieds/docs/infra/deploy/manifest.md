# Манифест деплоя

**Манифест деплоя** - описания yml конфигурации деплоя сервиса

Все манифесты находятся в [services/deploy](https://a.yandex-team.ru/arc_vcs/classifieds/services/deploy)

Изменяются/добавляются через PR.

## Конфигурация приложения

### Примеры конфигурации

{% cut "Все в манифесте (common_params, config.params)" %}

**Манифест**
```yaml
common_params:
  PARAM1: common_value_1
  PARAM2: common_value_2
  PARAM3: common_value_3
prod:
  config:
    params:
      PARAM3: prod_value_3
      PARAM4: prod_value_4
      PARAM5: prod_value_5
test:
  config:
    params:
      PARAM6: test_value_6
```
**Итог prod:**
```yaml
PARAM1: common_value_1
PARAM2: common_value_2
PARAM3: prod_value_3
PARAM4: prod_value_4
PARAM5: prod_value_5
```
**Итог test:**
```yaml
PARAM1: common_value_1
PARAM2: common_value_2
PARAM3: common_value_3
PARAM6: test_value_6
```
{% endcut %}

{% cut "В файлах с переопределением в манифесте (config.files, config.params)" %}

**Манифест:**
```
prod:
  config:
    files:
      - conf/my_service/common.yml
      - conf/my_service/prod.yml
    params:
      # Решение коллизии между файлами
      PARAM3: prod_value_3
test:
  config:
    files:
      - conf/my_service/common.yml
      - conf/my_service/test.yml
```
**Файл conf/my_service/common.yml:**
```
PARAM1: common_value_1
PARAM2: common_value_2
PARAM3: common_value_3
```
**Файл conf/my_service/prod.yml:**
```
PARAM3: prod_value_3
PARAM4: prod_value_4
PARAM5: prod_value_5
```
**Файл conf/my_service/test.yml:**
```
PARAM6: test_value_6
```
**Итог prod:**
```
PARAM1: common_value_1
PARAM2: common_value_2
PARAM3: prod_value_3
PARAM4: prod_value_4
PARAM5: prod_value_5
```
**Итог test:**
```
PARAM1: common_value_1
PARAM2: common_value_2
PARAM3: common_value_3
PARAM6: test_value_6
```

{% endcut %}

### Переменные

{% cut "Пример" %}

```
API_TIMEOUT: '2m'
ADDRESS: pg-rw-mdbgaq38umqnon8vdctu.query.consul:6432
API_PORT: 85
DB_PASSWORD: '${sec-01db0cb5aspraxjdrs11vsrefg:ver-01dt8zbenf836hx06v8205jvrs:DB_PASSWORD}'
```

{% endcut %}

Переменные окружения описываются как yaml словарь, где

**Ключи**
- В формате [A-Z,0-9,_]

**Значения:**
- Строки с/без 'кавычек'
- Шаблоны, [подробнее](https://docs.yandex-team.ru/classifieds-infra/deploy/templates)

### common_params

{% cut "Пример" %}

```yaml
common_params:
  key: value
```

{% endcut %}

Общие переменные окружения по умолчанию для слоя `prod/test`. Они будут перезаписаны переменными (из `config.files` и `config.params`) из блока [config](https://docs.yandex-team.ru/classifieds-infra/deploy/mainfest#config) в соответствующем слое.

### config

{% cut "Пример" %}

**Манифест:**
```
prod:
  config:
    files:
      - shiva/db/prod.yml
      - shiva/updater/common.yml
      - shiva/updater/prod.yml
    params:
      INT: 1
      STRING: string
      STRING_2: 'string'
      SECRET: '${sec-id:ver-id:key}'
```
**Файл конфигурации:**
```
INT: 1
STRING: string
STRING_2: 'string'
SECRET: '${sec-id:ver-id:key}'
```

{% endcut %}

Список файлов конфигурации с переменными окружения которые будут переданы в контейнеры. Файлы конфигурации находятся в директории.

{% note warning %}

При изменении файлов конфигурации будут перепроверены все манифесты использующие их на коллизии и доступности к секретам

{% endnote %}

*блок `config` не поддерживает наследование через блок `general`*

#### Механизм работы
1. В первую очередь берутся переменные из `common_params`. Они имеют самый низкий приоритет.
2. Далее собираются все переменные из файлов `config.files`. Они перетрут значения из `common_params`.
3. Далее поверх будут добавлены значения из `config.params`, причем они:
   1. Решают коллизии в `config.files` (Если коллизии не будут решены, это вызовет ошибку валидации)
   2. Переопределяют переменные в `common_params` и `config.files`
   3. Добавляют новые переменные
4. Далее поверх будут наложены  [базовые переменные c _DEPLOY](https://docs.yandex-team.ru/classifieds-infra/deploy/default-env)
5. Итоговый набор будет доставлен как переменные окружения в приложение

## Layer

Манифест содержит два основных блока соответствующих слоям: `test`|`prod`

Они позволяют переопределять конфигурацию и переменные окружения для определенного слоя. Поля описаны ниже.

## Fields

### name
Имя связанной [карты сервиса](https://docs.yandex-team.ru/classifieds-infra/service-map#name)

**Обязательно:**
- иметь одинаковое имя сервиса и название файла с манифестом

### image
Название образа в docker registry. Если поле не заполнено, в качестве `image` используется `name`

Например, если в нашем registry был запушен образ `registry.yandex.net/vertis/shiva`, то в это поле нужно вписать `shiva`. Но если `name` и так `shiva`, то поля можно не заполнять

### canary

{% cut "Пример" %}

```yaml
canary:
  promote: manual
```

{% endcut %}

Включает возможность выкладки в prod через промежуточный stage с небольшим количеством трафика.

На текущий момент реализован только ручной способ через `promote`.

Подробно можно почитать [тут](https://docs.yandex-team.ru/classifieds-infra/deploy/specification/canary).

### production_mirroring

{% cut "Пример" %}

```yaml
production_mirroring: true
```

{% endcut %}


Включает зеркалирование прода в тестинге - то есть при выкатке новой версии в prod автоматически запустится выкатка такой же версии и конфигурации в ветку `production` в тестинге

### datacenters

{% cut "Пример" %}

```yaml
datacenters:
 any:
  count: 1
```

{% endcut %}

Конфигурация количества инстансов приложения

На данный момент поддерживаются ДЦ:
- sas
- vla
- any

#### any

* При использовании `any` шедулер сам выберет в какой ДЦ поселить приложение.
* Если `count` больше 1, то в теории шедулер равномерно размажет количество инстансов между доступными ДЦ, но мы не даем гарантий.
* При отключении ДЦ приложение будет поднято в другом ДЦ и там останется при возращении ДЦ.
* Если `count` равен 1, то во время деплоя будет **простой** на время поднятия новой версии. Аналогично при отлючение ДЦ.
* Если используется any, то нельзя указывать другие ДЦ

### resources

{% cut "Пример" %}

```yaml
resources:
  cpu: 1500
  memory: 256
```

{% endcut %}

Конфигурация требуемых ресурсов приложения

#### auto_cpu

{% cut "Пример" %}

```yml
resources:
  auto_cpu: true
  memory: 256
```

{% endcut %}

Делегировать выставление лимита CPU на автоматику. При этом, для сервиса будет вычислен CPU исходя из фактически потребляемых значений, исключая редкие спайки.

Изменение лимита будет происходить раз в сутки, основываясь на исторических данных по потребляемому CPU за две недели.

{% cut "Особенности поселения нового сервиса с auto_cpu" %}

При поселении нового сервиса исторические данные по CPU отсутствуют, поэтому в качестве лимита будет взято максимальное значение в 12Ghz.
Если новый сервис состоит из большого количества контейнеров, то велика вероятность, что места по CPU для такого большого сервиса не найдется (`количество_контейнеров * 12Ghz`).
Для поселения нужно указать оба свойства `auto_cpu` и `cpu`

```yml
resources:
  auto_cpu: true
  cpu: 3000
  memory: 256
```

При таком манифесте, значение в 3Ghz будет использоваться как fallback при отсутствии исторических данных.

{% endcut %}

#### cpu

Количество Mhz, при пересчете в ядра 3000Mhz ~ 1 ядро

*По умолчанию, если не задан cpu, то будет считать как `auto_cpu`*

{% note info %}

Для тестинга рекомендуется использовать только auto_cpu

{% endnote %}

#### memory

Количество памяти в мегабайтах

*По умолчанию 100*

*Максимально возможное значение 65536 (64 Гб)*
### periodic

{% cut "Пример" %}

```
periodic: '*/1 * * * *'
```

{% endcut %}

Расписания в cron формате для [типа карты batch](https://docs.yandex-team.ru/classifieds-infra/service-map#batch)

### upgrade

{% cut "Пример" %}

upgrade:
  parallel: 5

{% endcut %}

Конфигурация деплоя новой версии

#### parallel

Количество одновременно перезапускаемых контейнеров в каждом дц

### geobase_version

Версия геобазы, которую использует приложение. Полный путь до бинаря будет передан в env `_DEPLOY_GEOBASE_PATH`.
На данный момент поддерживается версия 6.
