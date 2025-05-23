# Сборка. Gulp

Исходные файлы, реализованные на priv/bemxjst/i-bem технологиях собираются [gulp-тасками](../../.enb/gulp-tasks) (кроме тасок typescript и webpack). В тасках используются [собственные плагины](../../.enb/gulp-plugins) и [borschik](https://github.com/borschik/borschik) (он же "борщик").

- [Терминология](#Терминология)
- [Структура папок](#Структура-папок)
- [Сборка](#Сборка)
- [Кеши](#кеши)
- [Пересборка в dev-сервере](#Пересборка-в-dev-сервере)
- [FAQ](#FAQ)
  - [Какие расширения собираются gulp-ом](#Какие-расширения-собираются-gulp-ом)
  - [Можно ли "вычитать" зависимости?](#Можно-ли-вычитать-зависимости?)
- [Ссылки](#Ссылки)

## Терминология

- **Блок** — минимальная сущность проекта. Блоком с точки зрения сборки является и priv-адаптер, и блок Конструктора. Блок может быть реализован в нескольких технологиях (scss, js, priv.js и проч.) и в нескольких файлах (разбит на элементы и модификаторы)
- **Бандл** — сущность, объединяющая в себе файлы нескольких блоков, реализующих какую-то функциональность (попап, табик, иконка, фича)
- **Страница** — самая крупная сущность проекта. В проекте [несколько страниц](../../.enb/config/pages.js), основная — поисковая "search". По сути не отличается от бандла, но функциональностью является "обвязка страницы" (блоки, которые всегда присутствуют на странице)

## Структура папок

```bash
├── blocks-*/ — "доконструкторский" код
├── bundles-*/ — декларации бандлов
├── adapters/ — priv-адаптеры
├── construct/ — конструкторские блоки
├── experiments/ — экспериментальные уровня Конструктора
├── configs/ — переопределения кода для разных режимов сборки
├── pages-*/* — декларации страниц
|   ├── blocks/ — переопределения кода для разных режимов сборки
```

## Сборка

### Основные этапы сборки

Gulp-таски (любую из них можно запустить отдельно через `npx gulp ?`), собирающие priv/bemxjst/i-bem технологии:

- bem-stack
  - [build-server-i18n](../../.enb/gulp-tasks/build-server-i18n.js) — сборка всех переводов для использования в серверном коде
  - [build-adapters](../../.enb/gulp-tasks/build-adapters.js) — сборка priv-адаптеров
  - [build-priv-exp](../../.enb/gulp-tasks/build-priv-exp.js) — cборка priv-кода из `experiments/`
  - [build-exp-bundles](../../.enb/gulp-tasks/build-exp-bundles.js) — статики из `experiments/`
  - [build-expflags-allowed](../../.enb/gulp-tasks/build-expflags-allowed.js) — объединение json-деклараций флагов в один файл
  - [build-client-bemhtml](../../.enb/gulp-tasks/build-client-bemhtml.js) — сборка клиентского bemhtml-я (саджест, просмотрщик картинок на touch-phone)
  - [build-bemdecls](../../.enb/gulp-tasks/build-bemdecls.js) — раскрытие `.bemdecl.js` (бандлов и страниц) в `.deps.js`
  - [build-bemhtml](../../.enb/gulp-tasks/build-bemhtml.js) — сборка серверного bemhtml-я
  - [build-priv](../../.enb/gulp-tasks/build-priv.js) — сборка priv-кода блоков (не адаптеры)
  - [clean-deleted-bundles](../../.enb/gulp-tasks/clean-deleted-bundles.js) — очищает артефакты от предыдущих сборок.
  - [build-page-static](../../.enb/gulp-tasks/build-page-static.js) — сборка статики страниц
  - [build-additional-exp-bundles](../../.enb/gulp-tasks/build-additional-exp-bundles.js) — сборка дополнительных экспериментальных бандлов (см. [gulp-additional-exp-tasks](../../.enb/gulp-additional-exp-tasks))
  - [build-merged-bundles](../../.enb/gulp-tasks/build-merged-bundles.js) — объединяем собранную статику всех бандлов в один файл
  - [build-templates](../../.enb/gulp-tasks/build-templates.js) — собираем итоговые `wrapped-server-templates.priv.js`-файлы, которые потом подключаются в ReportRenderer как точка входа в шаблоны

При сборке стилей используется цепочка postcss-плагинов (см. подробности в [helpres/post-process-css](../../.enb/helpers/post-process-css.js)).

### Сборка тестов

- [priv-tests](../../.enb/gulp-tasks/priv-test.js) — собирает все `*.test-priv.js` в `all.test-priv.js` и запускает их
- [client-test](../../.enb/gulp-tasks/client-test.js) — собирает все `*.test.js` в `tests/_all.js` и запускает их

## Кеши

В сборке, собирающей priv/bemxjst/i-bem технологии, используется два уровня кеширования:

- в `bundles-*/build-meta.json`-файлах кешируется содержимое всех собранных бандлов (build-bundle-static) и mtime исходных файлов, которые попадают в бандлы. Далее собирается только те бандлы, у которых поменялся состав или исходные файлы (см. [реализацию](../../.enb/helpers/changed-bundles.js))
- в `pages-*/.borschik-cache.{meta,processed}.json`-файлах кешируются зависимости файлов, использующих "borschik:include", и результат раскрытия include-ов. При любом вызове "борщика" в сборке (таких много), проверяется состав и mtime зависимостей, если изменений не было — берется закешированный результат (см. [реализацию](../../.enb/helpers/borschik-cache.js))
- в `node_modules/.cache/.file-list.*.json`-файлах кешируются пути до файлов, которые используются при сборке. Для принудительного отключения кеширования можно использовать переменную окружения `DISABLE_BEM_STACK_CACHE=1`

## Пересборка в dev-сервере

### Пересборка после изменения файла

Пересборка после изменения исходного файла (**кроме "deps", "bemdecl" и "bemhtml" файлов**), выполняется [automake](../../.enb/automake)-ом.

После обновления страницы, dev-сервер обращается к статике и основному файлу шаблонов. Это обращение пропускается через automake (см. [rebuild-мидлвару](../../.config/kotik/middlewares/rebuild/index.js)), которая просто запускает внутри себя "борщик". На первом обращении отрабатывает сам "борщик" — подхватит изменения и сохранит в кеш. При следующих обращениях, если не было изменений (см. логику про кеш), будет возвращаться собранный файл.

### Пересборка после добавления/удаления файла

После добавления/удаления исходного файла **или изменения "deps"/"bemdecl" файла** выполняется полная сборка. Полная сборка проекта может использовать результаты предыдущей полной сборки для сокращения числа необходимых операций. Благодаря кешам собираются только бандлы, которых коснулись изменения.

Полную пересборку так же инициирует "rebuild"-мидлвара котика.

### Пересборка bemhtml

Борщик не смотрит за изменениями bemhtml файлов, поэтому при внесении изменений нужно запускать их сборку вручную `npm run build:bemhtml`. После этого при обновлении страницы автомейк подхватит изменения в all.bemhtml файле и применит их.

## FAQ

### Какие расширения собираются gulp-ом?

Стили:

- `.scss` — стили в синтаксисе css, расширенном за счет postcss-плагинов
- `.css` — стили на голом css, обычно там константы (цвета, размеры)

Клиентский код:

- `.js` – код, исполняемый на клиенте на основе [i-bem](https://lego.yandex-team.ru/libs/bem-bl/dev/desktop/i-bem/jsdoc/)-фреймворка
- `.{i18n,js-i18n}/*.js` — переводы для клиентского кода

Серверный код:

- `.priv.js` — код адаптеров и конструкторских (и "доконструкторских") блоков
- `.bemhtml.js` — [bem-xjst](https://github.com/bem/bem-xjst)-шаблоны
- `i18n/*.js` — переводы для клиентского кода

Декларация зависимостей:

- `.deps.js` — зависимости блоков, описанные на [технологии deps](https://ru.bem.info/platform/deps/)
- `.bemdecl.js` — декларации бандлов и страниц

Юнит-тесты:

- `.test.js` — тесты на клиентский код
- `.test-priv.js` — тесты на серверный priv-код

### Можно ли "вычитать" зависимости?

Иногда (например, в целях оптимизации) есть необходимость вычитать зависимости из бандла.
Иногда (например, при замене зависимости) может потребоваться вычитание зависимости сразу из всех бандлов.

В обоих случаях вместо запрещенного "noDeps" следует использовать "минус-deps", описанный в [конфиге сборки](../../.enb/config/deps/minus.js).

Вычитание из отдельных бандлов конфигурируется под ключом "bundles", вычитание из страниц — под ключом "pages".

Под ключом "all" перечислены зависимости, вычитаемые из всех бандлов и страниц.

Из всех бандлов основного уровня `bundles-*` всегда вычитаются зависимости основной страницы "search" для соответствующей платформы.

Формат вычитаемых сущностей:

```js
/**
 * @property {String} block
 * @property {String} [elem]
 * @property {String} [mod]
 * @property {String} [val]
 */
```

Пример:

```js
exports.deps = [
  { block: 'button' },
  { block: 'button', mod: 'theme' },
  { block: 'button', mod: 'theme', val: 'normal' },
  { block: 'button', elem: 'icon' },
  { block: 'button', elem: 'icon', mod: 'type', val: 'check' }
];
```

## Ссылки

- [основной хелпер сборки](../../.enb/helpers/project-config.js)
- [хелпер запуска борщика](../../.enb/helpers/borschik-api.js)
