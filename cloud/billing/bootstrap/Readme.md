# YC Billing справочники

Тут располагается исходная информация для сборки бандлов sku биллинга Яндекс Облака в различных инстралляциях:
 - [тестовый пакет для экспериментов и отладке](./testing)
 - [биллинг внутренней инсталляции Яндекс](./internal)


В каталоге `tools` расположены вспомогательные утилиты и настройки сборки

## Структура каталогов справочников

- `services` - описания сервисов
- `skus` - описания SKU сервисов (`stock keeping unit`, тарифицируемая единица потребления облака)
- `schemas` - описания требований к схемам метрик сервисов (обязательные и опциональные теги)
- `bundles/<bundle name>` - тут располагаются описания идентификаторов и цен sku, включаемый в отдельную сборку
- `units` - описания конвертации единиц измерения, применяющихся в sku
- `metrics` - каталог, в котором располагаются данные для тестирования резолвинга метрик в описанные sku

### Описания сервисов

Описание каждого сервиса должно располагаться в отдельном файле yaml. Структура подкаталогов не важна.

В описании поддерживаются следующие поля:
 - id - идентификатор без префикса (17 символов нижнего регистра [0-9a-v])
 - name - внутренне имя сервиса (строка симвлов [0-9a-z._-])
 - description - человекочитаемое описание сервиса
 - group - группа, к которой относится сервис

### SKU сервисов

Описания располагаются в файлах yaml, структура каталогов не имеет значения.
В одном файле могут располагаться множество SKU одного сервиса, в разных файлах тот же сервис может использоваться повторно.

Структура файла:
```
service: service.name
skus:
  sku_name:
    ru: Русское название sku
    en: English name of sku
    reporting_service: service.name/subservice
    private: false
    pricing_formula: mul(usage.quantity, `2`)
    units:
      usage: usage_unit
      pricing: pricing_unit
    schemas:
      - some.service.schema
    resolving_policy: tags.some_tag=='some value'
```

Поля описания sku:
  - `ru`, `en` - названия sku на соответствующих языках
  - `reporting_service` - поле вида `<service for reporting>/<subservice>` (используется для группировок в аналитической отчетности)
  - `private` - является ли sku скрытым от публичных пользователей
  - `pricing_formula` - JMESPath формула вычисления оплачиваемого потребления
  - `usage_type` - тип потребления "delta" или "cumulative" (по-умолчанию delta)
  - `units.usage` - единица измерения потребления, в которой получается число после применения `pricing_formula`
  - `units.pricing` - единица измерения, в которой к которой применяется цена. Если не совпадает с `units.usage`, то обязана быть запись в `units`
  - `schemas` - схемы метрик, для которых возможен резолвинг в этот SKU
  - `resolving_policy` - JMESPath выражение, которое должно выполниться для резолвинга метрики в это SKU
  - `resolving_rules` - список требований к полям метрики для резолвинга. Если выполняется хотя бы одно треобование из списка, то SKU применим.

### Описания требований к схемам метрик

Требования располагаются в yaml файлах. Структура и разбиение по файлам не важно для процесса загрузки.
В каждом файле содержится набор ключей с названиями схем (обязательно должны использоваться хотя бы в одном SKU) и 2 поля с описанием схемы:
  - `required` - список обязательных тегов, проверяется при обработке метрик
  - `optional` - список опциональных полей, носит справочный характер

Если к схеме не предъявляются требования по набору тегов, то лучше не вносить ее в требования.

### Описания бандлов

По общему описанию справочников собираются отдельные бандлы (самоприменяющиеся бинарники).
Для описания подмножества информации, которую надо включить в такой бинарник используется подкаталог `bundles/<bundle name>`

В файлах yaml располагаются ключи sku, которые надо включить в бандл и дополнительная информация:
  - `id` - идентификатор без префикса (17 символов нижнего регистра [0-9a-v])
  - `prices` - список описаний схем:
    - `start_date` - дата или дата и время начала действия цены (либо "YYYY-MM-DD", либо "YYYY-MM-DDThh:mm:ss+03")
    - `price` - цена в случае если не применяются пороги потребления
    - `rates` - список порогов потребления
      - `quantity` - порог потребления
      - `price` - цена после достижения порога

При сборке бандла выбираются только сущности, связанные с перечисленными sku.

### Описания конвертации единиц измерения

В файлах yaml располагаются списки правил для конвертации единиц измерения:
  - `src_unit` - из какой единицы переводить (usage)
  - `dst_unit` - в какую единицу переводить (pricing)
  - `factor` - число, на которое надо **поделить** потребление для конвертации

### Тесты резолвинга метрик

Для проверки корректности работы резолвинга метрик в SKU необходимо все кейсы добавить в yaml файлы
в каталоге `metrics`. Файлы подерживают несколько yaml документов (надо использовать разделитель "---")

Структура кейса для тестирования:
  - `metric` - описание части структуры метрики, влияющией не резолвинг (обязательные теги должны присутствовать)
    - `schema`
    - `version`
    - `usage`
    - `tags`
  - `skus` - маппиг SKU, которые должны получиться для метрики и их потребления:
    - `usage.qantity` и `usage.unit` - потребление и единица измерения Usage
    - `pricing.qantity` и `pricing.unit` - потребление и единица измерения Pricing

## Сборка и тестирование

Инструкции по сборке располагаются в каталоге `packaging`
 - `tests` - тесты на Go с использованием библиотек из [selfsku](https://a.yandex-team.ru/arc_vcs/cloud/billing/go/pkg/selfsku).
    ya.make содержит директивы для добавления данных справочников в тесты.
 - `scripts` - скрипты для публикации собранных пакетов и вспомогательные скрипты для скачивания
 - `pkg.json` - инструкции для сборки бандлов и всего необходимого для публикации (как запускать см. [скрипт](./tools/build/build_bundle.sh) )

Остальные каталоги содержат минимальный код для сборки бинарных бандлов.
