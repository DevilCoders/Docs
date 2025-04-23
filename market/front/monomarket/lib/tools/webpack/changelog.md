# 4.7.2

**PR:** [#2740663](https://a.yandex-team.ru/review/2740663)
**Author:** @bykhovtsev **Date:** 2022-07-18

MARKETFRONTECH-4463 Добавляем интеграцию core, template и проброс твм-тикетов

- `@yandex-market/shared` => `@yandex-market/market-shared` в опция externals white list

# 4.7.1

**PR:** [#2704008](https://a.yandex-team.ru/review/2704008)
**Author:** @robot-metatron **Date:** 2022-07-06

**Уменьшаем количество неиспользуемых зависимостей в webpack, для того, чтобы облегчик package-lock в маркетфронте [[MARKETFRONT-96587]]**

# 4.7.0

**PR:** [#2666004](https://a.yandex-team.ru/review/2666004)
**Author:** @asker-k **Date:** 2022-06-22

добавлена возможность указания пути для вебпакманифеста

### Usage

нужно в конфиг функции генератора браузера передать поле  manifestPath

# 4.6.1

**PR:** [#2650527](https://a.yandex-team.ru/review/2650527)
**Author:** @robot-metatron **Date:** 2022-06-20

Добавление @yandex-market/shared в вайтлист node-externals
[undefined](https://st.yandex-team.ru/undefined) - undefined

# 4.6.0

**PR:** [#2568922](https://a.yandex-team.ru/review/2568922)
**Author:** @gluhovroma **Date:** 2022-05-25

**Обновлен babel конфиг [[MARKETFRONT-87639]]**

### Usage

**Обновлен babel конфиг [[MARKETFRONT-87639]]**

# 4.5.0

**PR:** [#2489763](https://a.yandex-team.ru/review/2489763)
**Author:** @gluhovroma **Date:** 2022-05-05

**Обновил babel и его плагины до последних версий [[MARKETFRONT-83092]]**

### Usage

**Обновите babel в своих проектах [[MARKETFRONT-83092]]**

### Updates

  * `@yandex-market/remote-resolvers-loader`: [2.2.0](../../lib/remote-resolvers-loader/changelog.md#220) (was [2.1.1](../../lib/remote-resolvers-loader/changelog.md#211))

# 4.4.3

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 4.4.2

**PR:** [#2463243](https://a.yandex-team.ru/review/2463243)
**Author:** @a-ekhin **Date:** 2022-04-21

Обновление зависимостей

### Updates

  * `@yandex-market/remote-resolvers-loader`: [2.1.1](../../lib/remote-resolvers-loader/changelog.md#211) (was [2.1.0](../../lib/remote-resolvers-loader/changelog.md#210))

# 4.4.1

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

# 4.4.0

**PR:** [#938](https://github.yandex-team.ru/market/monomarket/pull/938)
**Author:** @kykint **Date:** 2022-03-18

Обновление зависимостей

### Updates

  * `@yandex-market/remote-resolvers-loader`: [2.1.0](../../lib/remote-resolvers-loader/changelog.md#210) (was [2.0.1](../../lib/remote-resolvers-loader/changelog.md#201))

# 4.3.1

**PR:** [#880](https://github.yandex-team.ru/market/monomarket/pull/880)
**Author:** @avdotion **Date:** 2022-02-21

- Исправлен баг, при котором не пробрасывался контекст
- Исправлен баг, при котором не работала нормализация статов
- Больше сорсы не попадают в отчет: это должно сэкономить размер отчета

# 4.3.0

**PR:** [#844](https://github.yandex-team.ru/market/monomarket/pull/844)
**Author:** @avdotion **Date:** 2022-02-08

- Обновлена версия Statoscope до `^1.20.1`.
- Теперь Статоскоп -- peer dependency. Можно управлять версией не через монорепу.
- Включена функция нормализации статов для уменьшения размера артефактов.
- `process.cwd()` -- теперь дефолтный контекст, если не передана env-переменная `STATOSCOPE_CONTEXT`.

### Usage

- Теперь `@statoscope/webpack-plugin` нужно ставить как дополнительную dev-зависимость.

# 4.2.4

**PR:** [#810](https://github.yandex-team.ru/market/monomarket/pull/810)
**Author:** @gheljenor **Date:** 2022-01-31

[MARKETFRONTECH-3151](https://st.yandex-team.ru/MARKETFRONTECH-3151) - [Монорепа] Обновление nodejs 12 -> 14/16

# 4.2.3

**PR:** [#795](https://github.yandex-team.ru/market/monomarket/pull/795)
**Author:** @xavescor **Date:** 2022-01-27

Корректно заполняем browserslist у @babel/preset-env.
До этого момента почему-то формировался не ["@babel/preset-env", options],
а ["@babel/preset-env", options, .targets]. т.е. поле targets зачем-то писали внутрь массива

# 4.2.2

**PR:** [#744](https://github.yandex-team.ru/market/monomarket/pull/744)
**Author:** @bykhovtsev **Date:** 2022-01-11

Обновляем зависимость из-за
https://github.blog/2021-09-01-improving-git-protocol-security-github/#when-are-these-changes-effective

# 4.2.1

**PR:** [#739](https://github.yandex-team.ru/market/monomarket/pull/739)
**Author:** @bykhovtsev **Date:** 2022-01-11

Убираем неиспользуемый кусок отчета, который к тому же пока не полезен и приносит даже неприятности

# 4.2.0

**PR:** [#720](https://github.yandex-team.ru/market/monomarket/pull/720)
**Author:** @bykhovtsev **Date:** 2021-12-27

- В мастере @yandex-market/webpack версия статоскопа, которая падает. Понижаем до рабочей.
- Исправлено сравнение статов из-за неверного контекста. Теперь его можно сформировать сверху.

### Usage

Для того чтобы прокинуть нужный контекст статов, его нужно передать как env-переменную `STATOSCOPE_CONTEXT`.
Таким образом пути до файлов можно формировать используя относительные пути.

# 4.1.0

**PR:** [#707](https://github.yandex-team.ru/market/monomarket/pull/707)
**Author:** @bykhovtsev **Date:** 2021-12-24

В сборку добавлена возможность форсировать часть оптимизаций. Например, тришейкинг, конкатенацию модулей и часть минификаций

### Usage

В `browser` передать опцию `forceOptimizations: true`

# 4.0.1

**PR:** [#603](https://github.yandex-team.ru/market/monomarket/pull/603)
**Author:** @bykovski-ilya **Date:** 2021-12-21

**Починил ошибку в зависимости пакета - openapi-to-bcm**

# 4.0.0

**PR:** [#672](https://github.yandex-team.ru/market/monomarket/pull/672)
**Author:** @avdotion **Date:** 2021-12-15

- Обновление зависимости Statoscope
- Теперь отчет Статоскопа поддерживает конкат-модули
- Теперь файлики отчета Статоскопа собираются с учетом имени сборки
- Удалил webpack-bundle-analyzer, он встроен в отчет Статоскопа

### Usage

Если вы используете Statoscope, обновите версии Statoscope
Важно, что теперь имена артефактов отчета Статоскопа будут отличаться

### Migration

`webpack-bundle-analyzer` больше не поддерживается, от него придется отказаться

# 3.1.2

**PR:** [#539](https://github.yandex-team.ru/market/monomarket/pull/539)
**Author:** @gheljenor **Date:** 2021-11-10

[MARKETFRONTECH-3342](https://st.yandex-team.ru/MARKETFRONTECH-3342) - package-lock.json + npm run bootstrap = большой взрыв

# 3.1.1

**PR:** [#393](https://github.yandex-team.ru/market/monomarket/pull/393)
**Author:** @avdotion **Date:** 2021-09-30

Обновление зависимостей

# 3.1.0

**PR:** [#342](https://github.yandex-team.ru/market/monomarket/pull/342)
**Author:** @avdotion **Date:** 2021-09-15

Обновление зависимостей:
- `"@statoscope/webpack-plugin": "5.8.0"`

Удалены ненужные зависимости:
- `"@statoscope/cli"`
- `"@statoscope/ui-webpack"`

### Usage

В последних версиях Statoscope поддержали правила, gui-отчет и уменьшение размера html-отчета. Подробности можно посмотреть в ченжлоге статоскопа.

# 3.0.1

**PR:** [#305](https://github.yandex-team.ru/market/monomarket/pull/305)
**Author:** @gheljenor **Date:** 2021-09-08

[MARKETFRONTECH-3121](https://st.yandex-team.ru/MARKETFRONTECH-3121) - Отключить тред-лоадер для вотч-режима

# 3.0.0

**PR:** [#249](https://github.yandex-team.ru/market/monomarket/pull/249)
**Author:** @kuvshinov-vl **Date:** 2021-08-30

Переезд в монорепу.

Обновление версий зависимостей.

### Usage

Без изменений

### Migration

Без изменений

### Updates

  * `@yandex-market/remote-resolvers-loader`: [2.0.1](../../lib/remote-resolvers-loader/changelog.md#201) (was [2.0.0](../../lib/remote-resolvers-loader/changelog.md#200))
