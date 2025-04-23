# assessors-cli

> CLI утилита для запуска тестирования на асессорах.

Узнайте больше про запуск на асессоров [на вики](https://wiki.yandex-team.ru/search-interfaces/infra/crowdtest/tech/).

## Установка

```shell
npm install @yandex-int/si.ci.assessors-cli --registry=https://npm.yandex-team.ru
```

## Команды

### `fetch`

```console
$ assessors.js fetch

Download data from TestPalm for the specified set of test runs. Applies
the definitions to all properties of each test case.

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
  --project-id   TestPalm project id                         [string] [required]
  --testrun-ids  Id's of test runs that you want to run       [array] [required]
```

### `configure`

Конвертирует тестраны в старый формат конфига. Сохранит два файла:
- `--output` с валидными запусками;
- `--error` с невалидными.

При генерации запуска все тесткейсы в тестране будут провалидированы и отфильтрованы по браузерам. Фильтрация происходит так:

1. В sandbox силами [Алексея Остроумова](https://staff.yandex-team.ru/ostroumov) публикуются ресурсы в формате JSON со списком доступных браузеров. Найти свежий можно по фильтру [OTHER_RESOURCE, attrs.type=assessors_devices](https://sandbox.yandex-team.ru/resources?type=OTHER_RESOURCE&state=READY&limit=20&attrs=%7B%22type%22%3A%22assessors_devices%22%7D). Для запуска команды `configure` нужно скачать JSON-файл из самого свежего ресурса, и передать путь к нему команде `configure` через опцию `--devices`.
2. В файле с тестранами (который вы выкачали командой `fetch`) у каждого тестрана должно быть поле `currentEnvironment` (в [UI Testpalm](https://testpalm.yandex-team.ru/) вы можете увидеть его при редактировании тестрана) и свойство (property) `platform`.
3. Для каждого тестрана по этим двум полям — `currentEnvironment` и `platform` — мы находим подходящий «девайс» из файла `device.json`.
4. Затем для каждого тесткейса в тестране мы смотрим в его атрибут `browsers`, и если хотя бы один браузер из атрибута есть в найденном в п. 3 девайсе (с точностью до регистра), то тесткейс попадёт в запуск. Если же совпадения по браузеру между тесткейсом и найденным девайсом не нашлось, тесткейс будет поскипан с комментарием `Тест-кейс не поддерживается девайсом`. Исключать тесткейсы из запуска можно и по другим полям, см. [код](./src/commands/configure/api.ts#L219-231).

```console
$ assessors.js configure

Convert test runs to config with old format for backward compatibility to other
utils.
Right now it support only minimal set of properties for yml2tsv.

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
  --project-id   TestPalm project id                         [string] [required]
  --service      The name of service                         [string] [required]
  --testruns     The filepath to the file with test runs     [string] [required]
  --devices      The filepath to the file with devices       [string] [required]
  --output       The filepath to the file that will contain correct launches
                                                             [string] [required]
  --error        The filepath to the file that will contain broken launches
                                                             [string] [required]
```

### `links`

```console
$ assessors.js links

Generate sticky URL's for beta & control in each test case.

Options:
  --help, -h             Show help                                     [boolean]
  --version, -v          Show version number                           [boolean]
  --config               The filepath to config file         [string] [required]
  --testid-exp-flag-tag  The tag name of testid for experimental flag
                                                             [string] [required]
  --sign-ttl             How long sticky URL will be active
                                                      [number] [default: 432000]
  --sign-redirect-ttl    How long user can use sticky URL after sticking
                                                      [number] [default: 432000]
```

### `report-invalid-launches`

```console
$ assessors.js report-invalid-launches

Sends a comment to the test run that it was skipped.

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
  --config       The filepath to the file with the invalid launches
                                                             [string] [required]
```

### `report-yml2tsv-errors`

```console
$ assessors.js report-yml2tsv-errors

Skip test case in test run with reason in comments.
Uses error output of yml2tsv as input config.

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
  --project-id   TestPalm project id                         [string] [required]
  --config       The filepath to the file with errors from yml2tsv
                                                             [string] [required]
```

### `finish`

```console
$ assessors.js finish

Finish testrun without affixing statuses

Options:
  --help, -h     Show help             [boolean]
  --version, -v  Show version number   [boolean]
  --project-id   TestPalm project id
                             [string] [required]
  --testrun-ids  Id's of test runs that you want
                 to finish    [array] [required]
```
