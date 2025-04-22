# 4.2.1

**PR:** [#2712490](https://a.yandex-team.ru/review/2712490)
**Author:** @robot-metatron **Date:** 2022-07-11

**Добавил булевый тип для полей query**

# 4.2.0

**PR:** [#2587715](https://a.yandex-team.ru/review/2587715)
**Author:** @bykhovtsev **Date:** 2022-06-01

Добавляем параметр forceQueryString в настройки транспорта,
который отключает формирование query-строки из объекта и отдает его на откуп клиентскому коду

### Usage

```ts
const params = {
    forceQueryString: '?foo=1',
}
```

# 4.1.0

**PR:** [#2494438](https://a.yandex-team.ru/review/2494438)
**Author:** @creazero **Date:** 2022-04-29

[undefined](https://st.yandex-team.ru/undefined) - undefined: во все зависящие от ответа ошибки было добавлено поле headers

### Usage

Чтобы была возможность доставать дебаг-инфу из хедеров при любых ошибках.

# 4.0.5

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

# 4.0.4

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

# 4.0.3

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))

# 4.0.2

**PR:** [#570](https://github.yandex-team.ru/market/monomarket/pull/570)
**Author:** @owngr **Date:** 2022-01-21

Сделал понятный вывод ошибки BCM.HttpTransportPrepareError.EINVALID [MARKETFRONTTECH-3404]

# 4.0.1

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

# 4.0.0

**PR:** [#703](https://github.yandex-team.ru/market/monomarket/pull/703)
**Author:** @asker-k **Date:** 2022-01-12

Добавлена возможность передачи retry и retryDelay в bcm2 в конфиге ручки
Добавлена возможность установки 0 в качестве retryDelay

### Usage

Теперь можно передавать retryDelay и retry в параметрах метода send, и они будут иметь более высокий приоритет

### Migration

Если раньше передавали 0, то устанавливалось дефолтное значение, а теперь будет ставится 0. Надо предусмотреть это при переходе на новую версию

# 3.4.0

**PR:** [#591](https://github.yandex-team.ru/market/monomarket/pull/591)
**Author:** @asker-k **Date:** 2021-11-26

[MARKETFRONT-3409](https://st.yandex-team.ru/MARKETFRONT-3409) - Прокидывание error вторым аргументом в retryDelay. TransportResponseError обогащен полем headers - заголовками ответа
Прокидываем error вторым аргументом в retryDelay
TransportResponseError обогащен полем headers - заголовками ответа

### Usage

Можем использовать информацию об ошибке в retryDelay, чтобы выставить задержку.

# 3.3.5

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

Обновление зависимостей

# 3.3.4

**PR:** [#320](https://github.yandex-team.ru/market/monomarket/pull/320)
**Author:** @ashwets **Date:** 2021-09-15

Обновление зависимостей

# 3.3.3

**PR:** [#209](https://github.yandex-team.ru/market/monomarket/pull/209)
**Author:** @pavelko95 **Date:** 2021-09-15

Обновление зависимостей

# 3.3.2

**PR:** [#307](https://github.yandex-team.ru/market/monomarket/pull/307)
**Author:** @gheljenor **Date:** 2021-09-08

[MARKETFRONTECH-3123](https://st.yandex-team.ru/MARKETFRONTECH-3123) - Поправить типы в BCM

# 3.3.1

**PR:** [#206](https://github.yandex-team.ru/market/monomarket/pull/206)
**Author:** @antonk52 **Date:** 2021-09-06

Обновление зависимостей

# 3.3.0

**PR:** [#204](https://github.yandex-team.ru/market/monomarket/pull/204)
**Author:** @maslov-rn **Date:** 2021-09-01

Добавлено измерение времени на парсинг сырых данных

### Usage

Без изменений

# 3.2.4

**PR:** [#207](https://github.yandex-team.ru/market/monomarket/pull/207)
**Author:** @juleari **Date:** 2021-08-09

Обновление зависимостей

# 3.2.3

**PR:** [#222](https://github.yandex-team.ru/market/monomarket/pull/222)
**Author:** @juleari **Date:** 2021-08-09

[MARKETFRONTECH-2993](https://st.yandex-team.ru/MARKETFRONTECH-2993) - [Монорепа] Починить ссылки в ченжлогах

# 3.2.2

**PR:** [#215](https://github.yandex-team.ru/market/monomarket/pull/215)
**Author:** @gheljenor **Date:** 2021-08-04

[MARKETFRONTECH-2974](https://st.yandex-team.ru/MARKETFRONTECH-2974) - [Монорепа] Убираем скрипты из генерируемых пакетов

# 3.2.1

**PR:** [#201](https://github.yandex-team.ru/market/monomarket/pull/201)
**Author:** @gheljenor **Date:** 2021-08-02

Изменение версий зависимостей

# 3.2.0

**PR:** [#198](https://github.yandex-team.ru/market/monomarket/pull/198)
**Author:** @maslov-rn **Date:** 2021-07-28

Добавил доступные из got метрики http запроса

### Usage

Без изменений

# 3.1.1

**PR:** [#189](https://github.yandex-team.ru/market/monomarket/pull/189)
**Author:** @gheljenor **Date:** 2021-07-26

Изменён формат описания времени сборки

# 3.1.0

**PR:** [#184](https://github.yandex-team.ru/market/monomarket/pull/184)
**Author:** @gheljenor **Date:** 2021-07-21

Добавлена возможность использовать прокачаный keep-alive агент

### Usage

- bcm теперь умеет примнимать в агентов из библиотеки `agentkeepalive`.
 - при передаче описании опций агента можно передать опцию `keepAliveEnhanced: true`, в этом случае будет создан агент из `agentkeepalive`

# 3.0.9

**PR:** [#165](https://github.yandex-team.ru/market/monomarket/pull/165)
**Author:** @antsa4 **Date:** 2021-07-16

Обновление версий зависимостей

# 3.0.8

Проставлено время сборки

### Updates

  * `@yandex-market/yammy`: [2.0.0](../../scripts/yammy/changelog.md#200) (was [1.15.0](../../scripts/yammy/changelog.md#1150))

# 3.0.7

Обновление зависимостей

### Updates

  * `eslint-plugin-stout`: [1.0.4](../../tools/eslint-plugin-stout/changelog.md#104) (was [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103))

# 3.0.6

Небольшая правка unit-тестов.
Из-за неточности работы setTimeout увеличил диапазон проверки в одном тесте и удалил второй тест

# 3.0.5

Игнорим node_modules-prod для автотестов

# 3.0.4

Правки eslint'а

### Updates

  * `eslint-plugin-stout`: [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103) (was [1.0.2](../../tools/eslint-plugin-stout/changelog.md#102))

# 3.0.3

Правильно конфигурим независимость артефактов

# 3.0.2

Для запросов с protobuf можно указать `allowProtoUnknownValues`, чтобы запрос не падал на неизвестных значениях (например, значение энама, отсутсвующее в схеме) и `onProtoVerifyError` для обработки ошибки

# 3.0.1

Обновление версий зависимостей

# 3.0.0

Переезд bcm2 в монорепу

### Usage

Ничего нового не добавлено, старое тоже не изменено

### Migration

По идее никаких изменений не требуется