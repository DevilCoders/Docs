# Прогноз откруток видеохостинга в Видеопоиске в разбивке по типу контента

Тикет: [https://st.yandex-team.ru/FORECASTING-38](https://st.yandex-team.ru/FORECASTING-38)


## Получение факта
Для разбивки откруток по типу контента нужно поле `contentid`. Его нет в кубе РСЯ, но есть в product-money.

Нужно приджойнить сегментацию РСЯ к product-money, и взять только сервис Видеопоиск. Видеохостинг внутри него определяется по флагу `is_vh`.

YQL-запросы: https://st.yandex-team.ru/FORECASTING-38#62ac8acdf5f81f122e892510

## Методика
1. Получаем факт видеопоиска и видеохостинга
2. Разбивваем факт видеопоиска по типу контента и вычисляем их доли
3. Делаем прогноз **долей** срезов
4. Делаем прогноз откруток всего Видеопоиска (не здесь, а в рамках [обычной прогнозной модели РСЯ](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/regular/yan))
5. Перемножаем прогноз откруток Видеопоиска на спрогнозированную долю видеохостинга, а затем и на доли разных типов контента
 
## Прогноз
1. Примонтировать Аркадию
    ```sh
    $ cd ~/arc
    $ arc mount -m arcadia/ -S store/
    $ cd arcadia/search/analytics_keymetrics/regular/forecasts/video_by_content
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
    ```sh
    $ python -m analyticskeymetrics.forecasting --model=video_by_content --session=session_name --version-name=2021-12-08_test --skip-fact-uploading --skip-pred-uploading
    ```
6. Посмотреть результат

    Plotly-графики лежат в `out/video_by_content/video_by_content/session_name/plots/`

    csv-файл с прогнозом - в `out/video_by_content/video_by_content/session_name/prediction/`
