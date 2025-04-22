# Сборка. TS/React

Исходные файлы, реализованные на ts/react технологиях собираются с помощью [tsc](https://www.typescriptlang.org/docs/handbook/compiler-options.html), [ts-node](https://www.npmjs.com/package/ts-node) и [webpack](https://webpack.js.org/).

Кроме того, в проекте используется [Табурет](https://a.yandex-team.ru/arc_vcs/frontend/packages/taburet) со своим набором webpack-плагинов, включая их [доопределения на уровне проекта](../../src/vendors/taburet/build).

- [Терминология](#Терминология)
- [Структура папок](#Структура-папок)
- [Сборка в dev](#Сборка-в-dev)
- [Сборка в testing/production](#Сборка-в-testing/production)
- [Алиасы](#алиасы)
- [Кеши](#кеши)
- [FAQ](#FAQ)
  - [Почему в проекте несколько конфигов для typescript](#Почему-в-проекте-несколько-конфигов-для-typescript)
  - [Как проверить типы локально](#Как-проверить-типы-локально)
  - [Почему не проверять типы в pre-commit хуке](#Почему-не-проверять-типы-в-pre-commit-хуке)
  - [Чем отличается webpack-сборка в dev от testing/production](#Чем-отличается-webpack-сборка-в-dev-от-testing/production)
  - [Где брать полифилы](#Где-брать-полифилы)
  - [Как посмотреть, что попало в собранную статику](#Как-посмотреть-что-попало-в-собранную-статику)
  - [Есть способ профилировать webpack-сборку](#Есть-способ-профилировать-webpack-сборку)
  - [Как проверить, что node_modules не занимают слишком много места](#Как-проверить-что-node_modules-не-занимают-слишком-много-места)

## Терминология

- **entry-файл** — исходный файл, который передается как [entry в webpack](https://webpack.js.org/concepts/entry-points/)
- **чанк** — артефакт сборки webpack, включает в себя несколько модулей (один модуль — один исходный файл)
- **main-чанк** — особый чанк, который включает в себе наиболее популярные модули проекта (см. [конфиг](../../src/vendors/taburet/build/config/main-chunk.js)), всегда доставляется на клиента

## Структура папок

```bash
├── src/
|   ├── components/ — общие React-компоненты
|   ├── experiments/ — эксперименты с фичами и компонентами
|   ├── features/ — фичи (поисковые результаты)
|   ├── lib/ — библиотеки проекта
|   ├── typings/ — общие типы
|   ├── vendors/ — доопределения библиотек из node_modules
```

В typescript-сборке участвует весь код из "src", но для ускорения используется более явное перечисление папок (см. "include" из [tsconfig.build.json](../../tsconfig.build.json)).

В webpack-сборке в качестве entry-файлов используется `features/**/*.entries/{desktop,touch-phone}.tsx` и `src/experiments/*/components.entries/{desktop,touch-phone}.ts` (см. "resolveSerpEntries" из [vendors/taburet/build/config](../../src/vendors/taburet/build/config/index.js)).

При сборке стилей используется цепочка postcss-плагинов (см. [конфиг](../../postcss.config.js)).

## Сборка в dev

В dev ts/react-код собирается внутри dev-сервера:

- серверный код шаблонов собирается за счет "ts-node" (см. `require('ts-node').register` из [configs/development/taburet](../../configs/development/taburet.js)). Собранный код не попадает на файловую систему
- клиентский код собирается webpack-ом из [отдельного dev-конфига](../../src/vendors/taburet/build/webpack.config.dev.js) в рамках [wdm](../../.config/kotik/presets/wdm.js) (Webpack Dev Middleware). Собранный код попадает в `.build/dev`

Команда для запуска dev-сервера с WDM:

> npm run dev

Для прогона hermione-тестов реализована отдельная мидлвара — [wssm](../../.config/kotik/presets/wssm.js) (Webpack Server Static Middleware). Она просто отдает собранные "wdm" файлы с диска.

Команда для прогона тестов с WSSM:

> npm run hermione:local

## Сборка в testing/production

В testing/production код собирается так:

- серверный код шаблонов собирается через tsc (см. "compileTs" из [gulp-tasks/typescript](../../.enb/gulp-tasks/typescript.js)), некоторые дополнительные файлы при этом копируются "руками". Собранный код попадает в `.build/src`
- клиентский код собирается webpack-ом из [отдельного prod-конфига](../../src/vendors/taburet/build/webpack.config.prod.js) в рамках [gulp-tasks/webpack](../../.enb/gulp-tasks/webpack.js). Собранный код попадает в `.build/static` и в `.build/assets/*.json`

Команда для сборки проекта в testing для локальных проверок:

> npm run build:testing

Она не используется в конвейере. Конвейер запускает только команды с префиксом `ci:*`. См. таску [sandbox_ci_web4_build](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_web4_build/__init__.py?rev=6897340#L77-90).

## Алиасы

Алиасы решают проблему вычисления относительного пути до модуля.
Пример: У нас в фиче есть компонент, который внутри себя рисует общий компонент из src/components. Чтобы импортировать требуемые компоненты нужно написать портянку из `../` до src или корня web4, а потом путь до модуля.

Было: ```
import { createApp } from '../../../../../components/Root/Root@desktop';
```
Стало: ```
import { createApp } from '@components/Root/Root@desktop';
```
Все алиасы можно посмотреть в [конфиге](../../tsconfig.json) (compilerOptions.paths)

Во время сборки эти алиасы подменяются на относительный путь.

### серверный код

#### dev (ts-node)

В dev модифицируется [module.resolve](../../configs/common/aliases.js), который подменяет импорты в рантайме.

#### testing/production (tsc)

В testing/production применяется [transformer](../../src/lib/taburet/packages/build/import-transformer.js), который заменяет все импорты во время сборки.

### Клиентский код

Клиентский код собирается webpack'ом, который уже поддерживает [алиасы](https://webpack.js.org/configuration/resolve/), для него сделан отдельный [конфиг](../../src/vendors/taburet/build/config/aliases.js)

## Кеши

В сборке ts-код для северных шаблонов используется оптимизация `incremental: true`, которая сохраняет результаты компиляции в `.build/tsconfig.tsbuildinfo`, ускоряя последующую компиляцию при условии, что исходные файлы изменились мало (инкрементальная компиляция).

В webpack-сборке ts-loader подключается через [cache-loader](https://www.npmjs.com/package/cache-loader) (в testing/production используется форк [ci-cache-loader](../../src/vendors/taburet/build/ci-cache-loader)), который сохраняет результаты компиляции, ускоряя последующие компиляции.

## FAQ

### Почему в проекте несколько конфигов для typescript?

- [tsconfig.json](../../tsconfig.json) - базовый конфиг, который используется в IDE и как основа для других конфигов
- [tsconfig.build.json](../../tsconfig.build.json) - конфиг, который используется при сборке
- [tsconfig.typechecking.json](../../tsconfig.typechecking.json) - конфиг, который используется для проверки типов.

### Как проверить типы локально?

Для полной проверки типов используется команда `npm run typechecking`.

В большинстве случаев для контроля типов не нужно выполнять особых действий: большинство соверменных средств IDE могут проверять файлы с которыми вы работаете на корректность типов.
Если вы поменяли часто используемый интерфейс или изменили общие типы / компоненты, то есть смысл запустить полную проверку типов локально.
Это позволит узнать о проблемы с типами оперативней, чем ждать прохождения проверки в PR.

### Почему не проверять типы в pre-commit хуке?

Web4 большой проет: проверка типов занимает много времени.
А для особых случаев всегда можно запустить [проверку локально](#Как-проверить-типы-локально)
Так же проверка типов всегда отработает в PR, что защищает проект от влития кода с некорректными типами.

### Чем отличается webpack-сборка в dev от testing/production?

|  | dev | testing/production |
|--|-----|--------------------|
| `optimization.minimizer` | нет | UglifyJsPlugin и OptimizeCSSAssetsPlugin |
| `optimization.splitChunks` | node_modules и src/lib собираются в один отдельный чанк, асинхронные модули собираются в отдельные чанки. Весь остальной код собирается в чанки entry-файлов | node_modules, src/lib и src/components собираются в отдельные чанки, в чанках entry-файлов остается только специфичный для данной фичи код
| `optimization.runtimeChunk` | да | нет, рантайм-код собирается в main-чанк (см. MainChunkPlugin) |
| `plugins` (diff) | — | HashedChunksIdsPlugin, MainChunkPlugin и AssetsJsonPlugin |

Уточнения:
- HashedChunksIdsPlugin заменяет числовые id чанков на хеши от содержимого
- MainChunkPlugin собирает main-чанк по [конфигу](../../src/vendors/taburet/build/config/main-chunk.js)
- AssetsJsonPlugin генерирует манифест-файлы (assets-файлы) для собранных чанков и "фризит" статику (см. подробности в [документации](../../src/lib/taburet/packages/build/plugins/AssetsJsonPlugin/AssetsJsonPlugin.md))

### Где брать полифилы?

Полифилы для `Set`, `Map` и `rAF` загружаются вместе React-ом c "//yastatic.net/".

Дополнительные полифилы проекта лежат в папке [src/vendors/polyfill](../../src/vendors/polyfill).

### Как посмотреть, что попало в собранную статику?

В testing/production-сборке есть возможность включить плагин [webpack-bundle-analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer) с помощью переменной окружения `BUNDLE_ANALYZER_MODE`. Поддерживаюся значения `server`, `static` и `disabled`.

Пример команды:

> BUNDLE_ANALYZER_MODE=static YENV=testing npx gulp typescript

После сборки отчет со статикой откроется в браузере автоматически.

### Есть способ профилировать webpack-сборку?

Переменная окружения `WEBPACK_SPEED_MEASURE` включает [специальный webpack-плагин](https://github.com/stephencookdev/speed-measure-webpack-plugin), замеряющий время работы разных плагинов и лоадеров. Следует использовать в задачах по оптимизации сборки.

Пример запуска:

> WEBPACK_SPEED_MEASURE=1 NODE_OPTIONS=--max_old_space_size=4096 YENV=testing npx gulp webpack

### Как проверить, что node_modules не занимают слишком много места

__Проблема__: в проде динамический пакет распаковывается на HDD и если размер пакета увеличится значительно, то распаковка может занимать слишком много времени. Например, при размере пакета ~110MB, распаковка может доходить до нескольких минут. Это замедляет релизы и время подготовки бет.

До монорепы предлагается решать проблему по мере возникновения.

Что можно сделать:
- оценить размеры установленных зависимостей: `du -sh ./node_modules/* | sort -hr`,
- оценить количество файлов по типам: `find ./node_modules/ -type f | sed -e 's/.*\.//' | sed -e 's/.*\///' | sort | uniq -c | sort -rn`,
- проверить размеры зависимостей, сгруппированных попакетно, с помощью `./tools/get-npm-deps-file-sizes.sh`,
- сравнить время распаковки после исправлений с [пакетом из CI](https://sandbox.yandex-team.ru/resources/?type=WEB_MICRO_PACKAGE&limit=20&attrs=%7B%22released%22%3A%22stable%22%7D&created=14_days),
- сделать или дождаться задачи про `npm ci --production` https://st.yandex-team.ru/SERP-106338.
