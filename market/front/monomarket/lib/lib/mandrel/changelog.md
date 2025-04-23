# 28.9.2

**PR:** [#2767267](https://a.yandex-team.ru/review/2767267)
**Author:** @robot-metatron **Date:** 2022-07-28

Обновление зависимостей

### Updates

  * `@yandex-market/cia-src`: [4.3.0](../cia/changelog.md#430) (was [4.2.1](../cia/changelog.md#421))

# 28.9.1

**PR:** [#2750224](https://a.yandex-team.ru/review/2750224)
**Author:** @robot-metatron **Date:** 2022-07-19

поправлена ссылка с девтулзами при запуске мандреля

# 28.9.0

**PR:** [#2740663](https://a.yandex-team.ru/review/2740663)
**Author:** @bykhovtsev **Date:** 2022-07-18

MARKETFRONTECH-4463 Добавляем интеграцию core, template и проброс твм-тикетов

- В мандреле появилась возможность использовать `TvmModel` без прокидывания бекенда целиком, а указанием только лишь его названия
- Исправлен баг. Теперь `TvmUserTicket` проверяется в `AbstractPage` приложения
- Добавлена возможность полностью скипнуть MDA-проверки: `export type MDAType = 'MDA_v1' | 'MDA_v2' | 'none';`
- Добавлена привязка ошибок для `MarketUserlessContext`
- CSP-виджет теперь не только проставляет но и возвращает сформированный хедер

### Usage

none

# 28.8.5

**PR:** [#2744856](https://a.yandex-team.ru/review/2744856)
**Author:** @dv-mikhaylov **Date:** 2022-07-18

**[[MARKETFRONTECH-4687]]**

### Updates

  * `@yandex-market/cia-src`: [4.2.1](../cia/changelog.md#421) (was [4.2.0](../cia/changelog.md#420))

# 28.8.4

**PR:** [#2737993](https://a.yandex-team.ru/review/2737993)
**Author:** @robot-metatron **Date:** 2022-07-15

**Не пишем статистику по виджетам, у которых тайминги меньше 10 мс [undefined](https://st.yandex-team.ru/undefined) - undefined**

# 28.8.3

**PR:** [#2664658](https://a.yandex-team.ru/review/2664658)
**Author:** @robot-metatron **Date:** 2022-07-15

Обновление зависимостей

### Updates

  * `@yandex-market/cia-src`: [4.2.0](../cia/changelog.md#420) (was [4.1.1](../cia/changelog.md#411))

# 28.8.2

**PR:** [#2712490](https://a.yandex-team.ru/review/2712490)
**Author:** @robot-metatron **Date:** 2022-07-11

Обновление зависимостей

### Updates

  * `@yandex-market/bcm2`: [4.2.1](../bcm2/changelog.md#421) (was [4.2.0](../bcm2/changelog.md#420))

# 28.8.1

**PR:** [#2688793](https://a.yandex-team.ru/review/2688793)
**Author:** @avdotion **Date:** 2022-06-30

Error Booster больше не считает ворнинги ResizeObserver за ошибку.
Подробнее о проблеме можно [почитать на SO](https://stackoverflow.com/a/50387233).

# 28.8.0

**PR:** [#2685883](https://a.yandex-team.ru/review/2685883)
**Author:** @robot-metatron **Date:** 2022-06-29

Теперь мандрель сначала пытается прочитать vhost из runDir, и только потом из docroot

### Usage

не поменялось

# 28.7.3

**PR:** [#2663215](https://a.yandex-team.ru/review/2663215)
**Author:** @robot-metatron **Date:** 2022-06-28

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.11.1](../apiary/changelog.md#4111) (was [4.11.0](../apiary/changelog.md#4110))
  * `@yandex-market/apiary-annex-src`: [2.5.0](../apiary-annex/changelog.md#250) (was [2.4.0](../apiary-annex/changelog.md#240))
  * `@yandex-market/cia-src`: [4.1.1](../cia/changelog.md#411) (was [4.1.0](../cia/changelog.md#410))

# 28.7.2

**PR:** [#2681050](https://a.yandex-team.ru/review/2681050)
**Author:** @lengl **Date:** 2022-06-28

MARKETFRONT-85986: Revert https://a.yandex-team.ru/arc/review/2569822/details

Течёт память у сервера, откатываем изменения

# 28.7.1

**PR:** [#2676796](https://a.yandex-team.ru/review/2676796)
**Author:** @asker-k **Date:** 2022-06-27

добавлено логирование ошибки при старте

# 28.7.0

**PR:** [#2628400](https://a.yandex-team.ru/review/2628400)
**Author:** @robot-metatron **Date:** 2022-06-20

Учим BCM в новый контекст, который не содержит запроса пользователя

### Usage

```typescript
const requestId = generateMarketRequestId();

const ctx = MarketUserlessContext.fromRequestParams({
    pageId: 'page:identifier',
    requestIdModule: {
        reqId: requestId,
        marketReqId: requestId,
        subReqId: 1,
    },
});

bcmResource.fetch(ctx);
```

### Updates

  * `@yandex-market/stout`: [1.8.0](../stout/changelog.md#180) (was [1.7.0](../stout/changelog.md#170))
  * `@yandex-market/apiary-src`: [4.11.0](../apiary/changelog.md#4110) (was [4.10.2](../apiary/changelog.md#4102))
  * `@yandex-market/apiary-annex-src`: [2.4.0](../apiary-annex/changelog.md#240) (was [2.3.5](../apiary-annex/changelog.md#235))
  * `@yandex-market/cia-src`: [4.1.0](../cia/changelog.md#410) (was [4.0.1](../cia/changelog.md#401))

# 28.6.8

**PR:** [#2650527](https://a.yandex-team.ru/review/2650527)
**Author:** @robot-metatron **Date:** 2022-06-20

добавлено логирование ошибки при старте

### Updates

  * `@yandex-market/declarations`: [3.1.3](../../shared/declarations/changelog.md#313) (was [3.1.2](../../shared/declarations/changelog.md#312))
  * `@yandex-market/apiary-src`: [4.10.2](../apiary/changelog.md#4102) (was [4.10.1](../apiary/changelog.md#4101))
  * `@yandex-market/apiary-annex-src`: [2.3.5](../apiary-annex/changelog.md#235) (was [2.3.4](../apiary-annex/changelog.md#234))
  * `@yandex-market/cia-src`: [4.0.1](../cia/changelog.md#401) (was [4.0.0](../cia/changelog.md#400))

# 28.6.7

**PR:** [#2635759](https://a.yandex-team.ru/review/2635759)
**Author:** @dylukanin **Date:** 2022-06-16

**Теперь для процессов тестов не делается require tvm модели - ранее это приводило к падениям [[MARKETFRONT-92869]]**

# 28.6.6

**PR:** [#2614119](https://a.yandex-team.ru/review/2614119)
**Author:** @as-kondratev **Date:** 2022-06-16

Обновление зависимостей

### Updates

  * `@yandex-market/cia-src`: [4.0.0](../cia/changelog.md#400) (was [3.7.5](../cia/changelog.md#375))

# 28.6.5

**PR:** [#2622549](https://a.yandex-team.ru/review/2622549)
**Author:** @leonidlebedev **Date:** 2022-06-09

Добавление констант для виджетов devTools

# 28.6.4

**PR:** [#2620413](https://a.yandex-team.ru/review/2620413)
**Author:** @anseal **Date:** 2022-06-08

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.10.1](../apiary/changelog.md#4101) (was [4.10.0](../apiary/changelog.md#4100))
  * `@yandex-market/apiary-annex-src`: [2.3.4](../apiary-annex/changelog.md#234) (was [2.3.3](../apiary-annex/changelog.md#233))
  * `@yandex-market/cia-src`: [3.7.5](../cia/changelog.md#375) (was [3.7.4](../cia/changelog.md#374))

# 28.6.3

**PR:** [#2616231](https://a.yandex-team.ru/review/2616231)
**Author:** @a-novichkov-k **Date:** 2022-06-08

Обновление зависимостей

### Updates

  * `@yandex-market/cia-src`: [3.7.4](../cia/changelog.md#374) (was [3.7.3](../cia/changelog.md#373))

# 28.6.2

**PR:** [#2605379](https://a.yandex-team.ru/review/2605379)
**Author:** @nybble **Date:** 2022-06-02

Обновление зависимостей

### Updates

  * `@yandex-market/region-initialization`: [6.1.2](../region-initialization/changelog.md#612) (was [6.1.1](../region-initialization/changelog.md#611))

# 28.6.1

**PR:** [#2595101](https://a.yandex-team.ru/review/2595101)
**Author:** @hurtsok **Date:** 2022-06-01

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.10.0](../apiary/changelog.md#4100) (was [4.9.1](../apiary/changelog.md#491))
  * `@yandex-market/apiary-annex-src`: [2.3.3](../apiary-annex/changelog.md#233) (was [2.3.2](../apiary-annex/changelog.md#232))
  * `@yandex-market/cia-src`: [3.7.3](../cia/changelog.md#373) (was [3.7.2](../cia/changelog.md#372))

# 28.6.0

**PR:** [#2587715](https://a.yandex-team.ru/review/2587715)
**Author:** @bykhovtsev **Date:** 2022-06-01

- Поддержка `queryString` из bcm2
- Поддержка проксирования в Stout

### Usage

`STOUT_UNKNOWN_ROUTE` спец символ, который стаут будет трактовать, как роут-фолбэк

### Updates

  * `@yandex-market/bcm2`: [4.2.0](../bcm2/changelog.md#420) (was [4.1.0](../bcm2/changelog.md#410))
  * `@yandex-market/server-exps`: [2.1.1](../server-exps/changelog.md#211) (was [2.1.0](../server-exps/changelog.md#210))
  * `@yandex-market/stout`: [1.7.0](../stout/changelog.md#170) (was [1.6.0](../stout/changelog.md#160))
  * `@yandex-market/apiary-src`: [4.9.1](../apiary/changelog.md#491) (was [4.9.0](../apiary/changelog.md#490))
  * `@yandex-market/apiary-annex-src`: [2.3.2](../apiary-annex/changelog.md#232) (was [2.3.1](../apiary-annex/changelog.md#231))
  * `@yandex-market/cia-src`: [3.7.2](../cia/changelog.md#372) (was [3.7.1](../cia/changelog.md#371))

# 28.5.2

**PR:** [#2569822](https://a.yandex-team.ru/review/2569822)
**Author:** @lisenque **Date:** 2022-05-31

[undefined](https://st.yandex-team.ru/undefined) - undefined: Отладочная информация о вызове bcm ресурсов складывается в новое поле стаутного контекста

# 28.5.1

**PR:** [#2536350](https://a.yandex-team.ru/review/2536350)
**Author:** @anseal **Date:** 2022-05-31

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.9.0](../apiary/changelog.md#490) (was [4.8.0](../apiary/changelog.md#480))
  * `@yandex-market/apiary-annex-src`: [2.3.1](../apiary-annex/changelog.md#231) (was [2.3.0](../apiary-annex/changelog.md#230))
  * `@yandex-market/cia-src`: [3.7.1](../cia/changelog.md#371) (was [3.7.0](../cia/changelog.md#370))

# 28.5.0

**PR:** [#2568174](https://a.yandex-team.ru/review/2568174)
**Author:** @maslov-rn **Date:** 2022-05-31

Убрал сбор метрик для Solomon из под флага эксперимента. Сбор включается параметром в конфиге сервиса

### Usage

Добавить в конфиг сервиса:
```
solomonMetrics: {
    errors: true,
    backendsRps: true,
    backendsTimings: true
}
```

### Updates

  * `@yandex-market/stout`: [1.6.0](../stout/changelog.md#160) (was [1.5.0](../stout/changelog.md#150))

# 28.4.0

**PR:** [#2585474](https://a.yandex-team.ru/review/2585474)
**Author:** @xavescor **Date:** 2022-05-30

Откат механизма отмены

### Usage

--

### Updates

  * `@yandex-market/apiary-src`: [4.8.0](../apiary/changelog.md#480) (was [4.7.0](../apiary/changelog.md#470))
  * `@yandex-market/apiary-annex-src`: [2.3.0](../apiary-annex/changelog.md#230) (was [2.2.0](../apiary-annex/changelog.md#220))
  * `@yandex-market/cia-src`: [3.7.0](../cia/changelog.md#370) (was [3.6.0](../cia/changelog.md#360))

# 28.3.3

**PR:** [#2581855](https://a.yandex-team.ru/review/2581855)
**Author:** @e-golikov **Date:** 2022-05-27

Обновление зависимостей

### Updates

  * `@yandex-market/abt-headers-src`: [3.1.9](../abt-headers/changelog.md#319) (was [3.1.8](../abt-headers/changelog.md#318))

# 28.3.2

**PR:** [#2559308](https://a.yandex-team.ru/review/2559308)
**Author:** @sa-maksimov **Date:** 2022-05-24

Продолжил добавлять loginId в юзера
прокинул get_login_id в oauth так как мобилы ходят туда - и loginId не приходит https://st.yandex-team.ru/MARKETFRONT-86124

# 28.3.0

**PR:** [#2528234](https://a.yandex-team.ru/review/2528234)
**Author:** @xavescor **Date:** 2022-05-20

Изменения контекста для поддержки новой версии апиари

### Usage

Ничего не изменилось

### Updates

  * `@yandex-market/server-exps`: [2.1.0](../server-exps/changelog.md#210) (was [2.0.5](../server-exps/changelog.md#205))
  * `@yandex-market/stout`: [1.5.0](../stout/changelog.md#150) (was [1.4.0](../stout/changelog.md#140))
  * `@yandex-market/apiary-src`: [4.7.0](../apiary/changelog.md#470) (was [4.6.0](../apiary/changelog.md#460))
  * `@yandex-market/apiary-annex-src`: [2.2.0](../apiary-annex/changelog.md#220) (was [2.1.1](../apiary-annex/changelog.md#211))
  * `@yandex-market/cia-src`: [3.6.0](../cia/changelog.md#360) (was [3.5.1](../cia/changelog.md#351))

# 28.2.3

**PR:** [#2549557](https://a.yandex-team.ru/review/2549557)
**Author:** @smelukov **Date:** 2022-05-20

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.6.0](../apiary/changelog.md#460) (was [4.5.0](../apiary/changelog.md#450))
  * `@yandex-market/apiary-annex-src`: [2.1.1](../apiary-annex/changelog.md#211) (was [2.1.0](../apiary-annex/changelog.md#210))
  * `@yandex-market/cia-src`: [3.5.1](../cia/changelog.md#351) (was [3.5.0](../cia/changelog.md#350))

# 28.2.2

**PR:** [#2526047](https://a.yandex-team.ru/review/2526047)
**Author:** @nkiyko **Date:** 2022-05-13

**Добавление новых бакетов [undefined](https://st.yandex-team.ru/undefined) - undefined**

### Updates

  * `@yandex-market/stout`: [1.4.0](../stout/changelog.md#140) (was [1.3.1](../stout/changelog.md#131))

# 28.2.1

**PR:** [#2522594](https://a.yandex-team.ru/review/2522594)
**Author:** @as-kondratev **Date:** 2022-05-11

Обновление зависимостей

### Updates

  * `@yandex-market/cia-src`: [3.5.0](../cia/changelog.md#350) (was [3.4.0](../cia/changelog.md#340))

# 28.2.0

**PR:** [#2489763](https://a.yandex-team.ru/review/2489763)
**Author:** @gluhovroma **Date:** 2022-05-05

**Обновил babel и его плагины до последних версий [[MARKETFRONT-83092]]**

### Usage

**Обновите babel в своих проектах [[MARKETFRONT-83092]]**

### Updates

  * `@yandex-market/apiary-src`: [4.5.0](../apiary/changelog.md#450) (was [4.4.19](../apiary/changelog.md#4419))
  * `@yandex-market/apiary-annex-src`: [2.1.0](../apiary-annex/changelog.md#210) (was [2.0.25](../apiary-annex/changelog.md#2025))
  * `@yandex-market/cia-src`: [3.4.0](../cia/changelog.md#340) (was [3.3.9](../cia/changelog.md#339))

# 28.1.0

**PR:** [#2494438](https://a.yandex-team.ru/review/2494438)
**Author:** @creazero **Date:** 2022-04-29

[undefined](https://st.yandex-team.ru/undefined) - undefined: Поддержка traceHeaders для трассировок

### Usage

Новое поле позволяет ресурсам логировать в своих трассах заранее предопределенные заголовки.

### Updates

  * `@yandex-market/bcm2`: [4.1.0](../bcm2/changelog.md#410) (was [4.0.5](../bcm2/changelog.md#405))

# 28.0.0

**PR:** [#2513244](https://a.yandex-team.ru/review/2513244)
**Author:** @polyakovda **Date:** 2022-04-29

Откат [[MARKETFRONT-69107]]

### Usage

Особых действий не нужно

### Migration

Дополнительных действий не нужно

# 27.1.0

**PR:** [#2506921](https://a.yandex-team.ru/review/2506921)
arc**Author:** @nkiyko **Date:** 2022-04-27

**Backend Timings Solomon [undefined](https://st.yandex-team.ru/undefined) - undefined**

### Usage

**Без изменений [undefined](https://st.yandex-team.ru/undefined) - undefined**

# 27.0.1

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

### Updates

  * `@yandex-market/asker`: [3.1.7](../../fix/asker/changelog.md#317) (was [3.1.6](../../fix/asker/changelog.md#316))
  * `luster-trace-log`: [2.0.2](../luster-trace-log/changelog.md#202) (was [2.0.1](../luster-trace-log/changelog.md#201))
  * `@yandex-market/region-initialization`: [6.1.1](../region-initialization/changelog.md#611) (was [6.1.0](../region-initialization/changelog.md#610))
  * `@yandex-market/invariant`: [1.1.8](../invariant/changelog.md#118) (was [1.1.7](../invariant/changelog.md#117))
  * `@yandex-market/tskv-writer-src`: [3.0.8](../tskv-writer/changelog.md#308) (was [3.0.7](../tskv-writer/changelog.md#307))
  * `@yandex-market/bcm2`: [4.0.5](../bcm2/changelog.md#405) (was [4.0.4](../bcm2/changelog.md#404))
  * `@yandex-market/abt-headers-src`: [3.1.8](../abt-headers/changelog.md#318) (was [3.1.7](../abt-headers/changelog.md#317))
  * `@yandex-market/server-exps`: [2.0.5](../server-exps/changelog.md#205) (was [2.0.4](../server-exps/changelog.md#204))
  * `@yandex-market/logger-src`: [3.0.13](../logger/changelog.md#3013) (was [3.0.12](../logger/changelog.md#3012))
  * `@yandex-market/stout`: [1.3.1](../stout/changelog.md#131) (was [1.3.0](../stout/changelog.md#130))
  * `@yandex-market/resource`: [1.1.4](../../fix/resource/changelog.md#114) (was [1.1.3](../../fix/resource/changelog.md#113))
  * `@yandex-market/yate`: [0.0.84](../../fix/yate/changelog.md#0084) (was [0.0.83](../../fix/yate/changelog.md#0083))
  * `@yandex-market/apiary-src`: [4.4.19](../apiary/changelog.md#4419) (was [4.4.18](../apiary/changelog.md#4418))
  * `@yandex-market/apiary-annex-src`: [2.0.25](../apiary-annex/changelog.md#2025) (was [2.0.24](../apiary-annex/changelog.md#2024))
  * `@yandex-market/cia-src`: [3.3.9](../cia/changelog.md#339) (was [3.3.8](../cia/changelog.md#338))

# 27.0.0

**PR:** [#2492431](https://a.yandex-team.ru/review/2492431)
**Author:** @polyakovda **Date:** 2022-04-27

🔌 Переезд в сервис Валидации [[MARKETFRONT-69107]

### Usage

-

### Migration

Обновить в конфигах адрес `mobileValidator` с `mobilevalidator.vs.market.yandex.net` -> `narwhal.yandex.net`

# 26.24.2

**PR:** [#2501985](https://a.yandex-team.ru/review/2501985)
**Author:** @sa-maksimov **Date:** 2022-04-26

Прокинул параметр loginId в юзера https://st.yandex-team.ru/MARKETFRONT-83758

# 26.24.0

**PR:** [#2495391](https://a.yandex-team.ru/review/2495391)
**Author:** @maslov-rn **Date:** 2022-04-25

Добавил monlib в зав-ти. Эксперимент для отправки метрик в соломон

### Usage

Без изменений

### Updates

  * `@yandex-market/apiary-src`: [4.4.18](../apiary/changelog.md#4418) (was [4.4.17](../apiary/changelog.md#4417))
  * `@yandex-market/apiary-annex-src`: [2.0.24](../apiary-annex/changelog.md#2024) (was [2.0.23](../apiary-annex/changelog.md#2023))
  * `@yandex-market/cia-src`: [3.3.8](../cia/changelog.md#338) (was [3.3.7](../cia/changelog.md#337))

# 26.23.2

**PR:** [#2486686](https://a.yandex-team.ru/review/2486686)
**Author:** @sa-maksimov **Date:** 2022-04-21

**Передал в blackbox параметр get_login_id: 'yes' https://st.yandex-team.ru/MARKETFRONT-82410**

# 26.23.0

**PR:** [#2482886](https://a.yandex-team.ru/review/2482886)
**Author:** @polyakovda **Date:** 2022-04-20

Обновление зависимостей

### Usage

-

### Updates

  * `@yandex-market/region-initialization`: [6.1.0](../region-initialization/changelog.md#610) (was [6.0.5](../region-initialization/changelog.md#605))
  * `@yandex-market/stout`: [1.3.0](../stout/changelog.md#130) (was [1.2.5](../stout/changelog.md#125))

# 26.22.0

**PR:** [#2481007](https://a.yandex-team.ru/review/2481007)
**Author:** @nybble **Date:** 2022-04-19

Добавлена трассировка regionIdsBySources в traceDecorator.ts [undefined](https://st.yandex-team.ru/undefined) - undefined

### Usage

-

# 26.21.5

**PR:** [#2464128](https://a.yandex-team.ru/review/2464128)
**Author:** @gheljenor **Date:** 2022-04-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.2](../../shared/declarations/changelog.md#312) (was [3.1.1](../../shared/declarations/changelog.md#311))
  * `@yandex-market/apiary-src`: [4.4.17](../apiary/changelog.md#4417) (was [4.4.16](../apiary/changelog.md#4416))
  * `@yandex-market/apiary-annex-src`: [2.0.23](../apiary-annex/changelog.md#2023) (was [2.0.22](../apiary-annex/changelog.md#2022))
  * `@yandex-market/cia-src`: [3.3.7](../cia/changelog.md#337) (was [3.3.6](../cia/changelog.md#336))

# 26.21.4

**PR:** [#2463913](https://a.yandex-team.ru/review/2463913)
**Author:** @gheljenor **Date:** 2022-04-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.1](../../shared/declarations/changelog.md#311) (was [3.1.0](../../shared/declarations/changelog.md#310))
  * `@yandex-market/apiary-src`: [4.4.16](../apiary/changelog.md#4416) (was [4.4.15](../apiary/changelog.md#4415))
  * `@yandex-market/apiary-annex-src`: [2.0.22](../apiary-annex/changelog.md#2022) (was [2.0.21](../apiary-annex/changelog.md#2021))
  * `@yandex-market/cia-src`: [3.3.6](../cia/changelog.md#336) (was [3.3.5](../cia/changelog.md#335))

# 26.21.3

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

### Updates

  * `@yandex-market/asker`: [3.1.6](../../fix/asker/changelog.md#316) (was [3.1.5](../../fix/asker/changelog.md#315))
  * `luster-trace-log`: [2.0.1](../luster-trace-log/changelog.md#201) (was [2.0.0](../luster-trace-log/changelog.md#200))
  * `@yandex-market/region-initialization`: [6.0.5](../region-initialization/changelog.md#605) (was [6.0.4](../region-initialization/changelog.md#604))
  * `@yandex-market/invariant`: [1.1.7](../invariant/changelog.md#117) (was [1.1.6](../invariant/changelog.md#116))
  * `@yandex-market/tskv-writer-src`: [3.0.7](../tskv-writer/changelog.md#307) (was [3.0.6](../tskv-writer/changelog.md#306))
  * `@yandex-market/bcm2`: [4.0.4](../bcm2/changelog.md#404) (was [4.0.3](../bcm2/changelog.md#403))
  * `@yandex-market/abt-headers-src`: [3.1.7](../abt-headers/changelog.md#317) (was [3.1.6](../abt-headers/changelog.md#316))
  * `@yandex-market/server-exps`: [2.0.4](../server-exps/changelog.md#204) (was [2.0.3](../server-exps/changelog.md#203))
  * `@yandex-market/logger-src`: [3.0.12](../logger/changelog.md#3012) (was [3.0.11](../logger/changelog.md#3011))
  * `@yandex-market/stout`: [1.2.5](../stout/changelog.md#125) (was [1.2.4](../stout/changelog.md#124))
  * `@yandex-market/resource`: [1.1.3](../../fix/resource/changelog.md#113) (was [1.1.2](../../fix/resource/changelog.md#112))
  * `@yandex-market/yate`: [0.0.83](../../fix/yate/changelog.md#0083) (was [0.0.83-r](../../fix/yate/changelog.md#0083-r))
  * `@yandex-market/apiary-src`: [4.4.15](../apiary/changelog.md#4415) (was [4.4.14](../apiary/changelog.md#4414))
  * `@yandex-market/apiary-annex-src`: [2.0.21](../apiary-annex/changelog.md#2021) (was [2.0.20](../apiary-annex/changelog.md#2020))
  * `@yandex-market/cia-src`: [3.3.5](../cia/changelog.md#335) (was [3.3.4](../cia/changelog.md#334))

# 26.21.2

**PR:** [#1012](https://github.yandex-team.ru/market/monomarket/pull/1012)
**Author:** @bykhovtsev **Date:** 2022-04-06

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.14](../apiary/changelog.md#4414) (was [4.4.13](../apiary/changelog.md#4413))
  * `@yandex-market/apiary-annex-src`: [2.0.20](../apiary-annex/changelog.md#2020) (was [2.0.19](../apiary-annex/changelog.md#2019))
  * `@yandex-market/cia-src`: [3.3.4](../cia/changelog.md#334) (was [3.3.3](../cia/changelog.md#333))

# 26.21.1

**PR:** [#970](https://github.yandex-team.ru/market/monomarket/pull/970)
**Author:** @maslov-rn **Date:** 2022-03-31

Правка прекомитной проверки check-flow-files

### Updates

  * `@yandex-market/apiary-src`: [4.4.13](../apiary/changelog.md#4413) (was [4.4.12](../apiary/changelog.md#4412))
  * `@yandex-market/apiary-annex-src`: [2.0.19](../apiary-annex/changelog.md#2019) (was [2.0.18](../apiary-annex/changelog.md#2018))
  * `@yandex-market/cia-src`: [3.3.3](../cia/changelog.md#333) (was [3.3.2](../cia/changelog.md#332))

# 26.21.0

**PR:** [#981](https://github.yandex-team.ru/market/monomarket/pull/981)
**Author:** @xavescor **Date:** 2022-03-31

Докидываем дополнительные метрики к lcp

### Usage

--

# 26.20.0

**PR:** [#952](https://github.yandex-team.ru/market/monomarket/pull/952)
**Author:** @ed-novikov **Date:** 2022-03-29

[MARKETFRONT-78957](https://st.yandex-team.ru/MARKETFRONT-78957) - Добавил параметр proxyCookies для класса MarketHttpBackend

### Usage

Добавлена обработка параметра proxyCookies в prepareRequest для класса MarketHttpBackend. Добавлены тесты на параметр.

# 26.19.2

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

### Updates

  * `@yandex-market/invariant`: [1.1.6](../invariant/changelog.md#116) (was [1.1.5](../invariant/changelog.md#115))
  * `@yandex-market/tskv-writer-src`: [3.0.6](../tskv-writer/changelog.md#306) (was [3.0.5](../tskv-writer/changelog.md#305))
  * `@yandex-market/bcm2`: [4.0.3](../bcm2/changelog.md#403) (was [4.0.2](../bcm2/changelog.md#402))
  * `@yandex-market/abt-headers-src`: [3.1.6](../abt-headers/changelog.md#316) (was [3.1.5](../abt-headers/changelog.md#315))
  * `@yandex-market/server-exps`: [2.0.3](../server-exps/changelog.md#203) (was [2.0.2](../server-exps/changelog.md#202))
  * `@yandex-market/logger-src`: [3.0.11](../logger/changelog.md#3011) (was [3.0.10](../logger/changelog.md#3010))
  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))
  * `@yandex-market/apiary-src`: [4.4.12](../apiary/changelog.md#4412) (was [4.4.11](../apiary/changelog.md#4411))
  * `@yandex-market/apiary-annex-src`: [2.0.18](../apiary-annex/changelog.md#2018) (was [2.0.17](../apiary-annex/changelog.md#2017))
  * `@yandex-market/cia-src`: [3.3.2](../cia/changelog.md#332) (was [3.3.1](../cia/changelog.md#331))

# 26.19.1

**PR:** [#972](https://github.yandex-team.ru/market/monomarket/pull/972)
**Author:** @gheljenor **Date:** 2022-03-28

[MARKETFRONTECH-3877](https://st.yandex-team.ru/MARKETFRONTECH-3877) - Настроить генерацию симлинков скриптами в монорепе

### Updates

  * `@yandex-market/apiary-src`: [4.4.11](../apiary/changelog.md#4411) (was [4.4.10](../apiary/changelog.md#4410))
  * `@yandex-market/apiary-annex-src`: [2.0.17](../apiary-annex/changelog.md#2017) (was [2.0.16](../apiary-annex/changelog.md#2016))
  * `@yandex-market/cia-src`: [3.3.1](../cia/changelog.md#331) (was [3.3.0](../cia/changelog.md#330))

# 26.19.0

**PR:** [#929](https://github.yandex-team.ru/market/monomarket/pull/929)
**Author:** @xavescor **Date:** 2022-03-11

Отключаю отправку событий widgets.*

### Usage

Отключаю отправку событий widgets.*

# 26.18.5

**PR:** [#854](https://github.yandex-team.ru/market/monomarket/pull/854)
**Author:** @as-kondratev **Date:** 2022-03-10

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.0](../../shared/declarations/changelog.md#310) (was [3.0.2](../../shared/declarations/changelog.md#302))
  * `@yandex-market/apiary-src`: [4.4.10](../apiary/changelog.md#4410) (was [4.4.9](../apiary/changelog.md#449))
  * `@yandex-market/apiary-annex-src`: [2.0.16](../apiary-annex/changelog.md#2016) (was [2.0.15](../apiary-annex/changelog.md#2015))
  * `@yandex-market/cia-src`: [3.3.0](../cia/changelog.md#330) (was [3.2.16](../cia/changelog.md#3216))

# 26.18.4

**PR:** [#920](https://github.yandex-team.ru/market/monomarket/pull/920)
**Author:** @nkiyko **Date:** 2022-03-05

Обновление зависимостей

### Updates

  * `@yandex-market/region-initialization`: [6.0.4](../region-initialization/changelog.md#604) (was [6.0.3](../region-initialization/changelog.md#603))

# 26.18.3

**PR:** [#907](https://github.yandex-team.ru/market/monomarket/pull/907)
**Author:** @nkiyko **Date:** 2022-03-03

Обновление зависимостей

### Updates

  * `@yandex-market/region-initialization`: [6.0.3](../region-initialization/changelog.md#603) (was [6.0.2](../region-initialization/changelog.md#602))

# 26.18.2

**PR:** [#892](https://github.yandex-team.ru/market/monomarket/pull/892)
**Author:** @dylukanin **Date:** 2022-02-28

**Добавлена обработка новых кук автотестов. MARKETFRONTECH-3640**

# 26.18.1

**PR:** [#894](https://github.yandex-team.ru/market/monomarket/pull/894)
**Author:** @kykint **Date:** 2022-02-25

Обновление зависимостей

### Updates

  * `@yandex-market/stout`: [1.2.4](../stout/changelog.md#124) (was [1.2.3](../stout/changelog.md#123))

# 26.18.0

**PR:** [#891](https://github.yandex-team.ru/market/monomarket/pull/891)
**Author:** @bykovski-ilya **Date:** 2022-02-25

**MARKETFRONTECH-3748**

### Usage

**MARKETFRONTECH-3748**

### Updates

  * `luster-trace-log`: [2.0.0](../luster-trace-log/changelog.md#200) (was [1.1.7](../luster-trace-log/changelog.md#117))

# 26.17.8

**PR:** [#866](https://github.yandex-team.ru/market/monomarket/pull/866)
**Author:** @bykhovtsev **Date:** 2022-02-24

Заполняем секцию `watchIgnore`, чтобы `yammy watch mandrel` не уходил в бесконечный цикл

### Updates

  * `@yandex-market/apiary-src`: [4.4.9](../apiary/changelog.md#449) (was [4.4.8](../apiary/changelog.md#448))
  * `@yandex-market/apiary-annex-src`: [2.0.15](../apiary-annex/changelog.md#2015) (was [2.0.14](../apiary-annex/changelog.md#2014))
  * `@yandex-market/cia-src`: [3.2.16](../cia/changelog.md#3216) (was [3.2.15](../cia/changelog.md#3215))

# 26.17.7

**PR:** [#806](https://github.yandex-team.ru/market/monomarket/pull/806)
**Author:** @asvasilenko **Date:** 2022-02-17

[MARKETFRONT-71352](https://st.yandex-team.ru/MARKETFRONT-71352) - добавит .idea в gitignore Исправил отправку метрик виджетов stuffing, hydrating с sendTimeMark на sendDelta

### Updates

  * `@yandex-market/apiary-src`: [4.4.8](../apiary/changelog.md#448) (was [4.4.7](../apiary/changelog.md#447))
  * `@yandex-market/apiary-annex-src`: [2.0.14](../apiary-annex/changelog.md#2014) (was [2.0.13](../apiary-annex/changelog.md#2013))
  * `@yandex-market/cia-src`: [3.2.15](../cia/changelog.md#3215) (was [3.2.14](../cia/changelog.md#3214))

# 26.17.6

**PR:** [#877](https://github.yandex-team.ru/market/monomarket/pull/877)
**Author:** @kykint **Date:** 2022-02-17

- Более корректная типизация Stout

### Updates

  * `@yandex-market/stout`: [1.2.3](../stout/changelog.md#123) (was [1.2.2](../stout/changelog.md#122))

# 26.17.5

**PR:** [#869](https://github.yandex-team.ru/market/monomarket/pull/869)
**Author:** @kaboskin **Date:** 2022-02-16

**[MARKETFRONT-73637](https://st.yandex-team.ru/MARKETFRONT-73637) - удалён старый код жука Удалён старый код жука**

# 26.17.4

**PR:** [#823](https://github.yandex-team.ru/market/monomarket/pull/823)
**Author:** @albert-fibikh **Date:** 2022-02-15

[MARKETFRONT-70222](https://st.yandex-team.ru/MARKETFRONT-70222) - Изменил qr devtools Изменил стили qr кода

# 26.17.3

**PR:** [#857](https://github.yandex-team.ru/market/monomarket/pull/857)
**Author:** @kykint **Date:** 2022-02-10

- Чуть более корректный тип resource

# 26.17.2

**PR:** [#850](https://github.yandex-team.ru/market/monomarket/pull/850)
**Author:** @dgudenkov **Date:** 2022-02-09

- Поправен тип символа в контексте

# 26.17.1

**PR:** [#830](https://github.yandex-team.ru/market/monomarket/pull/830)
**Author:** @chafilin **Date:** 2022-02-08

кнопка CE в девтулзах теперь показыввает все cms страницы, а не только первую[undefined](https://st.yandex-team.ru/undefined) - undefined

# 26.17.0

**PR:** [#826](https://github.yandex-team.ru/market/monomarket/pull/826)
**Author:** @grumpy **Date:** 2022-02-03

- Обновили версию rum-counter. Теперь собираются метрика image-goodness и расширенные данные по first-input. ([MARKETFRONT-72415](https://st.yandex-team.ru/MARKETFRONT-72415) - Update RUM-counter in mandrel)

### Usage

- ...

# 26.16.8

**PR:** [#797](https://github.yandex-team.ru/market/monomarket/pull/797)
**Author:** @dv-mikhaylov **Date:** 2022-02-03

Добавлена прекомитная проверка check-flow-files, которая сравнивает файл с разрешением ts в папке src и ищет такой же файл в папке flow https://st.yandex-team.ru/MARKETFRONTECH-3273

### Updates

  * `@yandex-market/check-flow-files`: [1.0.1](../../scripts/check-flow/changelog.md#101) (was [1.0.0](../../scripts/check-flow/changelog.md#100))
  * `@yandex-market/apiary-src`: [4.4.7](../apiary/changelog.md#447) (was [4.4.6](../apiary/changelog.md#446))
  * `@yandex-market/apiary-annex-src`: [2.0.13](../apiary-annex/changelog.md#2013) (was [2.0.12](../apiary-annex/changelog.md#2012))
  * `@yandex-market/cia-src`: [3.2.14](../cia/changelog.md#3214) (was [3.2.13](../cia/changelog.md#3213))

# 26.16.7

**PR:** [#810](https://github.yandex-team.ru/market/monomarket/pull/810)
**Author:** @gheljenor **Date:** 2022-01-31

Обновление зависимостей

### Updates

  * `@yandex-market/asker`: [3.1.5](../../fix/asker/changelog.md#315) (was [3.1.4](../../fix/asker/changelog.md#314))
  * `@yandex-market/error`: [1.5.1](../error/changelog.md#151) (was [1.5.0](../error/changelog.md#150))
  * `@yandex-market/invariant`: [1.1.5](../invariant/changelog.md#115) (was [1.1.4](../invariant/changelog.md#114))
  * `@yandex-market/abt-headers-src`: [3.1.5](../abt-headers/changelog.md#315) (was [3.1.4](../abt-headers/changelog.md#314))
  * `@yandex-market/apiary-src`: [4.4.6](../apiary/changelog.md#446) (was [4.4.5](../apiary/changelog.md#445))
  * `@yandex-market/apiary-annex-src`: [2.0.12](../apiary-annex/changelog.md#2012) (was [2.0.11](../apiary-annex/changelog.md#2011))
  * `@yandex-market/cia-src`: [3.2.13](../cia/changelog.md#3213) (was [3.2.12](../cia/changelog.md#3212))

# 26.16.6

**PR:** [#792](https://github.yandex-team.ru/market/monomarket/pull/792)
**Author:** @pasha-deev **Date:** 2022-01-25

[MARKETFRONTECH-3631](https://st.yandex-team.ru/MARKETFRONTECH-3631) - проброс экспериментов, полученных из uaas

# 26.16.5

**PR:** [#570](https://github.yandex-team.ru/market/monomarket/pull/570)
**Author:** @owngr **Date:** 2022-01-21

Обновление зависимостей

### Updates

  * `@yandex-market/bcm2`: [4.0.2](../bcm2/changelog.md#402) (was [4.0.1](../bcm2/changelog.md#401))

# 26.16.4

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

### Updates

  * `@yandex-market/region-initialization`: [6.0.2](../region-initialization/changelog.md#602) (was [6.0.1](../region-initialization/changelog.md#601))
  * `@yandex-market/invariant`: [1.1.4](../invariant/changelog.md#114) (was [1.1.3](../invariant/changelog.md#113))
  * `@yandex-market/tskv-writer-src`: [3.0.5](../tskv-writer/changelog.md#305) (was [3.0.4](../tskv-writer/changelog.md#304))
  * `@yandex-market/bcm2`: [4.0.1](../bcm2/changelog.md#401) (was [4.0.0](../bcm2/changelog.md#400))
  * `@yandex-market/abt-headers-src`: [3.1.4](../abt-headers/changelog.md#314) (was [3.1.3](../abt-headers/changelog.md#313))
  * `@yandex-market/server-exps`: [2.0.2](../server-exps/changelog.md#202) (was [2.0.1](../server-exps/changelog.md#201))
  * `@yandex-market/logger-src`: [3.0.10](../logger/changelog.md#3010) (was [3.0.9](../logger/changelog.md#309))
  * `@yandex-market/apiary-src`: [4.4.5](../apiary/changelog.md#445) (was [4.4.4](../apiary/changelog.md#444))
  * `@yandex-market/apiary-annex-src`: [2.0.11](../apiary-annex/changelog.md#2011) (was [2.0.10](../apiary-annex/changelog.md#2010))
  * `@yandex-market/cia-src`: [3.2.12](../cia/changelog.md#3212) (was [3.2.11](../cia/changelog.md#3211))

# 26.16.3

**PR:** [#767](https://github.yandex-team.ru/market/monomarket/pull/767)
**Author:** @pasha-deev **Date:** 2022-01-18

[MARKETTECH-2407](https://st.yandex-team.ru/MARKETTECH-2407) - Сделал id пользователя для qr кода 9ти байтным

# 26.16.2

**PR:** [#760](https://github.yandex-team.ru/market/monomarket/pull/760)
**Author:** @nkiyko **Date:** 2022-01-18

Fix unknown service

# 26.16.1

**PR:** [#770](https://github.yandex-team.ru/market/monomarket/pull/770)
**Author:** @dv-mikhaylov **Date:** 2022-01-17

Обновление зависимостей

### Updates

  * `@yandex-market/region-initialization`: [6.0.1](../region-initialization/changelog.md#601) (was [6.0.0](../region-initialization/changelog.md#600))

# 26.16.0

**PR:** [#677](https://github.yandex-team.ru/market/monomarket/pull/677)
**Author:** @morozov-andre **Date:** 2022-01-17

[MARKETFRONT-67281](https://st.yandex-team.ru/MARKETFRONT-67281) - Убран поход в сервис валидации JWS-токена (/check_jws_token). Добавил логирование заголовка X-Antirobot-Jws-Info

### Usage

Убран поход в сервис валидации JWS-токена. Добавлено логирование заголовка X-Antirobot-Jws-Info

# 26.15.4

**PR:** [#747](https://github.yandex-team.ru/market/monomarket/pull/747)
**Author:** @dv-mikhaylov **Date:** 2022-01-14

**Перенос пакета https://github.yandex-team.ru/market/region-initialization в монорепу**

### Updates

  * `@yandex-market/asker`: [3.1.4](../../fix/asker/changelog.md#314) (was [3.1.3](../../fix/asker/changelog.md#313))
  * `@yandex-market/region-initialization`: [6.0.0](../region-initialization/changelog.md#600) (was [5.1.1](../region-initialization/changelog.md#511))
  * `@yandex-market/resource`: [1.1.2](../../fix/resource/changelog.md#112) (was [1.1.1](../../fix/resource/changelog.md#111))

# 26.15.3

**PR:** [#703](https://github.yandex-team.ru/market/monomarket/pull/703)
**Author:** @asker-k **Date:** 2022-01-12

Обновление зависимостей

### Updates

  * `@yandex-market/bcm2`: [4.0.0](../bcm2/changelog.md#400) (was [3.4.0](../bcm2/changelog.md#340))

# 26.15.2

**PR:** [#603](https://github.yandex-team.ru/market/monomarket/pull/603)
**Author:** @bykovski-ilya **Date:** 2021-12-21

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.4](../apiary/changelog.md#444) (was [4.4.3](../apiary/changelog.md#443))
  * `@yandex-market/apiary-annex-src`: [2.0.10](../apiary-annex/changelog.md#2010) (was [2.0.9](../apiary-annex/changelog.md#209))
  * `@yandex-market/cia-src`: [3.2.11](../cia/changelog.md#3211) (was [3.2.10](../cia/changelog.md#3210))

# 26.15.1

**PR:** [#686](https://github.yandex-team.ru/market/monomarket/pull/686)
**Author:** @b-bari **Date:** 2021-12-19

Не падаем при логировании ошибки резолвера.
Исправляется ошибка при которой логирование ошибки резолвера валилось и валило все приложение. 
Дело было в том, что в методе getErrorLogData вызывается метод getStoutRequest который в некоторых случаях ничего не возвращает.
Дальше код пытается из undefined достать abt. Теперь все хорошо

# 26.15.0

**PR:** [#627](https://github.yandex-team.ru/market/monomarket/pull/627)
**Author:** @pasha-deev **Date:** 2021-12-13

[MARKETFRONT-65104](https://st.yandex-team.ru/MARKETFRONT-65104) - Генерация qr кода для лейбла devtools

### Usage

Добавлено формирование qr кода с информацией о пользователе и дне месяца 

```js
/* 
    генирация кода для разметки
*/
const qrUrl = `https://disk.yandex.net/qr/?clean=1&text=${qrRawData}&format=png`;
```

# 26.14.0

**PR:** [#647](https://github.yandex-team.ru/market/monomarket/pull/647)
**Author:** @grumpy **Date:** 2021-12-13

В launchClient добавлена поддержка параметра nannyServiceId.

Этот параметр пробрасывается как есть в Метрику.

### Usage

```js
launch({
    ...
    nannyServiceId: 'market_production_desktop_vla',
    ...
});
```

# 26.13.0

**PR:** [#552](https://github.yandex-team.ru/market/monomarket/pull/552)
**Author:** @maslov-rn **Date:** 2021-12-08

Установка переменной окружения process.env.LUSTER_METRICS_SOCK

### Usage

Подключить расширение luster - @yandex-market/luster-metrics

# 26.12.0

**PR:** [#640](https://github.yandex-team.ru/market/monomarket/pull/640)
**Author:** @maslov-rn **Date:** 2021-12-08

Добавил в trace в key/values инициатора запроса - widgetName + widgetId

Для bcm данные о виджете беру из контекста, для asker из заголовка resource-meta

### Usage

Без изменений

### Updates

  * `@yandex-market/apiary-src`: [4.4.3](../apiary/changelog.md#443) (was [4.4.2](../apiary/changelog.md#442))
  * `@yandex-market/apiary-annex-src`: [2.0.9](../apiary-annex/changelog.md#209) (was [2.0.8](../apiary-annex/changelog.md#208))
  * `@yandex-market/cia-src`: [3.2.10](../cia/changelog.md#3210) (was [3.2.9](../cia/changelog.md#329))

# 26.11.0

**PR:** [#621](https://github.yandex-team.ru/market/monomarket/pull/621)
**Author:** @owsanka **Date:** 2021-12-06

[MARKETFRONT-65242](https://st.yandex-team.ru/MARKETFRONT-65242) - хелпер exclude-params + тесты

### Usage

**Добавлен хелпер excludeQueryParams для удаления параметров, которые не хотим видеть в логах**

# 26.10.0

**PR:** [#623](https://github.yandex-team.ru/market/monomarket/pull/623)
**Author:** @gheljenor **Date:** 2021-12-06

[MARKETFRONTECH-3459](https://st.yandex-team.ru/MARKETFRONTECH-3459) - Удобное логгирование таймингов в ФАПИ

### Usage

Добавлены методы:

```js
FrontApiPage.prototype.logTimer = function (portion, duration, extra = null) {
    /* 
        Записывает в лог время с меткой portion
        Поле extra - простой объект, который будет записан в info_keys/info_values 
    */
}

FrontApiPage.prototype.measure = async function (portion, callback, extra) {
    /* 
        Запусает асинхронный коллбек и записывает в лог длительность обработки колбека с меткой portion 
    */
}
```

# 26.9.1

**PR:** [#385](https://github.yandex-team.ru/market/monomarket/pull/385)
**Author:** @asker-k **Date:** 2021-12-03

[MARKETFRONTECH-3074](https://st.yandex-team.ru/MARKETFRONTECH-3074) - фикс для уитилиты isAutotest

# 26.9.0

**PR:** [#591](https://github.yandex-team.ru/market/monomarket/pull/591)
**Author:** @asker-k **Date:** 2021-11-26

[MARKETFRONT-3409](https://st.yandex-team.ru/MARKETFRONT-3409) - Прокидывание error вторым аргументом в retryDelay. TransportResponseError обогащен полем headers - заголовками ответа
Обновлен bcm2

### Usage

Обогащен HttpTransportResponseError
В HttpTransportRetryDelay добавлено прокидывание ошибки

### Updates

  * `@yandex-market/bcm2`: [3.4.0](../bcm2/changelog.md#340) (was [3.3.5](../bcm2/changelog.md#335))

# 26.8.0

**PR:** [#569](https://github.yandex-team.ru/market/monomarket/pull/569)
**Author:** @nickshevr **Date:** 2021-11-25

Весь функционал, кроме _mod=robot теперь доступен только для стаффовых сетей.
В `user/region` добавлено поле `isYandexNet` для проверки принадлежности сетям Яндекса.

### Usage

Обновить mandrel

# 26.7.0

**PR:** [#544](https://github.yandex-team.ru/market/monomarket/pull/544)
**Author:** @fenruga **Date:** 2021-11-25

Прокидываю заголовки для фапи

### Usage

none

# 26.6.3

**PR:** [#514](https://github.yandex-team.ru/market/monomarket/pull/514)
**Author:** @ajzekv **Date:** 2021-11-24

[MARKETFRONTECH-3327](https://st.yandex-team.ru/MARKETFRONTECH-3327) - cartSharer config Добавляет cartSharer в конфиг в мандреле

# 26.6.2

**PR:** [#587](https://github.yandex-team.ru/market/monomarket/pull/587)
**Author:** @oske **Date:** 2021-11-24

**Поправлено залезание devtools попапов под шапку [[https://st.yandex-team.ru/MARKETFRONT-63750]]**

# 26.6.1

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

[MARKETFRONTECH-3408](https://st.yandex-team.ru/MARKETFRONTECH-3408) - Починить сборки

### Updates

  * `@yandex-market/invariant`: [1.1.3](../invariant/changelog.md#113) (was [1.1.2](../invariant/changelog.md#112))
  * `@yandex-market/tskv-writer-src`: [3.0.4](../tskv-writer/changelog.md#304) (was [3.0.3](../tskv-writer/changelog.md#303))
  * `@yandex-market/bcm2`: [3.3.5](../bcm2/changelog.md#335) (was [3.3.4](../bcm2/changelog.md#334))
  * `@yandex-market/abt-headers-src`: [3.1.3](../abt-headers/changelog.md#313) (was [3.1.2](../abt-headers/changelog.md#312))
  * `@yandex-market/server-exps`: [2.0.1](../server-exps/changelog.md#201) (was [2.0.0](../server-exps/changelog.md#200))
  * `@yandex-market/logger-src`: [3.0.9](../logger/changelog.md#309) (was [3.0.8](../logger/changelog.md#308))
  * `@yandex-market/apiary-src`: [4.4.2](../apiary/changelog.md#442) (was [4.4.1](../apiary/changelog.md#441))
  * `@yandex-market/apiary-annex-src`: [2.0.8](../apiary-annex/changelog.md#208) (was [2.0.7](../apiary-annex/changelog.md#207))
  * `@yandex-market/cia-src`: [3.2.9](../cia/changelog.md#329) (was [3.2.8](../cia/changelog.md#328))

# 26.6.0

**PR:** [#528](https://github.yandex-team.ru/market/monomarket/pull/528)
**Author:** @mtvv **Date:** 2021-11-12

Мод для подсчета диффа для StateDivergence

### Usage

В урл добавить параметр `_mod=withMissmatch`

### Updates

  * `@yandex-market/apiary-src`: [4.4.1](../apiary/changelog.md#441) (was [4.4.0](../apiary/changelog.md#440))
  * `@yandex-market/apiary-annex-src`: [2.0.7](../apiary-annex/changelog.md#207) (was [2.0.6](../apiary-annex/changelog.md#206))
  * `@yandex-market/cia-src`: [3.2.8](../cia/changelog.md#328) (was [3.2.7](../cia/changelog.md#327))

# 26.5.1

**PR:** [#540](https://github.yandex-team.ru/market/monomarket/pull/540)
**Author:** @lengl **Date:** 2021-11-10

**Поправлено залезание формы жука под паранджу [[https://st.yandex-team.ru/MARKETFRONT-52100]]**

# 26.5.0

**PR:** [#519](https://github.yandex-team.ru/market/monomarket/pull/519)
**Author:** @bykhovtsev **Date:** 2021-11-09

Позволяем отключить серверный рендеринг для ленивых виджетов. Опционально, его можно вернуть.

### Usage

Чтобы выключить серверный рендеринг, в параметры для `LazyLoader` необходимо передать опцию `disableServerRender: true`

# 26.4.1

**PR:** [#513](https://github.yandex-team.ru/market/monomarket/pull/513)
**Author:** @fenruga **Date:** 2021-11-02

Обновление зависимостей

### Updates

  * `luster-trace-log`: [1.1.7](../luster-trace-log/changelog.md#117) (was [1.1.6](../luster-trace-log/changelog.md#116))

# 26.4.0

**PR:** [#509](https://github.yandex-team.ru/market/monomarket/pull/509)
**Author:** @grumpy **Date:** 2021-11-02

- Добавлена опция для настройки батчинга ленивых виджетов. [MARKETFRONTECH-3324](https://st.yandex-team.ru/MARKETFRONTECH-3324) - Добавить в mandrel опцию для батчинга ленивых виджетов

### Usage

```ts
const LazyLoader = createLazyLoader({
    bulkTimerDuration: 0, // отключаем батчинг
    ...
});
```

# 26.3.1

**PR:** [#477](https://github.yandex-team.ru/market/monomarket/pull/477)
**Author:** @arekuts **Date:** 2021-11-01

**Поправлено залезание кнопок дебага на форму жука [[https://st.yandex-team.ru/MARKETFRONT-52100]]**

# 26.3.0

**PR:** [#496](https://github.yandex-team.ru/market/monomarket/pull/496)
**Author:** @maslov-rn **Date:** 2021-10-29

Добавил параметр url параметр _blacklistWidget - для отключения виджетов по id на странице
Добавил в devTools ссылку в виде 🚫 для перехода на страницу без выбранного виджета

### Usage

https://market.yandex.ru/?_blacklistWidget=widgetId

### Updates

  * `@yandex-market/apiary-src`: [4.4.0](../apiary/changelog.md#440) (was [4.3.2](../apiary/changelog.md#432))
  * `@yandex-market/apiary-annex-src`: [2.0.6](../apiary-annex/changelog.md#206) (was [2.0.5](../apiary-annex/changelog.md#205))
  * `@yandex-market/cia-src`: [3.2.7](../cia/changelog.md#327) (was [3.2.6](../cia/changelog.md#326))

# 26.2.1

**PR:** [#423](https://github.yandex-team.ru/market/monomarket/pull/423)
**Author:** @juleari **Date:** 2021-10-21

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.3.2](../apiary/changelog.md#432) (was [4.3.1](../apiary/changelog.md#431))
  * `@yandex-market/apiary-annex-src`: [2.0.5](../apiary-annex/changelog.md#205) (was [2.0.4](../apiary-annex/changelog.md#204))
  * `@yandex-market/cia-src`: [3.2.6](../cia/changelog.md#326) (was [3.2.5](../cia/changelog.md#325))

# 26.2.0

**PR:** [#351](https://github.yandex-team.ru/market/monomarket/pull/351)
**Author:** @asker-k **Date:** 2021-10-20

# Accessed Fields Logger (AFL)
AFL - это утилита, которая поможет собрать список полей, которыми фронт действительно пользуется.

## Управление утилитой
Утилита управляется экспом `all_accessed_fields_logger`

## Концепция работы утилиты
На результат вызова бэкенда (в основном это нормализованная коллекция) вешается детектор. Детектор обнаруживает любое обращение к полям своей коллекции и логирует это.
За счет этого, мы можем понять к каким полям действительно было обращение, а какие мы зря храним.

## Техническое описание работы

### Usage

Утилита управляется экспом `all_accessed_fields_logger`

# 26.1.2

**PR:** [#450](https://github.yandex-team.ru/market/monomarket/pull/450)
**Author:** @lisenque **Date:** 2021-10-13

Добавилась проверка на функцию перед вызовом

# 26.1.1

**PR:** [#352](https://github.yandex-team.ru/market/monomarket/pull/352)
**Author:** @fenruga **Date:** 2021-10-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.0.2](../../shared/declarations/changelog.md#302) (was [3.0.1](../../shared/declarations/changelog.md#301))
  * `@yandex-market/apiary-src`: [4.3.1](../apiary/changelog.md#431) (was [4.3.0](../apiary/changelog.md#430))
  * `@yandex-market/apiary-annex-src`: [2.0.4](../apiary-annex/changelog.md#204) (was [2.0.3](../apiary-annex/changelog.md#203))
  * `@yandex-market/cia-src`: [3.2.5](../cia/changelog.md#325) (was [3.2.4](../cia/changelog.md#324))

# 26.1.0

**PR:** [#438](https://github.yandex-team.ru/market/monomarket/pull/438)
**Author:** @lisenque **Date:** 2021-10-12

[MARKETFRONT-58868](https://st.yandex-team.ru/MARKETFRONT-58868) - Пробрасывает событие в document, если ответ похож на капчу от антиробота
Добавляем поддержку captcha в ремоут-резолвер.

### Usage

Если запрос был перехвачен антироботом и отдал ответ с ссылкой на капчу, вызываем событие @mandrel/captchaRedirect на уровне document, которое в последствии обрабатывается приложением самостоятельно.
Чтобы включить, необходимо дообавить ```captchaSupported: true``` в настройки launchClient приложения

# 26.0.0

**PR:** [#410](https://github.yandex-team.ru/market/monomarket/pull/410)
**Author:** @maslov-rn **Date:** 2021-10-07

Добавил в тип Stout Page 2 поля: widgetName, widgetId
Перенес работу с конфигом серверных экспов в отдельный пакет

### Usage

В объекте context._page доступны поля widgetId, widgetName
`import {isInExperiment} from '@yandex-market/mandrel/launchServer/experiments'`->
`import {isInExperiment} from '@yandex-market/server-exps`

### Migration

Замена `import {isInExperiment} from '@yandex-market/mandrel/launchServer/experiments` в коде b2c

### Updates

  * `@yandex-market/server-exps`: [2.0.0](../server-exps/changelog.md#200) (was [1.0.0](../server-exps/changelog.md#100))
  * `@yandex-market/apiary-src`: [4.3.0](../apiary/changelog.md#430) (was [4.2.3](../apiary/changelog.md#423))
  * `@yandex-market/apiary-annex-src`: [2.0.3](../apiary-annex/changelog.md#203) (was [2.0.2](../apiary-annex/changelog.md#202))
  * `@yandex-market/cia-src`: [3.2.4](../cia/changelog.md#324) (was [3.2.3](../cia/changelog.md#323))

# 25.1.0

**PR:** [#414](https://github.yandex-team.ru/market/monomarket/pull/414)
**Author:** @dgudenkov **Date:** 2021-10-07

Добавил прокидывание oauthScope в авторизацию [undefined](https://st.yandex-team.ru/undefined) - undefined

### Usage

Указать в конфиге приложения oauthScope, или при вызове передать скоуп:

```javascript
user.initAuth({ctx, token, oauthScope: 'market:pi'});
```

# 25.0.5

**PR:** [#420](https://github.yandex-team.ru/market/monomarket/pull/420)
**Author:** @nybble **Date:** 2021-10-06

Пофикшено поле error в эпике виджета LazyLoader в случае, если payload пришел как undefined

MARKETFRONTECH-2403

# 25.0.4

**PR:** [#424](https://github.yandex-team.ru/market/monomarket/pull/424)
**Author:** @gheljenor **Date:** 2021-10-06

[MARKETFRONTECH-3239](https://st.yandex-team.ru/MARKETFRONTECH-3239) - [Монорепа] сломались типы и проверки типов

### Updates

  * `@yandex-market/apiary-src`: [4.2.3](../apiary/changelog.md#423) (was [4.2.2](../apiary/changelog.md#422))
  * `@yandex-market/apiary-annex-src`: [2.0.2](../apiary-annex/changelog.md#202) (was [2.0.1](../apiary-annex/changelog.md#201))
  * `@yandex-market/cia-src`: [3.2.3](../cia/changelog.md#323) (was [3.2.2](../cia/changelog.md#322))

# 25.0.3

**PR:** [#403](https://github.yandex-team.ru/market/monomarket/pull/403)
**Author:** @akimy **Date:** 2021-10-05

Обновление зависимостей

### Updates

  * `@yandex-market/stout`: [1.2.2](../stout/changelog.md#122) (was [1.2.1](../stout/changelog.md#121))

# 25.0.2

**PR:** [#400](https://github.yandex-team.ru/market/monomarket/pull/400)
**Author:** @gheljenor **Date:** 2021-10-01

[MARKETFRONTECH-2852](https://st.yandex-team.ru/MARKETFRONTECH-2852) - [Идея]: Включаем keep-alive для top-5 бэкендов [3%cpu] -- фикс отсутствующего агента

# 25.0.1

**PR:** [#389](https://github.yandex-team.ru/market/monomarket/pull/389)
**Author:** @nickshevr **Date:** 2021-09-28

[luster] Обновлена ссылка на дебаг

# 25.0.0

**PR:** [#347](https://github.yandex-team.ru/market/monomarket/pull/347)
**Author:** @gheljenor **Date:** 2021-09-17

[MARKETFRONTECH-3172](https://st.yandex-team.ru/MARKETFRONTECH-3172) - Отказ от глобальной геобазы и uatraits

### Usage

Используется как раньше

### Migration

Скрестить пальцы

# 24.5.2

**PR:** [#202](https://github.yandex-team.ru/market/monomarket/pull/202)
**Author:** @pasha-deev **Date:** 2021-09-15

[MARKETFRONTECH-2942](https://st.yandex-team.ru/MARKETFRONTECH-2942) - Добавил логирование экспериментов для fapi

# 24.5.1

**PR:** [#320](https://github.yandex-team.ru/market/monomarket/pull/320)
**Author:** @ashwets **Date:** 2021-09-15

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.2](../invariant/changelog.md#112) (was [1.1.1](../invariant/changelog.md#111))
  * `@yandex-market/tskv-writer-src`: [3.0.3](../tskv-writer/changelog.md#303) (was [3.0.2](../tskv-writer/changelog.md#302))
  * `@yandex-market/bcm2`: [3.3.4](../bcm2/changelog.md#334) (was [3.3.3](../bcm2/changelog.md#333))
  * `@yandex-market/abt-headers-src`: [3.1.2](../abt-headers/changelog.md#312) (was [3.1.1](../abt-headers/changelog.md#311))
  * `@yandex-market/logger-src`: [3.0.8](../logger/changelog.md#308) (was [3.0.7](../logger/changelog.md#307))
  * `@yandex-market/apiary-src`: [4.2.2](../apiary/changelog.md#422) (was [4.2.1](../apiary/changelog.md#421))
  * `@yandex-market/apiary-annex-src`: [2.0.1](../apiary-annex/changelog.md#201) (was [2.0.0](../apiary-annex/changelog.md#200))
  * `@yandex-market/cia-src`: [3.2.2](../cia/changelog.md#322) (was [3.2.1](../cia/changelog.md#321))

# 24.5.0

**PR:** [#343](https://github.yandex-team.ru/market/monomarket/pull/343)
**Author:** @gheljenor **Date:** 2021-09-15

[MARKETFRONTECH-3161](https://st.yandex-team.ru/MARKETFRONTECH-3161) - [Монорепа] всяческие правки yammy

Добавлен скрипт `build-version`, который возвращает текущую мажорную версию ноды

### Usage

Записываем версию ноды во время сборки:

```json
{
  "build:node-version": "build-version > configs/node_version",
}
```

Запускаем с правильной версией ноды:

```shell
BUILD_VERSION=$(cat "${docroot}/app/configs/node_version")
export PATH="/opt/nodejs/${BUILD_VERSION}/bin:${PATH}"
```

# 24.4.3

**PR:** [#209](https://github.yandex-team.ru/market/monomarket/pull/209)
**Author:** @pavelko95 **Date:** 2021-09-15

Обновление версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.1](../invariant/changelog.md#111) (was [1.1.0](../invariant/changelog.md#110))
  * `@yandex-market/tskv-writer-src`: [3.0.2](../tskv-writer/changelog.md#302) (was [3.0.1](../tskv-writer/changelog.md#301))
  * `@yandex-market/bcm2`: [3.3.3](../bcm2/changelog.md#333) (was [3.3.2](../bcm2/changelog.md#332))
  * `@yandex-market/abt-headers-src`: [3.1.1](../abt-headers/changelog.md#311) (was [3.1.0](../abt-headers/changelog.md#310))
  * `@yandex-market/logger-src`: [3.0.7](../logger/changelog.md#307) (was [3.0.6](../logger/changelog.md#306))
  * `@yandex-market/apiary-src`: [4.2.1](../apiary/changelog.md#421) (was [4.2.0](../apiary/changelog.md#420))
  * `@yandex-market/apiary-annex-src`: [2.0.0](../apiary-annex/changelog.md#200) (was [1.1.0](../apiary-annex/changelog.md#110))
  * `@yandex-market/cia-src`: [3.2.1](../cia/changelog.md#321) (was [3.2.0](../cia/changelog.md#320))

# 24.4.2

**PR:** [#334](https://github.yandex-team.ru/market/monomarket/pull/334)
**Author:** @naygeborin **Date:** 2021-09-15

Убрал дублирование CmsEditor в DevTools

# 24.4.1

**PR:** [#333](https://github.yandex-team.ru/market/monomarket/pull/333)
**Author:** @lisenque **Date:** 2021-09-14

Исправлена 500 для ?_mod=requests

# 24.4.0

**PR:** [#327](https://github.yandex-team.ru/market/monomarket/pull/327)
**Author:** @b-bari **Date:** 2021-09-13

[MARKETBTOBAPP-39](https://st.yandex-team.ru/MARKETBTOBAPP-39) - детали ошибок в FrontApiPage: FrontApiPage теперь может в дефолтном ответе с ошибкой так же вернуть details.

### Usage

```typescript
// Создаете класс ошибки с деталями

type ValidationErrorDetails = Record<string, string>;

export class ValidationError extends BaseError {
    details: ValidationErrorDetails;

    constructor(details) {
        super();

        this.details = details;
    }
}

// Из хендлера возвращаете ошибку

return {
    error: new ValidationError({
        someField: 'field validation error'
    }),
}

// Ответ

{
    "results": [
    {
        "handler": "myAwesomeHandler",
        "error": {
            "kind": "ValidationError",
            "message": "",
            "details": {
                "someField": "field validation error"
            }
        }
    }
],
    "collections": {}
}
```

# 24.3.0

**PR:** [#313](https://github.yandex-team.ru/market/monomarket/pull/313)
**Author:** @ivan-afanasov **Date:** 2021-09-10

Обновление зависимостей

### Updates

  * `@yandex-market/error`: [1.5.0](../error/changelog.md#150) (was [1.4.6](../error/changelog.md#146))
  * `@yandex-market/invariant`: [1.1.0](../invariant/changelog.md#110) (was [1.0.5](../invariant/changelog.md#105))
  * `@yandex-market/abt-headers-src`: [3.1.0](../abt-headers/changelog.md#310) (was [3.0.8](../abt-headers/changelog.md#308))
  * `@yandex-market/apiary-src`: [4.2.0](../apiary/changelog.md#420) (was [4.1.1](../apiary/changelog.md#411))
  * `@yandex-market/cia-src`: [3.2.0](../cia/changelog.md#320) (was [3.1.8](../cia/changelog.md#318))

# 24.2.1

**PR:** [#307](https://github.yandex-team.ru/market/monomarket/pull/307)
**Author:** @gheljenor **Date:** 2021-09-08

Обновление зависимостей

### Updates

  * `@yandex-market/bcm2`: [3.3.2](../bcm2/changelog.md#332) (was [3.3.1](../bcm2/changelog.md#331))

# 24.2.0

**PR:** [#294](https://github.yandex-team.ru/market/monomarket/pull/294)
**Author:** @maslov-rn **Date:** 2021-09-08

Новые метрики (http тайминги, время на парсинг) теперь логируются только при наличии
флага extraLogging: true в конфиге для mandrel

### Usage

Флаг extraLogging: true в конфиге для mandrel включает доп. метрики

# 24.1.1

**PR:** [#206](https://github.yandex-team.ru/market/monomarket/pull/206)
**Author:** @antonk52 **Date:** 2021-09-06

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.5](../invariant/changelog.md#105) (was [1.0.4](../invariant/changelog.md#104))
  * `@yandex-market/tskv-writer-src`: [3.0.1](../tskv-writer/changelog.md#301) (was [3.0.0](../tskv-writer/changelog.md#300))
  * `@yandex-market/bcm2`: [3.3.1](../bcm2/changelog.md#331) (was [3.3.0](../bcm2/changelog.md#330))
  * `@yandex-market/abt-headers-src`: [3.0.8](../abt-headers/changelog.md#308) (was [3.0.7](../abt-headers/changelog.md#307))
  * `@yandex-market/logger-src`: [3.0.6](../logger/changelog.md#306) (was [3.0.5](../logger/changelog.md#305))
  * `@yandex-market/apiary-src`: [4.1.1](../apiary/changelog.md#411) (was [4.1.0](../apiary/changelog.md#410))
  * `@yandex-market/cia-src`: [3.1.8](../cia/changelog.md#318) (was [3.1.7](../cia/changelog.md#317))

# 24.1.0

**PR:** [#295](https://github.yandex-team.ru/market/monomarket/pull/295)
**Author:** @nickshevr **Date:** 2021-09-03

Согласно: https://wiki.yandex-team.ru/geotargeting/libgeobase/faq/#osobennostiadresnogoja-prostranstvastaff/net
Для подсчета isInternalNetwork упрощаем ограничение:
- yandex_net - любые запросы из внутренней сети, в т.ч. роботы
- yandex_staff - позволяет доуточнить привязку адреса конкретно до пользовательских сетей сотрудников в офисах + VPN

Достаточно любого из двух флагов.

### Usage

None

# 24.0.0

**PR:** [#293](https://github.yandex-team.ru/market/monomarket/pull/293)
**Author:** @dmbaranov **Date:** 2021-09-03

Заменил библиотеку, т.к. она обрезала длину логируемой строки.

### Usage

Как и прежде, но с обработкой reject

### Migration

Теперь так же нужно обработать ошибку, которую вернут ф-я:
будет возвращать Promise.reject(err) ошибку если не смогли преобразовать в json

# 23.4.0

**PR:** [#204](https://github.yandex-team.ru/market/monomarket/pull/204)
**Author:** @maslov-rn **Date:** 2021-09-01

Добавлена новая метрика в traceLog - время на парсинг

### Usage

Без изменений

### Updates

  * `@yandex-market/bcm2`: [3.3.0](../bcm2/changelog.md#330) (was [3.2.4](../bcm2/changelog.md#324))

# 23.3.0

**PR:** [#275](https://github.yandex-team.ru/market/monomarket/pull/275)
**Author:** @dgudenkov **Date:** 2021-08-31

Добавил создание хипдампа при ООМ. Будет складываться в директорию с логами

### Usage

Вотчер запустится автоматом при запуске сервера.

# 23.2.4

**PR:** [#261](https://github.yandex-team.ru/market/monomarket/pull/261)
**Author:** @senz **Date:** 2021-08-30

Обновлена зависимость @yandex-market/tskv-writer

### Updates

  * `@yandex-market/tskv-writer-src`: [3.0.0](../tskv-writer/changelog.md#300) (was [2.0.0](../tskv-writer/changelog.md#200))

# 23.2.3

**PR:** [#256](https://github.yandex-team.ru/market/monomarket/pull/256)
**Author:** @yatamik **Date:** 2021-08-23

Обновление зависимостей

### Updates

  * `@yandex-market/abt-headers-src`: [3.0.7](../abt-headers/changelog.md#307) (was [3.0.6](../abt-headers/changelog.md#306))

# 23.2.2

**PR:** [#257](https://github.yandex-team.ru/market/monomarket/pull/257)
**Author:** @yatamik **Date:** 2021-08-19

-   Исправлена ошибка типов в StoutUser

# 23.2.1

**PR:** [#248](https://github.yandex-team.ru/market/monomarket/pull/248)
**Author:** @makhataibar **Date:** 2021-08-16

[MARKETFRONT-47632](https://st.yandex-team.ru/MARKETFRONT-47632) - Изменил версию Жучка, чтобы появились новые апи

# 23.2.0

**PR:** [#234](https://github.yandex-team.ru/market/monomarket/pull/234)
**Author:** @nickshevr **Date:** 2021-08-16

- убираем вызов конструктора AbtDisabled в экспе
- убираем вызов записи логгера в экспе

### Usage

Выставить флаг minimize_logs в серверных экспериментах

### Updates

  * `@yandex-market/apiary-src`: [4.1.0](../apiary/changelog.md#410) (was [4.0.8](../apiary/changelog.md#408))
  * `@yandex-market/cia-src`: [3.1.7](../cia/changelog.md#317) (was [3.1.6](../cia/changelog.md#316))

# 23.1.0

**PR:** [#242](https://github.yandex-team.ru/market/monomarket/pull/242)
**Author:** @nybble **Date:** 2021-08-12

[Добавлен попап](https://st.yandex-team.ru/MARKETFRONTECH-3000) со ссылкой на трассировку для кнопки Серверная Трассировка (Т) в жучке

### Usage

зажать кнопку, подождать пока откроется попуп

# 23.0.0

**PR:** [#239](https://github.yandex-team.ru/market/monomarket/pull/239)
**Author:** @dgudenkov **Date:** 2021-08-12

- изменил сборку mandrel-a

### Usage

- как было

### Migration

- обновить mandrel в package.json

# 22.5.3

**PR:** [#172](https://github.yandex-team.ru/market/monomarket/pull/172)
**Author:** @dimakomkov **Date:** 2021-08-12

Добавлена маскировка sessionId куки в режимах **"_mod=requests"** и **?wombat=1**

# 22.5.2

**PR:** [#233](https://github.yandex-team.ru/market/monomarket/pull/233)
**Author:** @dgudenkov **Date:** 2021-08-11

- фикс сета tld в юзере

# 22.5.1

**PR:** [#224](https://github.yandex-team.ru/market/monomarket/pull/224)
**Author:** @dgudenkov **Date:** 2021-08-10

- фикс импорта трейс-логгера

# 22.5.0

**PR:** [#149](https://github.yandex-team.ru/market/monomarket/pull/149)
**Author:** @sudokey **Date:** 2021-08-09

* Добавлена возможность отключать эксперименты. Необходимо для того, чтобы автотесты, в пайплайнах, не попадали в эксперименты.

### Usage

Чтобы выключить попадание в эксперименты нужно передать в AbtHeaders флаг disableExps равный true

# 22.4.8

**PR:** [#207](https://github.yandex-team.ru/market/monomarket/pull/207)
**Author:** @juleari **Date:** 2021-08-09

Добавила типы

### Updates

  * `@yandex-market/invariant`: [1.0.4](../invariant/changelog.md#104) (was [1.0.3](../invariant/changelog.md#103))
  * `@yandex-market/bcm2`: [3.2.4](../bcm2/changelog.md#324) (was [3.2.3](../bcm2/changelog.md#323))
  * `@yandex-market/abt-headers-src`: [3.0.6](../abt-headers/changelog.md#306) (was [3.0.5](../abt-headers/changelog.md#305))
  * `@yandex-market/logger-src`: [3.0.5](../logger/changelog.md#305) (was [3.0.4](../logger/changelog.md#304))
  * `@yandex-market/apiary-src`: [4.0.8](../apiary/changelog.md#408) (was [4.0.7](../apiary/changelog.md#407))
  * `@yandex-market/cia-src`: [3.1.6](../cia/changelog.md#316) (was [3.1.5](../cia/changelog.md#315))

# 22.4.7

**PR:** [#222](https://github.yandex-team.ru/market/monomarket/pull/222)
**Author:** @juleari **Date:** 2021-08-09

[MARKETFRONTECH-2993](https://st.yandex-team.ru/MARKETFRONTECH-2993) - [Монорепа] Починить ссылки в ченжлогах

### Updates

  * `@yandex-market/bcm2`: [3.2.3](../bcm2/changelog.md#323) (was [3.2.2](../bcm2/changelog.md#322))
  * `@yandex-market/abt-headers-src`: [3.0.5](../abt-headers/changelog.md#305) (was [3.0.4](../abt-headers/changelog.md#304))
  * `@yandex-market/logger-src`: [3.0.4](../logger/changelog.md#304) (was [3.0.3](../logger/changelog.md#303))
  * `@yandex-market/apiary-src`: [4.0.7](../apiary/changelog.md#407) (was [4.0.6](../apiary/changelog.md#406))
  * `@yandex-market/cia-src`: [3.1.5](../cia/changelog.md#315) (was [3.1.4](../cia/changelog.md#314))

# 22.4.6

**PR:** [#217](https://github.yandex-team.ru/market/monomarket/pull/217)
**Author:** @dgudenkov **Date:** 2021-08-06

- перевыкатка битого пакета

# 22.4.5

**PR:** [#216](https://github.yandex-team.ru/market/monomarket/pull/216)
**Author:** @dgudenkov **Date:** 2021-08-05

- перевыкатка в npm

# 22.4.4

**PR:** [#215](https://github.yandex-team.ru/market/monomarket/pull/215)
**Author:** @gheljenor **Date:** 2021-08-04

[MARKETFRONTECH-2974](https://st.yandex-team.ru/MARKETFRONTECH-2974) - [Монорепа] Убираем скрипты из генерируемых пакетов

### Updates

  * `@yandex-market/bcm2`: [3.2.2](../bcm2/changelog.md#322) (was [3.2.1](../bcm2/changelog.md#321))
  * `@yandex-market/abt-headers-src`: [3.0.4](../abt-headers/changelog.md#304) (was [3.0.3](../abt-headers/changelog.md#303))
  * `@yandex-market/logger-src`: [3.0.3](../logger/changelog.md#303) (was [3.0.2](../logger/changelog.md#302))
  * `@yandex-market/apiary-src`: [4.0.6](../apiary/changelog.md#406) (was [4.0.5](../apiary/changelog.md#405))
  * `@yandex-market/cia-src`: [3.1.4](../cia/changelog.md#314) (was [3.1.3](../cia/changelog.md#313))

# 22.4.3

**PR:** [#212](https://github.yandex-team.ru/market/monomarket/pull/212)
**Author:** @bykhovtsev **Date:** 2021-08-04

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.0.5](../apiary/changelog.md#405) (was [4.0.4](../apiary/changelog.md#404))
  * `@yandex-market/cia-src`: [3.1.3](../cia/changelog.md#313) (was [3.1.2](../cia/changelog.md#312))

# 22.4.2

**PR:** [#211](https://github.yandex-team.ru/market/monomarket/pull/211)
**Author:** @dgudenkov **Date:** 2021-08-03

- убрал опциональный параметр

# 22.4.1

**PR:** [#210](https://github.yandex-team.ru/market/monomarket/pull/210)
**Author:** @dgudenkov **Date:** 2021-08-03

- сделал более строгие типы для резолверов, добавил несколько экспортов типов

# 22.4.0

**PR:** [#208](https://github.yandex-team.ru/market/monomarket/pull/208)
**Author:** @nybble **Date:** 2021-08-03

Добавлено [срабатывание кнопки трассировок жучка на тач события](https://st.yandex-team.ru/MARKETFRONTECH-2963) для копирования ссылки на трассировку в цуме

### Usage

Зажать кнопку 'Т' жучка, удержать до появления надписи 'copied!', отпустить. Ссылка в буфере!

# 22.3.2

**PR:** [#201](https://github.yandex-team.ru/market/monomarket/pull/201)
**Author:** @gheljenor **Date:** 2021-08-02

Изменение версий зависимостей

### Updates

  * `@yandex-market/asker`: [3.1.3](../../fix/asker/changelog.md#313) (was [3.1.2](../../fix/asker/changelog.md#312))
  * `@yandex-market/invariant`: [1.0.3](../invariant/changelog.md#103) (was [1.0.2](../invariant/changelog.md#102))
  * `@yandex-market/bcm2`: [3.2.1](../bcm2/changelog.md#321) (was [3.2.0](../bcm2/changelog.md#320))
  * `@yandex-market/abt-headers-src`: [3.0.3](../abt-headers/changelog.md#303) (was [3.0.2](../abt-headers/changelog.md#302))
  * `@yandex-market/declarations`: [3.0.1](../../shared/declarations/changelog.md#301) (was [3.0.0](../../shared/declarations/changelog.md#300))
  * `@yandex-market/resource`: [1.1.1](../../fix/resource/changelog.md#111) (was [1.1.0](../../fix/resource/changelog.md#110))
  * `@yandex-market/logger-src`: [3.0.2](../logger/changelog.md#302) (was [3.0.1](../logger/changelog.md#301))
  * `@yandex-market/apiary-src`: [4.0.4](../apiary/changelog.md#404) (was [4.0.3](../apiary/changelog.md#403))
  * `@yandex-market/cia-src`: [3.1.2](../cia/changelog.md#312) (was [3.1.1](../cia/changelog.md#311))

# 22.3.1

**PR:** [#205](https://github.yandex-team.ru/market/monomarket/pull/205)
**Author:** @dgudenkov **Date:** 2021-07-30

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.0.0](../../shared/declarations/changelog.md#300) (was [2.0.0](../../shared/declarations/changelog.md#200))
  * `@yandex-market/apiary-src`: [4.0.3](../apiary/changelog.md#403) (was [4.0.2](../apiary/changelog.md#402))
  * `@yandex-market/cia-src`: [3.1.1](../cia/changelog.md#311) (was [3.1.0](../cia/changelog.md#310))

# 22.3.0

**PR:** [#192](https://github.yandex-team.ru/market/monomarket/pull/192)
**Author:** @dgudenkov **Date:** 2021-07-29

Поправил сборку

### Usage

-

# 22.2.1

**PR:** [#193](https://github.yandex-team.ru/market/monomarket/pull/193)
**Author:** @bra31k **Date:** 2021-07-29

Обновление зависимостей

### Updates

  * `@yandex-market/cia-src`: [3.1.0](../cia/changelog.md#310) (was [3.0.1](../cia/changelog.md#301))

# 22.2.0

**PR:** [#198](https://github.yandex-team.ru/market/monomarket/pull/198)
**Author:** @maslov-rn **Date:** 2021-07-28

Добавление логирования новых метрик в bcm, resource

### Usage

Без изменений

### Updates

  * `@yandex-market/asker`: [3.1.2](../../fix/asker/changelog.md#312) (was [3.1.1](../../fix/asker/changelog.md#311))
  * `@yandex-market/bcm2`: [3.2.0](../bcm2/changelog.md#320) (was [3.1.1](../bcm2/changelog.md#311))
  * `@yandex-market/resource`: [1.1.0](../../fix/resource/changelog.md#110) (was [1.0.0](../../fix/resource/changelog.md#100))

# 22.1.0

**PR:** [#187](https://github.yandex-team.ru/market/monomarket/pull/187)
**Author:** @flack **Date:** 2021-07-28

Перенос resource в монорепозиторий

### Usage

Без изменений

### Updates

  * `@yandex-market/asker`: [3.1.1](../../fix/asker/changelog.md#311) (was [3.1.0](../../fix/asker/changelog.md#310))
  * `@yandex-market/resource`: [1.0.0](../../fix/resource/changelog.md#100) (was [0.20.0](../../fix/resource/changelog.md#0200))

# 22.0.1

**PR:** [#191](https://github.yandex-team.ru/market/monomarket/pull/191)
**Author:** @avdotion **Date:** 2021-07-26

Обновление зависимостей

### Updates

  * `@yandex-market/cia-src`: [3.0.1](../cia/changelog.md#301) (was [3.0.0](../cia/changelog.md#300))

# 22.0.0

**PR:** [#175](https://github.yandex-team.ru/market/monomarket/pull/175)
**Author:** @loyd **Date:** 2021-07-26

Обновление зависимостей

### Usage

Ничего не изменилось

### Migration

Обновите библиотеку `@yandex-market/cia` до актуальной версии

### Updates

  * `@yandex-market/declarations`: [2.0.0](../../shared/declarations/changelog.md#200) (was [1.0.0](../../shared/declarations/changelog.md#100))
  * `@yandex-market/apiary-src`: [4.0.2](../apiary/changelog.md#402) (was [4.0.1](../apiary/changelog.md#401))
  * `@yandex-market/cia-src`: [3.0.0](../cia/changelog.md#300) (was [2.2.0](../cia/changelog.md#220))

# 21.0.1

**PR:** [#189](https://github.yandex-team.ru/market/monomarket/pull/189)
**Author:** @gheljenor **Date:** 2021-07-26

Изменён формат описания времени сборки

### Updates

  * `@yandex-market/error`: [1.4.6](../error/changelog.md#146) (was [1.4.5](../error/changelog.md#145))
  * `@yandex-market/invariant`: [1.0.2](../invariant/changelog.md#102) (was [1.0.1](../invariant/changelog.md#101))
  * `@yandex-market/bcm2`: [3.1.1](../bcm2/changelog.md#311) (was [3.1.0](../bcm2/changelog.md#310))
  * `@yandex-market/abt-headers-src`: [3.0.2](../abt-headers/changelog.md#302) (was [3.0.1](../abt-headers/changelog.md#301))
  * `@yandex-market/stout`: [1.2.1](../stout/changelog.md#121) (was [1.2.0](../stout/changelog.md#120))
  * `@yandex-market/logger-src`: [3.0.1](../logger/changelog.md#301) (was [3.0.0](../logger/changelog.md#300))
  * `@yandex-market/apiary-src`: [4.0.1](../apiary/changelog.md#401) (was [4.0.0](../apiary/changelog.md#400))

# 21.0.0

**PR:** [#176](https://github.yandex-team.ru/market/monomarket/pull/176)
**Author:** @avdotion **Date:** 2021-07-22

Обновление зависимостей

### Usage

Ничего не изменилось

### Migration

Нужно обновить `@yandex-market/logger` в зависимых пакетах до последней версии

### Updates

  * `@yandex-market/logger-src`: [3.0.0](../logger/changelog.md#300) (was [2.1.0](../logger/changelog.md#210))

# 20.0.1

**PR:** [#183](https://github.yandex-team.ru/market/monomarket/pull/183)
**Author:** @pasha-deev **Date:** 2021-07-21

Обновление зависимостей

### Updates

  * `@yandex-market/abt-headers-src`: [3.0.1](../abt-headers/changelog.md#301) (was [3.0.0](../abt-headers/changelog.md#300))

# 20.0.0

**PR:** [#168](https://github.yandex-team.ru/market/monomarket/pull/168)
**Author:** @avdotion **Date:** 2021-07-21

Обновление версий зависимостей

### Usage

Ничего не поменялось

### Migration

Обновите `@yandex-market/declarations` в связанных проектах

### Updates

  * `@yandex-market/declarations`: [1.0.0](../../shared/declarations/changelog.md#100) (was [0.22.1](../../shared/declarations/changelog.md#0221))
  * `@yandex-market/apiary-src`: [4.0.0](../apiary/changelog.md#400) (was [3.4.1](../apiary/changelog.md#341))

# 19.0.2

**PR:** [#184](https://github.yandex-team.ru/market/monomarket/pull/184)
**Author:** @gheljenor **Date:** 2021-07-21

[MARKETFRONTECH-2852](https://st.yandex-team.ru/MARKETFRONTECH-2852) - [Идея]: Включаем keep-alive для top-5 бэкендов [3%cpu]

 - эксперимент `keepalive-default` - используем keep-alive для bcm-бэкендов
 - эксперимент `keepalive-enhanced` - используем прокачанный keep-alive агент для bcm-бэкендов

### Updates

  * `@yandex-market/bcm2`: [3.1.0](../bcm2/changelog.md#310) (was [3.0.9](../bcm2/changelog.md#309))

# 19.0.1

**PR:** [#173](https://github.yandex-team.ru/market/monomarket/pull/173)
**Author:** @maslov-rn **Date:** 2021-07-21

Обновление зависимостей

### Updates

  * `@yandex-market/asker`: [3.1.0](../../fix/asker/changelog.md#310) (was [3.0.0](../../fix/asker/changelog.md#300))

# 19.0.0

**PR:** [#154](https://github.yandex-team.ru/market/monomarket/pull/154)
**Author:** @dgudenkov **Date:** 2021-07-21

Перевел mandrel на тайпскрипт

### Usage

Теперь есть ts-типы

### Migration

Изменить require() на require().default.

Пример:
```
const smth = require('@yandex-market/madnrel/smth');
->
const smth = require('@yandex-market/madnrel/smth').default;
```

### Updates

  * `@yandex-market/stout`: [1.2.0](../stout/changelog.md#120) (was [1.1.25](../stout/changelog.md#1125))

# 18.7.0

**PR:** [#169](https://github.yandex-team.ru/market/monomarket/pull/169)
**Author:** @kaero **Date:** 2021-07-20

Замена asker => @yandex-market/asker в package.json

### Usage

Ничего не изменилось

### Updates

  * `@yandex-market/asker`: [3.0.0](../../fix/asker/changelog.md#300) (was [2.0.0](../../fix/asker/changelog.md#200))

# 18.6.2

**PR:** [#165](https://github.yandex-team.ru/market/monomarket/pull/165)
**Author:** @antsa4 **Date:** 2021-07-16

Обновление версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.1](../invariant/changelog.md#101) (was [1.0.0](../invariant/changelog.md#100))
  * `@yandex-market/bcm2`: [3.0.9](../bcm2/changelog.md#309) (was [3.0.8](../bcm2/changelog.md#308))
  * `@yandex-market/abt-headers-src`: [3.0.0](../abt-headers/changelog.md#300) (was [2.3.0](../abt-headers/changelog.md#230))
  * `@yandex-market/apiary-src`: [3.4.1](../apiary/changelog.md#341) (was [3.4.0](../apiary/changelog.md#340))

# 18.6.1

**PR:** [#158](https://github.yandex-team.ru/market/monomarket/pull/158)
**Author:** @dgudenkov **Date:** 2021-07-16

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [3.4.0](../apiary/changelog.md#340) (was [3.3.0](../apiary/changelog.md#330))

# 18.6.0

Обновлен `@yandex-market/invariant`.

### Usage

При обновлении мандреля обнови и `invariant`.

### Updates

  * `@yandex-market/invariant`: [1.0.0](../invariant/changelog.md#100) (was [0.5.0](../invariant/changelog.md#050))
  * `@yandex-market/apiary-src`: [3.3.0](../apiary/changelog.md#330) (was [3.2.3](../apiary/changelog.md#323))

# 18.5.5

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [0.5.0](../invariant/changelog.md#050) (was [0.4.2](../invariant/changelog.md#042))
  * `@yandex-market/apiary-src`: [3.2.3](../apiary/changelog.md#323) (was [3.2.2](../apiary/changelog.md#322))

# 18.5.4

* обновляем рум счётчик до 4.4.1

# 18.5.3

* не роняем запуск сервера в деве при отсутствии version.txt

# 18.5.2

Обновилась версия пакета `abt-headers`

# 18.5.1

Проставлено время сборки

### Updates

  * `@yandex-market/invariant`: [0.4.2](../invariant/changelog.md#042) (was [0.4.1](../invariant/changelog.md#041))
  * `@yandex-market/bcm2`: [3.0.8](../bcm2/changelog.md#308) (was [3.0.7](../bcm2/changelog.md#307))
  * `@yandex-market/yammy`: [2.0.0](../../scripts/yammy/changelog.md#200) (was [1.15.0](../../scripts/yammy/changelog.md#1150))
  * `@yandex-market/apiary-src`: [3.2.2](../apiary/changelog.md#322) (was [3.2.1](../apiary/changelog.md#321))

# 18.5.0

Ошибка, созданная снаружи и отправленная на журнализацию, обогащается рядом переменных из контекста (логин, страница, регион...).
Они потом записываются в таблицу market_errors в колонки extra_keys и extra_values.
Добавлена возможность передать свои кастомные значения в эти переменные.

### Usage

```javascript
class FoobarError extends Error {
	constructor(...args) {
		super(...args);
		this.extra = {};
	}
}

const err = new FoobarError();
err.extra['bar'] = 42;
ctx.logger.error(err);
```

# 18.4.1

Добавлено правило санитайзинга '<!' в UNSAFE_CHARS_RE

### Updates

  * `@yandex-market/apiary-src`: [3.2.1](../apiary/changelog.md#321) (was [3.2.0](../apiary/changelog.md#320))

# 18.4.0

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [3.2.0](../apiary/changelog.md#320) (was [3.1.1](../apiary/changelog.md#311))

# 18.3.1

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [3.1.1](../apiary/changelog.md#311) (was [3.1.0](../apiary/changelog.md#310))

# 18.3.0

Добавляет возможность использовать очередь с приоритетами для гидрации виджетов

### Usage

В `launchClient` необходимо передать параметр `useHydrationHeap`
```js
type Options = {
    /* ... */
    useHydrationHeap: {
        priorityForceStart?: number,
        startDelay?: number,
    }
}
```

### Updates

  * `@yandex-market/apiary-src`: [3.1.0](../apiary/changelog.md#310) (was [3.0.4](../apiary/changelog.md#304))

# 18.2.2

- Починено логирование размера ответа для легаси ресурсов (https://st.yandex-team.ru/MARKETFRONTECH-2702)

# 18.2.1

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [0.4.1](../invariant/changelog.md#041) (was [0.4.0](../invariant/changelog.md#040))
  * `@yandex-market/bcm2`: [3.0.7](../bcm2/changelog.md#307) (was [3.0.6](../bcm2/changelog.md#306))
  * `@yandex-market/stout`: [1.1.25](../stout/changelog.md#1125) (was [1.1.24](../stout/changelog.md#1124))
  * `@yandex-market/apiary-src`: [3.0.4](../apiary/changelog.md#304) (was [3.0.3](../apiary/changelog.md#303))
  * `eslint-plugin-stout`: [1.0.4](../../tools/eslint-plugin-stout/changelog.md#104) (was [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103))

# 18.2.0

[Добавлена возможность прокидывать заголовок X-Yandex-Antirobot-Degradation](https://st.yandex-team.ru/MARKETFRONT-42015)

- Добавлена обработка заголовка `X-Yandex-Antirobot-Degradation`.
    - реализован автоматический проброс заголовка в бэкенды
    - значение заголовка кладётся в общие поля метрики `antirobotDegradation`.

### Usage

Имеется возможность получать его через резолвер `resolveAntirobotDegradationSync`,
который находится в `lib/lib/mandrel/src/resolvers/page.js`, в который нужно передать контекст.

# 18.1.6

* не роняем запуск сервера в деве при отсутствии version.txt

# 18.1.5

Включаем beacon API для отправки метрики в RUM

# 18.1.4

Обновляем дев-тулы

- более понятные алиасы
- менее яркий цвет на зональной кнопке
- копирование по наведению на серверной трассировке
- чуть более интуитивный порядок кнопок

# 18.1.3

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [3.0.3](../apiary/changelog.md#303) (was [3.0.2](../apiary/changelog.md#302))

# 18.1.2

Чиним ошибку запуска ноды, если выставлен NODE_PATH с путями до дефолтных глобальных node_modules.

# 18.1.1

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [3.0.2](../apiary/changelog.md#302) (was [3.0.1](../apiary/changelog.md#301))

# 18.1.0

Добавлена возможность вручную выставлять загововки и тело ответа в FAPI.

### Usage

```js
// handler.js

import {createCustomResponse, createHandler} from '@yandex-market/mandrel/handler';
// Резолвер, который возвращает .pdf
import {resolveSomePdf} from './path/to/resolver'

const handle = async (ctx: Context, ...args) => {
    // Дергаем резолвер
    const result = await resolver(ctx, ...args);
    
    // Первым аргументом передаем объект с заголовками
    // Вторым аргументом передаем тело ответа
    return createCustomResponse(
        {
            'content-type': 'application/pdf'
        },
        result
    )
}
 
// Передаем handle в createHandler
```

# 18.0.7

We need to go deeper. Теперь `LazyLoader` может отрисовать `LazyLoader`. Это чинит сценарии использования `MultiScrollBox`

# 18.0.6

Увеличение таймаута на ручке fetchIosToken
из за долгого ответа сервиса apple.

# 18.0.5

Чтобы понять, правильно ли мы шлем метрики скорости, повесили логирование на отправку некорректных данных.
Оказалось, что таких случаев много, и теперь слишком много логов отправляется error-booster. Убираем логирование. 

[Пример](https://error.yandex-team.ru/projects/market_front_blue/projectDashboard?filter=page%20==%20blue-market%3Aproduct&from=2021-06-01%2010:54:00&to=2021-06-02%2010:35:00)

# 18.0.4

Добавлено правило санитайзинга '<!' , для обработки случаев  `<!--<script>`

### Updates

  * `@yandex-market/apiary-src`: [3.0.1](../apiary/changelog.md#301) (was [3.0.0](../apiary/changelog.md#300))

# 18.0.3

Обработчик ошибки при остутсвии  Ya

# 18.0.2

Выставляем лимит в 50 виджетов для ручки /api/lazy-render

# 18.0.1

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [0.4.0](../invariant/changelog.md#040) (was [0.3.5](../invariant/changelog.md#035))
  * `@yandex-market/apiary-src`: [3.0.0](../apiary/changelog.md#300) (was [2.0.8](../apiary/changelog.md#208))

# 18.0.0

MARKETFRONTECH-2548: Исправление поля slots для rum counter - теперь данные берутся из expBuckets (нужно будет их прокинуть из всех фронтов) - так что там будут правильные buckets.

### Usage

Так же, как и раньше Т_Т

### Migration

Теперь в Options инициализации надо прокидывать expBuckets, например, так:
```js
        expBuckets: pathOrUnsafe({}, ['abt', 'expBuckets'], request)
```

И нужно убрать оттуда testIds - они не используется более в мандреле.

# 17.5.1

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [2.0.8](../apiary/changelog.md#208) (was [2.0.7](../apiary/changelog.md#207))

# 17.5.0

Правим сбор клиентских метрик для виджета.  

- Ленивые виджеты соибирались чудом, т.к. вотчер их не дожидался и срабытывал по dom-complete
- В RUM отсылается плохая метрика (c `Infinity`), что приводит к выбросу всей записи

Подробности тут: MARKETFRONT-40392

### Usage

Как и раньше, при создании `LazyLoader` надо правильно заполнять `measured` и `timerId`

- ```{measured: `lazy-${slotName}`}```
- ```timerId: slotName```

# 17.4.2

Исправлена 500 при _mod=requests и удалены сертификаты из ответа

# 17.4.1

Обновление зависимостей

### Updates

  * `@yandex-market/bcm2`: [3.0.6](../bcm2/changelog.md#306) (was [3.0.5](../bcm2/changelog.md#305))

# 17.4.0

Правки в валидации FAPI

### Usage

Осталась проверка возможности валидации через UserAgent только для определённых ручек белого,
в которые ходит синее приложение.
https://st.yandex-team.ru/MARKETFRONT-18958#60a3d4dbeb87c85cf4102a48

# 17.3.0

* Добавлена новая кнопка во внутренних девтулзах во фронте (буква - C)

* Кнопка открывает редактор CMS главного CMS контента находящегося на просматриваемой странице в новой вкладке

* Если нет контента от CMS виджет неактивен (серый фон, нет перехода в редактор)

* Поиск CMS контента производится по аттрибуту [data-cms-page-id] с указанным id страницы

### Usage

* DevTools кнопка - C

# 17.2.1

Игнорим node_modules-prod для автотестов

### Updates

  * `@yandex-market/error`: [1.4.5](../error/changelog.md#145) (was [1.4.4](../error/changelog.md#144))
  * `@yandex-market/invariant`: [0.3.5](../invariant/changelog.md#035) (was [0.3.4](../invariant/changelog.md#034))
  * `@yandex-market/bcm2`: [3.0.5](../bcm2/changelog.md#305) (was [3.0.4](../bcm2/changelog.md#304))
  * `@yandex-market/stout`: [1.1.24](../stout/changelog.md#1124) (was [1.1.23](../stout/changelog.md#1123))
  * `@yandex-market/apiary-src`: [2.0.7](../apiary/changelog.md#207) (was [2.0.6](../apiary/changelog.md#206))

# 17.2.0

**Валидация ios приложений в fapi**

### Usage

**Валидация ios приложений в fapi**

# 17.1.7

* Выпилен image-goodness.min в Rum. Это полечило клиентские падения в marketfront.

* Исправлена ошибка сборки динамического импорта в дев-тулзах.

Теперь можно попытаться вмержить новый монорепный мандрель в маркетфронт.

# 17.1.6

Нативная зависимость от yate

### Updates

  * `@yandex-market/apiary-src`: [2.0.6](../apiary/changelog.md#206) (was [2.0.5](../apiary/changelog.md#205))

# 17.1.5

Нативная зависимость от yate

### Updates

  * `@yandex-market/apiary-src`: [2.0.5](../apiary/changelog.md#205) (was [2.0.4](../apiary/changelog.md#204))

# 17.1.4

* добавлена документация про клиентские метрики через Gauge и RUM
* добавлены события старта и окончания инициализации Apiary на клиенте

# 17.1.3

* добавлена ручка `api/profile` для снятия профиля CPU

# 17.1.2

* Вернул mandrel-src статус private

# 17.1.1

* Делаем репозиторий mandrel public

# 17.1.0

* Удалил нодовый assert из зависимостей logger
* Поднял версию logger в мандреле

### Usage

* Нужно установить свежий логгер

# 17.0.2

Более правильно настроенное поле bin

# 17.0.1

Фиксы тестов

### Updates

  * `@yandex-market/error`: [1.4.4](../error/changelog.md#144) (was [1.4.3](../error/changelog.md#143))
  * `@yandex-market/invariant`: [0.3.4](../invariant/changelog.md#034) (was [0.3.3](../invariant/changelog.md#033))
  * `@yandex-market/apiary-src`: [2.0.4](../apiary/changelog.md#204) (was [2.0.3](../apiary/changelog.md#203))

# 17.0.0

Переезд в монорепу

### Usage

Ничего нового не добавлено

### Migration

Установить свежие версии:

- @yandex-market/apiary
- @yandex-market/stout
- @yandex-market/invariant
- @yandex-market/error
- luster-trace-log

Поменять источник установки пакетов:

- Установить yate из npm: `"yate": "npm:@yandex-market/yate@0.0.83-r"`
- Установить Response из npm: `"Response": "npm:@yandex-market/Response@^1.0.9"`

### Updates

  * `luster-trace-log`: [1.1.6](../luster-trace-log/changelog.md#116) (was [1.1.5](../luster-trace-log/changelog.md#115))
  * `@yandex-market/stout`: [1.1.23](../stout/changelog.md#1123) (was [1.1.22](../stout/changelog.md#1122))
  * `@yandex-market/apiary-src`: [2.0.3](../apiary/changelog.md#203) (was [2.0.2](../apiary/changelog.md#202))
