# linux-commit-api

Это наш набор изменений и улучшений для [etckeeper](https://etckeeper.branchable.com/), код которого [лежит в Аркадии](https://a.yandex-team.ru/arcadia/noc/linux-commit-api), который

1. держит конфиги системы в СКВ `git`,
2. перезагружает демоны, когда их конфиги меняются,
3. откатывает состояние при проблемах применения новой конфигурации.


## Когда запускается linux-commit-api

Изменение конфига и вызов etckeeper может инициироваться:

* Аннушкой - в коде Аннушки есть прямой вызов `etckeeper commitreload`
* ЦК+ЧК, когда катят патчи на устройство (сценарий `checkist`), то применяется пост-деплой из аннушкиного генератора, который релоадит
* `comocutor-contrib` содержит фреймворк для фиксирования и отката конфигов, который явно вызывает `etckeeper commitreload` и `etckeeper rollback` - например, используется в ЦК
* другими средствами: вручную (зашли на Whitebox через ssh/nocssh, поправили конфиг и запустили `etckeeper commitreload`), автоматическим скриптом и т.п.


## Использование linux-commit-api

После изменения конфигов зафиксировать зарелоадить сервисы и зафиксировать изменения в `git` можно командой (опция `-d` включает дебаг):

``
etckeeper commitreload -d
``

Можно явно указывать файлы, которые нужно подхватить:

``
etckeeper commitreload /etc/my-changed-file -d
``

Для отката изменений на нужный коммит с соответствующим релоадом сервисов можно командой:

``
etckeeper rollback <commit_id> -d
``

TODO: описать `check`, `branchstash` и `sendtrap`


## Сборка linux-commit-api и использование пакетов

`linux-commit-api` собирается в виде `deb`-пакета в ArcCI-пайплайне и заливается в Dist в репозиторий `noc`: [https://dist.yandex.ru/api/v1/search?pkg=linux-commit-api&human=true](https://dist.yandex.ru/api/v1/search?pkg=linux-commit-api&human=true)

Для обновления надо сделать следующее:

1. внести изменения
2. пойти [собрать в Arcadia CI](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Flinux-commit-api&id=linux-commit-api-release)
3. полученную версию из Диста поставить принудительно на тестовый свич, чтобы протестить,
4. если пакет годный, и его можно продвинуть в продовый репозиторий, там дождаться сборки пакета (второй квадрат) и вручную пройти гендальфа нажатием кнопки в правом квадратике

![screenshot](./_images/linux-commit-api_build_screenshot.png)

Деплой `linux-commit-api` непосредственно на whitebox-ы происходит из `deb`-пакета при наливке:

* для Cumulus-ов пакет `linux-commit-api` прописан в Ansible-плейбуке [тут](https://noc-gitlab.yandex-team.ru/nocdev/ansible/-/blob/40ebe6e66f17620012309e5474797f647f1b3682/roles/cumulus-switch/tasks/main.yml#L86), и этот плейбук используется в наливке [https://noc-gitlab.yandex-team.ru/nocdev/cumulus-zeroconf](https://noc-gitlab.yandex-team.ru/nocdev/cumulus-zeroconf)
* для Switchdev пакет `linux-commit-api` указан в зависимостях мета-пакета `yandex-switchdev` (тут)[https://a.yandex-team.ru/arcadia/noc/switchdev/yandex-switchdev/package.json#L13]

Обновление `linux-commit-api` на уже работающих whitebox-ах - это не очень приятное занятие


## Внутреннее устройство linux-commit-api

Общая логика работы `linux-commit-api` следующая:

- через `git` определяется список изменившихся файлов
- через `apt/dpkg` определяется пакет, которому принадлежит каждый изменившийся файл
- через `apt/dpkg` определяется список установленных systemd-unit файлов
- через `systemd` определяется, что сервис работает или умер
- если сервис работает или умер, то делается попытка зарелоадить systemd-сервис
- изменения в файлах фиксируются в `git`

При прохождении изменившегося файла по этим шагам могут использоваться хаки/оверрайды/white-листы/black-листы, чтобы кастомизировать некоторые особенности.

`linux-commit-api` явно поддерживает следующие сервисы/компоненты:

- `bird`
- `frr`
- `telegraf`
- `snmpd`
- `grub`
- `systctl
- конфигурация интерфейсов (изменение `/etc/network/interfaces`)
- смена `hostname`
- `ann-copp-svc`
- `ann-hostname-svc`
- `ann-qos-svc`
- `ann-splitport-svc`
- `sx-ecmp-hash`
- изменение ##/etc/tacplus_servers##
- `cumulus acl` (изменение файлов в директории `/etc/cumulus/acl/policy.d`)
- изменение `/etc/cumulus/datapath/traffic.conf`
