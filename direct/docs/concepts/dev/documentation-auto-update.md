# Автоматическое обновление документации
Сайт с документацией **автоматически** обновляется при изменениях в репозитории через newCI.
От коммита до обновления обычно проходит минуты 2.

## Документация из транка { #from-trunk }
New CI action [update-docs](https://a.yandex-team.ru/projects/direct/ci/actions/launches?dir=direct%2Fdocs&id=update-docs)
отслеживает коммиты в транке аркадии,
содержащие изменения в `direct/docs/`.
Для каждого из них запускается Sandbox-задача [DEPLOY_ARCADIA_DOCS](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/arcadia/DeployArcadiaDocs), которая последовательно:

- собирает документацию из репозитория
- заливает собранную документацию в S3 облака
- переключает [тестинг](https://testing.docs.yandex-team.ru/direct-dev/) на собранную версию
- переключает [продакшн](https://docs.yandex-team.ru/direct-dev/) на собранную версию


## Документация из ревью { #from-review }
Другой action [build-docs-in-pr](https://a.yandex-team.ru/projects/direct/ci/actions/launches?dir=direct%2Fdocs&id=build-docs-in-pr)
отслеживает все ревью (Pull-Request арканума) затрагивающие документацию — позволяет без ручной сборки в точности понять — какой получится документация.  
Та же sandbox-таска, что и для транка:

- соберёт документацию с патчем из ревью
- зальёт её в S3
- оставит в ревью комментарий со ссылкой на собранную документацию ([пример](https://a.yandex-team.ru/review/2052627/details)) *(там по два коммментария, так как старый способ через TestEnv еще не отключился)*

## Полезные ссылки
- [конфигурация](https://a.yandex-team.ru/arc/trunk/arcadia/direct/docs/a.yaml) конфигурация new CI
- [документация платформы](https://docs.yandex-team.ru/docstools/#deploy) про автоматический деплой (старая версия), [черновик про new CI](https://1680269-8347182.testing.docs.yandex-team.ru/docstools/#deploy)
