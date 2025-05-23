# Инфра кросс валидации прогноза

## Концепция

Собираем в едином месте в аркадии построение датасета и кросс валидацию,
чтобы запуском одной команды получать полный и воспроизводимый результат проверки гипотезы в прогнозе.

## Основы

* msku — она же market_sku, единое обозначение для карточки товара на маркете,
   в отличие от ssku не завязана на поставщика. Прогноз должен происходить на уровне msku
* date — дата факта, единое обозначение для даты в которое произошло то или иное событие или агрегированый факт,
  например, количество продаж, или средняя выставленная цена
* forecast_date — дата составления прогноза, может быть явно использована для таких фактов как корзины на
  момент составления прогноза, или ценовые стратегии на момент составления прогноза. forecast_date > date
* таргет/target — датасет, содержащий ключ (может варьироваться от реализации) и значение предсказуемой метрики.
К таргету джоинятся все фичи лефт джоином.
* фича/feature — датасет, содержащий подмножество ключей таргета и значение (или несколько) какого то признака.
* таска — реализация интерфейса market.monetize.stapler.v1.tasks.task.Task которая транслируется степлером в кубик нирваны. Может содержать как произвольный python код, так и nile/spark/yql/chyt код.
* степлер — фреймворк для построения графов в нирване, на основе аркадийного кода подробнее https://wiki.yandex-team.ru/users/arakhmatulin/sozdanie-grafov-s-pomoshhju-monetizationutils/

## Основные таски и объекты

* BuildReplenishmentMskusYqlTask — таска с фильтрацией на ассортимент, например только ассортимент под репленишментом или ассортимент конкретного КМ для ускорения. Чтобы уменьшить ассортимент до конкретного КМ, нужно добавить фильтр в yql-запрос.
* BuildMskuDataTask — таска, формирующая таблицу, где для каждой скю таймлайн событий/фактов по дням. Ключом является msku, date примером факта может быть количество продаж в этот день (sales) или средняя цена продажи в этот день (price). Служит для построения таргетов и фичей-счетчиков.
* Build*FeatureTask — таска, формирующая таблицу, содержащую конкретную фичу. Критически важно чтобы все ичи имели строгую схему и были сортированы в порядке msku, forecast_date. Это позволит при сборке датасета задействовать мерж джоин.

* BuildTargetTask — пример таски, формирующий таргет
* BuildDatasetYqlTask — таска джоинящая все фичи в датасет.

* Model — интерфейс, который необходимо реализовать для валидации моделей
* ModelTrainTaskFabric — фабрика, на основе инстанса BaseCatboostModel генерирующая таску обучения
* ModelCrossValTaskFabric — фабрика, на основе инстанса BaseCatboostModel генерирующая таску валидации


## Предусмотреные сценарии

