# 1.1.7

**PR:** [#2503816](https://a.yandex-team.ru/review/2503816)
**Author:** @gheljenor **Date:** 2022-04-27

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.5.4](../../lib/yammy-lib/changelog.md#154) (was [1.5.3](../../lib/yammy-lib/changelog.md#153))
  * `@yandex-market/node-root`: [1.0.1](../../tools/node-root/changelog.md#101) (was [1.0.0](../../tools/node-root/changelog.md#100))

# 1.1.6

**PR:** [#1018](https://github.yandex-team.ru/market/monomarket/pull/1018)
**Author:** @gheljenor **Date:** 2022-04-11

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.5.3](../../lib/yammy-lib/changelog.md#153) (was [1.5.2](../../lib/yammy-lib/changelog.md#152))

# 1.1.5

**PR:** [#1008](https://github.yandex-team.ru/market/monomarket/pull/1008)
**Author:** @gheljenor **Date:** 2022-04-06

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.5.2](../../lib/yammy-lib/changelog.md#152) (was [1.5.1](../../lib/yammy-lib/changelog.md#151))

# 1.1.4

**PR:** [#992](https://github.yandex-team.ru/market/monomarket/pull/992)
**Author:** @gheljenor **Date:** 2022-04-04

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.5.1](../../lib/yammy-lib/changelog.md#151) (was [1.5.0](../../lib/yammy-lib/changelog.md#150))

# 1.1.3

**PR:** [#979](https://github.yandex-team.ru/market/monomarket/pull/979)
**Author:** @gheljenor **Date:** 2022-03-29

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.5.0](../../lib/yammy-lib/changelog.md#150) (was [1.4.1](../../lib/yammy-lib/changelog.md#141))

# 1.1.2

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.4.1](../../lib/yammy-lib/changelog.md#141) (was [1.4.0](../../lib/yammy-lib/changelog.md#140))

# 1.1.1

**PR:** [#883](https://github.yandex-team.ru/market/monomarket/pull/883)
**Author:** @gheljenor **Date:** 2022-02-28

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.4.0](../../lib/yammy-lib/changelog.md#140) (was [1.3.0](../../lib/yammy-lib/changelog.md#130))

# 1.1.0

**PR:** [#594](https://github.yandex-team.ru/market/monomarket/pull/594)
**Author:** @nybble **Date:** 2021-11-26

Добавлены s3-скрипты для просмотра списка бакетов и удаления устаревших файлов 

**[MARKETFRONTECH-3388](https://st.yandex-team.ru/MARKETFRONTECH-3388) - add s3 cleaning script**

### Usage

Список всех бакетов: `yammy bin s3-buckets`

Удаление устаревших файлов: `yammy bin s3-find-old <bucket> [days=360] [prefix] > old-files.out && yammy bin s3-delete <bucket> < old-files.out`, где `<bucket>` - это бакет, `[days=360]` - кол-во дней, ранее которых удалять, `[prefix]` - префикс.

# 1.0.9

**PR:** [#556](https://github.yandex-team.ru/market/monomarket/pull/556)
**Author:** @juleari **Date:** 2021-11-19

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.3.0](../../lib/yammy-lib/changelog.md#130) (was [1.2.1](../../lib/yammy-lib/changelog.md#121))

# 1.0.8

**PR:** [#542](https://github.yandex-team.ru/market/monomarket/pull/542)
**Author:** @juleari **Date:** 2021-11-15

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.2.1](../../lib/yammy-lib/changelog.md#121) (was [1.2.0](../../lib/yammy-lib/changelog.md#120))

# 1.0.7

**PR:** [#522](https://github.yandex-team.ru/market/monomarket/pull/522)
**Author:** @juleari **Date:** 2021-11-09

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.2.0](../../lib/yammy-lib/changelog.md#120) (was [1.1.9](../../lib/yammy-lib/changelog.md#119))

# 1.0.6

**PR:** [#527](https://github.yandex-team.ru/market/monomarket/pull/527)
**Author:** @juleari **Date:** 2021-11-09

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.1.9](../../lib/yammy-lib/changelog.md#119) (was [1.1.8](../../lib/yammy-lib/changelog.md#118))

# 1.0.5

**PR:** [#442](https://github.yandex-team.ru/market/monomarket/pull/442)
**Author:** @juleari **Date:** 2021-11-02

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.1.8](../../lib/yammy-lib/changelog.md#118) (was [1.1.7](../../lib/yammy-lib/changelog.md#117))

# 1.0.4

**PR:** [#423](https://github.yandex-team.ru/market/monomarket/pull/423)
**Author:** @juleari **Date:** 2021-10-21

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.1.7](../../lib/yammy-lib/changelog.md#117) (was [1.1.6](../../lib/yammy-lib/changelog.md#116))

# 1.0.3

**PR:** [#189](https://github.yandex-team.ru/market/monomarket/pull/189)
**Author:** @gheljenor **Date:** 2021-07-26

Изменён формат описания времени сборки

# 1.0.2

Обновление зависимостей

### Updates

  * `@yandex-market/yammy-lib`: [1.1.6](../../lib/yammy-lib/changelog.md#116) (was [1.1.5](../../lib/yammy-lib/changelog.md#115))

# 1.0.1

Первый релиз

### Updates

  * `@yandex-market/yammy-lib`: [1.1.5](../../lib/yammy-lib/changelog.md#115) (was [1.1.4](../../lib/yammy-lib/changelog.md#114))