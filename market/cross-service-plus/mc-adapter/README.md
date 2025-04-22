# mc-adapter: Адаптер между событиями чекаутера и компонентом Mission control

## Генерация проекта

1. `cd ~/arcadia/market/cross-service-plus/mc-adapter`
2. `./generate_project.sh`

## Локальный запуск
Приложение при старте начинает читать события чекаутера. Для этого нужно либо установить секрет (пункт 1) либо выключить чтение топика (пункт 2):
1. Устанавливаем секрет (если чтение событий не нужно, то пропускаем этот пункт)
    1. Получить секрет `ya vault get version sec-01g65vtj6s8ntyhn9fdns49g90 -o client_secret`
    2. Установить полученный секрет в переменную `MC_ADAPTER_SECRET_KEY`.
   Это можно сделать следующим способом: добавить в файл `~/.bash_profile` или `~/.zprofile` следующую строчку
```bash
export MC_ADAPTER_SECRET_KEY=ПОЛУЧЕННЫЙ_СЕКРЕТ
```

2. Отключаем чтение топика (если нужно читать события, то пропускам этот пункт). Для отключения чтения топика установите в `false` пропертю: `market.mc.adapter.logbroker.checkouter.readEnabled`
3. Открыть проект в IntelliJ IDEA
4. Запустить конфигурацию: `Run Service (generated)`


## Logbroker
Приложение работает с logbroker. Мы читаем события из очереди событий по заказам чекаутера и пишем события в наш
собственный топик.

Консюмеры и собственный топик находятся в инсталяции LGKX по адресам:
1) топик записи: plus/(testing|production)/user-actions
2) топик чтения: mc-adapter/(testing|production)/order-events
