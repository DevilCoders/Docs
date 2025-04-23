# testpalm-united-runner-cli

> CLI-утилита для запуска тестирования в объединённой схеме.

## Установка

```shell
npm install @yandex-int/si.ci.testpalm-united-runner-cli --registry=https://npm.yandex-team.ru
```

## Использование

```shell
tpur --config version.json --testpalmToken token --hitmanToken token
```

## Описание аргументов

### `prepare`

```console
$ tpur.js prepare

Создаёт тест-раны на основе подготовленного конфига, рассчитывает дедлайн
и насыщает входной конфиг идентификаторами созданных тест-ранов.

Выводит насыщенный конфиг в stdout.

Требует токен для доступа к TestPalm в переменной окружения TESTPALM_OAUTH_TOKEN.

Input & Output
  --config  Путь к файлу, в котором описана конфигурация запуска      [required]

Network
  --ipv6-only  Использовать только IPv6 для работы с сетью
                                                      [boolean] [default: false]

Deadline
  --enable-deadline-calculation             Автоматически рассчитывать дедлайн
                                            по параметрам запуска
                                                      [boolean] [default: false]
  --min-deadline-in-hours                   Минимальный дедлайн в часах, по
                                            умолчанию равно 3 часам
                                                           [number] [default: 3]
  --max-deadline-in-hours                   Максимальный дедлайн, который будет
                                            установлен тест-ранам с тегом
                                            without-deadline
                                                          [number] [default: 60]
  --ignore-deadline-calculation             Список тегов тест-ранов, для которых
                                            не будет рассчитываться дедлайн
                                                  [array] [default: ["release"]]
  --min-test-run-count-for-calculation      Число тест-ранов, которое должно
                                            быть в запуске, чтобы рассчитывать
                                            дедлайн. Если число тест-ранов
                                            меньше указанного значения, то
                                            всегда применяется минимальный
                                            дедлайн       [number] [default: 20]
  --additional-time-by-test-run-count-time  Время, выраженное в часах, которое
                                            добавляется к дедлайну каждый шаг,
                                            определённый в опции
                                            "additional-time-by-test-run-count-s
                                            tep"           [number] [default: 1]
  --additional-time-by-test-run-count-step  Шаг, выраженный в числе тест-ранов,
                                            при достижении которого добавляется
                                            час к дедлайну[number] [default: 10]

Runner
  --additional-test-run-tags  Дополнительные теги для тест-ранов
                                                           [array] [default: []]
  --version-id                Идентификатор версии, к которой будут прилинкованы
                              созданные тест-раны. Если версии не существует, то
                              она будет создана. Если аргумент не передан, то
                              используется `testpalmRunGroup` из конфига.
                              Идентификатор может содержать латинские буквы,
                              цифры и символ _.                         [string]

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
```

### `run`

```console
$ tpur.js run

Запускает Hitman-процесс на основе подготовленной версии.

Выводит результат запуска в stdout.

Требует токен для доступа к Hitman в переменной окружения HITMAN_TOKEN.

Input & Output
  --config  Путь к файлу, в котором описана конфигурация запуска      [required]

Network
  --ipv6-only  Использовать только IPv6 для работы с сетью
                                                      [boolean] [default: false]

Runner
  --hitman-process-id  Идентификатор Hitman-процесса, который будет запущен для
                       каждой группы тест-ранов
                               [default: "united_assessors_adapter_{{service}}"]

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
```

## Обновление кубика в Nirvana

1. Найти в [списке][latest-tpur] последнюю релевантную операцию (кубик).
1. В выпадушке справа нажать **Clone**, создастся черновик.
1. На вкладке _Overview_ обновить _Version number_. В качестве версии кубика используется версия пакета `testpalm-united-runner-cli`.
1. На вкладке _Options_ обновить _job-command_:

    1. Указать новую версию пакета в команде `npx`

1. Обновить входные и выходные данные, а также опции, если это нужно.
1. Сверху справа нажать галочку без щитка (_Save changes and Approve_).
1. Пометить оригинальную операцию устаревшей, выбрав _Optional_.

[latest-tpur]: https://nirvana.yandex-team.ru/operations/1/filter?@filterName=customFilter&tags=ExprTagsIn(tpur)&deprecation=ExprFlowchartBlockTypeDeprecation(active)&@sorting=official:true,created:true
