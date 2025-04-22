# 2.5.0

**PR:** [#2663215](https://a.yandex-team.ru/review/2663215)
**Author:** @robot-metatron **Date:** 2022-06-28

AmpHtml

### Usage

При вызове metaJob из apiary-anex, можно передать поле со ссылкой на amp страницу
    после чего ссылка будет встроена в html при рендере в виде

```html
<link rel="amphtml" href=[amphtml]>
```

В контроллере компонента это выглядит вот так:

```javascript
            jobs: [
                metaJob({
                    ampHtml: Promise.resolve('url to page')
                }),
            ],
```

### Updates

  * `@yandex-market/apiary-src`: [4.11.1](../apiary/changelog.md#4111) (was [4.11.0](../apiary/changelog.md#4110))

# 2.4.0

**PR:** [#2628400](https://a.yandex-team.ru/review/2628400)
**Author:** @robot-metatron **Date:** 2022-06-20

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.11.0](../apiary/changelog.md#4110) (was [4.10.2](../apiary/changelog.md#4102))

# 2.3.5

**PR:** [#2650527](https://a.yandex-team.ru/review/2650527)
**Author:** @robot-metatron **Date:** 2022-06-20

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.3](../../shared/declarations/changelog.md#313) (was [3.1.2](../../shared/declarations/changelog.md#312))
  * `@yandex-market/apiary-src`: [4.10.2](../apiary/changelog.md#4102) (was [4.10.1](../apiary/changelog.md#4101))

# 2.3.4

**PR:** [#2620413](https://a.yandex-team.ru/review/2620413)
**Author:** @anseal **Date:** 2022-06-08

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.10.1](../apiary/changelog.md#4101) (was [4.10.0](../apiary/changelog.md#4100))

# 2.3.3

**PR:** [#2595101](https://a.yandex-team.ru/review/2595101)
**Author:** @hurtsok **Date:** 2022-06-01

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.10.0](../apiary/changelog.md#4100) (was [4.9.1](../apiary/changelog.md#491))

# 2.3.2

**PR:** [#2587715](https://a.yandex-team.ru/review/2587715)
**Author:** @bykhovtsev **Date:** 2022-06-01

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.9.1](../apiary/changelog.md#491) (was [4.9.0](../apiary/changelog.md#490))
  * `@yandex-market/server-exps`: [2.1.1](../server-exps/changelog.md#211) (was [2.1.0](../server-exps/changelog.md#210))

# 2.3.1

**PR:** [#2536350](https://a.yandex-team.ru/review/2536350)
**Author:** @anseal **Date:** 2022-05-31

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.9.0](../apiary/changelog.md#490) (was [4.8.0](../apiary/changelog.md#480))

# 2.3.0

**PR:** [#2585474](https://a.yandex-team.ru/review/2585474)
**Author:** @xavescor **Date:** 2022-05-30

Откат механизма отмены

### Usage

--

### Updates

  * `@yandex-market/apiary-src`: [4.8.0](../apiary/changelog.md#480) (was [4.7.0](../apiary/changelog.md#470))

# 2.2.0

**PR:** [#2528234](https://a.yandex-team.ru/review/2528234)
**Author:** @xavescor **Date:** 2022-05-20

Обновили тайпинги для компонентов

### Usage

Пустоо

### Updates

  * `@yandex-market/apiary-src`: [4.7.0](../apiary/changelog.md#470) (was [4.6.0](../apiary/changelog.md#460))
  * `@yandex-market/server-exps`: [2.1.0](../server-exps/changelog.md#210) (was [2.0.5](../server-exps/changelog.md#205))

# 2.1.1

**PR:** [#2549557](https://a.yandex-team.ru/review/2549557)
**Author:** @smelukov **Date:** 2022-05-20

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.6.0](../apiary/changelog.md#460) (was [4.5.0](../apiary/changelog.md#450))

# 2.1.0

**PR:** [#2489763](https://a.yandex-team.ru/review/2489763)
**Author:** @gluhovroma **Date:** 2022-05-05

**Обновил babel и его плагины до последних версий [[MARKETFRONT-83092]]**

### Usage

**Обновите babel в своих проектах [[MARKETFRONT-83092]]**

### Updates

  * `@yandex-market/apiary-src`: [4.5.0](../apiary/changelog.md#450) (was [4.4.19](../apiary/changelog.md#4419))

# 2.0.25

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

### Updates

  * `@yandex-market/invariant`: [1.1.8](../invariant/changelog.md#118) (was [1.1.7](../invariant/changelog.md#117))
  * `@yandex-market/apiary-src`: [4.4.19](../apiary/changelog.md#4419) (was [4.4.18](../apiary/changelog.md#4418))
  * `@yandex-market/server-exps`: [2.0.5](../server-exps/changelog.md#205) (was [2.0.4](../server-exps/changelog.md#204))
  * `@yandex-market/logger-src`: [3.0.13](../logger/changelog.md#3013) (was [3.0.12](../logger/changelog.md#3012))

# 2.0.24

**PR:** [#2495391](https://a.yandex-team.ru/review/2495391)
**Author:** @maslov-rn **Date:** 2022-04-25

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.18](../apiary/changelog.md#4418) (was [4.4.17](../apiary/changelog.md#4417))

# 2.0.23

**PR:** [#2464128](https://a.yandex-team.ru/review/2464128)
**Author:** @gheljenor **Date:** 2022-04-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.2](../../shared/declarations/changelog.md#312) (was [3.1.1](../../shared/declarations/changelog.md#311))
  * `@yandex-market/apiary-src`: [4.4.17](../apiary/changelog.md#4417) (was [4.4.16](../apiary/changelog.md#4416))

# 2.0.22

**PR:** [#2463913](https://a.yandex-team.ru/review/2463913)
**Author:** @gheljenor **Date:** 2022-04-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.1](../../shared/declarations/changelog.md#311) (was [3.1.0](../../shared/declarations/changelog.md#310))
  * `@yandex-market/apiary-src`: [4.4.16](../apiary/changelog.md#4416) (was [4.4.15](../apiary/changelog.md#4415))

# 2.0.21

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

### Updates

  * `@yandex-market/invariant`: [1.1.7](../invariant/changelog.md#117) (was [1.1.6](../invariant/changelog.md#116))
  * `@yandex-market/apiary-src`: [4.4.15](../apiary/changelog.md#4415) (was [4.4.14](../apiary/changelog.md#4414))
  * `@yandex-market/server-exps`: [2.0.4](../server-exps/changelog.md#204) (was [2.0.3](../server-exps/changelog.md#203))
  * `@yandex-market/logger-src`: [3.0.12](../logger/changelog.md#3012) (was [3.0.11](../logger/changelog.md#3011))

# 2.0.20

**PR:** [#1012](https://github.yandex-team.ru/market/monomarket/pull/1012)
**Author:** @bykhovtsev **Date:** 2022-04-06

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.14](../apiary/changelog.md#4414) (was [4.4.13](../apiary/changelog.md#4413))

# 2.0.19

**PR:** [#970](https://github.yandex-team.ru/market/monomarket/pull/970)
**Author:** @maslov-rn **Date:** 2022-03-31

Правка прекомитной проверки check-flow-files

### Updates

  * `@yandex-market/apiary-src`: [4.4.13](../apiary/changelog.md#4413) (was [4.4.12](../apiary/changelog.md#4412))

# 2.0.18

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.6](../invariant/changelog.md#116) (was [1.1.5](../invariant/changelog.md#115))
  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))
  * `@yandex-market/apiary-src`: [4.4.12](../apiary/changelog.md#4412) (was [4.4.11](../apiary/changelog.md#4411))
  * `@yandex-market/server-exps`: [2.0.3](../server-exps/changelog.md#203) (was [2.0.2](../server-exps/changelog.md#202))
  * `@yandex-market/logger-src`: [3.0.11](../logger/changelog.md#3011) (was [3.0.10](../logger/changelog.md#3010))

# 2.0.17

**PR:** [#972](https://github.yandex-team.ru/market/monomarket/pull/972)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.11](../apiary/changelog.md#4411) (was [4.4.10](../apiary/changelog.md#4410))

# 2.0.16

**PR:** [#854](https://github.yandex-team.ru/market/monomarket/pull/854)
**Author:** @as-kondratev **Date:** 2022-03-10

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.0](../../shared/declarations/changelog.md#310) (was [3.0.2](../../shared/declarations/changelog.md#302))
  * `@yandex-market/apiary-src`: [4.4.10](../apiary/changelog.md#4410) (was [4.4.9](../apiary/changelog.md#449))

# 2.0.15

**PR:** [#866](https://github.yandex-team.ru/market/monomarket/pull/866)
**Author:** @bykhovtsev **Date:** 2022-02-24

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.9](../apiary/changelog.md#449) (was [4.4.8](../apiary/changelog.md#448))

# 2.0.14

**PR:** [#806](https://github.yandex-team.ru/market/monomarket/pull/806)
**Author:** @asvasilenko **Date:** 2022-02-17

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.8](../apiary/changelog.md#448) (was [4.4.7](../apiary/changelog.md#447))

# 2.0.13

**PR:** [#797](https://github.yandex-team.ru/market/monomarket/pull/797)
**Author:** @dv-mikhaylov **Date:** 2022-02-03

Добавлена прекоммитная проверка check-flow-files, которая сравнивает файл с разрешением ts в папке src и ищет такой же файл в папке flow https://st.yandex-team.ru/MARKETFRONTECH-3273

### Updates

  * `@yandex-market/check-flow-files`: [1.0.1](../../scripts/check-flow/changelog.md#101) (was [1.0.0](../../scripts/check-flow/changelog.md#100))
  * `@yandex-market/apiary-src`: [4.4.7](../apiary/changelog.md#447) (was [4.4.6](../apiary/changelog.md#446))

# 2.0.12

**PR:** [#810](https://github.yandex-team.ru/market/monomarket/pull/810)
**Author:** @gheljenor **Date:** 2022-01-31

[MARKETFRONTECH-3151](https://st.yandex-team.ru/MARKETFRONTECH-3151) - [Монорепа] Обновление nodejs 12 -> 14/16

### Updates

  * `@yandex-market/invariant`: [1.1.5](../invariant/changelog.md#115) (was [1.1.4](../invariant/changelog.md#114))
  * `@yandex-market/error`: [1.5.1](../error/changelog.md#151) (was [1.5.0](../error/changelog.md#150))
  * `@yandex-market/apiary-src`: [4.4.6](../apiary/changelog.md#446) (was [4.4.5](../apiary/changelog.md#445))

# 2.0.11

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.4](../invariant/changelog.md#114) (was [1.1.3](../invariant/changelog.md#113))
  * `@yandex-market/apiary-src`: [4.4.5](../apiary/changelog.md#445) (was [4.4.4](../apiary/changelog.md#444))
  * `@yandex-market/server-exps`: [2.0.2](../server-exps/changelog.md#202) (was [2.0.1](../server-exps/changelog.md#201))
  * `@yandex-market/logger-src`: [3.0.10](../logger/changelog.md#3010) (was [3.0.9](../logger/changelog.md#309))

# 2.0.10

**PR:** [#603](https://github.yandex-team.ru/market/monomarket/pull/603)
**Author:** @bykovski-ilya **Date:** 2021-12-21

**Починил ошибку в зависимости пакета - openapi-to-bcm**

### Updates

  * `@yandex-market/apiary-src`: [4.4.4](../apiary/changelog.md#444) (was [4.4.3](../apiary/changelog.md#443))

# 2.0.9

**PR:** [#640](https://github.yandex-team.ru/market/monomarket/pull/640)
**Author:** @maslov-rn **Date:** 2021-12-08

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.3](../apiary/changelog.md#443) (was [4.4.2](../apiary/changelog.md#442))

# 2.0.8

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.3](../invariant/changelog.md#113) (was [1.1.2](../invariant/changelog.md#112))
  * `@yandex-market/apiary-src`: [4.4.2](../apiary/changelog.md#442) (was [4.4.1](../apiary/changelog.md#441))
  * `@yandex-market/server-exps`: [2.0.1](../server-exps/changelog.md#201) (was [2.0.0](../server-exps/changelog.md#200))
  * `@yandex-market/logger-src`: [3.0.9](../logger/changelog.md#309) (was [3.0.8](../logger/changelog.md#308))

# 2.0.7

**PR:** [#528](https://github.yandex-team.ru/market/monomarket/pull/528)
**Author:** @mtvv **Date:** 2021-11-12

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.1](../apiary/changelog.md#441) (was [4.4.0](../apiary/changelog.md#440))

# 2.0.6

**PR:** [#496](https://github.yandex-team.ru/market/monomarket/pull/496)
**Author:** @maslov-rn **Date:** 2021-10-29

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.4.0](../apiary/changelog.md#440) (was [4.3.2](../apiary/changelog.md#432))

# 2.0.5

**PR:** [#423](https://github.yandex-team.ru/market/monomarket/pull/423)
**Author:** @juleari **Date:** 2021-10-21

[MARKETFRONTECH-3236](https://st.yandex-team.ru/MARKETFRONTECH-3236) - Починить парсинг тикета

### Updates

  * `@yandex-market/apiary-src`: [4.3.2](../apiary/changelog.md#432) (was [4.3.1](../apiary/changelog.md#431))

# 2.0.4

**PR:** [#352](https://github.yandex-team.ru/market/monomarket/pull/352)
**Author:** @fenruga **Date:** 2021-10-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.0.2](../../shared/declarations/changelog.md#302) (was [3.0.1](../../shared/declarations/changelog.md#301))
  * `@yandex-market/apiary-src`: [4.3.1](../apiary/changelog.md#431) (was [4.3.0](../apiary/changelog.md#430))

# 2.0.3

**PR:** [#410](https://github.yandex-team.ru/market/monomarket/pull/410)
**Author:** @maslov-rn **Date:** 2021-10-07

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.3.0](../apiary/changelog.md#430) (was [4.2.3](../apiary/changelog.md#423))
  * `@yandex-market/server-exps`: [2.0.0](../server-exps/changelog.md#200) (was [1.0.0](../server-exps/changelog.md#100))

# 2.0.2

**PR:** [#424](https://github.yandex-team.ru/market/monomarket/pull/424)
**Author:** @gheljenor **Date:** 2021-10-06

Обновление зависимостей

### Updates

  * `@yandex-market/apiary-src`: [4.2.3](../apiary/changelog.md#423) (was [4.2.2](../apiary/changelog.md#422))

# 2.0.1

**PR:** [#320](https://github.yandex-team.ru/market/monomarket/pull/320)
**Author:** @ashwets **Date:** 2021-09-15

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.2](../invariant/changelog.md#112) (was [1.1.1](../invariant/changelog.md#111))
  * `@yandex-market/apiary-src`: [4.2.2](../apiary/changelog.md#422) (was [4.2.1](../apiary/changelog.md#421))

# 2.0.0

**PR:** [#209](https://github.yandex-team.ru/market/monomarket/pull/209)
**Author:** @pavelko95 **Date:** 2021-09-15

[MARKETFRONTECH-2846](https://st.yandex-team.ru/MARKETFRONTECH-2846) - Привезти @yandex-market/apiary-annex в монорепу

### Usage

Все как и раньше.

### Migration

Все как и раньше.

### Updates

  * `@yandex-market/invariant`: [1.1.1](../invariant/changelog.md#111) (was [1.1.0](../invariant/changelog.md#110))
  * `@yandex-market/apiary-src`: [4.2.1](../apiary/changelog.md#421) (was [4.2.0](../apiary/changelog.md#420))