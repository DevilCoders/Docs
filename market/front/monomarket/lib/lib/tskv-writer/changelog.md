# 3.0.8

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 3.0.7

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

# 3.0.6

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))

# 3.0.5

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

# 3.0.4

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

Обновление зависимостей

# 3.0.3

**PR:** [#320](https://github.yandex-team.ru/market/monomarket/pull/320)
**Author:** @ashwets **Date:** 2021-09-15

Обновление зависимостей

# 3.0.2

**PR:** [#209](https://github.yandex-team.ru/market/monomarket/pull/209)
**Author:** @pavelko95 **Date:** 2021-09-15

Обновление зависимостей

# 3.0.1

**PR:** [#206](https://github.yandex-team.ru/market/monomarket/pull/206)
**Author:** @antonk52 **Date:** 2021-09-06

Обновление зависимостей

# 3.0.0

**PR:** [#261](https://github.yandex-team.ru/market/monomarket/pull/261)
**Author:** @senz **Date:** 2021-08-30

Переезд в монорепу.

Обновление версий зависимостей.

Исправление контрактов, нарушенных при тайпскрипизация (а именно при отказе от lodash).
В версии пакета 1.1.1, функция `sanitizeAndEscape` внутри себя вызывала `_(value).trim()`,
а lodash, в свою очередь, приводил `value` к строке. 
Этот участок кода был заменён на `value.trim()`,
из-за чего начало выбрасываться исключение в случае, когда `value` не строка.
Добавлено приведение к строке в вызывающем методе `add`.

Также, в методе `add` была сломана проверка значения на `undefined`.
Условие `typeof value === undefined` никогда не будет выполнено, т.к. `typeof` всегда возвращает строку,
даже для `undefined`.
Проверка заменена на `value === undefined`.

### Usage

Без изменений.

### Migration

Теперь метод `add` принимает аргументы с типом `unknown` и внутри себя приводит их к строке.

Починена проверка на `undefined`, теперь метод `add` немедленно завершается,
если один из аргументов `undefined`.