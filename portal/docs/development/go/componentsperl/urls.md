# Методы для работы с урлами в perl

* [url_update_query](https://a.yandex-team.ru/svn/trunk/arcadia/portal/main/lib/MordaX/Utils.pm?rev=r9610691#L1751), [url_param_glue](https://a.yandex-team.ru/svn/trunk/arcadia/portal/main/lib/MordaX/Utils.pm?rev=r9610691#L1638)

В Го нет смысла переносить логику этих методов в таком же виде, т.к. подобные задачи решаются с помощью стандартной библиотеки [net/url](https://pkg.go.dev/net/url)

В Го не нужно работать с урлами, как со строками, необходимо использовать свойства и методы стандартной библиотеки [net/url](https://pkg.go.dev/net/url). Также не нужно вручную обрабатывать query-параметры и очищать их от лишних символов, библиотека сделает это сама.

В avocado реализован [urlbuilder](https://a.yandex-team.ru/arcadia/portal/avocado/libs/utils/urlbuilder), со вспомогательными функциями для работы с урлами. Пакет можно и нужно дополнять.
