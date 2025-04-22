[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/ambar)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/ambar) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=ambar)](https://oko.yandex-team.ru/pkg/ambar)

# Market Ambar 🌈

### Библиотека прикладных утилит фронтенда маркета

- [Документация](https://github.yandex-team.ru/pages/market/ambar/)
- [После lodash/fp](#После-fp)
- [Чат в telegram](https://t.me/joinchat/C-1ThlEJotBzLLrHv6EEkA)
- [Changelog](https://github.yandex-team.ru/market/ambar/blob/master/CHANGELOG.md)
- [Описание](#Описание)
- [Особенности ambar](#Особенности-ambar)
- [Установка и сборка](#Установка-и-сборка)
- [Как поучаствовать](#Как-поучаствовать)
- [FAQ](#FAQ)
- [Что дальше?](#Что-дальше)
- [Полезные ссылки](#Полезные-ссылки)

## Описание
ambar — библиотека прикладных утилит фронтенда маркета. ambar стремится упростить написание продуктового кода,
предоставляя типизированный набор функций общего назначения в функциональном стиле.
Внешний интерфейс функций во многом повторяет ramda, однако реализация может меняться.

ambar призван заменить lodash(/fp) в бело-синем маркете и ramda в ПИ.

## Особенности ambar
* Типобезопасность (никаких `any`, `Object`, `Function`\*, в отличии от lodash и частично Ramda)
* Типизация path-based функций
* Документация (в отличии от lodash/fp)
* Значимо не увеличивает (не считая маппинга) размер клиентских бандлов, поскольку может использовать lodash для реализации.
При наличии зависимостей занимает ~1kb gzip
* Data-last и автокаррирование (в отличии от lodash)
* Включает в себя часть ранее проектных, но потенциально полезных хелперов (ex `helpers/fp`)
* Не является еще одной библиотекой для функционального программирования на js,
в нем нет (и не планируется) линз, монад и имплементаций fantasy land.

\* Кроме `template`, где это допустимо

## Как поучаствовать
Во-первых, можно взять на себя часть [тикетов](https://st.yandex-team.ru/MARKETVERSTKA-31150) по покрытию тестами.

Во-вторых, всегда можно записать любую свою идею,
предложение или критику в [issues](https://github.yandex-team.ru/market/ambar/issues) или сразу сделать PR.

## Требования к экспортируемым функциям

Любая экспортируемая из ambar функция должна удовлетворять следующим требованиям:
* Функция содержит нативную, либо lodash реализацию
* Имеет jsdoc с текстовым описанием, описанием набора входных параметров, возвращаемого значения и примером
* Покрыта unit-тестами
* Покрыта flow-тестами
* Реализация функции соответствует ее типу
* По умолчанию каррирована и имеет data-last порядок аргументов
* Не является null-safe функцией (за несколькими особыми исключениями вроде pathOr)

В качестве примера можно посмотреть на функции [all](https://github.yandex-team.ru/market/ambar/blob/master/src/lodash/all.js),
[castArray](https://github.yandex-team.ru/market/ambar/blob/master/src/__tests__/castArray.spec.js)
и [curry](https://github.yandex-team.ru/market/ambar/blob/master/src/lodash/curry.js)

## Установка и сборка
Полная сборка и установка зависимостей
```console
$ yammy build ambar-src deep
```

Пересборка документации
```console
$  yammy run ambar-src docs
```

Запуск тестов
```console
$ yammy test ambar-src
```

## FAQ
> Зачем вообще нужен этот ambar? Все и так хорошо

Сохранение status quo приводит к тому, что мы пишем нетипизированный или, что еще хуже,
ошибочно типизированный код. Отсутствие документации у lodash/fp также регулярно приводит к проблемам.

> Почему бы тогда сразу не взять ramda?

Это и было одним из предварительных решений. У него есть только один, но большой недостаток: мы не можем себе позволить
увеличение клиентского бандла.

> Я смотрю на список функций и не вижу `$favorite_function_name`! Почему так?

* Функция адекватно не типизируется средствами flow
* Она не используется (или почти не используется) в проектах (на примере белого)
* Ее не было изначально / ее стоило оставить

Инструкция, что делать в этом случае лежит [тут](https://github.yandex-team.ru/market/ambar/blob/master/guides/absent-function.svg)

## После-fp
> Привык писать get и getOr. А что теперь?

Вместо них теперь есть две пары функций: [prop](https://github.yandex-team.ru/pages/market/ambar/#prop), [propOr](https://github.yandex-team.ru/pages/market/ambar/#propOr),
[path](https://github.yandex-team.ru/pages/market/ambar/#path) и [pathOrUnsafe](https://github.yandex-team.ru/pages/market/ambar/#pathOrUnsafe).

В отличии от `lodash`, все эти функции (кроме pathOrUnsafe) **не являются** [null-safe](https://en.wikipedia.org/wiki/Void_safety)
(для интересующихся, есть [issue](https://github.yandex-team.ru/market/ambar/issues/12)) и в основном нужны для частичного применения и композиций.

В случае, если null-safety необходим, можно спокойно применять `pathOrUnsafe`.


## Что дальше?
Что может ожидать ambar в будущем:
* Переезд на внешний гитхаб, отказ от маркетных зависимостей
* Тайпинги/переход на Typescript
* Отказ от lodash/fp в пользу lodash + конвертацию функций (для работающего tree-shaking)
* Отказ от lodash(*/fp) реализаций в пользу более легковесных нативных решений с сохранением интерфейса

## Полезные ссылки
* Хелперы для типизации [Flown](https://github.com/lttb/flown)
* Неописанные типы [flow](https://medium.com/netscape/secret-flow-types-86b2ebb30951)
* Ещё больше неописанных типов [flow](https://www.saltycrane.com/flow-type-cheat-sheet/latest/)
