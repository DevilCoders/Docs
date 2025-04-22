# Прогноз выручки бизнес-юнитов

Регулярный процесс в Nirvana:
1. ежедневное [обновление факта](https://nirvana.yandex-team.ru/browse?selected=11418320)
2. еженедельный пересчёт прогноза: **TODO**

### Источники данных
Открутки: [billing_raw_daily](https://yt.yandex-team.ru/hahn/navigation?path=//home/mcsanalytics/db/monthly_tiers/billing_raw_daily)

### Таблицы на кластере Vanga для визуализации:
Факт: [//home/operanalytics/dashboards/forecasts/business_units/v1/fact/latest](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/forecasts/business_units/v1/fact/latest)

Прогноз: [//home/operanalytics/dashboards/forecasts/business_units/v1/forecast/latest](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/forecasts/business_units/v1/forecast/latest)

### Таблицы на кластере Hahn для аналитики:
Факт, открутки: [//home/analyticskeymetrics/export/forecasts/fact/business_units/v1/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact/business_units/v1/latest)

Прогноз, открутки: [//home/analyticskeymetrics/export/forecasts/regular/business_units/v1/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/business_units/v1/latest)

### Запуск

#### Нужные доступы
1. YT, Hahn на чтение:[//home/mcsanalytics/db/monthly_tiers/billing_raw_daily](https://yt.yandex-team.ru/hahn/navigation?path=//home/mcsanalytics/db/monthly_tiers/billing_raw_daily)
2. YT, Hahn на запись: [//home/analyticskeymetrics/export/forecasts/regular/business_units/v1](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/business_units/v1)
3. YT, Vanga на запись: [//home/operanalytics/dashboards/forecasts/business_units/v1/forecast](https://yt.yandex-team.ru/vanga/navigation?path=//home/operanalytics/dashboards/forecasts/business_units/v1/forecast)

#### Локальный запуск
1. Примонтировать Аркадию
    ```sh
    $ cd ~/arc
    $ arc mount -m arcadia/ -S store/
    $ cd arcadia/search/analytics_keymetrics/regular/forecasts/business_units
    ```
2. Создать символическую ссылку на папку [analyticskeymetrics](https://a.yandex-team.ru/arc/trunk/arcadia/statbox/jam/actions/outer-action/analytics_keymetrics/research-3455/action/analyticskeymetrics) с [прогнозным фреймворком](https://wiki.yandex-team.ru/analytics/search/traf/forecasts/framework/) (пока нет pip-пакета, см. тикет [RESEARCH-3604](https://st.yandex-team.ru/RESEARCH-3604))
    ```sh
    $ ln -s ~/arc/arcadia/statbox/jam/actions/outer-action/analytics_keymetrics/research-3455/action/analyticskeymetrics/ analyticskeymetrics
    ```
3. Создать виртуальное окружение и установить пакеты из файла requirements3.txt
    ```sh
    $ sudo apt update && sudo apt install python3-venv  # или python3.X-venv в соответствии с вашей версией python3
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
    Флаг `--no-latest` запрещает переключать симлинк `latest` на последний загруженный прогноз: [//home/analyticskeymetrics/export/forecasts/regular/business_units/v1/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/business_units/v1/latest).
    ```sh
    $ python -m analyticskeymetrics.forecasting --model=business_units_revenue --session=session_name --version-name=2021-12-08_test --no-latest --no-vanga --skip-fact-uploading --skip-pred-uploading
    ```
6. Посмотреть результат

Plotly-графики лежат в `out/business_units_revenue/business_units_revenue/session_name/plots/`

csv-файл с прогнозом - в `out/business_units_revenue/business_units_revenue/session_name/prediction/`
