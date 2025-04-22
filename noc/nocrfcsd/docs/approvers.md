# Согласовщики

Демон nocrfcsd для ручного согласования использует сервис [OK](https://wiki.yandex-team.ru/intranet/ok/). Кого и как
демон будет призывать в это согласование, определяется параметрами RFC и содержимым конфигурационного файла с правилами
выбора согласовщиков.

## Расположение конфига

Файл лежит в Аркадии:

- прод: [noc/nocrfcsd/static/approvers.yaml](https://a.yandex-team.ru/arc_vcs/noc/nocrfcsd/static/approvers.yaml)
- тест: [noc/nocrfcsd/static/approvers-test.yaml](https://a.yandex-team.ru/arc_vcs/noc/nocrfcsd/static/approvers-test.yaml)

## Язык и формат файла

Файл представляет собой набор правил, описанных в формате YAML. Каждое правило представляет собой условие применения и
эффект от применения правила при выполнении условия:

```yaml
- approvers: []  # список групп согласовщиков
  # условия применения правила
  infra: ...
  rackCode: ...
  # порядок согласования
  order: ...
```

- `infra`, `rackCode` - условия, при выполнении которых срабатывает правило
- `approvers` - группы сотрудников, которые добавляются в OK-согласование при выполнении условий
- `order` - режим сбора ОКов, по-умолчанию параллельный (`parallel`), учитывается при выполнении условий

## Логика применения правил

Когда nocrfcsd решает создать OK-согласование для конкретного RFC, то он прогоняет этот RFC по всему набору правил
"сверху вниз" в том порядке, в котором правила перечислены в конфигурационном файле.

Встретив правило, nocrfcsd проверяет, матчится ли условие с этим RFC. Если условие выполняется, то группы согласовщиков
дополняются указанными в правиле.

Если хотя бы у одного "заматченного" правила был указан последовательный режим согласования (`order: serial`), то
всё согласование переходит в последовательный режим. Иначе согласование остаётся в параллельном режиме.

## Валидация конфига

Ошибки парсинга проверяются в CI, и закоммитить невалидный файл в trunk не получится.

Прочие проверки на "актуальность" конфига (поиск ссылок на несуществующие ABC-сервисы, поиск уволенных сотрудников и
т.п.) происходят в рантайме демона:

- при запуске демона
- через утилиту `nocrfcs-validate-approvers`:
  ```bash
  export STAFF_API_TOKEN=...
  export INFRA_API_TOKEN=...
  export ABC_API_TOKEN=...
  export APPROVERS_V2=static/approvers.yaml
  go run cmd/nocrfcs-validate-approvers/main.go
  ```

## Описание условий и групп согласовщиков

Условиями применения правил могут быть:

- `infra` - совпадение [Infra](https://infra.yandex-team.ru/)-окружения
- `rackCode` - вхождение устройства в рэккод [Racktables](https://racktables.yandex-team.ru/) (TODO)

Группа согласовщиков может быть указана следующим способом:

- `persons` - явное указание логинов сотрудников
- `abcDuty` - [дежурные в ABC-сервисе](https://wiki.yandex-team.ru/intranet/abc/docs/duty/)
- `abcService` - принадлежащие к [ABC-сервису](https://wiki.yandex-team.ru/intranet/abc/#terminologija) сотрудники
- `abcScope` - входящие в [скоуп ABC-сервиса](https://wiki.yandex-team.ru/intranet/abc/#terminologija) сотрудники

### Условие infra

```yaml
infra:
  environment: имя окружения
  service: имя сервиса
```

Матч работает путём сопоставления сервиса и окружения с тем, что был выбран в RFC (поле _Подсистема (как в Infra)_ в
форме).

Пример, указываем [Racktables](https://infra.yandex-team.ru/services/198/environments):

```yaml
infra:
  environment: Racktables
  service: NOC DEV
```

При валидации условия происходит поиск окружения в [Infra](https://infra.yandex-team.ru/).

### Группа persons

```yaml
persons:
  - login1
  - login2
```

Группа, представленная путём простого перечисления логинов сотрудников.

Пример:

```yaml
persons:
  - lytboris
  - smarochkin
  - ttl256
  - tekanov
```

Валидация группы происходит запросом в Staff с проверкой на:

- существование сотрудника
- отсутствия флага "Бывший" (сотрудник не должен быть уволившимся)

### Группа abcDuty

```yaml
abcDuty: serviceSlug
```

Группа, представленная дежурными ABC-сервиса

Например, [дежурные сервиса NocDev](https://abc.yandex-team.ru/services/NOCDEV/duty/):

```yaml
abcDuty: NOCDEV
```

При валидации происходит поиск в ABC сервиса по заданному slug-у.

### Группа abcService

```yaml
abcService: serviceSlug
```

Группа, представленная командой сотрудников ABC-сервиса

Например, команда сервиса [Автоматизация сети](https://abc.yandex-team.ru/services/netauto/):

```yaml
abcService: netauto
```

Валидация заключается в следующем:

- должен существовать ABC-сервис с указанным slug-ом
- команда ABC-сервиса должна содержать хотя бы одного сотрудника

### Группа abcScope

```yaml
abcScope:
  service: serviceSlug
  scope: scopeSlug
```

Группа, представленная сотрудниками, входящими в скоуп ABC-сервиса

Например, [скоуп Администрирование в сервиса NOCDEV](https://abc.yandex-team.ru/services/NOCDEV/?scope=administration):

```yaml
abcScope:
  service: NOCDEV
  scope: administration
```

Валидация требует непустого количества сотрудников в скоупе ABC-сервиса
