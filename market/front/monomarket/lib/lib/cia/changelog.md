# 4.3.0

**PR:** [#2767267](https://a.yandex-team.ru/review/2767267)
**Author:** @robot-metatron **Date:** 2022-07-28

MARKETFRONT-99209 Добавил возможность подкладывать метаинформацию во все события баобаба

### Usage

Для создания класса Sender используй `createSenderClass`

# 4.2.1

**PR:** [#2744856](https://a.yandex-team.ru/review/2744856)
**Author:** @dv-mikhaylov **Date:** 2022-07-18

**[[MARKETFRONTECH-4687]]**

# 4.2.0

**PR:** [#2664658](https://a.yandex-team.ru/review/2664658)
**Author:** @robot-metatron **Date:** 2022-07-15

Добавал API для создания Baobab-узлов на сервере, и регистрацию их на клиенте

### Usage

Использовать `Boabab.server(...)` для создания серверного билдера узлов и `Baobab.registerManually` для включения залогированого узла в UI дерево

# 4.1.1

**PR:** [#2663215](https://a.yandex-team.ru/review/2663215)
**Author:** @robot-metatron **Date:** 2022-06-28

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.11.1](../apiary/changelog.md#4111) (was [4.11.0](../apiary/changelog.md#4110))

# 4.1.0

**PR:** [#2628400](https://a.yandex-team.ru/review/2628400)
**Author:** @robot-metatron **Date:** 2022-06-20

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.11.0](../apiary/changelog.md#4110) (was [4.10.2](../apiary/changelog.md#4102))

# 4.0.1

**PR:** [#2650527](https://a.yandex-team.ru/review/2650527)
**Author:** @robot-metatron **Date:** 2022-06-20

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.3](../../shared/declarations/changelog.md#313) (was [3.1.2](../../shared/declarations/changelog.md#312))
  * `@yandex-market/apiary-src`: [4.10.2](../apiary/changelog.md#4102) (was [4.10.1](../apiary/changelog.md#4101))

# 4.0.0

**PR:** [#2614119](https://a.yandex-team.ru/review/2614119)
**Author:** @as-kondratev **Date:** 2022-06-16

Переделал механизм построения баобаб-дерева, теперь вместо useEffect используется MutationObserver

### Usage

После Baobab.configure нужно сделать Baobab.observe на нужном узле (document.body)

### Migration

После Baobab.configure нужно сделать Baobab.observe на нужном узле (document.body)

# 3.7.5

**PR:** [#2620413](https://a.yandex-team.ru/review/2620413)
**Author:** @anseal **Date:** 2022-06-08

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.10.1](../apiary/changelog.md#4101) (was [4.10.0](../apiary/changelog.md#4100))

# 3.7.4

**PR:** [#2616231](https://a.yandex-team.ru/review/2616231)
**Author:** @a-novichkov-k **Date:** 2022-06-08

Для ZoneContainer переписано решение как поставляется ref
чтобы не затирать ref внутри child компонента если он есть

# 3.7.3

**PR:** [#2595101](https://a.yandex-team.ru/review/2595101)
**Author:** @hurtsok **Date:** 2022-06-01

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.10.0](../apiary/changelog.md#4100) (was [4.9.1](../apiary/changelog.md#491))

# 3.7.2

**PR:** [#2587715](https://a.yandex-team.ru/review/2587715)
**Author:** @bykhovtsev **Date:** 2022-06-01

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.9.1](../apiary/changelog.md#491) (was [4.9.0](../apiary/changelog.md#490))
  * `@yandex-market/server-exps`: [2.1.1](../server-exps/changelog.md#211) (was [2.1.0](../server-exps/changelog.md#210))

# 3.7.1

**PR:** [#2536350](https://a.yandex-team.ru/review/2536350)
**Author:** @anseal **Date:** 2022-05-31

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.9.0](../apiary/changelog.md#490) (was [4.8.0](../apiary/changelog.md#480))

# 3.7.0

**PR:** [#2585474](https://a.yandex-team.ru/review/2585474)
**Author:** @xavescor **Date:** 2022-05-30

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.8.0](../apiary/changelog.md#480) (was [4.7.0](../apiary/changelog.md#470))

# 3.6.0

**PR:** [#2528234](https://a.yandex-team.ru/review/2528234)
**Author:** @xavescor **Date:** 2022-05-20

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.7.0](../apiary/changelog.md#470) (was [4.6.0](../apiary/changelog.md#460))
  * `@yandex-market/server-exps`: [2.1.0](../server-exps/changelog.md#210) (was [2.0.5](../server-exps/changelog.md#205))

# 3.5.1

**PR:** [#2549557](https://a.yandex-team.ru/review/2549557)
**Author:** @smelukov **Date:** 2022-05-20

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.6.0](../apiary/changelog.md#460) (was [4.5.0](../apiary/changelog.md#450))

# 3.5.0

**PR:** [#2522594](https://a.yandex-team.ru/review/2522594)
**Author:** @as-kondratev **Date:** 2022-05-11

https://st.yandex-team.ru/MARKETFRONT-82026 добавил подписку на `contextmenu` и `middle mouse button`
для логирования клика в Baobab

### Usage

Ничего не изменилось

# 3.4.0

**PR:** [#2489763](https://a.yandex-team.ru/review/2489763)
**Author:** @gluhovroma **Date:** 2022-05-05

**Обновил babel и его плагины до последних версий [[MARKETFRONT-83092]]**

### Usage

**Обновите babel в своих проектах [[MARKETFRONT-83092]]**

### Updates

  * `@yandex-market/apiary-src`: [4.5.0](../apiary/changelog.md#450) (was [4.4.19](../apiary/changelog.md#4419))

# 3.3.9

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

### Updates

  * `@yandex-market/invariant`: [1.1.8](../invariant/changelog.md#118) (was [1.1.7](../invariant/changelog.md#117))
  * `@yandex-market/logger-src`: [3.0.13](../logger/changelog.md#3013) (was [3.0.12](../logger/changelog.md#3012))
  * `@yandex-market/apiary-src`: [4.4.19](../apiary/changelog.md#4419) (was [4.4.18](../apiary/changelog.md#4418))
  * `@yandex-market/server-exps`: [2.0.5](../server-exps/changelog.md#205) (was [2.0.4](../server-exps/changelog.md#204))

# 3.3.8

**PR:** [#2495391](https://a.yandex-team.ru/review/2495391)
**Author:** @maslov-rn **Date:** 2022-04-25

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.18](../apiary/changelog.md#4418) (was [4.4.17](../apiary/changelog.md#4417))

# 3.3.7

**PR:** [#2464128](https://a.yandex-team.ru/review/2464128)
**Author:** @gheljenor **Date:** 2022-04-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.2](../../shared/declarations/changelog.md#312) (was [3.1.1](../../shared/declarations/changelog.md#311))
  * `@yandex-market/apiary-src`: [4.4.17](../apiary/changelog.md#4417) (was [4.4.16](../apiary/changelog.md#4416))

# 3.3.6

**PR:** [#2463913](https://a.yandex-team.ru/review/2463913)
**Author:** @gheljenor **Date:** 2022-04-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.1](../../shared/declarations/changelog.md#311) (was [3.1.0](../../shared/declarations/changelog.md#310))
  * `@yandex-market/apiary-src`: [4.4.16](../apiary/changelog.md#4416) (was [4.4.15](../apiary/changelog.md#4415))

# 3.3.5

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

### Updates

  * `@yandex-market/invariant`: [1.1.7](../invariant/changelog.md#117) (was [1.1.6](../invariant/changelog.md#116))
  * `@yandex-market/logger-src`: [3.0.12](../logger/changelog.md#3012) (was [3.0.11](../logger/changelog.md#3011))
  * `@yandex-market/apiary-src`: [4.4.15](../apiary/changelog.md#4415) (was [4.4.14](../apiary/changelog.md#4414))
  * `@yandex-market/server-exps`: [2.0.4](../server-exps/changelog.md#204) (was [2.0.3](../server-exps/changelog.md#203))

# 3.3.4

**PR:** [#1012](https://github.yandex-team.ru/market/monomarket/pull/1012)
**Author:** @bykhovtsev **Date:** 2022-04-06

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.14](../apiary/changelog.md#4414) (was [4.4.13](../apiary/changelog.md#4413))

# 3.3.3

**PR:** [#970](https://github.yandex-team.ru/market/monomarket/pull/970)
**Author:** @maslov-rn **Date:** 2022-03-31

Правка прекомитной проверки check-flow-files

### Updates

  * `@yandex-market/apiary-src`: [4.4.13](../apiary/changelog.md#4413) (was [4.4.12](../apiary/changelog.md#4412))

# 3.3.2

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.6](../invariant/changelog.md#116) (was [1.1.5](../invariant/changelog.md#115))
  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))
  * `@yandex-market/logger-src`: [3.0.11](../logger/changelog.md#3011) (was [3.0.10](../logger/changelog.md#3010))
  * `@yandex-market/apiary-src`: [4.4.12](../apiary/changelog.md#4412) (was [4.4.11](../apiary/changelog.md#4411))
  * `@yandex-market/server-exps`: [2.0.3](../server-exps/changelog.md#203) (was [2.0.2](../server-exps/changelog.md#202))

# 3.3.1

**PR:** [#972](https://github.yandex-team.ru/market/monomarket/pull/972)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.11](../apiary/changelog.md#4411) (was [4.4.10](../apiary/changelog.md#4410))

# 3.3.0

**PR:** [#854](https://github.yandex-team.ru/market/monomarket/pull/854)
**Author:** @as-kondratev **Date:** 2022-03-10

Добавил возможность логировать метрики в Баобаб [MARKETFRONT-62930](https://st.yandex-team.ru/MARKETFRONT-62930)

### Usage

Для включения логирования в Баобаб, нужно указать проп `mode: 'baobab'` или `mode: 'both'` у компонента `Zone` или у HOC-ов
`withZone` и `withConnectedZone`. Для включения сенсора передать в `initSensors` `true` вторым параметром. Подробнее в документации

### Updates

  * `@yandex-market/declarations`: [3.1.0](../../shared/declarations/changelog.md#310) (was [3.0.2](../../shared/declarations/changelog.md#302))
  * `@yandex-market/apiary-src`: [4.4.10](../apiary/changelog.md#4410) (was [4.4.9](../apiary/changelog.md#449))

# 3.2.16

**PR:** [#866](https://github.yandex-team.ru/market/monomarket/pull/866)
**Author:** @bykhovtsev **Date:** 2022-02-24

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.9](../apiary/changelog.md#449) (was [4.4.8](../apiary/changelog.md#448))

# 3.2.15

**PR:** [#806](https://github.yandex-team.ru/market/monomarket/pull/806)
**Author:** @asvasilenko **Date:** 2022-02-17

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.8](../apiary/changelog.md#448) (was [4.4.7](../apiary/changelog.md#447))

# 3.2.14

**PR:** [#797](https://github.yandex-team.ru/market/monomarket/pull/797)
**Author:** @dv-mikhaylov **Date:** 2022-02-03

Добавлена прекоммитная проверка check-flow-files, которая сравнивает файл с разрешением ts в папке src и ищет такой же файл в папке flow https://st.yandex-team.ru/MARKETFRONTECH-3273

### Updates

  * `@yandex-market/check-flow-files`: [1.0.1](../../scripts/check-flow/changelog.md#101) (was [1.0.0](../../scripts/check-flow/changelog.md#100))
  * `@yandex-market/apiary-src`: [4.4.7](../apiary/changelog.md#447) (was [4.4.6](../apiary/changelog.md#446))

# 3.2.13

**PR:** [#810](https://github.yandex-team.ru/market/monomarket/pull/810)
**Author:** @gheljenor **Date:** 2022-01-31

Обновление зависимостей

### Updates

  * `@yandex-market/error`: [1.5.1](../error/changelog.md#151) (was [1.5.0](../error/changelog.md#150))
  * `@yandex-market/invariant`: [1.1.5](../invariant/changelog.md#115) (was [1.1.4](../invariant/changelog.md#114))
  * `@yandex-market/apiary-src`: [4.4.6](../apiary/changelog.md#446) (was [4.4.5](../apiary/changelog.md#445))

# 3.2.12

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.4](../invariant/changelog.md#114) (was [1.1.3](../invariant/changelog.md#113))
  * `@yandex-market/logger-src`: [3.0.10](../logger/changelog.md#3010) (was [3.0.9](../logger/changelog.md#309))
  * `@yandex-market/apiary-src`: [4.4.5](../apiary/changelog.md#445) (was [4.4.4](../apiary/changelog.md#444))
  * `@yandex-market/server-exps`: [2.0.2](../server-exps/changelog.md#202) (was [2.0.1](../server-exps/changelog.md#201))

# 3.2.11

**PR:** [#603](https://github.yandex-team.ru/market/monomarket/pull/603)
**Author:** @bykovski-ilya **Date:** 2021-12-21

**Починил ошибку в зависимости пакета - openapi-to-bcm**

### Updates

  * `@yandex-market/apiary-src`: [4.4.4](../apiary/changelog.md#444) (was [4.4.3](../apiary/changelog.md#443))

# 3.2.10

**PR:** [#640](https://github.yandex-team.ru/market/monomarket/pull/640)
**Author:** @maslov-rn **Date:** 2021-12-08

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.3](../apiary/changelog.md#443) (was [4.4.2](../apiary/changelog.md#442))

# 3.2.9

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

[MARKETFRONTECH-3408](https://st.yandex-team.ru/MARKETFRONTECH-3408) - Починить сборки

### Updates

  * `@yandex-market/invariant`: [1.1.3](../invariant/changelog.md#113) (was [1.1.2](../invariant/changelog.md#112))
  * `@yandex-market/logger-src`: [3.0.9](../logger/changelog.md#309) (was [3.0.8](../logger/changelog.md#308))
  * `@yandex-market/apiary-src`: [4.4.2](../apiary/changelog.md#442) (was [4.4.1](../apiary/changelog.md#441))
  * `@yandex-market/server-exps`: [2.0.1](../server-exps/changelog.md#201) (was [2.0.0](../server-exps/changelog.md#200))

# 3.2.8

**PR:** [#528](https://github.yandex-team.ru/market/monomarket/pull/528)
**Author:** @mtvv **Date:** 2021-11-12

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.1](../apiary/changelog.md#441) (was [4.4.0](../apiary/changelog.md#440))

# 3.2.7

**PR:** [#496](https://github.yandex-team.ru/market/monomarket/pull/496)
**Author:** @maslov-rn **Date:** 2021-10-29

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.0](../apiary/changelog.md#440) (was [4.3.2](../apiary/changelog.md#432))

# 3.2.6

**PR:** [#423](https://github.yandex-team.ru/market/monomarket/pull/423)
**Author:** @juleari **Date:** 2021-10-21

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.3.2](../apiary/changelog.md#432) (was [4.3.1](../apiary/changelog.md#431))

# 3.2.5

**PR:** [#352](https://github.yandex-team.ru/market/monomarket/pull/352)
**Author:** @fenruga **Date:** 2021-10-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.0.2](../../shared/declarations/changelog.md#302) (was [3.0.1](../../shared/declarations/changelog.md#301))
  * `@yandex-market/apiary-src`: [4.3.1](../apiary/changelog.md#431) (was [4.3.0](../apiary/changelog.md#430))

# 3.2.4

**PR:** [#410](https://github.yandex-team.ru/market/monomarket/pull/410)
**Author:** @maslov-rn **Date:** 2021-10-07

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.3.0](../apiary/changelog.md#430) (was [4.2.3](../apiary/changelog.md#423))
  * `@yandex-market/server-exps`: [2.0.0](../server-exps/changelog.md#200) (was [1.0.0](../server-exps/changelog.md#100))

# 3.2.3

**PR:** [#424](https://github.yandex-team.ru/market/monomarket/pull/424)
**Author:** @gheljenor **Date:** 2021-10-06

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.2.3](../apiary/changelog.md#423) (was [4.2.2](../apiary/changelog.md#422))

# 3.2.2

**PR:** [#320](https://github.yandex-team.ru/market/monomarket/pull/320)
**Author:** @ashwets **Date:** 2021-09-15

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.2](../invariant/changelog.md#112) (was [1.1.1](../invariant/changelog.md#111))
  * `@yandex-market/logger-src`: [3.0.8](../logger/changelog.md#308) (was [3.0.7](../logger/changelog.md#307))
  * `@yandex-market/apiary-src`: [4.2.2](../apiary/changelog.md#422) (was [4.2.1](../apiary/changelog.md#421))

# 3.2.1

**PR:** [#209](https://github.yandex-team.ru/market/monomarket/pull/209)
**Author:** @pavelko95 **Date:** 2021-09-15

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.1](../invariant/changelog.md#111) (was [1.1.0](../invariant/changelog.md#110))
  * `@yandex-market/logger-src`: [3.0.7](../logger/changelog.md#307) (was [3.0.6](../logger/changelog.md#306))
  * `@yandex-market/apiary-src`: [4.2.1](../apiary/changelog.md#421) (was [4.2.0](../apiary/changelog.md#420))

# 3.2.0

**PR:** [#313](https://github.yandex-team.ru/market/monomarket/pull/313)
**Author:** @ivan-afanasov **Date:** 2021-09-10

Обновление зависимостей

### Updates

  * `@yandex-market/error`: [1.5.0](../error/changelog.md#150) (was [1.4.6](../error/changelog.md#146))
  * `@yandex-market/invariant`: [1.1.0](../invariant/changelog.md#110) (was [1.0.5](../invariant/changelog.md#105))
  * `@yandex-market/apiary-src`: [4.2.0](../apiary/changelog.md#420) (was [4.1.1](../apiary/changelog.md#411))

# 3.1.8

**PR:** [#206](https://github.yandex-team.ru/market/monomarket/pull/206)
**Author:** @antonk52 **Date:** 2021-09-06

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.5](../invariant/changelog.md#105) (was [1.0.4](../invariant/changelog.md#104))
  * `@yandex-market/logger-src`: [3.0.6](../logger/changelog.md#306) (was [3.0.5](../logger/changelog.md#305))
  * `@yandex-market/apiary-src`: [4.1.1](../apiary/changelog.md#411) (was [4.1.0](../apiary/changelog.md#410))

# 3.1.7

**PR:** [#234](https://github.yandex-team.ru/market/monomarket/pull/234)
**Author:** @nickshevr **Date:** 2021-08-16

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.1.0](../apiary/changelog.md#410) (was [4.0.8](../apiary/changelog.md#408))

# 3.1.6

**PR:** [#207](https://github.yandex-team.ru/market/monomarket/pull/207)
**Author:** @juleari **Date:** 2021-08-09

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.4](../invariant/changelog.md#104) (was [1.0.3](../invariant/changelog.md#103))
  * `@yandex-market/logger-src`: [3.0.5](../logger/changelog.md#305) (was [3.0.4](../logger/changelog.md#304))
  * `@yandex-market/apiary-src`: [4.0.8](../apiary/changelog.md#408) (was [4.0.7](../apiary/changelog.md#407))

# 3.1.5

**PR:** [#222](https://github.yandex-team.ru/market/monomarket/pull/222)
**Author:** @juleari **Date:** 2021-08-09

[MARKETFRONTECH-2993](https://st.yandex-team.ru/MARKETFRONTECH-2993) - [Монорепа] Починить ссылки в ченжлогах

### Updates

  * `@yandex-market/logger-src`: [3.0.4](../logger/changelog.md#304) (was [3.0.3](../logger/changelog.md#303))
  * `@yandex-market/apiary-src`: [4.0.7](../apiary/changelog.md#407) (was [4.0.6](../apiary/changelog.md#406))

# 3.1.4

**PR:** [#215](https://github.yandex-team.ru/market/monomarket/pull/215)
**Author:** @gheljenor **Date:** 2021-08-04

[MARKETFRONTECH-2974](https://st.yandex-team.ru/MARKETFRONTECH-2974) - [Монорепа] Убираем скрипты из генерируемых пакетов

### Updates

  * `@yandex-market/logger-src`: [3.0.3](../logger/changelog.md#303) (was [3.0.2](../logger/changelog.md#302))
  * `@yandex-market/apiary-src`: [4.0.6](../apiary/changelog.md#406) (was [4.0.5](../apiary/changelog.md#405))

# 3.1.3

**PR:** [#212](https://github.yandex-team.ru/market/monomarket/pull/212)
**Author:** @bykhovtsev **Date:** 2021-08-04

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.0.5](../apiary/changelog.md#405) (was [4.0.4](../apiary/changelog.md#404))

# 3.1.2

**PR:** [#201](https://github.yandex-team.ru/market/monomarket/pull/201)
**Author:** @gheljenor **Date:** 2021-08-02

Изменение версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.3](../invariant/changelog.md#103) (was [1.0.2](../invariant/changelog.md#102))
  * `@yandex-market/declarations`: [3.0.1](../../shared/declarations/changelog.md#301) (was [3.0.0](../../shared/declarations/changelog.md#300))
  * `@yandex-market/logger-src`: [3.0.2](../logger/changelog.md#302) (was [3.0.1](../logger/changelog.md#301))
  * `@yandex-market/apiary-src`: [4.0.4](../apiary/changelog.md#404) (was [4.0.3](../apiary/changelog.md#403))

# 3.1.1

**PR:** [#205](https://github.yandex-team.ru/market/monomarket/pull/205)
**Author:** @dgudenkov **Date:** 2021-07-30

- убрал саппресы flow

### Updates

  * `@yandex-market/declarations`: [3.0.0](../../shared/declarations/changelog.md#300) (was [2.0.0](../../shared/declarations/changelog.md#200))
  * `@yandex-market/apiary-src`: [4.0.3](../apiary/changelog.md#403) (was [4.0.2](../apiary/changelog.md#402))

# 3.1.0

**PR:** [#193](https://github.yandex-team.ru/market/monomarket/pull/193)
**Author:** @bra31k **Date:** 2021-07-29

Добавлена возможность прокидывать приватные экншы в метрику

### Usage

Теперь в зону можно прокинуть дополнительный параметр - allowPrivateActions, если он true - приватные экшны не будут скипаться

# 3.0.1

**PR:** [#191](https://github.yandex-team.ru/market/monomarket/pull/191)
**Author:** @avdotion **Date:** 2021-07-26

Изменён формат описания времени сборки

# 3.0.0

**PR:** [#175](https://github.yandex-team.ru/market/monomarket/pull/175)
**Author:** @loyd **Date:** 2021-07-26

Пакет `@yandex-market/cia` в монорепозитории!

### Usage

Как и раньше.

### Migration

Просто установите `@yandex-market/cia` и не забудьте обновиться до последних версий `prop-types@15.6.1`.

### Updates

  * `@yandex-market/declarations`: [2.0.0](../../shared/declarations/changelog.md#200) (was [1.0.0](../../shared/declarations/changelog.md#100))
  * `@yandex-market/apiary-src`: [4.0.2](../apiary/changelog.md#402) (was [4.0.1](../apiary/changelog.md#401))