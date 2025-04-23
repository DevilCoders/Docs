## Релиз Geohelper

### Шаг 1. Выкатка релиза на RC

1. Запустить релизный [флоу](https://a.yandex-team.ru/projects/geohelper/ci/releases/timeline?dir=portal%2Fgeohelper&id=release).

1. 
    1. Дождаться сборки и автоматического релиза
    1.  протестировать, проверить работоспособность [в тестинге](l7test.yandex.ru/geohelper)

### Шаг 2. Раскатка релиза

1. Подписаться на уведомления от мониторинга [в telegram - чате](https://t.me/joinchat/BlyRegsiusIHkvRRW8y7Ug)
1. Прожать кубик `Начать раскатку в продакшн`
1. Дождаться подготовки vla, sas, hamster.
1. Выкатить релиз во vla, прожав кубик `Выкатка во vla`.
1. Следить за ошибками на [панели мониторинга](https://yasm.yandex-team.ru/menu/Portal/Geohelper/geohelper/) не менее 10 минут.
1. Выкатить релиз в sas, прожав кубик `Выкатка во sas`.
1. Продолжать следить за ошибками на [панели мониторинга](https://yasm.yandex-team.ru/menu/Portal/Geohelper/geohelper/)
