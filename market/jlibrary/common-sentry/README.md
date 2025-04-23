# common-sentry

Библиотека для работы с Sentry

## Использование библиотеки
* [Создание проекта](https://wiki.yandex-team.ru/sentry/cloud/how-to-start/)
* После создания проекта указать в своих properties файлах:
    * `sentry.token` - токен, который является частью DSN до `@` (его нужно указывать в секретах, а не в коде)
    * `sentry.dsn` - часть DSN после `@`
    * `sentry.enable=true`
* Добавить в конфигурацию `log4j2.xml` `<Sentry name="SENTRY"/>` и в нужные Logger'ы 
`<AppenderRef ref="SENTRY" level="<LEVEL>"/>`, где `<LEVEL>` - нужный уровень логгирования

У Sentry имеются [ограничения](https://wiki.yandex-team.ru/sentry/cloud/restrictions/) на количество событий в минуту

## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)

## Релизы в ЦУМе
[pipeline](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/common-sentry), 
[dashboard](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/common-sentry)