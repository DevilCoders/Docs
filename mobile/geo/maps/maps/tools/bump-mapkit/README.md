# Утилита bump-mapkit

Утилита **bump-mapkit** предназначена для упрощения обновления mapkit'а в приложениях карт и навигатора.

Она делает следующее:
- поднимает версию mapkit'а в обоих приложениях
- обновляет файлы Podfile.lock приложений
- создаёт тикет в MAPSMOBILE и pr на обновление mapkit'а
- если тикет/pr уже существуют, то обновляет их
- находит и линкует к созданному тикету релизный тикет mapkit'а
- находит людей, трогавших idl файлы mapkit'а с предыдущего релиза, используемого приложениями, и добавляет их в тикет и pr

Пример созданного тикета https://st.yandex-team.ru/MAPSMOBILE-1523 и соответствующего pr'а https://a.yandex-team.ru/review/2229533/details

## Разработка bump-mapkit

Утилита является частью проекта `tools` Карт и для разработки в IDE нужно открывать папку https://a.yandex-team.ru/arc_vcs/mobile/geo/maps/maps/tools

### Dry mode

В **bump-mapkit** есть флаг `--dry`. Он позволяет не делать изменяющие запросы в arcanum или startrek.
Вместо выполнения таких запросов утилита выводит сообщение в консоль.

С какими флагами и как нужно запускать **bump-mapkit** можно посмотреть в [bump-mapkit.config.yaml](bump-mapkit.config.yaml). Исключение составляет флаг `--user` -- он нужен только для запуска в Sandbox.
Обратите внимание, что запуск там происходит в 2 стадии: сначала генерируются файлы `Podfile.lock`, и затем они перекидываются во 2-ю стадию.

Стоит учесть, что несмотря на то, что с флагом `--dry` утилита не делает изменяющих запросов по сети,
она делает изменения в локальном репозитории, такие как переключение веток и создание коммитов.
Из-за этого репозиторий стоит иметь в относительно чистом состоянии перед запуском утилиты.

### Запуск, приближенный к настоящему (для локальных тестов и экспериментов)

Как написано в предыдущем пункте, запускать **bump-mapkit** локально не очень удобно из-за того, что работа организована в несколько стадий,
и из-за необходимых переключений веток, которые могут остановить работу **bump-mapkit** в середине,
если локальный репозиторий был в плохом состоянии.

Для запуска утилиты была настроена конфигурация в teamcity https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_Navi_Infra_UpdateMapkitTest

Запускать её нужно через `Run ...`
![](https://jing.yandex-team.ru/files/kirilltatunov/bump-mapkit-run.png)

Версия mapkit'а указывается во вкладе `Parameters` в `sandbox.env`
![](https://jing.yandex-team.ru/files/kirilltatunov/bump-mapkit-specify-version.png)

По умолчанию эта конфигурация берёт код утилиты и отводит ветку из trunk'а.

Также можно запускать конфигурацию из произвольной ветки для тестов своих изменений в самой утилите. Сначала надо в настройках конфигурации добавить свою ветку в `arc.branch.spec`
![](https://jing.yandex-team.ru/files/kirilltatunov/bump-mapkit-branch-spec.png)

После небольшой задержки эта ветка будет доступна для выбора во вкладке `Changes` в `Run ...`.

### Роботы и права production запуска

В production утилита будет запускаться следующими роботами разработки МапКита:
- текущий: `robot-testenv`
- будущий: `robot-mapkit-ci`

Права, которые им необходимо иметь на данный момент:
- к [секретам Хомяка](https://yav.yandex-team.ru/secret/sec-01e8mp73ydq4541wbrkba0rhvn/explore/versions) (`robot-hamster`-а),
- `STARTREK_TOKEN`-у Хомяка из секрета выше - на поиск в очереди `MAPSMOBCORE`,
- к репозиториям подов,
- к групповым веткам `groups/mobile/maps`.
