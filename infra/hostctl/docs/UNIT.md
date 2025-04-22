# Управление юнитами на хосте hostctl'ем

## Доступные юниты
* [PortoDaemon](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/docs/PortoDaemon.md)
* [PackageSet](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/docs/PackageSet.md)
* [SystemService](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/docs/SystemService.md)

Мотивация в [HOSTMAN-39](https://st.yandex-team.ru/HOSTMAN-39).

Под управлением понимается:
  * поддержание актуального (описанного в `spec`) состояния пакетов и файлов
  * поддержание запущенным porto контейнера

### Установка
Запуск юнитов из файлов управляемых salt'ом:
  * положить YAML файл в `/var/lib/ya-salt/repo/current/*/units.d/` с соответствующим именем, например `juggler-client.yaml`
  * добавить [orly правило](https://a.yandex-team.ru/arc/trunk/arcadia/infra/orly/rules)
    названное `porto-daemon-{name}` или `package-set-{name}` и применить его: `orlyctl apply-rule -f <created_rule_file>`

Персистентное переопределение юнитов на хосте:
  * положить YAML файл конфигурации в `/etc/hostman/units.d`

Временное переопределение юнита на хосте:
  * положить YAML файл конфигурации в `/run/hostman/units.d`

Конфигурации читаются в порядке:
  * `/var/lib/ya-salt/repo/current/*/units.d/`
  * `/etc/hostman/units.d`
  * `/run/hostman/units.d`
  * директория указаная при запуске hostctl с флагом `--units`


#### Формат файла
Поддерживаемые форматы файлов:
  * `.yml` or `.yaml`

Файл обязан содержать:
  * `meta` с атрибутом `name`, смотри `ObjectMeta` в protobuf
  * `spec` с атрибутом `PortoDaemon`, `PackageSet` или `SystemService` смотри в protobuf ниже

Так как применение новых конфгураций опасное и деструктивное действие,
поэтому для удаления юнита мы должны напрямую об этом указать:
  * указать в конфигурации юнита `meta.delete_requested: true` атрибут

### Package manager
Все вызовы `apt-get install` будут иметь выставленную переменную HOSTMAN=1 env.
Это позволит производить меньше действий (т.е ручной рестарт демона)
если управляется hostman'ом.

### Unit env
* env.real

    Дефолтное окружение, применяются все изменения как описано в spec
* env.noop

    Изменения не применяются (не останавливаем/запускаем porto контейнеры, не останавливаем/запускаем systemd сервисы...)
    Режим можно выставить для локально для юнита указав в meta.annotations["env.noop"] = "True"
    и глобально вызовом hostctl manage/apply --noop
* env.shadow

    Джобы юнитов выполняются в том же окружени что и при env.noop. В отличии от noop создаются sha1 файлы для определения актуальности systemd сервиса.
    Режим можно выставить для локально для юнита указав в meta.annotations["env.shadow"] = "True"

### Пререндеринг на реальных host_info
* отрендерить spec на host_info какого-то хоста
  `hostctl render <unit>.yaml -c PRESTABLE -n man1-3720.search.yandex.net`
* отрендерить spec на host_info всех хостов локации
  `hostctl render-all <unit>.yaml -c PRESTABLE -o html`

### Ручное тестирование
Для ручного тестирования
`hostctl apply -f <unit-definition>.yaml -E`
  * читаем юнит из файла
  * рендерим meta и spec
  * показываем отрендеренные `meta`, `spec` и `plan` выполнения
  * не применяем изменения
`hostctl apply -f <unit-definition>.yaml --noop`
  * читаем юнит из файла
  * применяем изменения в noop режиме
`hostctl apply -f <unit-definition>.yaml`
  * читаем юнит из файла
  * применяем изменения юнита
  * показываем статус

