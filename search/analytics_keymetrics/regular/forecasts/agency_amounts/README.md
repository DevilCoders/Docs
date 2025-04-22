# Прогноз помесячных оборотов агентств

Регулярный процесс в Nirvana:
1. ежедневное [обновление планов геомедийной рекламы](https://nirvana.yandex-team.ru/browse?selected=10947089)
2. ежемесячный [пересчёт прогноза](https://nirvana.yandex-team.ru/browse?selected=9298388)
3. ежемесячный [пересчёт прогноза с учётом планов геомедийной рекламы](https://nirvana.yandex-team.ru/flow/82cbc127-8fe7-4ece-b4b0-0795426de582/0bb71ffe-46f4-46d8-9cb9-7e27063f1425/graph)


### Источники данных
Обороты: таблица на YT [//home/search-research/ga/agency_rewards/forecast/v1/fact/acts/by_month](https://yt.yandex-team.ru/hahn/navigation?path=//home/search-research/ga/agency_rewards/forecast/v1/fact/acts/by_month), которую готовит [Максим Пикалов](https://staff.yandex-team.ru/mpikalov).


### Таблицы на кластере Hahn
Прогноз: [//home/search-research/ga/agency_rewards/forecast/v1/predict/acts/igevorse/by_month](https://yt.yandex-team.ru/hahn/navigation?path=//home/search-research/ga/agency_rewards/forecast/v1/predict/acts/igevorse/by_month)

### Запуск

#### Нужные доступы
1. YT, Hahn на чтение: [//home/search-research/ga/agency_rewards/forecast/v1/fact/acts/by_month](https://yt.yandex-team.ru/hahn/navigation?path=//home/search-research/ga/agency_rewards/forecast/v1/fact/acts/by_month)
2. YT, Hahn на запись: [//home/search-research/ga/agency_rewards/forecast/v1/predict/acts/igevorse](https://yt.yandex-team.ru/hahn/navigation?path=//home/search-research/ga/agency_rewards/forecast/v1/predict/acts/igevorse)


#### Локальный запуск
1. Примонтировать Аркадию
    ```sh
    $ cd ~/arc
    $ arc mount -m arcadia/ -S store/
    $ cd arcadia/search/analytics_keymetrics/regular/forecasts/agency_amounts
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
    Параметр `--input-table-name=YYYYMM` отвечает за то, из какой таблицы брать факт: `//home/search-research/ga/agency_rewards/forecast/v1/fact/acts/by_month/YYYYMM`.
    Параметр `--output-table-name=YYYYMM` отвечает за то, в какую таблицу записать прогноз: `//home/search-research/ga/agency_rewards/forecast/v1/predict/acts/igevorse/by_month/YYYYMM`.
    ```sh
    $ python -m analyticskeymetrics.forecasting --model=agency_amount_monthly --session=session_name --skip-fact-uploading --skip-pred-uploading --input-table-name=202202 --output-table-name=202202_test
    ```
6. Посмотреть результат:

Plotly-графики лежат в `out/agency_amount_monthly/agency_amount_monthly/session_name/plots/`

csv-файл с прогнозом - в `out/agency_amount_monthly/agency_amount_monthly/session_name/prediction/`
