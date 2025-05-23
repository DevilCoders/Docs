## TL;DR

Мы мониторим размер бандлов на каждый релиз (постранично). Для измерения используется [bundlemeter](https://a.yandex-team.ru/arcadia/travel/frontend/bundlemeter). Сценарии для измерения живут [здесь](https://a.yandex-team.ru/arcadia/travel/frontend/portal/bundlemeter.js).

## Как это работает:

После деплоя релиза в тестинг, кулауд дергает хук в devtools, который запускает bundlemeter. Результаты измерения складываются в clickhouse. Релизная машина создает релизный тикет и помещает в тикет график, на котором отображается статистика по размеру бандлов из данных clickhouse. [Посмотреть на график](https://charts.yandex-team.ru/preview/editor/8gzcub99tivi5).

## Типы ресурсов на графике

**script** — все скрипты, которые загрузились на страницы (как внешние (реклама, метрика и т.д.), так и наша сборка)

**image** — картинки

**stylesheet** — стили

**font** — шрифты

**travelScript** — только скрипты из нашей сборки

**total** — script + image + stylesheet + font

**totalWithoutExternalScripts** — travelScript + image + stylesheet + font

## Необходимые доработки

1. Добавить все страницы портала.
2. /hotels/book сейчас замеряется некорректно, т.к. в ссылке указан устаревший токен, поэтому редиректит на главную.
3. /hotels/book/success отображается не страница успешного заказа, а форма для ввода телефона или почты, чтобы получить доступ к заказу. Тоже не совсем корректно.
4. Некоторые сборки видимо были не совсем удачные, из-за чего на графике отображаются резкие спады в 0 по размеру наших скриптов. Можно такие релизы отфильтровать, чтобы было проще читать график.

##FAQ

#### Что нужно сделать, чтобы моя страница попала в этот график?

Сделать пр [сюда](https://a.yandex-team.ru/arcadia/travel/frontend/portal/bundlemeter.js)

#### Почему на графике общий размер страницы (total) скачет от релиза к релизу?

Вероятно, это связано с динамическим размером внешних скриптов. Можно сравнить два типа ресурсов: script и travelScript.
