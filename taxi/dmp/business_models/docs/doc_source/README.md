
## Установка библиотеки
`pip2 install --user -i https://pypi.yandex-team.ru/simple business_models --upgrade`</br>
Если устанавливаете впервые, то в конце уберите `--upgrade`

Для корректной работы библиотеки с модулями `hahn` и `greenplum`, нужно в корневую папку добавить файл `mylib_config.json` вида:</br>
`{"yt_token": "AQAD-***",
"gp_token": "AQAD-***"}`

## О чем это?
Инструмент моделирование бизнеса (target - поездки) в зависимости от различных факторов (таких как субсидии, скидки и проч.)

Если у вас появится желание что-то самостоятельно дописать в библиотеку, то присылайте пулреквесты, мы будем очень рады! Если мы долго не смотрим, то можно написать, например, мне (rotax@yandex-team.ru или в телеграм - ksuabr). Особенная благодарность ждет тех, кто внесет свой вклад в тестирование библиотеки =) Но если вы что-то пишете, то обязательно добавляйте документацию (у нас она кстати почти везде есть, где нет или непонятная, пишите, будем исправлять).

Если в процессе использования, вы находите баги или хотите что-то добавить в библиотеку, то пишите нам (igorrubanov, rotax, rukireev) или заводите таски в очереди TAXIANALYTICS (естественно с кем-нибудь из нас в наблюдателях/исполнителях). Желательно при создании тикетов пользоваться [этим шаблоном](https://st.yandex-team.ru/settings/templates/issues?name=Баги%20и%20хотелки%20в%20business_models&owner=1120000000066976&queue=TAXIANALYTICS).

## Структура репозитория
Библиотека разбита на логические части:
  - `accuracy` - функции для скоринга абстрактных моделей (сравнение реальных и расчитанных данных)
  - `cohorts` - класс для работы с плоскими когортами (построить ретеншен, ltv, когортную матрицу и проч.)
  - `common_scripts` - для обмена скриптами, использующими модуль (там же всякие полезные примеры использования)
  - `cron` - скрипты, регулярно исполняемые роботом **robot-taxi-models**
  - `models` - модели бизнеса
  - `planning` - инструмент планирования бюджета
  - `plot` - отрисовка графиков по абстрактным входным данным
  - `queries` - расчет и чтение данных (YT)
  - `tests` - тесты для функций и классов во всей библиотеке (всегда будем рады, если вы напишете парочку)
  - `train` - обучалка модели (вход - любая модель, данные; выход - обученная модель)
  
## Основные примеры использования библиотеки
Все примеры собираются в папке <a href="https://github.yandex-team.ru/rotax/business_models/tree/master/common_scripts">common_scripts</a>. Если у вас есть какой-то полезный пример, то можете его добавлять.

`Все примеры имеют свойство устаревать. Так как обратная совместимость не всегда гарантируется, при возникновении ошибок во время исполнения кода изучайте документацию (через ? или функцию describe, например)`

  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/Пример%20использования%20business_models.ipynb">Основной пример использования библиотеки</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/greenplum_module_example.ipynb">Пример работы с модулем greenplum</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/hahn_module_example.ipynb">Пример работы с модулем hahn</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/Cohorts.ipynb">Расчет когорт, простых и сложных</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/scoring_parameters_search_example.ipynb">Подбор наилучших гиперпараметров модели</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/scoring.ipynb">Скоринг модели (оценка точности)</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/scoring-async.ipynb">Асинхронный вариант скоринга модели</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/Planning%20of%20main%20metrics.ipynb">Планирование основных метрик (первая версия)</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/scale_converter_example.ipynb">Пример конвертации скейлов</a>
  - <a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/base_region_converter_example.ipynb">Пример конвертации регионов иерархии</a>
  - [Пример использования библиотеки для работы с гуглдоками](https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/gdocs_helper_example.ipynb)
  - [Пример работы со стартреком](https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/Startrack%20example.ipynb)

## Development
[Доска](https://st.yandex-team.ru/dashboard/27035) в стартреке с бэклогом задач.

Тикеты с багами и пожеланиями можно создавать через шаблоны:
 - [основной шаблон для багов](https://st.yandex-team.ru/settings/templates/issues?name=Баги%20и%20хотелки%20в%20business_models&owner=1120000000066976&queue=TAXIANALYTICS)
 - [шаблон про библиотеку](https://st.yandex-team.ru/settings/templates/issues?name=Библиотека%20business_models&owner=1120000000066976&queue=TAXIANALYTICS)
 - [шаблон про code, без лишних наблюдателей](https://st.yandex-team.ru/settings/templates/issues?name=DEV%20business_models&owner=1120000000066976&queue=TAXIANALYTICS)

## Релизы
Библиотеку можно установить через pip с помощью команды:
`pip2 install --user -i https://pypi.yandex-team.ru/simple business_models`

**Список версий (от последней к первой)**
Все описания спрятаны под кат. В коде репозитория указана последняя существующая версия, но она по содержанию может отличаться от описания. Все изменения будут вноситься в следующую версию.

<details>
<summary><u>Версия 1.3.51</u></summary>
<ul>
<li>hahn.<b>HahnDataloader</b> научился читать и запускать запросы из файлов</li>
<li>greenplum.<b>GreenplumManager</b> научился читать и запускать запросы из файлов</li>
<li>(bugfix) databases.<b>ClickHouseClient</b> теперь правильно читает имена колонок датафрейма</li>
<li><b>setup</b> поставили правильные версии colorama и pandas</li>
<li>models.series_models.<b>CopyModel</b> новая модель: вставляет в будущее те же значения, что в прошлом со сдвигом на год и сглаживает переходы</li>
<li>models.series_models.<b>YoYSlowdownModel</b> новая модель: предсказывает по YoY значениеям, с затуханием  роста</li>
</ul>
</details>

<details>
<summary><u>Версия 1.3.51</u></summary>
<ul>
<li>databases.<b>ClickHouseClient</b> клиент для выполнения запросов к кликхаусу(обертка над вызовом консольного клиента). В databases.<b>transfer_functions</b> добавились функции копирования CH<->YT
<li>(bugfix)hahn.<b>HahnDataloader</b> Поправили баг с неправильно передававшимся syntax_version для yql
<li>util.<b>drop_quantiles</b> Появилась функция, дропающая из датафреймов выбросы
<li>cohort.<b>Cohort</b> научился продлевать ретеншеном когорты вперед на любую длину и по этому считать ltv в том числе
<li>Обновили setup скрипт, теперь он должен протягивать все-все зависимости нашей либы, и, в идеале, ее можно хоть себе на ноут ставить через pip 
<li>util.<b>diff_scales</b> может работать с pd.Series
<li>models.<b>AnomalyCorrector</b> Добавили AnomalyCorrector -- объект, умеющий исправлять аномалии в прогнозах, сравнивая факт и прогноз. К ней прилагается набор AnomalyRule -- правил поиска типов аномалий
<li>models.<b>ShiftModel</b> модель корректирует прогноз по уже сбывшейся части
</ul>
</details>

<details>
<summary><u>Версия 1.3.50</u></summary>
<ul>
<li>hahn.<b>HahnDataloader</b> в __call__ принимает аргументы files и urls, которые аттачат к запросу соответстветственно файл или файл по урлу.</li>
<li>В greenplum объекте connection по дефолту создается не в конструкторе, а при первом вызове какого-нибудь метода. Сильная экономия на времени импорта библиотеки в целом.</li>
<li>В common_scripts добавлен пример расширенный пример работы ScaleConverter (<a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/scale_converter_example.ipynb">Пример конвертации скейлов</a>)</li>
<li>В модуль <b>plot</b> добавлены переменые с корпоротивными цветами Яндекса (YANDEX_BLUE, YANDEX_YELLOW, YANDEX_RED)</li>
</ul>
</details>

<details>
<summary><u>Версия 1.3.49</u></summary>
<ul>
<li>(bugfix)В util.basic.<b>sendmail</b> починили баг с импортами</li>
<li>queries.<b>runner</b> теперь поддерживает обе версии yql. Вся зависимая от версий логика уехала в start_part, который существует в двух версия _v0 и _v1. Сейчас по дефолту подставляется версия 0. Первая включается при передаче run_yql_query `hahn_kwargs={"syntax_version": 1}`</li>
<li>Появилась startrack.<b>Startrack</b> -- обертка над клиентом StartTrack. С ней пример в common_scripts.<b>Startrack example.ipynb</b></li>
<li>hahn.<b>HahnDataloader</b> теперь умеет принимать в __call__ `query_kwargs`, которые пробросятся в `yql.client.query` и `request_kwargs`, которые пробросятся в `request.run`</li>
<li>botolib.<b>bot</b> теперь умеет в конструкторе получать  `default_chat_id`, так что параметр `chat` в методах send_* становится опциональным. Добавили врапперы над всеми методами, чтобы обеспечить обратную совместимость всем, кто передавал в методы неименованный список переменных.
Если вы используете `from botolib import bot`, то ему уже подставлен дефолтный чат `my_telegram_chat` из конфига</li>
<li>queries.<b>reader</b> добавлена возможность читать несколько параметров в одном запросе через read_raw_parameter. Так же доабавятся доверительные интервалы, если они есть и region_id</li>
<li>Появилась util.dataframes.<b>dataframes_close</b> -- функция для сравнения датафреймов с нечетким равенством численных колонок(через np.isclose)  </li>
<li>util.taskmanager.<b>TaskManager</b>  теперь умеет работать с генераторами kwarg</li>
<li>Появился common_scripts.<b>hahn_module_example.ipynb</b> -- ноутбук с примерами на <b>HahnDataLoader</b></li>
<li>(bugfix)В models.seasonality.<b>CohortSeasonality</b> починили исключение про broadcast</li>
<li>В models.<b>YoYForecastModel</b> ускорен forecast</li>
<li>converter.<b>HierarchyConverter</b> оптимизирован, снабжен документацией и в нем появилась возможность получать разбиение на базовые регионы из любого набора region_id</li>
<li>Появилась models.<b>TruncatedCohortModel</b>, которая делает базовый прогноз когортной моделью, выделяет ядро 
и предсказывает его отдельно, а потом размазывает прогноз ядра по исходному когортному прогнозу </li>
<li>Появилась models.<b>ActivityCohortModel</b>, которая разделяет активность и головы, предсказывает их отдельно, а потом склеивает в общий прогноз</li>
<li>В models.series_models.<b>NonLinearModel</b> появился флаг, форсящий неубывание подобранной функции</li>
</ul>
</details>
<details>
<summary><u>Версия 1.3.48</u></summary>
<ul>
<li>(bugfix) Из models удален SplitCityModel, который рушил библиотеку на этапе импорта</li>
</ul>
</details>

<details>
<summary><u>Версия 1.3.47 (версия содержит критический баг)</u></summary>
    <ul>
    <li>(bugfix) В <b>get_str_date</b> исправлен баг с именованием переменных, из-за которого функция не работала</li>
<li><b>simple_cohorts</b> теперь возвращают путь к созданным таблицам, с помощью аргумента read_table=True можно вернуть созданную таблицу</li>
<li>(bugfix) В <b>BruteForceStrategies</b> исправлен баг, не позволявший вызвать <b>start</b> у только что созданного объекта</li>
<li>Появилась функция <b>run_yql</b> + в <b>queries</b> стали до самого конца пробрасываться <b>hahn_kwargs</b></li>
<li>Новый класс <b>ImportIsolation</b> + под него немного переделан <b>Handler</b></li>
<li>Изолирована большая часть зависимостей в библиотеке, подробности в TAXIANALYTICS-6070</li>
<li><b>GLMModel</b> переименована в GLMCohortModel, вместо нее теперь создана более общая модель</li>
<li>Базовый функционал <b>botolib</b> въехал в библиотеку</li>
<li><b>send_mail</b> въехал в библиотеку</li>
<li><b>change_coding</b> работает также со строками и любыми кодировками</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.46</u></summary>
    <ul>
    <li>Классы в <b>optimize</b> получили возможность делать <b>truncate_to</b></li>
<li>(bugfix) <b>BruteForceStrategies.get_strategy_generator</b> корректно обрабатывает директории</li>
<li>Из основного <b>__init__</b> был собран отдельный модуль <b>utils</b></li>
<li>Глобальные переменные <b>POPULATION_SCOPES</b> и <b>scopes</b> удалены</li>
<li>В <b>HierarchyConverter</b> разбивка параметров теперь основана на <b>agg_management_report</b></li>
<li>В <b>HierarchyConverter</b> можно задать иерархию, которая используется</li>
<li>В <b>CohortModel</b> можно не передавать новых пользователей (или передавать константу)</li>
<li>Появилась новая модель <b>YoyForecastModel</b> , которая вычисляет прогноз по соотношениям год к году</li>
<li>В <b>plot.series_data</b> и <b>plot.frame_data</b> можно передавать <b>kwargs</b> для отрисовки</li>
<li>Внутри библиотеки больше не используются <b>Model.__main_params__</b> и <b>Model.__params__</b></li>
<li>Появился класс <b>ConfigHolder</b> для работы с токенами</li>
<li>В <b>optimize</b> появилось несколько новых методов отбрасывания стратегий, подробнее в тикете TAXIANALYTICS-5955</li>
<li>Из <b>mylib</b> скопированы функции <b>clickhouse_query</b> и <b>get_mongo_df</b> , а также константы <b>CONNECTIONS</b> и <b>MONGO_DATABASES</b></li>
<li><b>BruteForceStrategies</b> научилась сохраняться после каждой итерации и продолжать выполнение после остановки</li>
<li>Глобальный рефакторинг <b>hahn</b> : ушли от зависимости от nile, в <b>call</b> читабельные аргументы, возможность перезаписывать таблицу или аппендить через write_table, возможность не передавать туда <b>types</b></li>
<li>(bugfix) <b>QuantileOutliers</b> строгое неравенство исправлено на нестрогое</li>
<li><b>gdocs_helper</b> при первой авторизации будет отдавать ссылку, по которой нужно перейти, а не перекидывать на нее</li>
<li>В <b>simple_cohorts</b> доступен расчет когорт по неуникальным пользователям (в каждом городе/измерении новичок)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.45</u></summary>
    <ul>
    <li>Новая модель работы с выбросами: <b>QuantileOutliers</b></li>
<li><b>to_start</b> теперь работает и с векторами тоже</li>
<li>В <b>HALFMILLIONS</b> добавлены названия городов без "+"</li>
<li>В <b>planning</b> добавлены отрисовки графиков <b>YoY</b></li>
<li><b>BruteForceStrategies</b> научился считываться из нескольких файлов</li>
<li>(bugfix) В <b>ElasticityModel</b> исправлен критический баг при расчете эластичности (drop_duplicates)</li>
<li>В <b>GreenPlum</b> появился метод <b>dump</b> (загрузка <b>GP</b> -> <b>YT</b>)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.44</u></summary>
    <ul>
    <li>Исправлен баг в модели <b>NPreviousScaleMigration</b>: неправильно вычислялась последняя точка факта </li>
    <li>В <b>greenplum</b> добавлена возможность передать <i>user</i> и <i>token</i>, из под которых следует запустить запрос</li>
    <li>Добавлен новый тип кривой <b>DoubleLinearCurve</b> в models.curves </li>
    <li>В <b>hahn</b> и <b>greenplum</b> добавлены предупреждения, когда отсутсвует mylib_config.json</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.43</u></summary>
    <ul>
    <li>(bugfix) в <b>ScaleConverter</b> исправлен баг из-за которого нужно было обязательно передавать и <b>additive</b> и non-additive метрики (иначе все падало)</li>
<li>В рамках тикета <a href=https://st.yandex-team.ru/TAXIANALYTICS-5585>TAXIANALYTICS-5585</a> внесен ряд изменений в модуль <b>optimize</b> (в этой версии он уже полностью работоспособен)</li>
<li><b>TaskManager</b> научился делать перерыв между запусками процессов: <b>sleep_time</b></li>
<li>В <b>plot_many_bars</b> добавлен параметр <b>show_flg</b></li>
<li>Добавлен список <b>HALFMILLIONS</b> - в нем список городов с населением 500К+ (осторожно, там есть города вида "Махачкала + Каспийск", в этом случае город "Махачкала" отсутствует)</li>
<li>В список <b>MILLIONS</b> добавлены города Новосибирск, Нижний Новгород, Волгоград (раньше они были только вместе с "+ др.город")</li>
<li>В классе <b>Greenplum</b> добавлен метод <b>grant</b> - он позволяет дать доступ к таблице. В методы <b>replicate</b> и <b>write_table</b> добавлен соответствующий флаг <b>with_grant</b></li>
<li>В <b>ConfidenceInterval</b> добавлена обработка специфических дат (таких как новогодняя неделя, майские и т.п.)</li>
<li>(bugfix) в <b>split_scale</b> исправлен баг с индексированием разделяемых данных</li>
<li>В <b>MultipleConfigsModel</b> добавлена возможность использования дефолтного конфига для городов, которые не упоминаются ни в одном другом конфиге</li>
<li>(bugfix) в <b>plot.series_data</b> раньше для <b>shift</b> использовался просто slice, перешли на <b>iloc.</b> Это критично, потому что провоцировало ошибки, если индекс является числом</li>
<li>(bugfix) в <b>Trainer</b> выпилили захардкоженные куски, где использовалось 'week' вместо <b>scale</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.42</u></summary>
    <ul>
    <li><b>simple_cohorts</b> исправлен баг с регистром as/AS</li>
    <li>Доверительные интервалы группируются по скейлу (раньше по последней точке факта)</li>
    <li>В <b>read_score_parameters</b> 500k+ города теперь не группируются, а рассматриваются индивидуально</li>
    <li>В <b>Trainer</b> появилась возможность получения DataFrame из всех возможных конфигов c результатами их скоринга</li>
    <li>Обработка исключений в <b>TaskManager</b></li>
    <li>Реализация алгоритмов космолета TAXIANALYTICS-5585</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.41</u></summary>
    <ul>
    <li><b>Model</b> теперь можно сохранить в pickle</li>
    <li><b>CohortModel</b> не падает и возвращает пустой датафрейм, когда входные данный оказываются пустыми после фильтрации</li>
    <li><b>ElasticityModel</b> predicted_values is property</li>
    <li><b>ElasticityModel</b> фикс бага при использовании месячного скейла (правка)</li>
    <li>Реализация алгоритмов космолета TAXIANALYTICS-5585</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.40 (версия содержит критические баги)</u></summary>
    <ul>
    <li>Фикс бага в shift_date, когда date не итерируемая переменная</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.39 (версия содержит критические баги)</u></summary>
    <ul>
    <li><b>Model</b> фикс бага, когда date_to не None</li>
    <li>Добавлен новый тип сезонности <b>ClusterSeasonality</b>, который может сглаживать и кластеризовать сезонности, полученные для городов индивидуально другими методами</li>
    <li>Добавлен модуль <b>gdocs_helper</b> для работы с Google Sheets</li>
    <li><b>ElasticityModel</b> фикс бага при использовании месячного скейла</li>
    <li>Реализация алгоритмов космолета TAXIANALYTICS-5585</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.38</u></summary>
    <ul>
    <li>Появились функции для работы с гуглдоками: <b>gdocs_helper</b> (подробнее про них, смотрите в примере использования)</li>
<li>(bugfix) исправлен критический баг: <b>Model</b> игнорировала параметр <b>ndots_fit</b></li>
<li>(bugfix) <b>CohortModel</b> теперь не падает, если в <b>newbie</b> переданы лишние столбцы</li>
<li>в функция для считаывания резуьтатов скоринга вынесена из <b>ConfidenceInterval</b> в <b>reader.read_score_parameters</b></li>
<li>сам класс <b>ConfidenceInterval</b> был сильно упрощен</li>
<li>произошло упрощение объекта <b>optimize.properties.CohortProperties</b> (который изначально был скопирован из planning.properties.PlanObjectProperties)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.37</u></summary>
    <ul>
    <li>Попытка исправить баг в <b>shift_date</b> #2. Финальная</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.36 (версия содержит критические баги)</u></summary>
    <ul>
    <li>Добавлен модуль <b>confidence_interval</b> для работы с доверительными интервалами</li>
<li>Попытка исправить баг в <b>shift_date</b> #1</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.35 (версия содержит критические баги)</u></summary>
    <ul>
    <li>Исправлен досадный баг связанный с неймингом, из-за которого не работала оконная сезонность: max_diff использовался в нескольких функциях</li>
<li>В <b>queries_config</b> из custom_regions удалена удаленная из иерархии вершина</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.34 (версия содержит критические баги)</u></summary>
    <ul>
    <li>Внесены правки в модуль <b>convert</b>: появился учет новых регионов, добавлен класс для конвертации скейлов</li>
<li>Добавлен новый класс <b>HolidaySeasonality</b>: для метрики в дневном скейле вкупе с производственным календарем можно находить вектор сезонности (эффектов праздников на метрику) </li>
<li><b>greenplum</b> теперь может получать словарь с типами данных <b>dtype</b></li>
<li>Функции работы с датами <b>get_period_list, to_start, days_in_period, shift_date, diff_scales</b> теперь утилизируют функционал pandas (http://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html). Основные изменения -- возможность работать с итерируемыми объектами и скорость работы</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.33</u></summary>
    <ul>
    <li><b>FlatNewbieFunction</b> в <b>optimize.money_function</b> заработали</li>
<li><b>MoneyFunction</b> научились искать точку, где достигается верхний предел функции</li>
<li>По ряду причин попали в релиз, но все еще не работаю <b>optimize.properties</b></li>
<li><b>hahn</b> научился обрабатывать параметр <b>syntax_version</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.32</u></summary>
    <ul>
    <li>Функция <b>get_diff_scales</b> убрана из <b>seasonality</b> и перенесена в основной init, а работа метода <b>get_scale_number</b> ускорена (больше там не используется apply)</li>
<li>Метод отрисовки <b>plot_many_frames</b> теперь может работать с <b>Series</b></li>
<li>(bugfix) в <b>CohortSeasonality</b> если <b>scale</b> передан в индексе данных и не передан scale_number, то код теперь не будет падать</li>
<li>(bugfix) правильный учет <b>date_to</b> в ElasticityModel.get_fact()</li>
<li><b>Analyser</b> научился считать вклад от каждой метрики в <b>GMV</b> и <b>Trips</b></li>
<li><b>Analyser</b> научился считать расхождения план/факт по нескольким городам</li>
<li>Добавлен модуль <b>convert</b> : в нем содержатся классы для разбиения данных на разные регионы и скейлы</li>
<li>Добавлена функция <b>apply_multiple_factors</b> : она позволяет исправить когортные данные по дневной матрице коэффициентов</li>
<li>Добавлена функция <b>read_table_adjust_factors</b> : читает данные и сразу их исправляет с помощью <b>apply_multiple_factors</b></li>
<li>В <b>optimize</b> появилось несколько <b>money_function</b> (новички в нерабочем состоянии)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.31</u></summary>
    <ul>
    <li>метод <b>filter_data</b> в <b>Model</b> теперь может фильтровать по fit_scale. Нужно, если fit/forecast используют разные scale</li>
    <li>В <b>ElasticityModel</b> в методе <b>get_changes_for_balance</b> добавлена проверка деления на нулевой баланс</li>
    <li>Функция <b>convert_data_to_scale</b> обогащена опцией разбивки данных с наперед заданной пропорцией</li>
    </ul>
</details>
</br>

</br>
<details>
<summary>Более старые версии</summary>

<details>
<summary><u>Версия 1.3.30</u></summary>
    <ul>
    <li>методы <b>save</b> и <b>load</b> в <b>Model</b> теперь корректно обрабатывают списки и словари, содержащие модели</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.29</u></summary>
    <ul>
    <li>(bugfix) <b>smart_update</b> работает с <b>None</b> (в предыдущей версии из-за этого не работала часть yql-запросов)</li>
<li>(bugfix) в <b>__init__</b> добавлен метод <b>is_string</b> + на него переведена OneParameterModel, где не работала передача параметров через <b>unicode</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.28 (версия содержит критические баги)</u></summary>
    <ul>
    <li>было ускорено выполнение <b>split_scale</b> в случае если <b>proportions</b> передаются как <b>np.array</b></li>
<li><b>CurveFitter</b> также был существенно ускорен (за счет перехода на np.array)</li>
<li>расширена документация для Model, OneParameterModel, <b>ElasticityModel</b></li>
<li><b>plot.series_data</b> по-умолчанию изменила значение <b>shift</b> на 0</li>
<li><b>ElasticityModel</b> была переведена под капотом на <b>OneParameterModel</b> и получила некоторое ускорение в работе: подробности можно смотреть в тикете <a href="https://st.yandex-team.ru/TAXIANALYTICS-5304">TAXIANALYTICS-5304</a></li>
<li>функция <b>get_scale_number_in_year</b> перенесена в <b>__init__</b></li>
<li>в <b>LinearBoundedCurve</b> добавлена поддержка передачи в качестве аргумента <b>np.array</b></li>
<li>класс <b>Model</b> получил новое рождение: пока с сохранением обратной совместимости</li>
<li>в классе <b>Model</b> произошли переименования (старые названия работают, но deprecated): <b>__main_params__</b> —> main_parameters, <b>__params__</b> —> external_parameters, fit/forecast_incity —> fit/forecast_dimension</li>
<li>в классе <b>Model</b> методы save/load позволяют сохранять и загружать модели любой вложенности + загрузка сложной модели не требует дополнительных танцев с бубнами</li>
<li>в классе <b>Model</b> методы fit/forecast содержат логику: фильтруют данные и вызывают внутри *_dimension (поэтому не надо больше везде это писать заново). Причем там есть +/- гибкие настройки фильтрации, специфичные например для <b>OneParameterModel</b></li>
<li>(bugfix) в <b>budget_metrics</b> исправлено использование функции <b>NVL</b></li>
<li>в <b>queries.runner</b> добавлены шаблоны для вычисления когорт (simple_cohorts) по группам <b>run_group_cohorts</b> и обычных когорт <b>run_simple_cohorts.</b> Какие-то подробности есть в тикете <a href="https://st.yandex-team.ru/TAXIANALYTICS-5445">TAXIANALYTICS-5445</a></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.27</u></summary>
    <ul>
    <li>обновлен список городов-миллионников (MILLOINS) + добавили соответствие названий вершинам геоиерархии для миллионников (MILLIONS_GEO)</li>
<li>в <b>WindowSeasonality</b> обработка выбросов вынесена в отдельный параметр <b>drop_outliers</b></li>
<li>(bugfix) в <b>CohortSeasonality</b> исправлен баг, требующий наличия строки с нулями в самом начале когорт</li>
<li><b>CurveFitter</b> (и соответственно <b>OneParameterModel</b> ) получил параметр <b>seed_curve</b> (по этой кривой модель предобучается, результат затем используется как x0 для основной кривой)</li>
<li><b>OneParameterModel</b> получила совместимость с методами борьбы с выбросами через параметр <b>outliers</b></li>
<li><b>OneParameterModel</b> может делать прогноз (forecast) для данных без колонки <b>scale</b> (в этом случае прогноз будет делаться просто для всего DataFrame)</li>
<li>в <b>OneParameterModel</b> определен новый метод fast_forecast, который работает только с числами, зато быстро</li>
<li>в <b>ElasticityModel</b> добавлена возможность вычислять demand/supply_change не циклом, а через балансные значения конверсии, через параметр <b>iterative_change</b></li>
<li>по-умолчанию стали доступны загрузки discounts, <b>sub_gmv</b> и <b>commission</b> в таблицу planning/fact</li>
<li>появился вариант загрузки нескольких фактических метрик одним запросом (вместо нескольких маленьких)</li>
<li>в <b>recount_metric</b> появилась возможность самостоятельно задать <b>timeout</b> между запросами</li>
<li>расчеты когорт по <b>SH</b> перешли на <b>driver_session_reduced</b> + изменился порядок джойнов в запросе (все изменения направлены на ускорение расчета)</li>
<li><b>plot_many_scatters</b> научился получать как параметр <b>colormap</b> + общие для всех данных аргументы</li>
<li>Plan.from_excel() научился читать планы, в которых нет всех необходимых листов</li>
<li>добавлен модуль <b>optimize</b> (на данный момент в него вошли только базовые классы + функция эффекта от скидок)</li>
<li>появилась функция <b>describe</b> (она умеет выводить всю документацию по классу)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.26</u></summary>
    <ul>
<li>добавлен скрипт <b>hourly_metrics_restore</b> который позволяет восстановить данные старого <b>Uber</b> в часовых точках по <b>supply</b> и <b>demand</b></li>
<li>в модуль <b>planning</b> добавлена финальная работающая версия <b>hit_by_retention</b></li>
<li>(несовместимость с предыдущими версиями) из-за обновления иерархии название страны теперь берется из lvl2_name_ru</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.25</u></summary>
    <ul>
    <li><b>OneParameterModel</b> умеет отрисовывать веса точек цветом</li>
<li>добавлен модуль <b>greenplum</b> (по аналогии с hahn) для выполнения запросов на <b>GP</b> и перезаливки данных с <b>YT</b></li>
<li>(критичный bugfix) при переходе на неикрементальный расчет когорт по водительским сессиям данные раньше задваивались (исправлено)</li>
<li>модули <b>hahn</b> и <b>greenplum</b> не нарушают работу библиотеки, если отсутствует токен</li>
<li>в YQL-запросах теперь используется страна из геоиерархии, притянутая в запросе <b>hierarchy</b></li>
<li>в <b>hourly_trips</b> выделены поездки по старому <b>Uber</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.24 (некоторые функции обратно несовместимы)</u></summary>
    <ul>
    <li>в расчет бюджетных метрик <b>budget_metrics</b> добавлен <b>NI</b> + структурировали расчет скидок, субсидий и <b>GMV</b></li>
<li>в основной <b>__init__</b> добален декоратор <b>retry</b> : быстрый путь к перезапуску функции, если произошла ошибка</li>
<li>при запуске <b>queries.runner.recount_metric</b> с несколькими метриками, они запускаются с таймаутом в 5 секунд</li>
<li>в <b>Elasticity.get_balance_conversion</b> добавлена возможность вычислять баланс по стоимости (веса на <b>demand</b> и <b>supply</b> )</li>
<li>(несовместимость с предыдущими версиями, для инкрементальных расчетов) в расчет когорт по водителям добавлено разделение на найм и ренайм</li>
<li>модуль <b>planning</b> претерпел некоторые перемены и научился подгонять по ретеншену (но еще с багами)</li>
<li>расчет скрипта <b>surge</b> стал deprecated, теперь он перенесен в <b>budget_metrics</b> и считается по <b>dm_order</b></li>
<li>автоматически в <b>planning.fact</b> начала прогружаться метрика <b>demand_first_city</b></li>
<li>все параметры-исключения (с которыми можно пересчитывать без sub_path) вынесены в основной конфиг</li>
<li>(bugfix) исправлен расчет когорт в конфигурации: астрономические, по первому городу + с обрезанием по 45 дней</li>
<li>(bugfix) после расчета новых пользователей добавлен <b>commit</b> (ошибка сказывалась только на расчете, в котором не было новых водителей)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.23</u></summary>
    <ul>
<li>Фикс бага в версии 1.3.22</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.22 (баг)</u></summary>
    <ul>
<li>фикс бага в версии 1.3.21</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.21 (баг)</u></summary>
    <ul>
<li>добавлен инкрементальный расчет driver_sessions</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.20</u></summary>
    <ul>
<li>исправлен баг в query расчета surge</li>
<li>в init.py добавлен список городов-миллионников MILLIONS</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.19 (содержит баг в query расчета surge)</u></summary>
    <ul>
<li>инкрементальный расчет surge</li>
<li><i>queries/reader.py:</i> вспомогательная функция convert_to_datetime(), конвертирует колонки с датами-строками в тип datetime</li>
<li><i>queries/runner.py:</i> recount_metric() теперь может запускать YQL запросы для расчета метрик параллельно  </li>
<li><i>fact.yql:</i> не сохраняет старые версии факта при выгрузке</li>
<li><b>queries:</b> реализована возможность считать когорты, не обрезанные по последней неделе, т.е. текущая неделя будет неполная, задается параметром truncate_incomplete_scale</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.18</u></summary>
    <ul>
<li>В модуль <b>curves</b> добавлен класс LinearBoundedCurve</li>
<li>В класс <b>seasonality</b> добавлен метод <i>crop_seasonality()</i> он обрезает сезонность, делая ее такой, чтобы максимальное значение не превышало upper_bound, а минимальное было не меньше lower_bound</li>
<li><b>planning:</b> many retentions saved</li>
<li><b>planning:</b> comparing retention in any period</li>
<li>users_new.yql исправлен баг с подсчетом туристов</li>
<li><b>hit_by_activity:</b> handle None seasonality</li>
<li><b>hit_method:</b> fix bug with comparing error</li>
<li><b>planning:</b> newbie dependencies between cities</li>
<li><b>NPreviousScaleMigration:</b> исправлен баг с копированием модели</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.17</u></summary>
    <ul>
<li><i>budget_metrics.yql:</i> добавлены новые поля</li>
<li>в <b>NPreviousScaleMigration</b> добавлена возможность передавать сырую таблицу с миграциями + исправлены пара багов </li>
<li>в <i>queries/reader.py</i> добавлена read_planning_table() - функция чтения любых таблиц из папки planning на YT</li>
<li>в <i>queries/runner.py</i> добавлена upload_planning_table() - функция выгрузки любого датафрейма в папку planning на YT</li>
<li>исправлен баг в <b>OneParameterModel</b> фикс</li>
<li>в <i>queries/runner.py</i> добавлена функция __convert_dtypes_to_yql__(), преобразующая типы колонок датафрейма в типы YT</li>
<li><b>MultipleConfigs:</b> чтение параметров модели из папки, если вместо самих параметров передан путь</li>
<li>в <i>queries/runner.py</i> реализована возможность выгрузки фактических метрик одним чанком</li>
    </ul>
</details>
</br>
<details>

<summary><u>Версия 1.3.16</u></summary>
    <ul>
<li>Исправлен setup.py файл (папка curves добавлена)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.15 (версия не работает)</u></summary>
    <ul>
<li>В queries.runner.py в методе upload_forecast.py исправлена бага при инициализации today при scale=='month'</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.14</u></summary>
    <ul>
<li>Версия, не содержащая критических багов</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.13 (версия содержит критические баги)</u></summary>
    <ul>
<li>Были добавлены новые баги исправлены старые</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.12 (версия содержит критические баги)</u></summary>
    <ul>
<li>Были добавлены новые баги исправлены старые</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.11 (версия содержит критические баги)</u></summary>
    <ul>
<li>Были добавлены новые баги исправлены старые</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.10 (версия содержит критические баги)</u></summary>
    <ul>
<li><b>CohortModel</b>: передача скейла в <b><i>continue_retention_curves</b></i></li>
<li>добавлена <b>OneParameterModel</b>: Модель, подбирающая наилучшую кривую, описывающую зависимость одной переменной от другой. Вид кривой может быть задан параметрами модели.</li>
<li>создан отдельный модуль <b>curves</b>, состоящий из классов <b>Curve</b> (класс кривой) и <b>CurveFitter</b> (Подбирает для объекта класса <b>Curve</b> (или его наследника) параметры (вектор чисел), наилучшим образом описывающие переданный ему набор точек на плоскости)</li>
<li>в модели эластичности теперь вместо <b>ConversionCurve</b> используется класс <b>Curve</b></li>
<li>добавлен новый метод <b><i>plot_many_scatters</b></i>  в модуль <b>plot</b>: отрисовка нескольких Series/DataFrame на одном графике с возможностью передачи аргументов отрисовки</li>
<li><b>NPreviousScaleMigration</b> теперь сохраняет входные данные в своем теле</li>
<li>исправлен баг с последней неделей в <b><i>create_full_seasonality</b></i></li>
<li>в модуле <b>queries</b> переписаны запросы инкрементального добавления данных в таблицы через DEFINE ACTION</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.9</u></summary>
    <ul>
<li>исправлен метод <b><i>__deepcopy__</b></i> в классе <b>DictAlikeObject</b></li>
<li>в модуль <b>planning</b> добавлен скрипт форматирования Excel данных</li>
<li>рефакторинг <b>Planner</b></li>
<li>исправлен баг в <b>app_cannibalization.yql</b>, из-за которого дублировались данные</li>
<li><b>planning</b>: added fact diffs in retention list</li>
<li>в модуль <b>queries</b> добавлены запросы для подсчета метрик <b><i>demand/trips/supply</b></i> по любому скейлу</li>
<li>исправлена ошибка сдвига на 3 часа при подсчете метрик <b><i>demand/trips/supply</b></i></li>
<li>исправлен баг <b>series_models.NonLinearModel</b>, из-за которого он падал на некоторых входных параметрах</li>
<li>добавлен новый класс <b>SplittedSourcesElasticityModel</b>: позволяет реализовать возможность предсказания внутри модели эластичности сразу supply и demand в произвольной разбивке. Например, предсказать supply по всем водителям, а demand в разбивке на телефон и онлайн, а потом с учетом суммарного деманда предсказать поездки. Основной моделью (интерфейсом) при этом остается модель эластичности</li>
<li>исправлен баг проброски <b><i>region_id</b></i> из иерархии в таблицы из planning</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.8</u></summary>
    <ul>
<li>в <b>series_models.LinearModel</b> добавлен новый параметр <b><i>start_default_dot</i></b>, теперь <b><i>start_default_dot</i></b> отвечает за то, когда начинать заменять коэффициенты на default значения, а <b><i>start_corrections_dot</i></b> за то, когда ограничивать значения константой</li>
<li>в класс <b>Trainer</b> добавлен метод <b><i>get_closest_models(index, distance)</i></b>, он находит все конфиги, которые отличаются от модели под номером <b><i>index</i></b> на <b><i>distance значений</i></b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.7</u></summary>
    <ul>
    <li>исправлен баг с логгированием в файл в классе <b>Timer</b></li>
<li>(баг) была попытка исправить баг в <b>NonLinearModel</b> , из-за которого при указании fit_incremental=False код мог падать. В результате был выявлен другой баг, из-за которого при больших <b>non_linear_model_border</b> код падает</li>
<li>в когортной сезонности исправили баг с добавлением 53 недели (в предыдущих версиях сезонность на 52 неделе занижена)</li>
<li>исправлен баг в recount_all_metrics(): изменен алгоритм поиска всех скриптов</li>
<li>в plot.cohorts() добавлена возможность передавать <b>xlims</b> и <b>ylims</b></li>
<li>в расчеты когорт и метрик (по <b>dm_order</b> ) добавлена обработка случая, когда тарифная зона в источнике отсутствует</li>
<li>в <b>LinearModel</b> появился параметр <b>start_corrections_dot</b></li>
<li>в основной <b>init</b> добавлен новый класс DictAlikeObject, который делает наследуемый от него класс похожим на словарь</li>
<li>в основной <b>init</b> добавлена функция <b>get_period_list</b> возвращающая список дат из диапазона</li>
<li>в <b>budget_metrics.yql</b> <b>GMV</b> теперь считается по <b>order_cost</b> вместо <b>user_cost</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.6</u></summary>
    <ul>
<li>в <b>city_migration</b> добавлено восстановление данных Убера</i></li>
<li>в таблицах в <b>planning</b> добавлено новое поле - id региона по геоиерархии</li>
<li>вынесен список кастомных вершин иерархии в общие параметры (больше не надо их дублировать) + можно теперь посчитать что-нибудь только по кастомным вершинам</li>
<li>теперь hahn может логировать запускаемые запросы вместе с публичными ссылками на них (по умолчанию отключено)</li>
<li>добавлен запрос <b>budget_metrics.yql</b>, вычисляет основные метрики из бюджета для сравнения план/факт</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.5</u></summary>
    <ul>
<li>исправлен баг версии 1.3.4: в <b>MultipleConfigs</b> не сохранялись некоторые параметры</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.4 (версия содержит критические баги)</u></summary>
    <ul>
<li>в расчет часовых точек добавлена агрегация по глобальному скейлу (загружается в соответсвующие подпапки month/week/day)
<li>изменены дефолтные параметры для расчета когорт: теперь факт заливается из агрегированных часовых точек</li>
<li>добавлена возможность сохранять вложенные модели (когда параметром одной модели является инстанс другой модели)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.3</u></summary>
    <ul>
    <li>в расчет часовых точек добавлен параметер <i>use_first_city</i></li>
<li>добавлен запрос сохранения текущей таблицы иерархии</li>
<li>изменены дефолтные параметры для расчета когорт: по первому городу, без таймаутов </li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.2</u></summary>
    <ul>
    <li>исправлен баг в <b>CohortSeasonality</b>, из-за которого зависал расчет если в данных много нулей</li>
<li>в <b>MultipleConfigs</b> добавлена возможность пропуска ошибок при fit/forecast</li>
<li>добавлены новые вершины иерархии</li>
<li>в <b>runner</b> добавлена возможность пересчитывать часовые точки в любых периодах, не указывая при этом <b>sub_path</b> (параметры <b>first_date_shift</b> и <b>last_date_shift</b>)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.1</u></summary>
    <ul>
<li>добавлен новый класс <b>MultipleRetention</b>: в нем реализована возможность продлевать не единую кривую ретеншена, а каждую кривую для каждой когорты (его внедрение потребовало изменений в CohortModel, LinearModel)</li>
<li>изменена логика работы LinearModel: теперь она продлевает не одну кривую ретеншена, а матрицу ретеншенов. Работает в связке с <b>MultipleRetention</b></li>
<li>в <b>Trainer</b> добавлен метод сохранения посчитанных конфигов в файлы</li>
<li>расширена документация в <b>trainer.py</b> и <b>NonLinearModel</b></li>
<li>добавлена модель-обертка для использования в пердсказании нескольких конфигов <b>MultipleConfigs</b></li>
<li>создан новый класс <b>NPreviousScaleMigration</b>, раелизующий механику миграций из города в город, имея матрицу миграций и применяя ее к результатам работы другой модели, например, когортной	</li>
<li>в <b>NonLinearModel</b> из кода вынесена константа <b>max_regular_retention</b> , ограничивающая сверху значение ретеншена</li>
<li>в <b>CohortModel</b> добавлен параметр <b>only_add_value_seasonality</b> , который позволяет не вычитать сеонность из истории, а только добавлять ее в конце</li>	
<li>в базвый класс <b>Seasonality</b> добавлен атрибут, отвечающий за число периодов в году + метод, позволяющий получить сезонность из единиц <b>empty_season</b></li>
<li>все активные запросы переехали на иерархию: теперь агрегация происходит по единой иерархии https://tableau.taxi.yandex-team.ru/#/views/Geohierarchy/hierarchy?:iid=1 . То есть <b>city</b> теперь берется из тарифной зоны  + иерархии</li>
<li><b>(по техническим причинам не вошло в релиз)</b> добавлены запросы вычисляющие <b>surge</b> и каннибализацию новичков телефона и онлайна</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.0</u></summary>
    <ul>
    <li>(исправлен баг версии 1.2.34) окончательно перешли на поиск региона по названию города</li>
<li>данные убера теперь восстанавливаются в объектах <b>user_info</b> и <b>driver_info</b> , то что раньше называлось в них <b>sessions_with_wait</b> , <b>supply_hours</b> , <b>visited_users</b> , <b>drivers_on_line</b> , <b>trips</b> , <b>rides</b> теперь имеет суффикс <b>_yandex</b></li>
<li>в расчет по приложениям добавлен еще один флаг, а флаг <b>include_application</b> сменил свою роль. Теперь <b>use_application</b> говорит о том, надо ли вообще считать когорты с учетом тарифов, а <b>include_application</b> отвечает за то, хотите вы посчитать когорты по указанному приложению или по всем, <b>кроме</b> него</li>
<li>обновили документацию в <b>recount_all</b> и <b>recount_query</b></li>
<li>добавлена полноценно рабочая версия <b>HitMethod</b> и <b>HitByActivity</b></li>
<li>добавлен расчет метрики каннибализация приложений: <b>app_cannibalization</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.37</u></summary>
    <ul>
    <li>пофиксили минорный баг версии 1.2.36 при расширении <b>Score</b></li>
<li>в <b>weight_curves.py</b> добавлена экспоненциальная кривая веса (ExpExpWeightCurve)</li>
<li>в <b>Score</b> добавлен параметр <b>known_future</b> , который позволяет обучать модель на всех данных, а не только до <b>date_to</b> (работает только для когортной модели!)</li>
<li>в расчет миграций добавлены поездки (раньше были только пользовательские сессии)</li>
<li>в <b>Trainer</b> добавлен метод <b>get_config_files</b></li>
<li>в <b>WindowSeasonality</b> добавлена возможность отнормировать сезонность, чтобы в сумме она давала количество периодов</li>
<li>обновлен класс <b>series_models.NonLinearModel</b> (больше не используется <b>scipy.optimize.curve_fit</b> + добавлены разные варианты расчета)</li>
<li>в <b>__init__</b> добавлена функция <b>extend_index</b> , которая позволяет расширить индекс pandas-объекта (например, добавить в индекс содержащий только город, еще и недели из другого pandas-объекта)</li>
<li>в <b>__init__</b> добавлена функция <b>assign_series</b> , которая позволяет присвоить одной колонке в <b>DataFrame</b> или <b>Series</b> значение <b>Series</b> с другим индексом, при этом индекс расширяется до объединения индексов</li>
<li>исправлен минорный баг в <b>CohortModel</b> , из-за которого нельзя было передавать в качестве <b>dimensions</b> список</li>
<li>интерфейс базового класса <b>Model</b> приведен в соответствие с новой реальностью</li>
<li>бета-версия классов <b>HitMethod</b> и <b>HitByActivity</b> добавлена в <b>planning</b> (они позволяют корректировать прогноз с помощью активности новичков, чтобы попасть в цель по поездкам)</li>
<li>теперь в сообщении об ошибке при чтении таблицы будет сообщаться также переданное пользователем название таблицы</li>
<li>при расчете объекта <b>users_new_one_by_phone</b> теперь будет использоваться <b>dttm</b> в качестве <b>expire_from</b> , а не когорта (это позволит не терять сессии)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.36</u></summary>
    <ul>
    <li>в <b>Score</b> добавлен метод <b>add</b> , который позволяет объединить результаты двух объектов <b>Score</b> (не работает, если один из объектов пустой)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.35</u></summary>
    <ul>
    <li>в основной  <b>__init__.py</b> добавлена функция  <b>fill_missing_dates</b> , заполняющая пропущенные в когортах данные нулями</li>
<li>в функцию  <b>read_plan</b> добавлено преобразование  <b>value</b> к типу  <b>float</b></li>
<li>в запросе, загружающем прогноз заменили  <b>full</b> <b>join</b> со списком новых городов на  <b>left</b> <b>join</b></li>
<li> <b>Timer</b> научился писать стартовое сообщение</li>
<li>расчет метрики  <b>city_migration</b> теперь рассчитывает миграции из каждого города в каждый</li>
<li>из  <b>__mapping</b> 'ов убрали NULL'ы, чтобы ускорить расчет когорт</li>
<li>в  <b>ElasticityModel</b> параметр  <b>ndots_fact</b> в методе  <b>fit</b> , изменил свое название на  <b>ndots_fit</b></li>
<li>(исправлен баг версии 1.2.34) в той версии была добавлена лишняя строка, из-за которой  <b>ElasticityModel</b> фиттилась ровно для одного города, в этой версии баг исправлен</li>
<li>появился новый класс  <b>TaskManager</b> , который будет отвечать за многопоточность. Сейчас в нем есть один метод, параллельно вычисляющий функцию на нескольких, возможно меняющихся, параметрах</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.34 (версия содержит критические баги)</u></summary>
    <ul>
    <li>функция  <b>fill_gaps_array</b> вынесена в основной  <b>__init__.py</b></li>
<li>(допущена ошибка в реализации) в расчете пользовательских сессий вернулись к определению регионов МО и ЛО по городу</li>
<li>в  <b>ElasticityModel</b> добавлен параметр, позволяющий выкидывать точки, в которых конверсия больше 1 (по-умолчанию он включен)</li>
<li>поездки больше не фильтруются по  <b>fraud_order_flg</b> (ни в когортах, ни в часовых точках)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.33</u></summary>
    <ul>
    <li>по техническим причинам все еще не в релизе модуль  <b>train</b></li>
<li>в  <b>CohortModel</b> добавлен новый параметр - аномальная сезонность, которая выбрасывается из данных, но не применяется обратно</li>
<li>в  <b>plot</b> добавлен новый метод, позволяющий строить несколько DataFrame-like объектов на одном графике, передавая их вид через параметры</li>
<li>(исправлен баг версии 1.2.31) фича с фильтрацией данных через  <b>read_parameter</b> теперь работает</li>
<li>добавлен модуль  <b>planning</b> , позволяющий планировать поездки и новичков с учетом баланса</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.32</u></summary>
    <ul>
    <li>по техническим причинам все еще не в релизе модуль  <b>train</b></li>
<li>параметры  <b>from_date</b> и  <b>to_date</b> поменяли свой вид, теперь в них передается не дата, а количество дней</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.31</u></summary>
    <ul>
    <li>проведен рефакторинг расчета когорт, исправили баг в расчете user_sessions, из-за которого терялись первые поездки и сессии от этих поездок</li>
<li>добавили в объект  <b>user_phone_id_mapping</b> приложение, к которому относится указанный <b>user_id</b></li>
<li>(фича не работает) добавлена возможность фильтрации данных внутри запроса в функции  <b>read_parameter</b></li>
<li>в расчеты добавили возможность считать когорты по отдельным приложениям</li>
<li>убрали из функции  <b>retention_new_values</b> параметр  <b>limit_extreme</b> , обрезающий ретеншен, и вынесли его в NonLinearModel, где он сразу все обрезает (стало более прозрачно), параметр был переименован на  <b>global_limit_extreme</b></li>
<li>вернули расчет регионов МО и ЛО по-умолчанию</li>
<li>добавили данные для восстановления исторических провалов <b>SH</b> с учетом убера</li>
<li>(по техническим причинам не вошел в релиз) добавили модуль  <b>train</b> , позволяющий перебирать параметры моделей</li>
<li>в  <b>Score</b> добавлено ограничение на количество процессов (при параллельном вычислении)</li>
<li>теперь часовые данные по <b>SH</b> рассчитываются инкрементально (управлять этим можно через параметры  <b>from_date</b> и  <b>to_date</b> )</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.30</u></summary>
    <ul>
    <li>параметры  <b>script_contains</b> и  <b>force_scale_free</b> можно передавать в  runner.recount_all() без указания  <b>sub_path</b></li>
<li>(исправлен баг) больше история значений параметра не затирается, если попробовать передать пустой <b>DataFrame</b> для записи в таблицу palnning/forecast</li>
<li>параметр  <b>newbie</b> теперь не обязательно передавать в конструктор  <b>CohortModel</b> (хотя он все еще является обязательным параметром), этот параметр теперь добавлен в  <b>forecast</b> (через конструктор все тоже работает)</li>
<li>(исправлен баг) откатили расчет пользовательских когорт от первой сессии в силу нескольких критических багов</li>
<li>в класс  <b>Timer</b> теперь можно передавать файл, в который он будет логгировать события</li>
<li>исправлено использование параметра  <b>new_user_filter</b> (отвечает за способ расчета когорт: от первой поездки или сессии), теперь он действительно влияет на расчет</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.29</u></summary>
    <ul>
    <li>(исправлен баг) поправили порядок расчета когорт, до этого  <b>driver_info</b> считалось позже, чем  <b>driver_sessions</b></li>
<li>исправлен баг версии 1.2.28 с расчетом часовых точек по <b>supply</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.28 (версия содержит критические баги)</u></summary>
    <ul>
    <li>в файле  <b>start_part.yql</b> функция  $today больше не возвращает NULL, в случае неизвестного скейла возвращает переданный на вход день</li>
<li>очередной фикс параметра  <b>date_to</b> в  <b>ElasticityModel</b> , починен баг возникающий, когда в  <b>forecast</b> не передавали ни  <b>date_to</b> , ни <b>cities</b></li>
<li>по-умолчанию уникальным идентификатором водителя стал  <b>driver_license_normalized</b></li>
<li>(баг) расчет часовых точек по <b>supply</b> перестал работать из-за несовместимости названий идентификаторов водителей</li>
<li>в  <b>NonLinearModel</b> добавлен новый параметр  <b>limit_extreme</b> , обрезающий ретеншен (по-умолчанию он 1.4), все что выше него в кривой ретеншена заменится на 1</li>
    </ul>
</details>
</br>
<details>
<summary><u>Выкачена версия  1.2.27</u></summary>
    <ul>
    <li>hourly-метрики по умолчанию считаются с декабря 2016 года</li>
<li><b>score</b> сохраняет параметры моделей, которые скорит</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.26</u></summary>
    <ul>
    <li>был пофикшен баг с неправильной передачей параметров  <b>use_timed_out_drivers</b> и  <b>driver_timed_out_days</b> . Появился баг в верси  1.2.17</li>
<li>пофикшен баг в <b>hourly_trips</b> из версии  1.2.25</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.25 (версия содержит критические баги)</u></summary>
    <ul>
    <li>В <b>accuracy.init</b> добавлена возможность выгрузить словарь с датами, для оптимального расчета точности</li>
<li>в <b>ElasticityModel</b> при указании <b>date_to</b> не срезались города, которые не существовали до date_to, они возвращались с 0 прогнозом. Теперь они не возвращаются (это критично для расчета ошибки)</li>
<li>в <b>reader</b> разрешено чтение параметров, которые не были добавлены в конфиг (вместо исключения будет warning)</li>
<li>в <b>hourly_trips</b> добавлен средний чек и средний сурж</li>
<li>(баг) расчет <b>hourly_trips</b> падает из-за <b>driver_net_income</b></li>
<li>добавлена возможность расчета когорт пользователей от первой сессии или от первого заказа</li>
<li>мультипроцессинг полностью заработал</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.24</u></summary>
    <ul>
    <li>Добавлен фикс пропущенных в истории <b>SH</b> с учетом убера</li>
<li>исправлен баг версии  1.2.23</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.23 (версия содержит критические баги)</u></summary>
    <ul>
    <li>изменилась первоначальная догадка о минимуме функции в <b>get_supply</b> (из-за перехода на часовой скейл оптимизируемая функция немного поменяла форму)</li>
<li>в модуле <b>cohort</b> изменилась обработка ретеншена, когда переданы <b>split_dimensions</b> (теперь там просто <b>T</b> вместо unstack)</li>
<li>добавлен мультипроцессинг, но он зависает при больших объемах данных</li>
<li>добавлена возможность скопировать модель (необходимость появилась в мультипроцессинге)</li>
<li>расчет когорт по регионам Москва+МО и Санкт-Петербург+ЛО стал опциональным и по умолчанию не делается</li>
<li>вернулись на <b>demand</b> означающий <b>sessions_with_wait</b></li>
<li>(баг) в этой версии случайно был заложен расчет пользовательских когорт по первой сессии</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.22</u></summary>
    <ul>
    <li>загрузки плана/прогноза/факта исправлены в соответствии с новым форматом ods/mdb/city/city</li>
<li>расчеты перешли на новый <b>dm_order_ods_based</b></li>
<li>пофикшен поиск оптимального для города баланса (на часовом скейле поменялась форма минимизируемой функции)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.21</u></summary>
    <ul>
    <li><b>sub_path</b> работает корректно для вычисления метрик (todo: но почему-то читает их неправильно)</li>
<li>разделение недели на дни индивидуально для каждого города (не потеряна совместимость со старой версией)</li>
<li>в <b>warning</b> о том, что кривая ретеншена не зафиттилась добавлено название города</li>
<li>исправлены <b>nan</b> значения в расчете info, когда не было поездок в ЯТ</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.20 (версии 18 и 19 нерабочие)</u></summary>
    <ul>
    <li><b>SH</b> убера восстанавливаем по rides, а не <b>trips</b></li>
<li>убрали странный параметр <b>scale_fun</b> из yql-запросов</li>
<li>переделали расчет часовых данных: <b>elasticity</b> обобщено до metrics, убраны костыли</li>
<li>добавлено сохранение продленного ретеншена в когортной модели</li>
<li>добавили расчет когорт, где все атрибуцируется к городу первой поездки (в этом случае нет расчета по сложным регионам)</li>
<li>добавили вычисление метрик с миграциями поездок, водителей и пользователей между городами</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.17</u></summary>
    <ul>
    <li>небольшой фикс в конфиге, чтобы часовые данные считались</li>
<li>в <b>init</b> добавила функцию, которая разбивает данные в <b>series</b> из большего скейла в меньший в некоторой пропорции (например, из недель в дни): называется  <b>split_scale</b></li>
<li>в эластичности появились методы, которые отдают конверсию в балансе и восстанавливают <b>supply</b> из <b>demand</b> и <b>trips</b></li>
<li>убрала суммирование регионов мск+МО и спб+ЛО в <b>_total_</b> в нашем отчете</li>
<li>избавилась от грязного хака в сессиях для поиска этих регионов, теперь они берутся из <b>last_attr_regions</b></li>
<li>добавила в когорты вариант расчета когорт, когда все относится к городу первой поездки</li>
<li>когорты теперь можно считать по произвольному полю: ну то есть можно вместо <b>user_phone</b> в конфиге подставить user_phone_id, например (комменты забыла в этом месте добавить)</li>
    </ul>
</details>
</details>

