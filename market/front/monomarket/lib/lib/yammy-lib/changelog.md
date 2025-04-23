# 1.5.4

**PR:** [#2503816](https://a.yandex-team.ru/review/2503816)
**Author:** @gheljenor **Date:** 2022-04-27

Использование `@yandex-market/node-root` для определения корня репозитория

### Updates

  * `@yandex-market/node-root`: [1.0.1](../../tools/node-root/changelog.md#101) (was [1.0.0](../../tools/node-root/changelog.md#100))

# 1.5.3

**PR:** [#1018](https://github.yandex-team.ru/market/monomarket/pull/1018)
**Author:** @gheljenor **Date:** 2022-04-11

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

# 1.5.2

**PR:** [#1008](https://github.yandex-team.ru/market/monomarket/pull/1008)
**Author:** @gheljenor **Date:** 2022-04-06

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

# 1.5.1

**PR:** [#992](https://github.yandex-team.ru/market/monomarket/pull/992)
**Author:** @gheljenor **Date:** 2022-04-04

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

# 1.5.0

**PR:** [#979](https://github.yandex-team.ru/market/monomarket/pull/979)
**Author:** @gheljenor **Date:** 2022-03-29

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

- фиксы для arc clean
- хелпер `arc-clean`

### Usage

```shell
npm i -g @yandex-market/yammy-lib
arc-clean --help
```

# 1.4.1

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

[MARKETFRONTECH-3829](https://st.yandex-team.ru/MARKETFRONTECH-3829) - [git-arc] Yammy - адаптер для арка

# 1.4.0

**PR:** [#883](https://github.yandex-team.ru/market/monomarket/pull/883)
**Author:** @gheljenor **Date:** 2022-02-28

Добавлена функция `lib/clone-deep`

### Usage

```javascript
const cloneDeep = require(`@yandex-market/yammy-lib/lib/clone-deep`);
const clone = cloneDeep(obj);
```

# 1.3.0

**PR:** [#556](https://github.yandex-team.ru/market/monomarket/pull/556)
**Author:** @juleari **Date:** 2021-11-19

Добавлена функция teminal-link на замену библиотечной

### Usage

`terminalLink(text, url)`

# 1.2.1

**PR:** [#542](https://github.yandex-team.ru/market/monomarket/pull/542)
**Author:** @juleari **Date:** 2021-11-15

Добавлен цвет для аргументов в print

# 1.2.0

**PR:** [#522](https://github.yandex-team.ru/market/monomarket/pull/522)
**Author:** @juleari **Date:** 2021-11-09

Добавлен аналог chalk -- print, который выбирает жирность и цвет в зависимости от типа данных

### Usage

```
print.tip('Some tip text')
print.command('yammy build me')
```

Новые типы добавляются в lib/print.js

# 1.1.9

**PR:** [#527](https://github.yandex-team.ru/market/monomarket/pull/527)
**Author:** @juleari **Date:** 2021-11-09

[MARKETFRONTECH-3340](https://st.yandex-team.ru/MARKETFRONTECH-3340) - [Монорепа] Yammy портит git stash в прекоммит-хуке

# 1.1.8

**PR:** [#442](https://github.yandex-team.ru/market/monomarket/pull/442)
**Author:** @juleari **Date:** 2021-11-02

[MARKETFRONTECH-2609](https://st.yandex-team.ru/MARKETFRONTECH-2609) - [Монорепа] Более наглядно сообщаем о новых версиях пакетов

# 1.1.7

**PR:** [#423](https://github.yandex-team.ru/market/monomarket/pull/423)
**Author:** @juleari **Date:** 2021-10-21

[MARKETFRONTECH-3236](https://st.yandex-team.ru/MARKETFRONTECH-3236) - Починить парсинг тикета

# 1.1.6

Убрал лишний мьют промисов

# 1.1.5

Глушим непойманый промис в Concurency

# 1.1.4

Исправляет ошибку, при которой pre-commit хук падает при исполнении `git stash push -ku`

# 1.1.3

[MARKETFRONTECH-2523: [Монорепа] Трерья миля - починить stash](https://st.yandex-team.ru/MARKETFRONTECH-2523)

Более правильно кладём файлики в стеш

# 1.1.2

Правки eslint'а

### Updates

  * `eslint-plugin-stout`: [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103) (was [1.0.2](../../tools/eslint-plugin-stout/changelog.md#102))

# 1.1.1

Правильно конфигурим независимость артефактов

# 1.1.0

* Добавлен AsyncArray#join
* Добавлен AsyncArray#sort

### Usage

```javascript
const description = await new AsyncArray(getDescriptionChunks())
    .sort((a, b) => (a.order > b.order ? 1 : (a.order === b.order ? 0 : -1)))
    .map(({text}) => text)
    .join('<br/>');
```

# 1.0.3

Помечаем что @yandex-market/eslint не влияет не сборку

# 1.0.2

Создан changelog.md