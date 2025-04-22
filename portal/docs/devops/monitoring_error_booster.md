# Мониторинги в Error Booster'е

В проекте Авокадо мы отказались от записи ошибок в Кибану, выбрав в качестве альтернативы собственный аргегатор ошибок Error Booster. Среди прочих преимуществ можно выделить пару:

- индексирование специфичных для сервисов Яндекса полей: код геопозиции, идентификаторы запросов для отладки через SETrace, номера выборок в экспериментах и так далее
- возможность создать из коробки алерты на те или иные ошибки, отфильтрованные с помощью языка запросов

## Как завести {#how-to-create}

На примере проекта [Авокадо](https://error.yandex-team.ru/projects/avocado/projectDashboard)

1. Отфильтруйте в панели те сообщения об ошибках, на количество вы хотите завести алерт, введя запрос.
``
(page like topnews OR message like topnews) AND environment == production
``
	
![img.png](imgs/monitoring_error_booster_filter.png)
2. Заведите [новый алерт](https://error.yandex-team.ru/projects/avocado/settings/alerts) одного [из типов](https://wiki.yandex-team.ru/error-booster/alerts/#1.est4tipaalertov):
 
- `Count` – пороговое значение на количество отфильтрованных ошибок. Наиболее общее решение, схожее с проверками в Кибане на количество ошибок с `[interr]`, `[warning]` или `[nodata]` в сообщении.
- `CountNewErrors` - пороговое значение на количество ошибок с неповторяющимися сообщениями. Если за период времени придёт тысяча ошибок с разными атрибутами, но с одинаковым текстом `"some error message"`, то все они будут считаться как одна. Полезно, если в сообщении указывается значение, которое меняется от запроса к запросу (например, `yandexuid`). В Кибане есть пример подобной ошибки: `EXTERNAL: sk_check_failed for gpsave handler call sk: ya1234567890` про протухшую куку.
- `NewErrors` - то же, что и `CountNewErrors`, но без порога.
- `TrendErrors` – проверка на резкий всплекс роста ошибок, некоторый аналог разладок. В реализации считается среднее за несколько интервалов.

Обязательно укажите дополнительный тэг для Джагглера `morda-platform-{level}`, где уровень `{level}` стоит выбрать согласно [критичности оповещения](monitoring_notifications.md). Для отладки алерта укажите уровень `debug`. Другие тэги указывать не нужно.


Сгенерированный алерт получит имя вида `api.error.yandex-team.ru:alert-NNNN`, где `NNNN` - ID'шник алерта, со следующей конфигурацией:
```
{
  juggler: {
    stable_time: "2",
    critical_time: "3",
    tags: "morda-platform-debug"
  },
  period: {
    filter: "5min"
  },
  checks: {
    field: "count",
    warn: "200",
    crit: "500"
  },
  filter: {
    text: "(page like topnews OR message like topnews) AND environment == production"
  }
}
```

Подробней про заведение алертов EB [читайте здесь](https://wiki.yandex-team.ru/error-booster/alerts)