### Добавление фичи
Для добавления фичи необходимо реализовать таск сборки этой фичи.
Для этого необходимо
1. За основу можно брать `dummy_feature_task.py`. Эта таска, как и остальные таски в этом проекте, наследуются от
   `ForecastTask`. Это наша надстройка над степлеровксим `Task`, которая содержит функционал для тестирования результата
   работы таски. А именно — после исполнения основного кода таски вызываются тесты, проверяющие получившуюся таблицу на
   наличие дубликатов по ключу и на ошибки в построении фичи (таска фейлится, если весь столбец с фичей имеет одно
   константное значение). Если вы пишете таску на yql, то можно отнаследоваться от [`YqlSyncTask`](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/task/tasks.py?rev=r8601207#L13).
   Этот класс содержит метод для исполнения yql-запроса. Сейчас эта таска не наследуется от ForecastTask, это надо
   исправить, сделав `class YqlSyncTask(ForecastTask, YqlTask)`. Если видите, что какая-то таска не наследуется от
   ForecastTask, то просьба это поправить.
1. Создать файл для своей фичи в каталоге `lib/data_preparation`, например my_new_feature_task.py
1. Добавить упоминание созданного файла в `lib/ya.make`
1. Результат работы должен сохраняться на yt в self.result_path
1. Таска должна быть параметризуемой по start_date и today (end_date). Это нужно для того, чтобы мы могли как выбирать
   произвольный интервал данных для формирования трейн выборки, так и использовать тот же самый код для построения фичей
   во время инференса, передавая в качестве границ вчерашнюю и сегодняшнюю дату.
1. Внутри таски нужно будет ходить в какие-то таблицы, из которых будут строится фичи. Это удобнее всего делать через
   фреймворк [datasources](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/datasources/?rev=r8605806).
   Для него есть отдельная [документация](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/datasources/readme.md?rev=r8600145),
   в которой написано, как им пользоваться. Также примеры использования всегда можно подсмотреть в коде других тасок.
1. Таска должна учитывать внутри своей логики лаг, с которым мы во время инференса получаем данные из табличек,
   используемых при формировании фичей. То есть если читать таблицы по передаваемым в качестве аргументов таски датам в
   чистом виде, то при инференсе в проде мы рискуем попасть в следующую ситуацию. Мы пытаемся считать таблицу за сегодня,
   но ее еще не успели доставить, тогда мы ничего не прочитаем, а в `build_dataset_yql_task.py` приджоинимся и получим
   NULL'ы. Для того, чтобы учесть лаг, можно взять константу `FEATURE_LAG` из `constants.py` и перед тем как посчитать, какой
   диапазон таблиц мы хотим прочитать, сдвинуть все даты на `FEATURE_LAG` дней. После всей обработки перед записью
   результата результата таски в таблицу нужно будет сдвинуть все даты вперед на `FEATURE_LAG` дней, чтобы вернуться к
   исходным датам.
1. Если таска считает какую-либо оконную статистику, и ей для каждой строчки нужны данные за N дней назад, то необходимо
   учесть это внутри логики таски, сдвигая start_date на N дней назад, а на выходе фильтровать все строки до start_date,
   если это потребуется.
1. Не забыть поджоиниться с sku_transitions, чтобы учесть маппинги id msku. Для найл и спарк кода есть
   [вспомогательные функции](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/data_preparation/mappings_msku.py)
1. Результат работы должен быть строго схематизирован
1. Результат работы должен быть сортирован по msku, forecast_date
1. В `algorithms/lib/cli.py` необходимо создать инстанс объекта-таски,
   например, myNewFeatureTask = MyNewFeatureTask() так же полученный инстанс необходимо
   добавить в конструктор `cli = TasksCli(myNewFeatureTask, ...)`
1. Необходимо локально отладить таску. Для этого можно запустить `bin/calculator/run.sh MyNewFeatureTask`
   эта команда построит проект и выполнит только указанную таску на локальной машине. В качестве альтернативного способа
   можно переопределить define_graph в graph.py и запустить расчет с необходимым подмножеством кубиков графа.
   Для спарк тасок годится только альтернативный способ запуска.
   Запуск спарк таски через `bin/calculator/run.sh MyNewFeatureTask` не работает.
1. В случае успеха локальной отладки необходимо добавить таску/фичу в граф и датасет
1. Для добавления в граф необходимо в `lib/graph.py` в `_create_features` добавить вызов,
   например
   ```python
    self._add_feature(
        task=cli.buildCountersFeaturesTask,
        today=today,
        start_date=start_date,
        msku_data_path=msku_data_path,
        result_path=result_dir + 'f_counters'
    )
   ```
   На момент написания доки функция выглядит [следующим образом](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/graph.py?rev=r8606705#L407)
1. Для добавления новой таски с фичей в датасет больше ничего делать не нужно, _add_feature добавляет таску в список таблиц,
   которые нужно поджоинить в конце в `build_dataset_yql_task.py`
1. Для финальной кросс валидации необходимо запустить
   ```bash
   sh run.sh --command validate
   ```
   (см. код define_graph, там должен вызваться метод define_validation_graph).
   Эта команда создаст граф с построением всего датасета и новой фичи,
   а так же с кросс валидацией модели и выводом основных метрик.
   Есть некоторые опциональные команды, с которыми можно запускать `run.sh`, о них поговорим ниже.

### Опциональные аргументы `run.sh`
1. `--cache_uuid`, указав сюда непустую строку, можно задать имя поддиректории, в которую граф будет записывать таблицы.
   Например, в `validate` графе в `dev` режиме по-умолчанию весь результат будет записан в вашу домашнюю директорию в
   поддирекотрию с таймстемпом запуска.
   То есть при запуске
   ```bash
   sh run.sh --command validate --mode dev
   ```
   все таблицы с фичами будут записаны в корень в `/path/to/your/home/directory/timestamp/...`.
   Если же мы запустим следующим образом:
      ```bash
   sh run.sh --command validate --mode dev --cache_uuid new_feature_experiment
   ```
   то результат запишется в `/path/to/your/home/directory/new_feature_experiment/...`.
1. `--dataset_path`, передав сюда путь до существующего датасета на YT, мы сможем запустить расчет, не пересобирая
   датасет с нуля, а взяв существующий.
1. `--target` на каком таргете мы хотим учить модель. Возможные варианты:
    * `target` - наш самый первый таргет, суммарные продажи за 7 дней вперед. Сейчас используется для обучения моделей под прод.
    * `dn_target` - подневные продажи на n-ый день относительно сегодняшнего дня.
    * `dn_avg_target` - средние дневные продажи за n дней относительно сегодняшнего дня.
    * `d7_avg_target` - средние дневные продажи за 7 дней относительно сегодняшнего дня.
    Планируем в ближайшее время переходить с `target` на `dn_target`, чтобы прогнозировать спрос подневно.

1. `--infer_train` указав этот аргумент в train режиме, можно получить предикты модели на всем датасете. Бывает полезно,
   когда нужно посмотреть предикты модели на каких-то кейсах из прошлого.

1. `--today_date` в этот аргумент можно передать дату для predict графа.

### Подбор гиперпараметров
Для промера гиперпараметра предлагается создать инстанс BaseCatboostModel.

1. Чтобы промерить полезность фичи, необходимо создать модель, включив новые фичи в список фичей.
   Для этого необходимо в файле lib/data_preparation/catboost_model.py создать инстанс `BaseCatboostModel` с нужными
   аргументами. Есть несколько вариантов, как это сделать, об этом написано в следующей секции "Варианты сборки моделей"
1. Для финальной кросс-валидации необходимо запустить "./run.sh --command validate".
   Эта команда создаст граф с построением всего датасета и новой фичи, а так же с кросс валидацией
   перечисленных моделей.
1. В качестве бейзлайна можно брать текущие продовые модели из `cli.py`, они находятся в переменных `train_mean_model` и
    `train_q95_model`. Также всегда хорошо добавить модель среднего в валидацию.
1. Смотрим метрики. Для модели прогноза среднего спроса (при таргете `target`) смотрим WAPE и BIAS. Смотрим, чтобы средний абсолютный bias
   на CV не превышает 0.1. Эта комбинация метрик хорошо отражается с помощью метрики `value`, которая является комбинацией
   wape и bias. `value = wape + 0.15*(abs_bias)`, `abs_bias` - это средний абсолютный bias по фолдам. Для `q95` модели
   смотрим wape95. При переходе на подневные таргеты (`dn_target`) для модели среднего договорились смотреть уже не wape,
   а подневный rmse.
1. Если кросс-валидация проводится по существующему набору фичей, то свежий датасет можно взять [отсюда](//home/market/development/replenishment/demand_ml_forecast/cached_datasets/)

### Показываем результаты кросс-валидации
Сейчас есть два способа:
1. [Юпитер ноутбук](https://a.yandex-team.ru/arc/trunk/arcadia/junk/yurytrubitsyn/easy_cross_val_report.ipynb)
2. [YQL запрос cross_val.sql](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/data_preparation/sql/cross_val.sql),
  [пример работы YQL](https://yql.yandex-team.ru/Operations/YUG8HpfFtwh1p-ZustxvvuPjAnMQATBZsU8SYgCayZs=),

Берем, какой кажется удобнее, общей рекомендации тут нет.

### Варианты сборки моделей
* (удобный вариант) сгенерировать комбинации для перебора параметров с помощью [ModelsFromComponents](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/data_preparation/train_model_task.py?rev=r8606705#L654).
 Пример можно подсмотреть [здесь](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/cli.py?rev=r8601459#L214)
* (удобный вариант) сгенерировать комбинации для перебора параметров с помощью [GridParamsModels](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/data_preparation/train_model_task.py?rev=r8606705#L681)
* использовать [GetNamedModel](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/data_preparation/train_model_task.py?rev=r8606705#L595),
передав туда строковые имена аргументов, которые прописываются в [hyperparameters.py](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/lib/data_preparation/hyperparameters.py)
* напрямую собрать модель из `BaseCatboostModel` и обернуть ее в `ModelCrossValTaskFabric`

### Подготовка ПР
1. Для ПР нужно посчитать графы с `--command validate` и `--command predict`. Если ПР затрагивает инфру помимо самой таски,
   то `--command train` тоже стоит проверить. В скором времени мы объединим режимы train и validate, и для них будет один общий граф.
   Дальше нужно убедиться, что новая фича
   собирается корректно в обоих графах. `--command predict` мы здесь вызываем, чтобы проверить, что во время предикта
   фича будет собираться корректно с учетом указанного временного лага (таблица с данными успела доехать, и фичи посчитались).
1. В описании ПР нужно приложить графы исполнения и результаты кросс-валидации. Вообще любая доп информация, приложенная в описании упростит ревью ПР.
   Это могут быть как просто какие-то комментарии, так и ссылки на yql-запросы, например.
1. Сам ПР в названии должен содержать тикет с таской, в рамках которой фича делается. Пример: `REPLENISHMENT-1111, новые фичи продаж`.
   Коммиты внутри ПР тоже должны содержать название тикета, чтобы потом было легко отследить историю изменений кода.
   Перед ребейзом можно сквошнуть все свои коммиты в ветке в один, чтобы разрешать все конфликты в одну итерацию.
   Команда для сквоша есть [здесь](https://wiki.yandex-team.ru/arcadia/arc/faq/#eslijadelajuneskolkokommitovvodinyaprapotomxochufinalnujuversijuvtrankvkommititkakmneposkvoshitmoikommityvodinilijetoavtomaticheskiproizojjdjotkogdajavarkanumenazhmumerge).
1. Если ПР затрагивает какие-либо существующие таски, то нужно об этом указать в описании + дополнительно уведомить
   всех, кто участвует в разработке этой модели, чтобы при ребейзе на транк ни у кого не сломался код, который не ожидает
   изменений в уже существующих тасках. Автору ПР (исполнителю задачи) обязательно нужно указать изменения в описании ПР,
   а на дежурном лежит обязанность проконтролировать, что об этих изменениях узнали остальные разработчики
   (тегнуть в чате или рассказать на стендапе).
1. (если произошла ситуация из предыдущего пункта) Автору ПР стоит посмотреть существующие модели, которые собираются
   при кросс-валидации в транке, и удалить модели, которые перестают быть валидными с этим ПР. Например, убрали какую-то
   фичу/набор фичей => нужно почистить ее из списка колонок в `hyperparameters.py` и удалить модели, которые ее используют.
1. Обновить эту документацию в этом же ПР, если вносится какой-то новый функционал. Это должен сделать автор ПР, а
   ревьюер должен убедиться, что изменения в доке отображены.
1. (Рекомендация) Разделять ПР с фичами и инфровые ПР. Так меньше конфликтов, меньше общий размер ПР, быстрее проходит ревью, и код
скроее окажется в транке (что уменьшает вероятность того, что придется еще раз ребейзить). Чем меньше размер ПР, тем лучше.
1. Лучшие модели, которые получились во время кросс-валидации с новой фичей лучше заносить вместе с ПР. При новом релизе
   старые модели надо чистить.

### При релизе
1. Если за неделю смерджилось больше одного ПР, то дежурному нужно провести кросс-валидацию с учетом всех новых добавленных фичей и
   лучших моделей-кандидатов, чтобы определить нового кандидата на релиз. Если был всего один ПР с фичей и новым кандидатом,
   то можно кросс-валидацию не перегонять, а зарелизить его.
1. Положить нового лучшего кандидата в `train_mean_model` и `train_q95_model` в `cli.py`.
1. Запустить релиз.

### Этапы релиза
Релиз состоит из нескольких этапов:
* Трейн-граф модели. В нем собирается датасет, учатся модели среднего и q95 и складываются на YT.
* Проверка успешности трейн-графа (что ничего не упало). Этот блок имеет таймаут 3 часа, и поскольку трейн граф бежит
  дольше, то вы увидите Failure на релизе. Здесь надо просто рестартануть блок проверки.
* Тестовый-граф предикта. В нем читаются модели, формируется датасет за день перидикта, а дальше предикты
складываются в таблички на YT.
* Проверка успешности тестового графа предикта (аналогично трейну)
* Гендальф (ручной триггер). Нужен, чтобы посмотреть модель глазами, убедиться, что с ней все ок, и пустить ее на
следующий этап
* Поставка модели на препрод. Здесь модель будет стоять неделю перед раскаткой на прод. То есть второй гендальф мы
отжимаем перед релизом на следующей неделе.
* Гендальф (ручной триггер)
* Перестановка ссылок на модель, чтобы препрод модель уже смотрела на прод (+ проверка успешности)
* Поставка модели на прод
[Исходник](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_ml_forecast_validation/a.yaml) с описанием этапов релиза.
В будущем блок с переназначением ссылок с препрода на прод можно будет убрать, передавая через CLI тег ревизии,
и именуя модели через этот тег.

### Отслеживание релиза
1. В трейн графе в кубике обучения модели в stderr пишется лог с подневными метриками модели. WAPE, BIAS, суммарный предикт.
    Нужно убедиться, что значения метрик являются ожидаемыми в сравнении с результатами на кросс-валидации + посмотреть
   подневную сумму предсказаний и сравнить ее с фактом. Если она проседает больше, чем на 10-15%, то проверить, все ли верно
 посмтроилось
1. В тест-графе предикта смотрим подневную сумму предсказаний в табличке с результатом, и сравниваем ее с предсказаниями
 прод модели. Сейчас прод модель предиктит порядка 280к-290к суммарных продаж на каждый день.
1. Если с предыдущими пунктами все ок, то отжимаем гендальфа и смотрим, как модель работает на препроде. Отслеживать ее можно
 с помощью [дешборда](https://datalens.yandex-team.ru/ihjv425ii0xyb-replenishment-dashboard?tab=7aG)
1. На дешборде в меню `Прогноз` выбираем модели `прод` и `новый`. И смотрим недельный wape, если неделя прошла. Если
   хотим посмотреть метрики раньше, чем через неделю, то смотрим подневный wape. Если в день принятия решения о релизе
   на прод новая модель показывает лучший wape, то раскатываем новую модель на прод, отжимая второго Гендальфа.

### Если что-то в релизе идет не по плану
1. Проверяем лог метрик трейн-графа, возможно, там пропустили проблему.
1. Скачиваем пикл модели, смотрим ее параметры. Сверяем, что модель содержит ожидаемые параметры, которые предусматривались при релизе.
1. Смотрим трейн датасет, количество записей в нем, количество msku в msku_delivery_options, статистики таргета и фичей.

### Если что-то в проде/препроде идет не по плану
1. Проверяем пункты из релиза
1. Проверяем предикт датасет. Нет ли там фичей, которые не построились, из-за того что там не доехали таблицы источники.
   Если, например, какие-то фичи забыли отнаследовать от ForecastTask, то тесты не поймали этого. Смотрим еще,
   фильтруются ли даты в таблице с фичей, чтобы таблица содержала только один день. Потому что в проотивном случае,
   если там будет несколько дней, то тесты фичей не отловят проблемы.
1. Если все фичи доехали, то нет ли проблемы, что они заполнились не как на трейне. Строим трейн датасет, включая в него
   интересующую дату. Сравниваем распределение фичей на трейне и на предикте.

### Продвинутые техники

Ничего не запрещает для ускорения личной работы модифицировать граф генератор
algorithms/lib/graph.py define_validation_graph

Примеры полезных модификаций:
1. Замена уже собранных датасетов на константные пути
1. Джоин новой фичи к существюущему датасету
1. Кросс валидация сразу нескольких моделей с созданием в цикле для прохода сетки
