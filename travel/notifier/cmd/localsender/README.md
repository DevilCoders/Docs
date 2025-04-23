# Утилита быстрой отладочной отправки письма

Для запуска - нужно указать правильные параметры и пароли в подходящих переменных окружения среды,
установить ( https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon ) и запустить tvmtool:

```
./tvmtool --port 9005
```

и можно будет вот так отправить письмо для любого заказа на свой емейл:


```
./cmd/localsender/localsender --DEBUG_EMAIL=your-email@yandex-team.ru --DEBUG_ORDER_ID="b71597c9-7900-4231-992f-b83838ce0137"
```

можно указать и тип письма (adhoc, week-before, day-before):

```
./cmd/localsender/localsender --DEBUG_EMAIL=your-email@yandex-team.ru --DEBUG_ORDER_ID="b71597c9-7900-4231-992f-b83838ce0137" --DEBUG_SUBTYPE="adhoc"
```
