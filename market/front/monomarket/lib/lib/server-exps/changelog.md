# 2.1.1

**PR:** [#2587715](https://a.yandex-team.ru/review/2587715)
**Author:** @bykhovtsev **Date:** 2022-06-01

Правим watchList, чтобы `yammy watch mandrel deep` не уходил в цикл

# 2.1.0

**PR:** [#2528234](https://a.yandex-team.ru/review/2528234)
**Author:** @xavescor **Date:** 2022-05-20

Обновление зависимостей

# 2.0.5

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

### Updates

  * `@yandex-market/logger-src`: [3.0.13](../logger/changelog.md#3013) (was [3.0.12](../logger/changelog.md#3012))

# 2.0.4

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

### Updates

  * `@yandex-market/logger-src`: [3.0.12](../logger/changelog.md#3012) (was [3.0.11](../logger/changelog.md#3011))

# 2.0.3

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/logger-src`: [3.0.11](../logger/changelog.md#3011) (was [3.0.10](../logger/changelog.md#3010))
  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))

# 2.0.2

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

### Updates

  * `@yandex-market/logger-src`: [3.0.10](../logger/changelog.md#3010) (was [3.0.9](../logger/changelog.md#309))

# 2.0.1

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

Обновление зависимостей

### Updates

  * `@yandex-market/logger-src`: [3.0.9](../logger/changelog.md#309) (was [3.0.8](../logger/changelog.md#308))

# 2.0.0

**PR:** [#410](https://github.yandex-team.ru/market/monomarket/pull/410)
**Author:** @maslov-rn **Date:** 2021-10-07

Перенос файла experiments из mandrel в отдельный пакет. Причина - серверные эксперименты для apiary

### Usage

import {isInExperiment} from '@yandex-market/server-exps'

Проверка: isInExperiment(flagName)

### Migration

Замена import {isInExperiment} from '@yandex-market/mandrel/launchServer/experiments' на
import {isInExperiment} from '@yandex-market/server-exps'