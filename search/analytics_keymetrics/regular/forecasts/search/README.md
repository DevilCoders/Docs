# Прогноз коммерческих откруток Поиска вне РФ

Регулярный процесс в Nirvana: ежедневное [обновление факта](https://nirvana.yandex-team.ru/browse?selected=9296438), еженедельный [пересчёт прогноза](https://nirvana.yandex-team.ru/browse?selected=9296370)

## Источники данных
Открутки: [Product-money light v2](https://st.yandex-team.ru/RESEARCH-3977) (выжимка из Product-money)

## Таблицы на кластере Vanga для визуализации:
Факт: [//home/operanalytics/dashboards/search_revenue_forecast/not_russia/fact/latest](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/search_revenue_forecast/not_russia/fact/latest)

Прогноз: [//home/operanalytics/dashboards/search_revenue_forecast/not_russia/forecast](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/search_revenue_forecast/not_russia/forecast)

## Таблицы на кластере Hahn для аналитики:
Факт: [//home/analyticskeymetrics/export/forecasts/fact/search/not_russia/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact/search/not_russia/latest)

Прогноз: [//home/analyticskeymetrics/export/forecasts/regular/search/revenue_without_russia](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/search/revenue_without_russia)

## Запуск

### Нужные доступы
1. YT, Hahn: на чтение:
   1. Product-money light v2: [//home/analyticskeymetrics/export/product_money_light/v2](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/product_money_light/v2)
2. YT, Hahn на запись:
    1. [//home/analyticskeymetrics/export/forecasts/fact/search/not_russia](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact/search/not_russia)
    2. [//home/analyticskeymetrics/export/forecasts/fact_cleaned/search/not_russia](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact_cleaned/search/not_russia)
    3. [//home/analyticskeymetrics/export/forecasts/regular/search/revenue_without_russia](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/search/revenue_without_russia)
    4. [//statbox/heavy-dict/rsya_forecast](https://yt.yandex-team.ru/hahn/navigation?path=//statbox/heavy-dict/rsya_forecast)
3. YT, Vanga на запись: [//home/operanalytics/dashboards/search_revenue_forecast/not_russia](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/search_revenue_forecast/not_russia)

### Локальный запуск
1. Примонтировать Аркадию
    ```sh
    $ cd ~/arc
    $ arc mount -m arcadia/ -S store/
    $ cd arcadia/search/analytics_keymetrics/regular/forecasts/search
    ```
2. Создать символическую ссылку на папку [analyticskeymetrics](https://a.yandex-team.ru/arc/trunk/arcadia/statbox/jam/actions/outer-action/analytics_keymetrics/research-3455/action/analyticskeymetrics) с [прогнозным фреймворком](https://wiki.yandex-team.ru/analytics/search/traf/forecasts/framework/) (пока нет pip-пакета, см. тикет [RESEARCH-3604](https://st.yandex-team.ru/RESEARCH-3604))
    ```sh
    $ ln -s ~/arc/arcadia/statbox/jam/actions/outer-action/analytics_keymetrics/research-3455/action/analyticskeymetrics/ analyticskeymetrics
    ```
2. Создать виртуальное окружение и установить пакеты из файла requirements3.txt
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
    Флаг `--no-vanga` запрещает загружать что-либо на YT кластер Vanga.

    Флаг `--no-latest` запрещает переключать симлинк `latest` на последний загруженный прогноз: [//home/analyticskeymetrics/export/forecasts/regular/search/revenue_without_russia/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/search/revenue_without_russia/latest).
    ```sh
    $ python3 -m analyticskeymetrics.forecasting --model=search_without_russia --session=session_name --version-name=2021-12-08_test --no-latest --no-vanga --skip-fact-uploading --skip-pred-uploading
    ```
6. Посмотреть результат

    Plotly-графики лежат в `out/search_without_russia/search_without_russia/session_name/plots/`

    csv-файл с прогнозом - в `out/search_without_russia/search_without_russia/session_name/prediction/`
