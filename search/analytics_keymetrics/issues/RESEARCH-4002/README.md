# Прогноз еком откруток Директа по тирам (коммерция) и некоммерции

Процесс работы над моделью и основные шаги также описаны в тикете https://st.yandex-team.ru/RESEARCH-4002

### Источники данных
Открутки: [product-money](https://yt.yandex-team.ru/hahn/navigation?path=//statbox/cube/daily/product_money/v1), [product-money-light](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/product_money_light/v1)

Маппинг клиентов в еком/не еком: [История вердиктов еком классификатора](https://yt.yandex-team.ru/hahn/navigation?path=//home/bs/users/yabs-analytics/ecom/clients/ecom_clients_history)

Маппинг клиентов в тиры: [ДТС 2.0](https://yt.yandex-team.ru/hahn/navigation?path=//home/comdep-crm-advisor/prod/common/clients/latest)

Прогноз некоммерческих откруток Яндекс.Маркета: [Прогноз расходов по сертификатам](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/special/2021_ecom_forecast/v2/market) от [Кирилла Кузнецова](https://staff.yandex-team.ru/ker4)

### Таблицы на кластере Hahn:
Факт, открутки: [//home/analyticskeymetrics/export/forecasts/special/2021_ecom_forecast/v2/fact](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/special/2021_ecom_forecast/v2/fact)

Прогноз, открутки: [//home/analyticskeymetrics/export/forecasts/special/2021_ecom_forecast/v2/forecast](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/special/2021_ecom_forecast/v2/forecast)

Маппинг клиентов в еком и тир: [//home/analyticskeymetrics/export/forecasts/special/2021_ecom_forecast/v2/clients](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/special/2021_ecom_forecast/v2/clients)

### Использование

1. Обновить даты в запросах лежащих в папке queries/fact. Запустить их в том же порядке (clients.sql -> commerce.sql -> non_commerce.sql -> total.sql)

2. При необходимости выполнить дополнительную очистку данных в ecom_share.py или изменить гиперпараметры модели в ecom_share.yaml.

3. Запустить модель.

4. Для каждого тира загрузить подневные данные спрогнозированных доли екома в тире и доли тира в открутках на YT в папку для прогнозов (forecast) как таблицу shares. Прогноз откруток некоммерции загрузить на YT в ту же папку как таблицу non_commerce_raw.

5. Если Яндекс.Маркет изменил свой прогноз, для более точного сопоставления нашего прогноза некоммерческих откруток нужно обновить таблицу с прогнозом Маркета, так как он используется в оценке реалистичного и пессимистичного прогноза некоммерческих откруток.

6. Обновить даты в запросах лежащих в папке queries/forecast. Запустить их в том же порядке (commerce.sql -> market_comparison.sql -> non_commerce.sql -> total.sql)
