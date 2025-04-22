# Сервис для запуска интеграционных тестов по расписанию

## Деплой:
* testing - запускаются паки с тестовыми аккаунтами https://yd.yandex-team.ru/stage/mail_borador_testing
* production - запускаются паки с боевыми аккаунтами https://yd.yandex-team.ru/stage/mail_borador_production

Релиз можно выкатить через [dctl](https://wiki.yandex-team.ru/deploy/docs/tools/dctl/) вот такой командой:
```
ya tool dctl release docker --title <some text> --description <optional: some more text> --release-type testing|production --tag <docker tag> <docker image without registry.yandex.net>
```
Например:
```
ya tool dctl release docker --title 'My awesome release' --description 'It fixes everything' --release-type testing --tag '201912261329.brdr_test_accs' mail/borador/borador
```

За прогрессом наблюдать или получить ssh на тачку (то есть, в box borador в терминах ydeploy) можно в UI по одной из ссылок выше.

## Как работает:
Внутри контейнера живёт сервис borador, который имеет http интерфейс для запуска тестов, мониторинга их состояния и перезапуска упавших.
Сервис пишет в логи, которые читает плюсовый юнистат и отдаёт в unistat-ручку.
Рядом крутится на 80 порту сервис status_hook, который следит чтоб юнистат и borador были запущены.
Запуск тестов инициируется кроном раз в час и при старте контейнера.

**Всё приложение (логи, кроны, бинари etc) находится в папке `/app`**

Запуски паков можно посмотреть по тегам:
* https://aqua.yandex-team.ru/#/launches-tag?tag=borador_production
* https://aqua.yandex-team.ru/#/launches-tag?tag=borador_testing

Ещё есть вот такая yasm-панель (алерты заведены руками):
https://yasm.yandex-team.ru/panel/massaraksh.borador_production

## Unistat
Сервис имеет следующие сигналы:
* `launch_200_ammm`, `launch_400_ammm`, `launch_500_ammm` - строятся по кодам ответа ручки /launch
* `$PACK_NAME_total` - общее число запущенных тестов в паке
* `$PACK_NAME_failed` - число упавших тестов
* `$PACK_NAME_passed` - число успешных тестов
* `$PACK_NAME_times` - сколько раз запускали пак. 0 - пак пока не запускалка, -1 - прошли все траи, но пак не прошёл полностью
* `$PACK_NAME_running_ammm` - запущен ли сейчас пак
* `unistat_errors_ammm` - метрика ошибок и исключительных ситуаций в юнистате
* `borador_init` - сколько раз сервис стартовал
