# 1.0.5

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 1.0.4

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

# 1.0.3

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))

# 1.0.2

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

# 1.0.1

**PR:** [#603](https://github.yandex-team.ru/market/monomarket/pull/603)
**Author:** @bykovski-ilya **Date:** 2021-12-21

**Починил ошибку в зависимости пакета - openapi-to-bcm**

# 1.0.0

**PR:** [#607](https://github.yandex-team.ru/market/monomarket/pull/607)
**Author:** @gheljenor **Date:** 2021-12-06

[MARKETFRONTECH-3433](https://st.yandex-team.ru/MARKETFRONTECH-3433) - Фильтрация данных в ФАПИ

### Usage

```js
const filter = require('@yandex-market/fapi-filter');

const filtered = filter(inputObject, schema);
```

### Migration

Не требуется - это первая версия.