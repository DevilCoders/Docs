# Логи в Grafana

## Grafana explore

Исторические, а также потоковые логи можно смотреть в графане, в разделе [Explore](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22service%3Dadmin-www%22%7D,%7B%22mode%22:%22Logs%22%7D,%7B%22ui%22:%5Btrue,true,true,%22none%22%5D%7D%5D):

![grafana-context](grafana-context.png)
1. поделиться ссылкой на результат сохранённых логов
2. посмотреть clickhouse-запрос в YQL
3. Просмотр логов в live-режиме
4. При наведении на лог-запись появляется ссылка "show context". Показывает соседние лог-записи из того же allocation_id.

![grafana-example](grafana-example.png)

Особенности
- Запрос пишется с использованием [языка запросов](https://wiki.yandex-team.ru/vertis-admin/logs/query-syntax/).
  > Например, `service=admin-www layer=prod req.url=*ping* res.statusCode=200`
- Если развернуть лог запись, то можно увидеть, что поле `service` дополняется ссылкой на конкретный сервис в админку (напр.: https://admin.vertis.yandex-team.ru/services/admin-www)
- Также, если поле `requestId` заполнено, напротив него будет ссылка на Jaeger.
- Работают потоковые Live логи. Активируются кнопкой "Live" в правом вернем углу.

При фильтрации логов следует учесть:
- Обрабатывает только один запрос (кнопка "Add Query" может работать не ожидаемо) https://st.yandex-team.ru/VOID-969

## Grafana dashboard

Есть возможность добавить вывод логов в dashboard grafana:
- выбрать datasource vertis-logs
- выбрать тип визуализации Logs в секции Visualisation
- включить флаг Time в секции Display
- Переменные для выбора источника графиков Prometheus/Prometheus-testing автоматически превращается в test/prod для подстановки в layer

![grafana-dashboard.png](grafana-context.png)
