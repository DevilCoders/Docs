# Alerts

Алерты в Juggler https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-mobile-infra_production.app&project=geo.maps-front

**Каналы Карт** <br />
Telegram `MobileMonitorings` https://t.me/joinchat/BEZLVxy7N1NuHHhZtkVTbw <br />
Slack `#mobile-maps-alerts` https://app.slack.com/client/T02NRKTK0/C020D6ARV09 <br />

**Каналы Навигатора** <br />
Telegram `mobile-navi-monitorings` <br />
Slack `#navi-alerts` https://app.slack.com/client/T02NRKTK0/C024EE45B41

Подробная документация по Головану https://wiki.yandex-team.ru/golovan/ <br />
Подробная документация по Juggler https://docs.yandex-team.ru/juggler/ <br />

---

## Работа с шаблонами алертов (alerts)

Макрос для добавления алертов.<br />
[common-mobile-maps-alerts.jinja2](./common-mobile-maps-alerts.jinja2) <br />

Описание сигналов, на которые будут смотреть алерты. <br />
Меняем их, когда нужно добавить новый алерт или изменить пороги срабатывания существующего. <br />
[mobile-maps.jinja2](./mobile-maps.jinja2) <br />
[mobile-navigator.jinja2](./mobile-navigator.jinja2) <br />

---

Для изменения алертов нужно:
* Поменять конфиги.
* Обновить шаблоны алертов из конфига. <br />
`curl --data-binary @<path_to_config.jinja2> 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=<template_key>'`
* Применить измененные конфиги.
После применения конфигов изменения прорастут в Juggler <br />
`curl -XPOST 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/<template_key>'`

---

## Готовые запросы

### Общий шаблон
* **update** - `curl --data-binary @./common-mobile-maps-alerts.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=common-mobile-maps-alerts'`
  
### Maps
* **update** - `curl --data-binary @./mobile-maps.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=mobile-maps'`
* **apply** - `curl -XPOST 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/mobile-maps'`

### Navi
* **update** - `curl --data-binary @./mobile-navigator.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=mobile-navigator'`
* **apply** - `curl -XPOST 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/mobile-navigator'`

### Обновить и за-аплаить все
`curl --data-binary @./common-mobile-maps-alerts.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=common-mobile-maps-alerts' && curl --data-binary @./mobile-maps.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=mobile-maps' && curl -XPOST 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/mobile-maps' && curl --data-binary @./mobile-navigator.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=mobile-navigator' && curl -XPOST 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/mobile-navigator'`

---

## NO-DATA

В маросе для добавления алертов создается дополнительный сигнал,
который будет стрелять, если хотя-бы в одном из сигналов будет NO-DATA.

На NO-DATA сигнал навешен отедльный флаподав с большими задержками.
Алерт на NO-DATA будет писать в Telegram и Slack. Не будет звонить и создавать тикеты в startrek.

Выглядят сигналы на NO-DATA  примерно так:
`
min(
    or(na(sum(abs(unistat-maps_ios_json_parsing_error_10m_axxx), const(1))), const(0)),
    or(na(sum(abs(unistat-maps_ios_http_error_no_taxi_10m_axxx), const(1))), const(0)),
    or(na(sum(abs(unistat-maps_ios_crash_devices_percentage_10m_axxx), const(1))), const(0)),
    or(na(sum(abs(unistat-maps_ios_crash_sessions_percentage_10m_axxx), const(1))), const(0)),
    or(na(sum(abs(unistat-maps_ios_http_error_only_taxi_10m_axxx), const(1))), const(0)),
    const(1)
);
`

Каждый из сигналов оборачивается в `or`, `na`, `sum` и `abs`.
Если значение в сигнале будет, то `abs` сделает его положительным, а `sum` увеличит его на 1.
`na` нужен, что бы `sum` и `abs` вернули NO-DATA, если в исодном сигнале не было значения.
Еси значения в сигнале нет, то `or` вернет `0`.
Потом все сигналы мы оборачиваем в `min`
И если был хотя-бы один сингал с NO-DATA, то в `min` вернет `0`, если значение было, то вернутся `1`

---

## При переезде

Создать новый шаблон: <br />
`curl -d '{"key": "<template_key>", "owners": ["likhogrud", "sanllier" ]}' 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/create'`

Удалить старый: <br />
`curl -d '{"key": "<template_key>"}' 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/delete'`
