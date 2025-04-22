# Статические файлы десктопной версии Маркета

## Файлы

`closer.html` - компонент, который участвует в процессе логина через Паспорт (исходный код взят из `islands/common.blocks/social-broker/__closer/social-broker__closer.html`)

`google<SOME_NUMBERS>.html` - файлы, с помощью которых гугл определяет [принадлежность домена](https://support.google.com/a/answer/63026?hl=ru)

## CSP-правила

Статические HTML-файлы покрываются [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) на уровне nginx в конфиге
https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/nanny/front/desktop/tmpl/conf/nginx/sites-enabled/62-market.conf

В статических html-файлах инлайн скриптов и стилей запрещен на уровне CSP, поэтому их надо выносить в отдельные файлы.
Если возникают ошибки CSP, то соответствующие правила, разрешающие доступ к новым ресурсам, надо добавить в конфиг nginx.
