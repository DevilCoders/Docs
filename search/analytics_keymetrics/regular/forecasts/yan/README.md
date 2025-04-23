# Прогноз коммерческих откруток рекламной сети Яндекса (РСЯ)

Регулярный процесс в Nirvana:
1. ежедневное [обновление факта](https://nirvana.yandex-team.ru/browse?selected=11538005)
2. еженедельный [пересчёт прогноза](https://nirvana.yandex-team.ru/browse?selected=9925331)

### Источники данных
Факт откруток: [//home/analyticskeymetrics/export/forecasts/fact/yan](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact/yan)

### Таблицы на кластере Hahn

Прогноз: [//home/analyticskeymetrics/export/forecasts/regular/yan](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/yan)

### Запуск

#### Нужные доступы
1. YT, Hahn на чтение: [//home/analyticskeymetrics/export/forecasts/fact/yan](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact/yan)
2. YT, Hahn на запись: [//home/analyticskeymetrics/export/forecasts/regular/yan](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/yan)
3. **TODO**: [https://st.yandex-team.ru/FORECASTING-28](https://st.yandex-team.ru/FORECASTING-28)

#### Локальный запуск
1. Примонтировать Аркадию
    ```sh
    $ cd ~/arc
    $ arc mount -m arcadia/ -S store/
    $ cd arcadia/search/analytics_keymetrics/regular/forecasts/yan
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
    **WARNING: ** меняю прямо сейчас в [https://st.yandex-team.ru/FORECASTING-28](https://st.yandex-team.ru/FORECASTING-28)
    ```sh
    $ export YT_TOKEN=AQAD-***
    $ export YQL_TOKEN=AQAD-***
    $ export STAT_TOKEN=AQAD-***
    ```
5. Запустить прогноз
    Флаг `--no-latest` запрещает переключать симлинк `latest` на последний загруженный прогноз: [//home/analyticskeymetrics/export/forecasts/regular/yan/v6.3.6/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/yan/v6.3.6/latest).
    ```sh
    $ python -m analyticskeymetrics.forecasting --model=yan_revenue_6_3_4 --session=session_name --skip-fact-uploading --skip-pred-uploading --no-latest
    ```
6. Посмотреть результат:

Plotly-графики лежат в `out/yan_revenue_6_3_4/yan_revenue_6_3/session_name/plots/`

csv-файл с прогнозом - в `out/yan_revenue_6_3_4/yan_revenue_6_3_4/session_name/prediction/`
