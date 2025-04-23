# Прогноз коммерческих откруток Директа по индустриям
Дашборд: https://datalens.yandex-team.ru/ctv8abcstmdk8

Регулярный процесс в Nirvana: ежедневное [обновление факта](https://nirvana.yandex-team.ru/browse?selected=9422470), еженедельный [пересчёт прогноза](https://nirvana.yandex-team.ru/browse?selected=9432842)

### Источники данных
Открутки: [product-money](https://yt.yandex-team.ru/hahn/navigation?path=//statbox/cube/daily/product_money/v1)

Маппинг клиентов в индустрии: [ДТС 2.0](https://yt.yandex-team.ru/hahn/navigation?path=//home/comdep-analytics/public/client_tiers/fact)

### Таблицы на кластере Vanga для визуализации:
Факт: [//home/operanalytics/dashboards/industry_forecast/v1/fact](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/industry_forecast/v1/fact)

Прогноз: [//home/operanalytics/dashboards/industry_forecast/v1/forecast](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/industry_forecast/v1/forecast)

### Таблицы на кластере Hahn для аналитики:
Факт, открутки: [//home/analyticskeymetrics/export/forecasts/fact/revenue_by_industry/v1](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact/revenue_by_industry/v1)

Прогноз, открутки: [//home/analyticskeymetrics/export/forecasts/regular/revenue_by_industry/v1/revenue](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/revenue_by_industry/v1/revenue)

Прогноз, маппинг клиентов в индустрию: [//home/analyticskeymetrics/export/forecasts/regular/revenue_by_industry/v1/mapping](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/revenue_by_industry/v1/mapping)

### Запуск

#### Нужные доступы
1. YT, Hahn на чтение:[//home/analyticskeymetrics/export/forecasts/fact/revenue_by_industry/v1](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact/revenue_by_industry/v1)
2. YT, Hahn на запись: [//home/analyticskeymetrics/export/forecasts/regular/revenue_by_industry/v1](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/revenue_by_industry/v1)
3. YT, Vanga на запись: [//home/operanalytics/dashboards/industry_forecast/v1/forecast](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/industry_forecast/v1/forecast)

#### Локальный запуск
1. Примонтировать Аркадию
    ```sh
    $ cd ~/arc
    $ arc mount -m arcadia/ -S store/
    $ cd arcadia/search/analytics_keymetrics/regular/forecasts/industry_forecast
    ```
2. Создать символическую ссылку на папку [analyticskeymetrics](https://a.yandex-team.ru/arc/trunk/arcadia/statbox/jam/actions/outer-action/analytics_keymetrics/research-3455/action/analyticskeymetrics) с [прогнозным фреймворком](https://wiki.yandex-team.ru/analytics/search/traf/forecasts/framework/) (пока нет pip-пакета, см. тикет [RESEARCH-3604](https://st.yandex-team.ru/RESEARCH-3604))
    ```sh
    $ ln -s ~/arc/arcadia/statbox/jam/actions/outer-action/analytics_keymetrics/research-3455/action/analyticskeymetrics/ analyticskeymetrics
    ```
3. Создать виртуальное окружение и установить пакеты из файла requirements3.txt
    ```sh
    $ sudo apt update && sudo apt install python3-venv
    $ python3 -m venv env
    $ source env/bin/activate
    $ python -m pip install --upgrade pip
    $ pip install -i https://pypi.yandex-team.ru/simple/ -r analyticskeymetrics/requirements3.txt
    ```
4. Указать используемые токены. Для тестирования использовать свои токены, для прода - [роботные](https://yav.yandex-team.ru/secret/sec-01dea6ac3ee8vt78tkktq0amz3/explore/versions)
    ```sh
    $ export YT_TOKEN=AQAD-***
    ```
5. Запустить прогноз

    Для локального запуска указать `mcmc_samples: 0` в файле revenue_by_industries.yaml, тогда прогнозы будут запускаться в быстром MAP-режиме.
    Флаг `--no-vanga` запрещает загружать что-либо на YT кластер Vanga.
    Флаг `--no-latest` запрещает переключать симлинк `latest` на последний загруженный прогноз: [//home/analyticskeymetrics/export/forecasts/regular/revenue_by_industry/v1/revenue/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/revenue_by_industry/v1/revenue/latest).
    ```sh
    $ python -m analyticskeymetrics.forecasting --model=revenue_by_industries --session=session_name --version-name=2021-12-08_test --no-latest --no-vanga --skip-fact-uploading --skip-pred-uploading
    ```
6. Посмотреть результат

Plotly-графики лежат в `out/revenue_by_industries/revenue_by_industries/session_name/plots/`

csv-файл с прогнозом - в `out/revenue_by_industries/revenue_by_industries/session_name/prediction/`
