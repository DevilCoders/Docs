# Мониторинги

- [Production дашборд](https://yasm.yandex-team.ru/panel/inazarov-mi._qGMHW2/?range=21600000)
- [Sandbox дашборд](https://yasm.yandex-team.ru/panel/inazarov-mi._qR6HKt/?range=21600000)
- [Testing дашборд](https://yasm.yandex-team.ru/panel/inazarov-mi._7mWq2o/?range=21600000)

- [Error booster](https://error.yandex-team.ru/projects/pay) ошибки с веба фронта (prod и test вместе)

# Оповещение

Оповещения об ошибках с фронта (новых и участившихся) приходят в  телегу и [слак #pay-front-alerts](https://h.yandex-team.ru/?https%3A%2F%2Fyndx-all.slack.com%2Farchives%2FC028KNQL7HV)

 - [настройки алертов в error booster](https://error.yandex-team.ru/projects/pay/settings/alerts) (сами алерты улетают в juggler)
 - [настройки juggler](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3Dyandex-pay-front) которые отправляют сообщения в каналы

### Тестировать оповещения
1. жмём помочь[тут](https://всем-миром.рф/livefund-1/)
2. ждём загрузки формы оплаты. В консоли выбираем айфрейм
ya-pay**** вставляем это:
```
 Ya.Rum.logError({
        message: 'Testing error booster', 
        level: Ya.Rum.ERROR_LEVEL.ERROR, 
    })
```
