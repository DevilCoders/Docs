# 1.1.8

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 1.1.7

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

# 1.1.6

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))

# 1.1.5

**PR:** [#810](https://github.yandex-team.ru/market/monomarket/pull/810)
**Author:** @gheljenor **Date:** 2022-01-31

Обновление зависимостей

### Updates

  * `@yandex-market/error`: [1.5.1](../error/changelog.md#151) (was [1.5.0](../error/changelog.md#150))

# 1.1.4

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

# 1.1.3

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

Обновление зависимостей

# 1.1.2

**PR:** [#320](https://github.yandex-team.ru/market/monomarket/pull/320)
**Author:** @ashwets **Date:** 2021-09-15

Обновление зависимостей

# 1.1.1

**PR:** [#209](https://github.yandex-team.ru/market/monomarket/pull/209)
**Author:** @pavelko95 **Date:** 2021-09-15

Обновление зависимостей

# 1.1.0

**PR:** [#313](https://github.yandex-team.ru/market/monomarket/pull/313)
**Author:** @ivan-afanasov **Date:** 2021-09-10

Обновление зависимостей

### Updates

  * `@yandex-market/error`: [1.5.0](../error/changelog.md#150) (was [1.4.6](../error/changelog.md#146))

# 1.0.5

**PR:** [#206](https://github.yandex-team.ru/market/monomarket/pull/206)
**Author:** @antonk52 **Date:** 2021-09-06

Обновление зависимостей

# 1.0.4

**PR:** [#207](https://github.yandex-team.ru/market/monomarket/pull/207)
**Author:** @juleari **Date:** 2021-08-09

Обновление зависимостей

# 1.0.3

**PR:** [#201](https://github.yandex-team.ru/market/monomarket/pull/201)
**Author:** @gheljenor **Date:** 2021-08-02

Поправлен tsconfig

# 1.0.2

**PR:** [#189](https://github.yandex-team.ru/market/monomarket/pull/189)
**Author:** @gheljenor **Date:** 2021-07-26

Изменён формат описания времени сборки

### Updates

  * `@yandex-market/error`: [1.4.6](../error/changelog.md#146) (was [1.4.5](../error/changelog.md#145))

# 1.0.1

**PR:** [#165](https://github.yandex-team.ru/market/monomarket/pull/165)
**Author:** @antsa4 **Date:** 2021-07-16

Обновление версий зависимостей

# 1.0.0

Новый формат экспорта.

### Usage

Теперь нет `module.exports = invariant`. Импортируй через `import {invariant} from '@yandex-market/invariant'`.

### Migration

Заменить по проекту `import invariant from '@yandex-market/invariant'` на `import {invariant} from '@yandex-market/invariant'`.

# 0.5.0

- Поменял экспорт `InvariantViolation` на `export class`. Теперь можно импортировать `InvariantViolation` в фигурных скобках.
- Рефакторинг, теперь в два раза меньше кода

### Usage

Для импорта `InvariantViolation` используй `import {InvariantViolation} from '@yandex-market/invariant'`

# 0.4.2

Проставлено время сборки

### Updates

  * `@yandex-market/yammy`: [2.0.0](../../scripts/yammy/changelog.md#200) (was [1.15.0](../../scripts/yammy/changelog.md#1150))

# 0.4.1

Обновление зависимостей

### Updates

  * `eslint-plugin-stout`: [1.0.4](../../tools/eslint-plugin-stout/changelog.md#104) (was [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103))

# 0.4.0

Заменил export = invariant на export default для исправления ошибки при сборке apiary

Заменил в index.spec.ts  импорт вида require

### Usage

Нет изменений

# 0.3.5

Игнорим node_modules-prod для автотестов

### Updates

  * `@yandex-market/error`: [1.4.5](../error/changelog.md#145) (was [1.4.4](../error/changelog.md#144))

# 0.3.4

Фиксы тестов

### Updates

  * `@yandex-market/error`: [1.4.4](../error/changelog.md#144) (was [1.4.3](../error/changelog.md#143))

# 0.3.3

Обновление зависимостей

### Updates

  * `@yandex-market/error`: [1.4.3](../error/changelog.md#143) (was [1.4.2](../error/changelog.md#142))

# 0.3.2

Правки eslint'а

### Updates

  * `@yandex-market/error`: [1.4.2](../error/changelog.md#142) (was [1.4.1](../error/changelog.md#141))
  * `eslint-plugin-stout`: [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103) (was [1.0.2](../../tools/eslint-plugin-stout/changelog.md#102))

# 0.3.1

Переезд в монорепу