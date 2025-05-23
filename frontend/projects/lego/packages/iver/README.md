# iver 📝
-------

**Утилита для подготовки релиза:**

* Собирает все `merge`-коммиты с момента последнего изменения поля `version` в `package.json` пакета;
* На основе заголовков влитых PR собирает данные о задачах, в рамках которых были сделаны изменения, а также примечания к ним, если таковые имеются;
* Согласно `commit-messages` коммитов, входящих в `merge`-коммит, определяется "мажорность" задачи по `semver` (см. [соответствие версии и `commit-message`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/guidelines/contribs.md#conventional-commits));
* Общая версия релиза вычисляется на основе "мажорности" входящих в него задач. В некоторых случаях учитываются изменения в других пакета, см. [плагины](#plugins);
* Из заголовков задач, ссылок на PR и примечаний формирует `changelog`, разделяя изменения на мажорные, минорные и патчевые;
* Считает TRIVIAL пулреквесты не важными и пропускает публикацию пакетов для них;
* В режиме релиза проставляет `fix-version` компонент соответствующим задачам в Трекере (только для очереди `ISL`).

## Startrek-токен

Для работы утилиты необходимо получить свой [OAuth-токен](https://wiki.yandex-team.ru/tracker/api/#avtorizacija).

Полученный токен необходимо передать в виде переменной окружения или сохранить в `~/.bashrc`, `~/.zshrc` etc.

`STARTREK_TOKEN=<token>`

## Конфигурация

Утилита конфигурируется в специальном поле `iver` в `package.json` пакета.
Если поля в `package.json` нет, применятся настройки по умолчанию.

Пример:

```
  "iver": {
      "version": { "postfix": "beta" },
      "notesPath": "releases/notes ",
      "changelogPath": "releases",
      "plugins": [
          {
            "tech-deps-plugin": {
              "keyTechs": ["react.js"],
              "dependencies": {
                "packages/islands": ["css", "md", "assets", "react.js", "d.ts", "i18n"]
              }
            }
          },
          {
            "filter-tech-plugin": {
              "includeTechs": ["css", "md", "assets", "react.js", "d.ts", "i18n"]
          }}
      ]
  }
```

### `version`

В поле `version` можно указать постфикс для вашей версии. Если вы хотите версию вида `1.0.1-beta.0`, укажите `{ "postfix": "beta" }`.

**По умолчанию:** Проставляется версия без префикса.

### `notesPath`

Путь до директории, где хранятся примечания к задачам.

**По умолчанию:** `<PackageRoot>/releases/notes`.

### `changelogPath`

Путь до директории, в которой нужно сохранить `changelog`.

**По умолчанию:** `<PackageRoot>/releases/notes`.

### `plugins`
<a name="plugins"></a>

Список плагинов, которые нужно применить при определении релевантных коммитов. Если плагинов нет, применится фильтрация по умолчанию - по путям до файлов. Если плагины есть, фильтрация по путям применится последней. Плагины применяются в том порядке, в каком они указаны в конфиге. Если предыдущий плагин пометит коммит как релевантный или не-релевантный, последующие фильтры к ним применятся не будут.

`"plugins": [{ {String<PluginName>}: { "<Option>": <OptionValue> }}]`

**По умолчанию:** Коммиты будут отфильтрованы по путям.

## Расчёт версий

При вычислении версии, на которую надо бампнуть пакет, iver опирается на поле version из VCS из package.json, а так же на старшую версию опубликованную в npm (не считая prerelease-версий). За точку отстчёта берется старшая версия из двух источников.

Версия будет инкрементирована, если:

- изменения в пулл-реквесте прямо или косвенно затронули пакет;
- пакет не приватный — в `package.json` нет строки `"private": true`;
- в заголовке пулл-реквеста не указано ключевое слово `TRIVIAL`;
- в сообщениях коммитов пулл-реквеста (commit messages) есть хотя бы одно изменение, подходящее под инкремент версии согласно [Conventional Commits][conventional-commits].

Версия НЕ будет инкрементирована, если:

- пакет приватный и не является сервисом с настройкой `"autobumpversion": true` в `package.json`;
- в заголовке пулл-реквеста указано ключевое слово `TRIVIAL`;
- в сообщениях коммитов пулл-реквеста (commit messages) были указаны незначительные изменения: `build`, `chore`, `ci`, `docs`, `style`, `refactor`, `perf`, `test` и тому подобное. См. [Conventional Commits][conventional-commits].

## Плагины

### `tech-deps-plugin`

Плагин, который позволяет учитывать зависимость пакета от технологий другого пакета.
Например, пакет `lego-on-react` собирается из исходников пакета `islands`. Т.е. если были минорные изменения, например, в технологии `react.js`, для `lego-on-react` это также означает минор, а не патч.

В качестве опций для плагина указывается ключевая технология, а также список зависимостей вида:

`{String<PathToDependency>}: {Array<DependencyTechs>}`

Ключевая технология (`keyTech`) указывается для того, чтобы в выборку не попали компоненты, не реализованные в нужной технологии. Так, например, у блока `auth` есть `css`, но его нет в `react`-реализации, значит, учитывать его в изменения `lego-on-react` не нужно. А у блока `button2` есть `react`-реализация, следовательно, изменения в его `css` являются значимыми.

То есть, например:

```
  {
    "keyTechs": ["react.js"],
    "dependencies": {
      "packages/islands": ["css", "assets", "md", "react.js", "d.ts", "i18n"]
    }
  }
```
Если ключевая технология не указана, то будут учтены изменения для казанных технологий для всех БЭМ-сущности.

**Важно:** Пожалуйста, указывайте такие зависимости в `devDependencies` в `package.json` пакета, даже если эти зависимости используются только при сборке! В противном случае при построении графа зависимостей такая зависимость не будет учтена (используется `@lerna/package-graph`).

**В  качестве зависимостей указываются пакеты монорепозитория с файловой структурой по БЭМ, у которых  в корне есть `.bemrc.js`. Пожалуйста, убедитесь, что `.bemrc.js` корректно работает с `@bem/sdk.config@0.0.10` и `@bem/sdk.walk@0.6.0`**

### `filter-tech-plugin`

Плагин, который позволяет указать "white list" значимых технологий для пакета. К сожалению, нельзя гарантировать, что изменения в `hermione.js` не будут входить в коммит с типом `feat`, поэтому плагин предоставляет дополнительную страховку.

В качестве опций для плагина указывается список технологий вида:

`"includeTechs": {Array<Techs>}`

**Важно:** Изменения в `package.json` и `package-lock.json` учитываются всегда.

## Опции

Доступные опции:

* `--ci`
* `--release`
* `--first-step`
* `--since`
* `--till`
* `--dry-run`
* `--fix-version`

### `ci`

В режиме `ci` утилита не взаимодействует с пользователем. Пытается собрать примечания к релизу из минимального количества данных и выбрасывает ошибки только в случае, если дальнейшая работа невозможна ни в каком виде.

Например, в отличие об обычного режима, продолжит работу в случае, если:

- Обнаружатся PR с некорректным названием;
- Если не удалось получить полную информацию по задаче из Трекера

**По умолчанию добавляет к проставленной версии `-canary.<LastCommitHash>-<Date>`.**

### `release`

Этот флаг предполагается использовать совместно с флагом `ci`.
Нужен для того, чтобы **выпускать необходимо стабильную** и проставлять версию в Трекере.

### `first-step`

Дает возможность указать шаг, с которого нужно начать подготовку релиза (предполагается использовать в "ручном" режиме).

### `since`

Указание с какого коммита считать дифф.
По умолчанию используется последний тег.

### `till`

Указание до какого коммита считать дифф.
По умолчанию проверяется всё до текущего момента.

### `dry-run`

В этом режиме iver не будет оставлять артефакты, а только скажет, что изменилось.
Iver пропустит:
- проставку версию через `npm version ....`
- обновление package.json измененного пакета и зависимых
- генерацию примечаний к релизу и сохранению их на файловой системе
- создание и установку компонента Fix Version в трекере.

### `fix-version`

Флаг для включения создания и установки версии в Трекере. Устанавливает версию в поле Fix Version (только для очереди ISL).
Используется совместно с `release`.

## Команды

### `check-release`

Позволяет запустить `iver` в режиме проверки "мажорности" PR и наличия-отсутствия у него `release-notes`.
Используется в качестве линтера в `islands`.

[conventional-commits]: https://www.conventionalcommits.org/en/v1.0.0/#summary
