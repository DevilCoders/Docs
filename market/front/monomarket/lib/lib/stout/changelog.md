# 1.8.0

**PR:** [#2628400](https://a.yandex-team.ru/review/2628400)
**Author:** @robot-metatron **Date:** 2022-06-20

Расширяет возможности проставления кастомного роута. Теперь можно использовать свой роутер сбоку от стаута

### Usage

```js
stout.setUnknownPage(request => susanin.Route('/foo/bar'))
```

# 1.7.0

**PR:** [#2587715](https://a.yandex-team.ru/review/2587715)
**Author:** @bykhovtsev **Date:** 2022-06-01

Поддержка проксирования на стауте.
В случае наличия спец-роута, стаут вместо 404 запустит его страницу

### Usage

`stout.setUnknownPageRoute`, чтобы задать этот роут

### Updates

  * `@yandex-market/server-exps`: [2.1.1](../server-exps/changelog.md#211) (was [2.1.0](../server-exps/changelog.md#210))

# 1.6.0

**PR:** [#2568174](https://a.yandex-team.ru/review/2568174)
**Author:** @maslov-rn **Date:** 2022-05-31

Флаг для сбора ttlb прогрессивной страницы

### Usage

Добавить в конфиг сервиса:
```
solomonMetrics: {
   ttlb: true
}

# 1.5.0

**PR:** [#2528234](https://a.yandex-team.ru/review/2528234)
**Author:** @xavescor **Date:** 2022-05-20

Обновление зависимостей

### Updates

  * `@yandex-market/server-exps`: [2.1.0](../server-exps/changelog.md#210) (was [2.0.5](../server-exps/changelog.md#205))

# 1.4.0

**PR:** [#2526047](https://a.yandex-team.ru/review/2526047)
**Author:** @nkiyko **Date:** 2022-05-13

**Метрики SelfTimings [undefined](https://st.yandex-team.ru/undefined) - undefined**

### Usage

**Не изменился**

# 1.3.1

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 1.3.0

**PR:** [#2482886](https://a.yandex-team.ru/review/2482886)
**Author:** @polyakovda **Date:** 2022-04-20

Обновление Response, у которого обновились тайпинги.

### Usage

Дополнительных действий не требуется.

# 1.2.5

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

# 1.2.4

**PR:** [#894](https://github.yandex-team.ru/market/monomarket/pull/894)
**Author:** @kykint **Date:** 2022-02-25

- Более корректная типизация Stout

# 1.2.3

**PR:** [#877](https://github.yandex-team.ru/market/monomarket/pull/877)
**Author:** @kykint **Date:** 2022-02-17

- Более корректная типизация Stout

# 1.2.2

**PR:** [#403](https://github.yandex-team.ru/market/monomarket/pull/403)
**Author:** @akimy **Date:** 2021-10-05

Поправить декларацию типов в Router.d.ts (второй параметр конструктора класса опциональный)
MARKETFRONTECH-3217

# 1.2.1

**PR:** [#189](https://github.yandex-team.ru/market/monomarket/pull/189)
**Author:** @gheljenor **Date:** 2021-07-26

Изменён формат описания времени сборки

# 1.2.0

**PR:** [#154](https://github.yandex-team.ru/market/monomarket/pull/154)
**Author:** @dgudenkov **Date:** 2021-07-21

Дополнил ts типы

### Usage

-

# 1.1.25

Обновление зависимостей

### Updates

  * `eslint-plugin-stout`: [1.0.4](../../tools/eslint-plugin-stout/changelog.md#104) (was [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103))

# 1.1.24

Игнорим node_modules-prod для автотестов

# 1.1.23

- Обновление версий зависимостей
- Исправление ts-типизации

# 1.1.22

Переезд в монорепу
