# Скрипт для генерации отчета о продажах сервиса Яндекс.Автобусы

## Генерация отчета за месяц
```
YENV_TYPE=production ./order_report month -y 2019 -m 5 -e your_login@yandex-team.ru
```

## Генерация подробного отчёта за месяц
```
YENV_TYPE=production ./order_report detailed -y 2019 -m 5 -e your_login@yandex-team.ru
```

## Генерация отчета за год
```
YENV_TYPE=production ./order_report year -y 2018 -e your_login@yandex-team.ru
```
