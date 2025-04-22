# 3.0.13

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 3.0.12

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

# 3.0.11

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))

# 3.0.10

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

# 3.0.9

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

Обновление зависимостей

# 3.0.8

**PR:** [#320](https://github.yandex-team.ru/market/monomarket/pull/320)
**Author:** @ashwets **Date:** 2021-09-15

Обновление зависимостей

# 3.0.7

**PR:** [#209](https://github.yandex-team.ru/market/monomarket/pull/209)
**Author:** @pavelko95 **Date:** 2021-09-15

Обновление зависимостей

# 3.0.6

**PR:** [#206](https://github.yandex-team.ru/market/monomarket/pull/206)
**Author:** @antonk52 **Date:** 2021-09-06

Обновление зависимостей

# 3.0.5

**PR:** [#207](https://github.yandex-team.ru/market/monomarket/pull/207)
**Author:** @juleari **Date:** 2021-08-09

Обновление зависимостей

# 3.0.4

**PR:** [#222](https://github.yandex-team.ru/market/monomarket/pull/222)
**Author:** @juleari **Date:** 2021-08-09

[MARKETFRONTECH-2993](https://st.yandex-team.ru/MARKETFRONTECH-2993) - [Монорепа] Починить ссылки в ченжлогах

# 3.0.3

**PR:** [#215](https://github.yandex-team.ru/market/monomarket/pull/215)
**Author:** @gheljenor **Date:** 2021-08-04

[MARKETFRONTECH-2974](https://st.yandex-team.ru/MARKETFRONTECH-2974) - [Монорепа] Убираем скрипты из генерируемых пакетов

# 3.0.2

**PR:** [#201](https://github.yandex-team.ru/market/monomarket/pull/201)
**Author:** @gheljenor **Date:** 2021-08-02

Актуализация времени сборки

# 3.0.1

**PR:** [#189](https://github.yandex-team.ru/market/monomarket/pull/189)
**Author:** @gheljenor **Date:** 2021-07-26

Изменён формат описания времени сборки

# 3.0.0

**PR:** [#176](https://github.yandex-team.ru/market/monomarket/pull/176)
**Author:** @avdotion **Date:** 2021-07-22

`@yandex-market/logger` на TS в монорепозитории!

### Usage

- Теперь логгер на тайпскрипте! На момент публикации TS-версия не была нигде установлена.

### Migration

- Если его тайпинги были заигнорены, теперь это не нужно;
- импорт в тайпсприпизированных модулях должен быть такой: `import * as logger from '@yandex-market/logger'` вместо `import logger from '@yandex-market/logger'`.