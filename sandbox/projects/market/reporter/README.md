# reporter

Sandbox задача для сбора и рассылки метрик стабильности доставки
Подробнее в описании на [wiki](https://wiki.yandex-team.ru/delivery/reliability/reporter/)

## Сбока

Выставляем Debug флаг в __init.py__
```py
debug = True
```

```bash
# перехдим в папку bin
cd sandbox/projects/market/reporter/CreateReportFromMarketAlarms/bin

# собираем бинарь
ya make

# запускаем бинарь в sandbox (только под линкусом, под макОС не заработает)
./CreateReportFromMarketAlarms run --type CREATE_REPORT_FROM_MARKET_ALARMS --enable-taskbox
```

## Ссылки
[Список метрик](https://wiki.yandex-team.ru/delivery/reliability/)
