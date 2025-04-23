# Определения языка пользователя

Описание портальной реализации (https://doc.yandex-team.ru/lib/lang-detect/concepts/lang-detect-descr.html)

## Принцип работы

-   если передан хедер XLang, то берем язык из него
-   TODO: если пользователь авторизован, то берём язык из Паспорта
-   иначе смотрим на 39й сегменг из [куки my](https://wiki.yandex-team.ru/mycookie)
-   если кука отсутсвует, то пробуем найти язык в заголовке
    [Accept-Language](https://developer.mozilla.org/ru/docs/Web/HTTP/Headers/Accept-Language)
-   в крайнем случае — показываем язык по-умолчанию

Для парсинга [My Cookie](https://wiki.yandex-team.ru/mycookie) используем
[yandex-mycookie](https://a.yandex-team.ru/arcadia/frontend/packages/wmfront-core/packages/yandex-mycookie)

Смена языка пользователя происходит через [Tune API](https://wiki.yandex-team.ru/tune/api)

Для добавления нового языка надо знать числовой идентификатор из файла
[lang_detect_data.txt](https://a.yandex-team.ru/arc/trunk/arcadia/junk/snowball/lang-detect/data/lang_detect_data.txt?rev=r2013747#L4)

Это требуется, чтобы правильно интерпретировать число из 39го сегмента [куки my](https://wiki.yandex-team.ru/mycookie)

## Полезные ссылки

-   [Описание библиотеки lang-detect](https://doc.yandex-team.ru/lib/lang-detect/concepts/lang-detect-descr.html)
-   [Исходный код lang-detect](https://a.yandex-team.ru/arc/trunk/arcadia/junk/snowball/lang-detect)
-   [@yandex-int/express-langdetect](https://a.yandex-team.ru/arcadia/frontend/packages/express-langdetect)
