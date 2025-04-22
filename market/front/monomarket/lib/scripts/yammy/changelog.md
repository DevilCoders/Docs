# 3.5.2

**PR:** [#2744856](https://a.yandex-team.ru/review/2744856)
**Author:** @dv-mikhaylov **Date:** 2022-07-18

**[[MARKETFRONTECH-4687]]**

# 3.5.1

**PR:** [#2704435](https://a.yandex-team.ru/review/2704435)
**Author:** @robot-metatron **Date:** 2022-07-12

исправлена схема yammy build

# 3.5.0

**PR:** [#2718309](https://a.yandex-team.ru/review/2718309)
**Author:** @asker-k **Date:** 2022-07-08

Добавлена возможность форсированной установки нодмодулей, даже если нет скриптов публикации.
Так-же исправлен баг в yammy ci apply-template, в котором {{}} заменялись на пустые строки

### Usage

в config секции package.json в build добавить "forceInstallNodeModules": true
```json
{
  "config": {
    "build": {
      "ci:build": {
        "duration": 1500,
        "forceInstallNodeModules": true
      }
    }
  }
}
```

# 3.4.2

**PR:** [#2714744](https://a.yandex-team.ru/review/2714744)
**Author:** @robot-metatron **Date:** 2022-07-08

обработка суффикса платформы в apply-template

# 3.4.1

**PR:** [#2712835](https://a.yandex-team.ru/review/2712835)
**Author:** @robot-metatron **Date:** 2022-07-07

Добавил поверку наличия publish.json в CI процесс

# 3.4.0

**PR:** [#2665102](https://a.yandex-team.ru/review/2665102)
**Author:** @asker-k **Date:** 2022-06-22

добавлена команда yammy create-symlinks, которая генерирует симлинки из секции links в конфиге

### Usage

yammy create-symlinks ...pkgs

# 3.3.3

**PR:** [#2643720](https://a.yandex-team.ru/review/2643720)
**Author:** @ochernyakova **Date:** 2022-06-17

**Поправлен мердж в монорепе**

# 3.3.2

**PR:** [#2628681](https://a.yandex-team.ru/review/2628681)
**Author:** @gheljenor **Date:** 2022-06-14

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 3.3.1

**PR:** [#2628028](https://a.yandex-team.ru/review/2628028)
**Author:** @gheljenor **Date:** 2022-06-09

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 3.3.0

**PR:** [#2627748](https://a.yandex-team.ru/review/2627748)
**Author:** @gheljenor **Date:** 2022-06-09

[MARKETFRONTECH-3752](https://st.yandex-team.ru/MARKETFRONTECH-3752) - [Пуск] Запуск ПУСКа для JS

### Usage

Добавлена новая переменная окружения для форсированной публикации пакетов. Ставит флаг изменённых артефактов на пакет, вызывая его публикацию.

```shell
YAMMY_FORCE_RELEASE=<pkg-name> yammy ci meta
```

# 3.2.0

**PR:** [#2618952](https://a.yandex-team.ru/review/2618952)
**Author:** @gheljenor **Date:** 2022-06-07

[undefined](https://st.yandex-team.ru/undefined) - undefined

### Usage

Добавлена новая команда

```shell
yammy why publish
```

Выводит информацию о причине публикации пакетов.

# 3.1.2

**PR:** [#2587715](https://a.yandex-team.ru/review/2587715)
**Author:** @bykhovtsev **Date:** 2022-06-01

Фикс для работы `yammy watch`.

# 3.1.1

**PR:** [#2573000](https://a.yandex-team.ru/review/2573000)
**Author:** @nybble **Date:** 2022-05-24

**Добавлена проверка на пустой лог коммита [undefined](https://st.yandex-team.ru/undefined) - undefined**

# 3.1.0

**PR:** [#2549237](https://a.yandex-team.ru/review/2549237)
**Author:** @polyakovda **Date:** 2022-05-17

[[MARKETFRONTECH-4358]]
Коммитить изменения в мономаркет можно с использованием git-шарда `https://git@git.arc-vcs.yandex-team.ru/monomarket`.

Базовая ветка у него `origin/trunk`. Вношу соотвествующие правки чтобы корректно отрабатывали прекоммит-хуки.

### Usage

Изменений нет.

# 3.0.10

**PR:** [#2512392](https://a.yandex-team.ru/review/2512392)
**Author:** @gheljenor **Date:** 2022-05-04

[MARKETFRONTECH-3750](https://st.yandex-team.ru/MARKETFRONTECH-3750) - [Пуск] Sandbox-таск создания проекта из шаблона в монорепе - локальный скрипт создания сервиса

# 3.0.9

**PR:** [#2508707](https://a.yandex-team.ru/review/2508707)
**Author:** @gheljenor **Date:** 2022-04-28

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 3.0.8

**PR:** [#2503816](https://a.yandex-team.ru/review/2503816)
**Author:** @gheljenor **Date:** 2022-04-27

Использование `@yandex-market/node-root` для определения корня репозитория

### Updates

  * `@yandex-market/yammy-lib`: [1.5.4](../../lib/yammy-lib/changelog.md#154) (was [1.5.3](../../lib/yammy-lib/changelog.md#153))
  * `@yandex-market/node-root`: [1.0.1](../../tools/node-root/changelog.md#101) (was [1.0.0](../../tools/node-root/changelog.md#100))
  * `@yandex-market/s3`: [1.1.7](../s3/changelog.md#117) (was [1.1.6](../s3/changelog.md#116))

# 3.0.7

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 3.0.6

**PR:** [#1018](https://github.yandex-team.ru/market/monomarket/pull/1018)
**Author:** @gheljenor **Date:** 2022-04-11

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

### Updates

  * `@yandex-market/yammy-lib`: [1.5.3](../../lib/yammy-lib/changelog.md#153) (was [1.5.2](../../lib/yammy-lib/changelog.md#152))
  * `@yandex-market/s3`: [1.1.6](../s3/changelog.md#116) (was [1.1.5](../s3/changelog.md#115))

# 3.0.5

**PR:** [#1016](https://github.yandex-team.ru/market/monomarket/pull/1016)
**Author:** @gheljenor **Date:** 2022-04-08

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

# 3.0.4

**PR:** [#1008](https://github.yandex-team.ru/market/monomarket/pull/1008)
**Author:** @gheljenor **Date:** 2022-04-06

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.5.2](../../lib/yammy-lib/changelog.md#152) (was [1.5.1](../../lib/yammy-lib/changelog.md#151))
  * `@yandex-market/s3`: [1.1.5](../s3/changelog.md#115) (was [1.1.4](../s3/changelog.md#114))

# 3.0.3

**PR:** [#1007](https://github.yandex-team.ru/market/monomarket/pull/1007)
**Author:** @gheljenor **Date:** 2022-04-05

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

# 3.0.2

**PR:** [#992](https://github.yandex-team.ru/market/monomarket/pull/992)
**Author:** @gheljenor **Date:** 2022-04-04

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

### Updates

  * `@yandex-market/yammy-lib`: [1.5.1](../../lib/yammy-lib/changelog.md#151) (was [1.5.0](../../lib/yammy-lib/changelog.md#150))
  * `@yandex-market/s3`: [1.1.4](../s3/changelog.md#114) (was [1.1.3](../s3/changelog.md#113))

# 3.0.1

**PR:** [#979](https://github.yandex-team.ru/market/monomarket/pull/979)
**Author:** @gheljenor **Date:** 2022-03-29

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.5.0](../../lib/yammy-lib/changelog.md#150) (was [1.4.1](../../lib/yammy-lib/changelog.md#141))
  * `@yandex-market/s3`: [1.1.3](../s3/changelog.md#113) (was [1.1.2](../s3/changelog.md#112))

# 3.0.0

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

### Usage

Внешний интерфейс не изменился

### Migration

Опасный релиз. Может ломать обратную совместимость.

### Updates

  * `@yandex-market/yammy-lib`: [1.4.1](../../lib/yammy-lib/changelog.md#141) (was [1.4.0](../../lib/yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../s3/changelog.md#112) (was [1.1.1](../s3/changelog.md#111))

# 2.15.4

**PR:** [#972](https://github.yandex-team.ru/market/monomarket/pull/972)
**Author:** @gheljenor **Date:** 2022-03-28

[MARKETFRONTECH-3877](https://st.yandex-team.ru/MARKETFRONTECH-3877) - Настроить генерацию симлинков скриптами в монорепе

# 2.15.3

**PR:** [#913](https://github.yandex-team.ru/market/monomarket/pull/913)
**Author:** @gheljenor **Date:** 2022-03-03

[MARKETFRONTECH-3791](https://st.yandex-team.ru/MARKETFRONTECH-3791) - [Монорепа] падает сборка на валидации кеша при сверхбольших диффах

# 2.15.2

**PR:** [#909](https://github.yandex-team.ru/market/monomarket/pull/909)
**Author:** @gheljenor **Date:** 2022-03-03

[MARKETFRONTECH-3789](https://st.yandex-team.ru/MARKETFRONTECH-3789) - [Монорепа] frozen-lockfile не работает для workspaces

# 2.15.1

**PR:** [#910](https://github.yandex-team.ru/market/monomarket/pull/910)
**Author:** @gheljenor **Date:** 2022-03-03

[MARKETFRONTECH-3790](https://st.yandex-team.ru/MARKETFRONTECH-3790) - [Монорепа] падает очистка кеша воркспейсов

# 2.15.0

**PR:** [#883](https://github.yandex-team.ru/market/monomarket/pull/883)
**Author:** @gheljenor **Date:** 2022-02-28

Изменён сценарий `yammy validate deps` - добавлена минимальная поддержка алиасов и пакетов из гита. Поставлен приоритет различных типов и префиксов версий.

Добавлен флаг `YAMMY_NO_INSTALL` для команды `yammy link`

Добавлен сценарий `yammy ci template-generator <pkg>`

### Usage

Для генерации шаблона нужно вызвать скрипт `yammy ci template-generator <pkg>`.

В package.json'е проекта нужно заполнить секцию `config.template`:
- `dist` - директория в которую сложить шаблон
- `rsync` - rsync фильтр файлов, которые забрать в шаблон
- `any`, `standalone`, `monomarket` -  секции с оверрайдом package.json'ов. Если указать значение `null` - поле из package.json будет удалено. Сначала применяется секция `any`, затем для монорепного шаблона применяется `monomarket`, для немонорепного `standalone`. Немонорепный шаблон сохраняется в `package.standalone.json`

### Updates

  * `@yandex-market/yammy-lib`: [1.4.0](../../lib/yammy-lib/changelog.md#140) (was [1.3.0](../../lib/yammy-lib/changelog.md#130))
  * `@yandex-market/s3`: [1.1.1](../s3/changelog.md#111) (was [1.1.0](../s3/changelog.md#110))

# 2.14.12

**PR:** [#866](https://github.yandex-team.ru/market/monomarket/pull/866)
**Author:** @bykhovtsev **Date:** 2022-02-24

Обновление скрипта watch.

Для некоторых пакетов недостаточно только dist, полученного из генератора.
Таким пакетом является mandrel. В ходе своей сборки он генерирует, а потом удаляет
папку build. Эта папка тригерит `nodemon` на очередную пересборку, которая опять создаст 
папку build - бесконечный цикл.

Добавляем возможность расширить конфиг кастомным полем `watchIgnore`, в которое 
можно перечислить проблемные папки, на которые не нужно смотреть при пересборке.

# 2.14.11

**PR:** [#862](https://github.yandex-team.ru/market/monomarket/pull/862)
**Author:** @gheljenor **Date:** 2022-02-11

[MARKETFRONTECH-3715](https://st.yandex-team.ru/MARKETFRONTECH-3715) - [Монорепа] валидация версии ноды

# 2.14.10

**PR:** [#336](https://github.yandex-team.ru/market/monomarket/pull/336)
**Author:** @gheljenor **Date:** 2022-02-07

[MARKETFRONTECH-3151](https://st.yandex-team.ru/MARKETFRONTECH-3151) - Обновление nodejs 12 -> 14/16

# 2.14.9

**PR:** [#821](https://github.yandex-team.ru/market/monomarket/pull/821)
**Author:** @gheljenor **Date:** 2022-02-02

[MARKETFRONTECH-3259](https://st.yandex-team.ru/MARKETFRONTECH-3259) - Выбор ноды в MQ

# 2.14.8

**PR:** [#819](https://github.yandex-team.ru/market/monomarket/pull/819)
**Author:** @gheljenor **Date:** 2022-02-02

[MARKETFRONTECH-3259](https://st.yandex-team.ru/MARKETFRONTECH-3259) - Выбор ноды в MQ

# 2.14.7

**PR:** [#818](https://github.yandex-team.ru/market/monomarket/pull/818)
**Author:** @gheljenor **Date:** 2022-02-01

[MARKETFRONTECH-3259](https://st.yandex-team.ru/MARKETFRONTECH-3259) - Выбор ноды в MQ

# 2.14.6

**PR:** [#810](https://github.yandex-team.ru/market/monomarket/pull/810)
**Author:** @gheljenor **Date:** 2022-01-31

[MARKETFRONTECH-3151](https://st.yandex-team.ru/MARKETFRONTECH-3151) - [Монорепа] Обновление nodejs 12 -> 14/16

# 2.14.5

**PR:** [#689](https://github.yandex-team.ru/market/monomarket/pull/689)
**Author:** @b-bari **Date:** 2021-12-20

Yammy теперь может устанавливать npm пакеты в названии которых присутствует точка.

# 2.14.4

**PR:** [#593](https://github.yandex-team.ru/market/monomarket/pull/593)
**Author:** @juleari **Date:** 2021-11-26

[MARKETFRONTECH-3419](https://st.yandex-team.ru/MARKETFRONTECH-3419) - Починить проверку версионирования

# 2.14.3

**PR:** [#594](https://github.yandex-team.ru/market/monomarket/pull/594)
**Author:** @nybble **Date:** 2021-11-26

Обновление зависимостей

### Updates

  * `@yandex-market/s3`: [1.1.0](../s3/changelog.md#110) (was [1.0.9](../s3/changelog.md#109))

# 2.14.2

**PR:** [#544](https://github.yandex-team.ru/market/monomarket/pull/544)
**Author:** @fenruga **Date:** 2021-11-25

Не падаем, если не указан тикет

# 2.14.1

**PR:** [#556](https://github.yandex-team.ru/market/monomarket/pull/556)
**Author:** @juleari **Date:** 2021-11-19

[MARKETFRONTECH-3371](https://st.yandex-team.ru/MARKETFRONTECH-3371) - [Монорепа] починить ошибку с terminal-link

### Updates

  * `@yandex-market/yammy-lib`: [1.3.0](../../lib/yammy-lib/changelog.md#130) (was [1.2.1](../../lib/yammy-lib/changelog.md#121))
  * `@yandex-market/s3`: [1.0.9](../s3/changelog.md#109) (was [1.0.8](../s3/changelog.md#108))

# 2.14.0

**PR:** [#542](https://github.yandex-team.ru/market/monomarket/pull/542)
**Author:** @juleari **Date:** 2021-11-15

[MARKETFRONTECH-3168](https://st.yandex-team.ru/MARKETFRONTECH-3168) - [Монорепа] Улучшить локальное тестирование

### Usage

`yammy test-only <pkg> <testName1> ... <testNameN>`

### Updates

  * `@yandex-market/yammy-lib`: [1.2.1](../../lib/yammy-lib/changelog.md#121) (was [1.2.0](../../lib/yammy-lib/changelog.md#120))
  * `@yandex-market/s3`: [1.0.8](../s3/changelog.md#108) (was [1.0.7](../s3/changelog.md#107))

# 2.13.1

**PR:** [#548](https://github.yandex-team.ru/market/monomarket/pull/548)
**Author:** @juleari **Date:** 2021-11-13

fix typo in tips

# 2.13.0

**PR:** [#533](https://github.yandex-team.ru/market/monomarket/pull/533)
**Author:** @juleari **Date:** 2021-11-09

[MARKETFRONTECH-3169](https://st.yandex-team.ru/MARKETFRONTECH-3169) - [Монорепа] Добавить команду invalidate-only

### Usage

`yammy invalidate-only <pkg> <build1> ... <buildN>`

Например:
`yammy invalidate-only market-billing-admin version app`

# 2.12.0

**PR:** [#522](https://github.yandex-team.ru/market/monomarket/pull/522)
**Author:** @juleari **Date:** 2021-11-09

[MARKETFRONTECH-3167](https://st.yandex-team.ru/MARKETFRONTECH-3167) - [Монорепа] tip-of-the-day

### Usage

yammy tip-of-the-day <type>
yammy tips-of-the-day <type>

Для добавления подсказок нового типа необходимо создать отдельный файл в папке tips и подключить его в tips/index.js.

### Updates

  * `@yandex-market/yammy-lib`: [1.2.0](../../lib/yammy-lib/changelog.md#120) (was [1.1.9](../../lib/yammy-lib/changelog.md#119))
  * `@yandex-market/s3`: [1.0.7](../s3/changelog.md#107) (was [1.0.6](../s3/changelog.md#106))

# 2.11.3

**PR:** [#527](https://github.yandex-team.ru/market/monomarket/pull/527)
**Author:** @juleari **Date:** 2021-11-09

[MARKETFRONTECH-3340](https://st.yandex-team.ru/MARKETFRONTECH-3340) - [Монорепа] Yammy портит git stash в прекоммит-хуке

### Updates

  * `@yandex-market/yammy-lib`: [1.1.9](../../lib/yammy-lib/changelog.md#119) (was [1.1.8](../../lib/yammy-lib/changelog.md#118))
  * `@yandex-market/s3`: [1.0.6](../s3/changelog.md#106) (was [1.0.5](../s3/changelog.md#105))

# 2.11.2

**PR:** [#529](https://github.yandex-team.ru/market/monomarket/pull/529)
**Author:** @juleari **Date:** 2021-11-09

[MARKETFRONTECH-3163](https://st.yandex-team.ru/MARKETFRONTECH-3163) - [Монорепа] поправить вывод ошибки в yammy validate branch

# 2.11.1

**PR:** [#530](https://github.yandex-team.ru/market/monomarket/pull/530)
**Author:** @gheljenor **Date:** 2021-11-09

[MARKETFRONTECH-3345](https://st.yandex-team.ru/MARKETFRONTECH-3345) - [Монорепа] поломалась сборка brotli

# 2.11.0

**PR:** [#442](https://github.yandex-team.ru/market/monomarket/pull/442)
**Author:** @juleari **Date:** 2021-11-02

Добавилась комманда tickets, которая выдаёт список тикетов, попавших в релиз

### Usage

```yammy tickets```
```YAMMY_RELEASE: {pkg_name} yammy tickets``` -- для получения списка тикетов, связанных с конкретным пакетом и теми пакетами, от которых он зависит.

### Updates

  * `@yandex-market/yammy-lib`: [1.1.8](../../lib/yammy-lib/changelog.md#118) (was [1.1.7](../../lib/yammy-lib/changelog.md#117))
  * `@yandex-market/s3`: [1.0.5](../s3/changelog.md#105) (was [1.0.4](../s3/changelog.md#104))

# 2.10.12

**PR:** [#492](https://github.yandex-team.ru/market/monomarket/pull/492)
**Author:** @gheljenor **Date:** 2021-10-29

[MARKETFRONTECH-3310](https://st.yandex-team.ru/MARKETFRONTECH-3310) - [Монорепа] На логрусе падает sky-copier

# 2.10.11

**PR:** [#478](https://github.yandex-team.ru/market/monomarket/pull/478)
**Author:** @juleari **Date:** 2021-10-25

[MARKETFRONTECH-3297](https://st.yandex-team.ru/MARKETFRONTECH-3297) - Починить ченжлоги в тикетах

# 2.10.10

**PR:** [#423](https://github.yandex-team.ru/market/monomarket/pull/423)
**Author:** @juleari **Date:** 2021-10-21

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.1.7](../../lib/yammy-lib/changelog.md#117) (was [1.1.6](../../lib/yammy-lib/changelog.md#116))
  * `@yandex-market/s3`: [1.0.4](../s3/changelog.md#104) (was [1.0.3](../s3/changelog.md#103))

# 2.10.9

**PR:** [#432](https://github.yandex-team.ru/market/monomarket/pull/432)
**Author:** @gheljenor **Date:** 2021-10-11

[MARKETFRONTECH-3248](https://st.yandex-team.ru/MARKETFRONTECH-3248) - [Монорепа] не пишем ярн-кеш в ramfs

# 2.10.8

**PR:** [#418](https://github.yandex-team.ru/market/monomarket/pull/418)
**Author:** @juleari **Date:** 2021-10-05

[MARKETFRONTECH-3223](https://st.yandex-team.ru/MARKETFRONTECH-3223) - [Монорепа] фильтровать ченжлог в релизном пайплайне

# 2.10.7

**PR:** [#399](https://github.yandex-team.ru/market/monomarket/pull/399)
**Author:** @gheljenor **Date:** 2021-10-05

Не падаем с ошибкой если .nvmrc отсутствует

# 2.10.6

**PR:** [#371](https://github.yandex-team.ru/market/monomarket/pull/371)
**Author:** @gheljenor **Date:** 2021-09-21

Удалены лишние скрипты

# 2.10.5

**PR:** [#343](https://github.yandex-team.ru/market/monomarket/pull/343)
**Author:** @gheljenor **Date:** 2021-09-15

[MARKETFRONTECH-3161](https://st.yandex-team.ru/MARKETFRONTECH-3161) - [Монорепа] всяческие правки yammy

- добавилась проверка версии ноды
- добавилась проверка актуальности yarn.lock в CI
- немножко правок кодстайла

# 2.10.4

**PR:** [#220](https://github.yandex-team.ru/market/monomarket/pull/220)
**Author:** @fenruga **Date:** 2021-09-08

Обновление зависимостей

### Updates

  * `@yandex-market/cilt`: [1.1.2](../../lib/cilt/changelog.md#112) (was [1.1.1](../../lib/cilt/changelog.md#111))

# 2.10.3

**PR:** [#297](https://github.yandex-team.ru/market/monomarket/pull/297)
**Author:** @gheljenor **Date:** 2021-09-06

[MARKETFRONTECH-3101](https://st.yandex-team.ru/MARKETFRONTECH-3101) - Убрать удаление .yarn-cache при билде

Удаляем кеш workspaces - он на 100% лишний и бажный.

# 2.10.2

**PR:** [#291](https://github.yandex-team.ru/market/monomarket/pull/291)
**Author:** @dgudenkov **Date:** 2021-09-02

- удаляем .yarn-cache перед билдом

# 2.10.1

**PR:** [#284](https://github.yandex-team.ru/market/monomarket/pull/284)
**Author:** @juleari **Date:** 2021-08-30

Починила `yammy start` без аргумента `server`

# 2.10.0

**PR:** [#282](https://github.yandex-team.ru/market/monomarket/pull/282)
**Author:** @gheljenor **Date:** 2021-08-27

[MARKETFRONTECH-3083](https://st.yandex-team.ru/MARKETFRONTECH-3083) - [Монорепа] алиас my

### Usage

Теперь можно делать так:

```shell
yammy build-only my client server
```

# 2.9.0

**PR:** [#253](https://github.yandex-team.ru/market/monomarket/pull/253)
**Author:** @dimakomkov **Date:** 2021-08-27

Создана команда `yammy build-only` , которая будет запускать сборки вида build:build-name

### Usage

`yammy build-only <pkg> <build1> <build2> ... <buildN>`

# 2.8.16

**PR:** [#280](https://github.yandex-team.ru/market/monomarket/pull/280)
**Author:** @gheljenor **Date:** 2021-08-26

[MARKETFRONTECH-3080](https://st.yandex-team.ru/MARKETFRONTECH-3080) - [Монорепа] Сломался прогрев yatool

# 2.8.15

**PR:** [#251](https://github.yandex-team.ru/market/monomarket/pull/251)
**Author:** @gheljenor **Date:** 2021-08-17

Не собираем в слой сборки, случайно сгенерившиеся `publish.json` и `release.md` файлы

# 2.8.14

**PR:** [#247](https://github.yandex-team.ru/market/monomarket/pull/247)
**Author:** @gheljenor **Date:** 2021-08-16

[MARKETFRONTECH-3015](https://st.yandex-team.ru/MARKETFRONTECH-3015) - [Монорепа] Не апдейтить хеши

# 2.8.13

**PR:** [#244](https://github.yandex-team.ru/market/monomarket/pull/244)
**Author:** @gheljenor **Date:** 2021-08-13

Фиксим инвалидацию сборок

# 2.8.12

**PR:** [#240](https://github.yandex-team.ru/market/monomarket/pull/240)
**Author:** @gheljenor **Date:** 2021-08-12

[MARKETFRONTECH-3008](https://st.yandex-team.ru/MARKETFRONTECH-3008) - [Монорепа] отключить jail -- удалена вся логика про jail

# 2.8.11

**PR:** [#236](https://github.yandex-team.ru/market/monomarket/pull/236)
**Author:** @gheljenor **Date:** 2021-08-12

[MARKETFRONTECH-3007](https://st.yandex-team.ru/MARKETFRONTECH-3007) - [Монорепа] улучшить import репозиториев

# 2.8.10

**PR:** [#232](https://github.yandex-team.ru/market/monomarket/pull/232)
**Author:** @gheljenor **Date:** 2021-08-11

Исправлена ошибка генерации carrier-бандла в CI x2

# 2.8.9

**PR:** [#230](https://github.yandex-team.ru/market/monomarket/pull/230)
**Author:** @gheljenor **Date:** 2021-08-11

Исправлена ошибка генерации carrier-бандла в CI

# 2.8.8

**PR:** [#207](https://github.yandex-team.ru/market/monomarket/pull/207)
**Author:** @juleari **Date:** 2021-08-09

Добавила разные кеши для разных видов сборок
Добавилась возможность не собирать пакет перед run'ом, с помощью указания команды в поле config.noAutoBuild в package.json.

# 2.8.7

**PR:** [#222](https://github.yandex-team.ru/market/monomarket/pull/222)
**Author:** @juleari **Date:** 2021-08-09

[MARKETFRONTECH-2993](https://st.yandex-team.ru/MARKETFRONTECH-2993) - [Монорепа] Починить ссылки в ченжлогах

# 2.8.6

**PR:** [#219](https://github.yandex-team.ru/market/monomarket/pull/219)
**Author:** @gheljenor **Date:** 2021-08-06

[MARKETFRONTECH-2992](https://st.yandex-team.ru/MARKETFRONTECH-2992) - [Монорепа] фикс нпма

# 2.8.5

**PR:** [#217](https://github.yandex-team.ru/market/monomarket/pull/217)
**Author:** @dgudenkov **Date:** 2021-08-06

Временный фикс разъехавшихся чексумм

# 2.8.4

**PR:** [#215](https://github.yandex-team.ru/market/monomarket/pull/215)
**Author:** @gheljenor **Date:** 2021-08-04

[MARKETFRONTECH-2974](https://st.yandex-team.ru/MARKETFRONTECH-2974) - [Монорепа] Убираем скрипты из генерируемых пакетов

- плюс исправлена ошибка построения оптимизированного графа сборки

# 2.8.3

**PR:** [#214](https://github.yandex-team.ru/market/monomarket/pull/214)
**Author:** @gheljenor **Date:** 2021-08-04

[MARKETFRONTECH-2777](https://st.yandex-team.ru/MARKETFRONTECH-2777) - [Монорепа] Мультисборка - накладывающиеся артефакты

Не собираем заглушки bin-файлов чтобы они не игнорились при сборке.

# 2.8.2

**PR:** [#203](https://github.yandex-team.ru/market/monomarket/pull/203)
**Author:** @dimakomkov **Date:** 2021-08-03

* Добавлена проверка конфига времени билда в `yammy validate`
* Добавлена проверка при которой если есть `ci:build:<name>` и `ci:build` одновременно, валидатор выведет ошибку
* Добавлена проверка на существования конфига билда

# 2.8.1

**PR:** [#201](https://github.yandex-team.ru/market/monomarket/pull/201)
**Author:** @gheljenor **Date:** 2021-08-02

- Изменение версий зависимостей 
- Исправление ошибок `yammy setup` и `yammy validate`

# 2.8.0

**PR:** [#199](https://github.yandex-team.ru/market/monomarket/pull/199)
**Author:** @juleari **Date:** 2021-07-30

[MARKETFRONTECH-2906](https://st.yandex-team.ru/MARKETFRONTECH-2906) - [Монорепа] Пятая миля - локальная селективная сборка

Добавлена возможность собирать пакеты не только при помощи `build`, но и при помощи `build:<YAMMY_BUILD>` скриптов. Добавлена возможность вынужденно собирать `build:<YAMMY_BUILD>` с помощью переменной окружения `YAMMY_BUILD_STRICT`.

### Usage

`YAMMY_BUILD=version YAMMY_BUILD_STRICT=1 yammy build market-billing-admin`

При указании переменной окружения `YAMMY_BUILD` проект (и все проекты из зависимостей, в случае `strategy == 'deep'`) будет пытаться собраться с помощью скрипта `build:<YAMMY_BUILD>` из секции `scripts` `package.lson`'а проекта. В случае неуспеха пакеты будут собираться с помощью `build`.

При указании переменной окружения `YAMMY_BUILD_STRICT`, отсутствие скрипта `build:<YAMMY_BUILD>` будет считаться ошибкой.
`YAMMY_BUILD_STRICT` может принимать следующие значения:
    * `1` -- тогда наличие скрипта обязательно для самомго пакета и всех его зависимостей, в случае `strategy == 'deep'`.
    * `(<pkg>,)*<pkg> -- набор пакетов, разделённых запятой` -- тогда наличие скрипта обязательно только для тех пакетов, которые указаны в списке и являются необходимыми для сборки. Остальные пакеты будут собираться с помощью `build`, если `build:<YAMMY_BUILD>` для них не найдётся.


Пример:
Допустим, нам нужно собрать пакет `A`.
У пакета `A` есть зависимости `B` и `C`.

У пакета `A` есть скрипты `build` и `build:X`.
У пакета `B` есть скрипты `build` и `build:Y`.
У пакета `C` есть только `build`.

Тогда
`YAMMY_BUILD_STRICT=1 YAMMY_BUILD=X yammy build A deep`
упадёт, потому что у пакетов `B` и `C` нет скрипта `build:X`.

`YAMMY_BUILD_STRICT=B YAMMY_BUILD=X yammy build A deep`
упадёт, потому что у пакета `B` нет скрипта `build:X`.

`YAMMY_BUILD_STRICT=B YAMMY_BUILD=Y yammy build A deep`
пройдёт, выполнив `build:Y` для `B`, `build` для `C` и `A`.

`YAMMY_BUILD=X yammy build A deep`
пройдёт, выполнив `build` для `B` и для `C`, затем `build:X` для `A`

`YAMMY_BUILD=Z yammy build A deep`
пройдёт, выполнив везде `build`, потому что `YAMMY_BUILD_STRICT` не задан.

# 2.7.0

**PR:** [#196](https://github.yandex-team.ru/market/monomarket/pull/196)
**Author:** @juleari **Date:** 2021-07-28

[MARKETFRONTECH-2907](https://st.yandex-team.ru/MARKETFRONTECH-2907) - [Монорепа] Пятая миля - локальный запуск

Появилась команда `yammy start <pkg> [<server>]`. Команда должна запускать скрипт `start` или `start:<server>`, если указан параметр `server`.

В валидацию пакетов добавлена проверка, что если задан хотя бы один сценарий `start:...`, то запрещаем иметь сценарий `start`.

### Usage

`yammy start <pkg> [<server>]`

# 2.6.2

**PR:** [#195](https://github.yandex-team.ru/market/monomarket/pull/195)
**Author:** @gheljenor **Date:** 2021-07-27

[MARKETFRONTECH-2930](https://st.yandex-team.ru/MARKETFRONTECH-2930) - [Монорепа] правильно отображаем перки публикации

# 2.6.1

**PR:** [#190](https://github.yandex-team.ru/market/monomarket/pull/190)
**Author:** @gheljenor **Date:** 2021-07-26

[MARKETFRONTECH-2915](https://st.yandex-team.ru/MARKETFRONTECH-2915) - [Монорепа] Куча мелких доработок

# 2.6.0

**PR:** [#189](https://github.yandex-team.ru/market/monomarket/pull/189)
**Author:** @gheljenor **Date:** 2021-07-26

- Изменён формат описания времени сборки
- [MARKETFRONTECH-2777](https://st.yandex-team.ru/MARKETFRONTECH-2777): [Монорепа] Мультисборка - накладывающиеся артефакты
- Добавлена возможность указывать локальную зависимость CI-сборок
- Добавлены команды для быстрой настройки основных фич
- Изменён порядок вызова валидаторов
- Поправлена валидация описаний для генерируемых пакетов
- Убран лишний патч

### Usage

Можно добавить кофиг `config.build.<buildName1>.dependsOn = [<buildName2>, <buildName2>]` - в этом случае сборка buildName1 будет запущена только после завершения buildName2 и buildName3

```shell
# Настройка eslint
yammy setup eslint <pkg>

# Настройка typescript
yammy setup typescript <pkg>

# Настройка flow
yammy setup flow <pkg>

# Настройка jest
yammy setup jest <pkg>

# Автоопределение и настройка фичей
yammy setup auto <pkg>
```

### Updates

  * `@yandex-market/s3`: [1.0.3](../s3/changelog.md#103) (was [1.0.2](../s3/changelog.md#102))

# 2.5.2

**PR:** [#185](https://github.yandex-team.ru/market/monomarket/pull/185)
**Author:** @gheljenor **Date:** 2021-07-21

[MARKETFRONTECH-2887](https://st.yandex-team.ru/MARKETFRONTECH-2887) - [Монорепа] Селективные билды

**FIX:** При рефакторинге вывалилась логика про генерируемые пакеты

# 2.5.1

**PR:** [#182](https://github.yandex-team.ru/market/monomarket/pull/182)
**Author:** @gheljenor **Date:** 2021-07-21

[MARKETFRONTECH-2887](https://st.yandex-team.ru/MARKETFRONTECH-2887) - [Монорепа] Селективные билды

# 2.5.0

**PR:** [#169](https://github.yandex-team.ru/market/monomarket/pull/169)
**Author:** @kaero **Date:** 2021-07-20

Добавил папку fix для импорта командой yammy import

### Usage

Как и раньше + можно выполнять команду yammy import fix [package]

# 2.4.4

**PR:** [#171](https://github.yandex-team.ru/market/monomarket/pull/171)
**Author:** @gheljenor **Date:** 2021-07-16

[MARKETFRONTECH-2509](https://st.yandex-team.ru/MARKETFRONTECH-2509) - [Монорепа] Парсить мета-инфу или выдавать какой-то простой формат хинтов

# 2.4.3

**PR:** [#165](https://github.yandex-team.ru/market/monomarket/pull/165)
**Author:** @antsa4 **Date:** 2021-07-16

Удобный вывод ошибки путей при импорте новых зависимостей

# 2.4.2

**PR:** [#167](https://github.yandex-team.ru/market/monomarket/pull/167)
**Author:** @juleari **Date:** 2021-07-15

[MARKETFRONTECH-2603](https://st.yandex-team.ru/MARKETFRONTECH-2603) - [Монорепа] Добавлять в ченжлог информацию об авторе и дату.

Фикс получения урла для pr'а

# 2.4.1

**PR:** [#162](git@github.yandex-team.ru:market/monomarket.git/pull/162)
**Author:** @juleari **Date:** 2021-07-15

[MARKETFRONTECH-2603](https://st.yandex-team.ru/MARKETFRONTECH-2603) - [Монорепа] Добавлять в ченжлог информацию об авторе и дату.

\[\[TICKET\]\] в описании теперь заменяется на ссылку на тикет.

# 2.4.0

Добавлен флаг скипа публикации

### Usage

В конфиг публикации ресурса можно добавить флаг skipPr и он не будет публиковаться в пайплайнах ПРов - только в релизных пайплайнах

### Updates

  * `@yandex-market/yammy-lib`: [1.1.6](../../lib/yammy-lib/changelog.md#116) (was [1.1.5](../../lib/yammy-lib/changelog.md#115))
  * `@yandex-market/s3`: [1.0.2](../s3/changelog.md#102) (was [1.0.1](../s3/changelog.md#101))

# 2.3.0

- Доработана команда подготовки статики для s3
- Добавлена команда загрузки статики на s3

### Usage

```shell
yammy ci s3-prepare <src> # подготавливает статику в директории src
yammy ci s3-upload <bucket> <prefix> # берёт статику из DIST_DIR
```

### Updates

  * `@yandex-market/yammy-lib`: [1.1.5](../../lib/yammy-lib/changelog.md#115) (was [1.1.4](../../lib/yammy-lib/changelog.md#114))
  * `@yandex-market/s3`: [1.0.1](../s3/changelog.md#101) (was [1.0.0](../s3/changelog.md#100))

# 2.2.2

Уменьшаем уровень заголовков с версией.

# 2.2.1

Фикс вычисления ченжлога для envy

# 2.2.0

Добавлена команда для формирования ченжлогов для тикетов envy

### Usage

```bash
yammy envy-log <pkg> <from> <to>
```

# 2.1.1

Добавлена поддержка автокомплита для маков

# 2.1.0

Добавлена возможность патчить node_modules

### Usage

Все патчи живут в `lib/scripts/yammy/patch`

# 2.0.0

- Оптимизация графа сборки
- Поддержка мульти-сборки

### Usage

Граф сборки оптимизируется на основании информации о времени сборки тасок. Для проставления настроек времени сборки используется скрипт `yammy build-time <pkg>`

Чтобы настроить мультисборку нужно завести скрипты `ci:build:<buildName>`. Скрипт `ci:build` в этом случае запрещён.

### Migration

Ломает текущие сендбокс-таски. Требуется сначала выкатить обновление сендбокс-тасок.

# 1.15.0

Добавлена команда для получения топовой ревизии пакета

### Usage

`yammy tip <pkg>`

### Updates

  * `eslint-plugin-stout`: [1.0.4](../../tools/eslint-plugin-stout/changelog.md#104) (was [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103))

# 1.14.0

Добавлена команда, подготавливающая файлы к заливке на s3

### Usage

```yammy ci prepare-static-to-s3 <src> <dist>```

#### Аргументы:
<src>  -  Путь к исходной папке 
Путь до папки с файлами, которые необходимо подготовить к заливке на s3

<dist> -  Путь до папки со статикой
  Путь до папки, в которую будет размещена подготовленная статика. Путь прописывается относительно src

# 1.13.3

Исправленна ошибка: когда не указывалась версия пакета команда падала.

# 1.13.2

Обновление зависимостей

### Updates

  * `@yandex-market/cilt`: [1.1.1](../../lib/cilt/changelog.md#111) (was [1.1.0](../../lib/cilt/changelog.md#110))

# 1.13.1

- Более аккуратно фильтруем пакеты для различных сценариев
- Проверяем наличие необходимых переменных окружения

# 1.13.0

Добавляет скрипт `yammy watch`, который отслеживает изменения в пакете и его зависимостях. 
При изменениях в них пакет пересобирается.

### Usage

`yammy watch <pkg> [alone | deps | deep]`

### Updates

  * `@yandex-market/yammy-lib`: [1.1.4](../../lib/yammy-lib/changelog.md#114) (was [1.1.3](../../lib/yammy-lib/changelog.md#113))

# 1.12.1

Исправлена ошибка настройки precommit-хука при начальной установке репозитория

# 1.12.0

Доработки для сборки фронтов

### Usage

Добавлена команда `yammy ci nanny-dist`, которая подготавливает типичный ресурс приложения для RTC

```shell
yammy ci nanny-dist <pkg> <rsync-filter>
```

Где `rsync-filter` - это относительный путь до файла rsync-фильтров относительно корня пакета

# 1.11.0

MARKETFRONTECH-2439: [Монорепа] вайтлист для расползания версий зависимостей.

### Usage

Для того чтобы валидатор перестал ругаться на устаревшую версию зависимостей нужно:

1. Завести тикет на обновление версии
2. Прописать в `package.json` пакета, в котором используем устаревшую зависимость секцию `config.freeze["имя зависимости"] = "номер тикета"`.

# 1.10.0

Упаковка артефактов сборки с помощью yammy, а не сендбокса

### Usage

```shell
yammy ci pack-pkg <pkg> <target> # для сборки артефакта пакета
yammy ci pack-layer <target> # для сборки артефакта слоя
```

# 1.9.0

Разрешаем фиксировать версии внутренних зависимостей

### Usage

Для того чтобы валидатор перестал ругаться на фиксированные версии внутренних зависимостей нужно:

  1. Завести тикет на возвращение зависимости по коду 
  2. Прописать в `package.json` пакета, в котором используем фиксированную зависимость секцию `config.freeze["имя зависимости"] = "номер тикета"`.

# 1.8.9

- Добавлена проверка запрещающая тащить пакеты с нашего гитхаба

# 1.8.8

Более сильная поддержка skip-режима публикации

# 1.8.7

- Отключаем автосборку в CI
  - Добавлена переменная `YAMMY_NO_AUTOBUILD` для ручного отключения автосборки

# 1.8.6

Фикс ошибки с дефолтными значениями аргументов в которые попадают алиасы

# 1.8.5

Более надёжно чиним конкуренцию при сборке

# 1.8.4

Добавил запрет на установку внутренних пакетов через yammy add

# 1.8.3

Исправлена ошибка с конкуренцией при сборке пакета

# 1.8.2

Добавлена проверка названия ветки
Правила:
- запрещены коммиты в master, при флаге STABLE_BUILD=false
- если STABLE_BUILD=true, можно коммитить в мастер
- в имени ветки обязан быть тикет
- ветка может начинаться с префикса, например feature/[TICKET NAME]
- после тикета можно добавлять слова через -, например MARKETFRONTECH-2502-fixes
- длина названия ветки ограничена 38 символами

# 1.8.1

Добавлены алиасы на пакеты, чтобы не писать лишний раз префиксы

### Updates

  * `@yandex-market/cilt`: [1.1.0](../../lib/cilt/changelog.md#110) (was [1.0.4](../../lib/cilt/changelog.md#104))

# 1.8.0

Исправлен порядок инициализации. Теперь pwd всегда возвращает актуальный путь.

Добавлена валидация совместимости глобальной и локальных версий ямми

### Usage

В `bin/init.js` можно добавлять правила валидации на совместимость глобальной и локальной версии.

# 1.7.1

[MARKETFRONTECH-2505: [Монорепа] Трерья миля - продовые нод-модули](https://st.yandex-team.ru/MARKETFRONTECH-2505)

Во время CI сборки кладём продовые нод-модули в node_modules-prod

# 1.7.0

[MARKETFRONTECH-2510: [Монорепа] Поддержка skip режима публикации](https://st.yandex-team.ru/MARKETFRONTECH-2510)

### Usage

Добавлена возможность указать skip в publish.json - при этом новая версия опубликована не будет

# 1.6.0

Добавлена автосборка пакетов и кеширование результатов сборки

### Usage

Команда build кеширует результат сборки. При сборке из того же состояния репозитория ничего пересобираться не будет. Для инвалидации кеша сборки есть 3 метода:
  
  - отредактировать/удалить файл .build-hash.json
  - вызвать команду `yammy invalidate <pkgs...>`
  - выставить переменную окружения `YAMMY_INVALIDATE` - значения `1` и `all` инвалидируют все кеши. Также можно напрямую указать название пакета кеш которого требуется инвалидировать (только одного пакета).

Теперь `yammy build deep` будет автоматически вызываться при запуске команд `yammy run`, `yammy each`, `yammy test`

# 1.5.1

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.1.3](../../lib/yammy-lib/changelog.md#113) (was [1.1.2](../../lib/yammy-lib/changelog.md#112))

# 1.5.0

[MARKETFRONTECH-2522: [Монорепа] Трерья миля - продумать сценарий реверта](https://st.yandex-team.ru/MARKETFRONTECH-2522)

### Usage

```bash
yammy revert <merge-commit>
```

**ВАЖНО:** мёржить в мастер напрямую эту ветку нельзя - её можно мёржить только через MQ
Если реверт сделан на последнем коммите, то тесты можно пропустить, если нет - то лучше дождаться отчёта о тестировании.

# 1.4.5

[MARKETFRONTECH-2497: [Монорепа] Трерья миля - переименнованные зависимости](https://st.yandex-team.ru/MARKETFRONTECH-2497)

# 1.4.4

[MARKETFRONTECH-2497: [Монорепа] Трерья миля - переименнованные зависимости](https://st.yandex-team.ru/MARKETFRONTECH-2497)

# 1.4.3

* исправлены опечатки
*

# 1.4.2

- более правильно работаем с полем bin при установке
- автоматом собираем на старте carrier для его использования из локальной инсталяции

# 1.4.1

При публикации пакетов включаем verbose логгирование чтобы удобнее расследовать проблемы

# 1.4.0

[MARKETFRONTECH-2441: [Монорепа] Трерья миля - импорт веток](https://st.yandex-team.ru/MARKETFRONTECH-2441)

### Usage

```yammy import-branch <repo> <branch>```

# 1.3.4

- Обновление версий зависимостей
- Поправлен скрипт генерации package.json для генерируемых пакетов
- Поправлен скрипт yammy clean
- Поправлено правило публикации npm-пакетов

# 1.3.3

[MARKETFRONTECH-2460: [Монорепа] Трерья миля - починить after-merge](https://st.yandex-team.ru/MARKETFRONTECH-2460)

# 1.3.2

Правки eslint'а

### Updates

  * `@yandex-market/cilt`: [1.0.4](../../lib/cilt/changelog.md#104) (was [1.0.3](../../lib/cilt/changelog.md#103))
  * `@yandex-market/yammy-lib`: [1.1.2](../../lib/yammy-lib/changelog.md#112) (was [1.1.1](../../lib/yammy-lib/changelog.md#111))
  * `eslint-plugin-stout`: [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103) (was [1.0.2](../../tools/eslint-plugin-stout/changelog.md#102))

# 1.3.1

[MARKETFRONTECH-2423: [Монорепа] Трерья миля - пофиксить внезапное падение скрипта импорта](https://st.yandex-team.ru/MARKETFRONTECH-2423)

Временное решение - форкнутый @lerna/import с фиксом на принудительное успешное завершение

# 1.3.0

[MARKETFRONTECH-2392: [Монорепа] Бандл yammy](https://st.yandex-team.ru/MARKETFRONTECH-2392)

Добавлена сборка yammy в бандл

### Usage

Используется для начальной инициализации монорепы.

```bash
.bundles/yammy up
```

# 1.2.6

* Сносим husky при импорте, чтобы он не ломал прекоммиты.
* Чуток более правильная последовательность команд
* Генерим release.md файлы для пакетов в которых апнулись зависимости

# 1.2.5

Правильно конфигурим независимость артефактов

### Updates

  * `@yandex-market/cilt`: [1.0.3](../../lib/cilt/changelog.md#103) (was [1.0.2](../../lib/cilt/changelog.md#102))
  * `@yandex-market/yammy-lib`: [1.1.1](../../lib/yammy-lib/changelog.md#111) (was [1.1.0](../../lib/yammy-lib/changelog.md#110))

# 1.2.4

Раскомментил строчку отключенную для отладки

# 1.2.3

Выводим в отладку информацию о версиях утилит
FIX: Исправлена ошибка с установкой node_modules при NODE_ENV=production

# 1.2.2

[MARKETFRONTECH-2391: [Монорепа] Оптимизация сборки - уменьшаем слой сборки](https://st.yandex-team.ru/MARKETFRONTECH-2391)

Не затаскиваем в сборочный слой собранные артефакты, которые не участвуют в тестах и т.д.

# 1.2.1

Пишем не только названия пакетов и их release-ноуты, но и тип релиза

# 1.2.0

[MARKETFRONTECH-2396: [Монорепа] Использовать release.md для описания ПРов](https://st.yandex-team.ru/MARKETFRONTECH-2396)

Добавлена команда для получения агрегированного отчёта из `release.md` файлов:
```bash
yammy describe [format]
```

### Usage

```bash
# в формате markdown
yammy describe
yammy describe md

# в формате html
yammy describe html
```

### Updates

  * `@yandex-market/yammy-lib`: [1.1.0](../../lib/yammy-lib/changelog.md#110) (was [1.0.3](../../lib/yammy-lib/changelog.md#103))

# 1.1.1

Мелкие фиксы в скриптах сборки

### Updates

  * `@yandex-market/cilt`: [1.0.2](../../lib/cilt/changelog.md#102) (was [1.0.1](../../lib/cilt/changelog.md#101))
  * `@yandex-market/yammy-lib`: [1.0.3](../../lib/yammy-lib/changelog.md#103) (was [1.0.2](../../lib/yammy-lib/changelog.md#102))

# 1.1.0

[MARKETFRONTECH-2378: [Монорепа] Трерья миля - Релиз-ноуты](https://st.yandex-team.ru/MARKETFRONTECH-2378)

Делаем генерацию релиз-ноутов для публикации пакетов

### Usage

Каждый npm-пакет, который мы редактируем в ветке требутся снабдить файлом `release.md`. В зависимости от типа релиза этот файл должен содержать секции **Desctiption**, **Usage** и **Migration** (migration только для мажора, usage для мажора и минора) именно в таком порядке. Каждая сеция пишется как заголовок 3 уровня: `### Description`. Дополнительные секции 3 уровня не допускаются. Черновик данного файла генерируется автоматически скриптом `yammy validate prepublish`. 

После вливания PR'а содержимое этого файла будет использовано для дополнения `changelog.md` файла с описаниями версий. Кроме текущих секций будет также добавлена секция с обновлёнными зависимостями и линками на их ченжлоги.

### Updates

  * `@yandex-market/yammy-lib`: [1.0.2](../../lib/yammy-lib/changelog.md#102) (was [1.0.1](../../lib/yammy-lib/changelog.md#101))
