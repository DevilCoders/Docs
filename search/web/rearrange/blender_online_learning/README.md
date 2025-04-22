# Общее описание
Переранжирование предназначено для онлайн обучения и применения блендерных моделей. Помимо переранжирования в состав решения входят rtmr процесс и sandbox шедулер.
Общее описание решения можно найти в [этом посте](https://clubs.at.yandex-team.ru/blender/190). Текущее решение отличается от описанного тем, что появилась возможность использовать для доставки данных механизм fast_data и соответственно не просаживать время работы поиска.
# Компоненты
### Noapache
Переранжирование в noapache выполняет две основные задачи:
* запись в логи данных для обучения
* применение моделей

Модели вычисляются непосредственно в переранжировании, для взаимодейcтвия с блендером используется метод SetIntentPosition с повышенным (относительно обычных моделей) приоритетом, поэтому в ApplyBlender.fmls никакой информации про онлайн модели нет. Также с этим связана необходимость аккуратно настраивать параметры, подробности см. в пункте **Примеры использования**    

Для доставки моделей до noapache может использоваться один из двух механизмов:
* rtmr - непосредственный запрос данных из rtmr таблички, не может быть использован в продакшене, т.к. просаживает время работы поиска, однако гарантирует минимальную задержку
* fast_data - быстрая папка под noapache, [документация](https://wiki.yandex-team.ru/users/dima-zakharov/upper-fast-data/), [директория с онлайн моделями](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast/blender_online_learning)

 
### RTMR
На RTMR запущен процесс состоящий из двух операций: 
* session_parser - строит пулы из user_sessions
* trainer - обучает модели

Исходники процесса лежат [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/rtmapreduce/mrtasks/blender_online_learning), конфиги - [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/rtmapreduce/config/user_tasks/blender_online_learning.py) 
Вот [так](https://rtmr.yandex-team.ru/production/processing/tasks/blender_online_learning/overview) можно понаблюдать за процессом через веб-интерфейс RTMR.

Две полезные тулзы:
* [offline_emulator](https://a.yandex-team.ru/arc/trunk/arcadia/yweb/blender/online_learning/bin/offline_emulator) - позволяет выполнять тот же код, что работает в RTMR поверх YT табличек, подробнее читай в разделе "Обучение"
* [rtmr_helper](https://a.yandex-team.ru/arc/trunk/arcadia/yweb/blender/online_learning/bin/rtmr_helper) - ручная работа с RTMR: получить метрики/модели по ключу, перегнать их из protobuf в json

В rtmr существует ограничение на размер стейта - 16Мб, [дока](https://wiki.yandex-team.ru/rtmapreduce/FAQ/#qestliogranichenienarazmerzapisejj). Про это нужно помнить при настройке параметров обучения, в стейте сейчас лежат две модели (последняя и лучшая) и батч. 

### Sandbox
Sandbox используется для периодического обновления моделей в fast_data, реализовано две компоненты:
* задача [UPDATE_BLENDER_ONLINE_MODELS](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/blender/update_blender_online_models) - достает модельки из rtmr, обновляет ya.make для fast_data, прогоняет тесты и делает коммит
* [шедулер](https://sandbox.yandex-team.ru/scheduler/11169/view) - выполняет периодический запуск задачи, раз в 30 минут 

Модели для fast_data должны быть зарегистрированы в [model_list.txt](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast/blender_online_learning/proto_models/model_list.txt). Логика обновления такая: 
* если модель не удается выкачать из RTMR, то берем предыдущую версию модельки (тем самым обрабатываем случай, когда модели больше не учатся, но применяются)
* если предыдущей версии нет, скипаем модель (это на случай начала обучения, когда модельки еще нет в RTMR)

# Схема данных
### Имя модели
Имя модели является важнейшим идентификатором для системы. Оно используется для матчинга конфигов обучения и применения 
на верхнем, выступает в качестве ключа в RTMR процессах, используется в качестве имени файла модели в fast_data. 
В настоящий момент генерация имени модели и обеспечение его уникальности находится в зоне ответственности пользователя.

### Формат модели
Для представления моделей (а также всех остальных объектов, которые обрабатываются в RTMR) используется protobuf, описание лежит [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/kernel/blender/online_learning/protos).

# Конфиги  
Для полного определения новой модели необходимо заполнить две секции конфига TrainModels и ApplyModels. Это словари: ключ - имя модели, значение - типизированная схема [TTrainModelParams](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/blender_online_learning/scheme/scheme.sc?rev=3883190#L15) или [TApplyModelParams](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/blender_online_learning/scheme/scheme.sc?rev=3883190#L35) соответственно.
В случае использования fast_data в качестве источника модели нужно дополнительно зарегистрировать модель в файле [model_list.txt](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast/blender_online_learning/proto_models/model_list.txt).

### Параметры обучения модели
Пример конфига:
*{"Intent": "NEWS_WIZARD", "FeatureSources": ["dssm_query_bigram", "dssm_serp_bigram", "constant"], "BatchSize": 30, "LearningRate": 0.1, "ClassNumber":11, "FeatureCount": 601, "EvaluateWindowSize": 300}*

Пояснение к параметрам:
* BatchSize - размер батча
* LearningRate - learning rate
* FeatureSources - какие эмбеддинги использовать при обучении, результирующий вектор получается конкатенацией эмбеддингов, **важно** всегда добавляйте constant в FeatureSources, в модельке отдельно не реализован bias, поэтому его нужно добавлять руками  
* FeatureCount - число факторов, используется для валидации (можно вычислять автоматически, но для этого нужно иметь информацию о размерности эмбеддингов, которой пока в явном виде в noapache нет)
* ClassNumber - число классов для задачи мультиклассифакации, равно числу позиций показа плюс непоказ, если хочется обучать модель для показа только в топ X, здесь нужно указать X + 1, последний класс всегда интепретируется как непоказ
* EvaluateWindowSize - размер окна (в запросах), по которому будут считаться метрики в процессе обучения

Дополнительно могут быть определены:
* Locales - ограничить поток срабатывания модели заданным списком локалей ([relev_locale](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/getrelevancelocale/))
* UserInterfaces - ограничить поток срабатывания модели заданным списком пользовательских интерфейсов (типы определены в рамках переранжирования)
* ModelType - тип модели для обучения, детали читай ниже
* ClickBoost - применить кликбуст при расчете таргета
* SurplusVersion - использовать версионнированный профицит для обучения модели, по умолчанию используется профицит v1 (aka старый профицит)
* UseLocalRandom - обучаться поверх сторонних сборов (см. пример ниже)
* RegValue - коэффициент при регуляризирующем слагаемом в фунцкии потерь (используется L2 регуляризация) 
* ModelVersion - версия модели, по умолчанию 0, можно делать инкремент, тогда текущий стейт в rtmr сбросится и обучение модели начнется снова

Параметры можно менять, при этом произойдет один из двух вариантов:
* параметр просто применится и обучение модели продолжится
* текущее обучение сбросится, моделька переинициализируется и обучение начнется с нуля, такой поведение происходит, например, при изменении числа классов или состава/количества фичей, полностью логика применения данного сценария приведена [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/yweb/blender/online_learning/lib/rt_trainer.cpp?rev=6661839#L253)

### Параметры применения модели
Пример конфига:
*{"Intent": "NEWS_WIZARD", "RandomizeParams":{"RandomizeBundle": "positional_local_random_hard", "MinRandomProb": 0.05, "RandomProbA": 20., "RandomProbFunc": "sqrt", "FixedPos": 2, "FixedPosReqCount": 1000, "FullRandomReqCount": 10000}, "FallBackBlenderPos": 2, "ModelSource": "fast_data"}* 

Пояснения к параметрам:
* ModelSource - источник модели: rtmr (default value), fast_data или doc_attr (достать модель из аттрибута документа)
* FallBackBlenderPos - какую позицию стоит выставить, в случае если модель не нашлась
* RandomizeParams - параметры рандомизации (aka exploration)

Дополнительно могут быть определены:
* UserInterfaces, Locales - аналогично ограничениям в параметрах обучения, только используются на этапе применения модели
* ApplyCondition - условие примение модели: всегда (always), только при наличии интента в блендере (has_intent), только при наличии документа по интенту (has_doc, default value)
* ApplyPriority - приоритет для выставления позиции в блендер (метод блендера SetIntentPosition)

Для exploration реализована простейшая схема, которая состоит в том, чтобы с вероятностью, 
зависящей от числа обработанных запросов, выполнить рандомизацию на запросе с использованием одного из стандартных блендерных бандлов.
Параметры рандомизации:
* RandomizeBundle - тип бандла используемого для рандомизации
* FullRandomReqCount - число запросов, до достижения которого, рандомизация будет выполняться безусловно
* RandomProbA, RandomProbB, RandomProbFunc - параметры функции оценки вероятности рандома, функция имеет вид ```RandomProbA / (1. + params.RandomProbB * RandomProbFunc(request_count))```,  пример эвристики: ```20 / 1. + sqrt(request_count)``` (вероятность на 100 запросах - 1.0, на 1000 - 0.6, на 10000 - 0.2, на 30000 - 0.11, на 100000 - 0.06)
* MinRandomProb - минимальное значение вероятности рандома
* FixedPosReqCount, FixedPos - до достижения числа запросов FixedPosReqCount использовать в качестве предикта FixedPos (может применяться в качестве средства повышения аггрессивности рандома) 
* RandomSaltMinutes - период смены соли в минутах (по умолчанию - 30 минут)

**Обратите внимание**, для того чтобы модель обучалась, необходимо указать либо RandomizeParams в настройках применения модели, 
либо UseLocalRandom в настройках обучения, в противном случае в логах не появится записей, используемых при обучении.

### Регистрация модели в fast_data
Для использования fast_data в качестве источника модель нужно добавить в файл [model_list.txt](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast/blender_online_learning/proto_models/model_list.txt).
Это сделает ее видимой для sandbox-шедулера, который раз в полчаса обновляет модели в fast_data.


# Примеры использования
#### Стандартный вариант (exploitation + exploration + fast_data)
Обучение: *scheme_Local/BlenderOnlineLearning/TrainModels/news_tr_touch_b30_lr01={"Intent": "NEWS_WIZARD", "FeatureSources": ["dssm_query_bigram", "dssm_serp_bigram", "constant"], "BatchSize": 30, "LearningRate": 0.1, "ClassNumber":11, "FeatureCount": 601, "EvaluateWindowSize": 300}*

Применение: *scheme_Local/BlenderOnlineLearning/ApplyModels/news_tr_touch_b30_lr01={"Intent": "NEWS_WIZARD", "RandomizeParams":{"RandomizeBundle": "positional_local_random_hard", "MinRandomProb": 0.05, "RandomProbA": 20., "RandomProbFunc": "sqrt", "FixedPos": 2, "FixedPosReqCount": 1000, "FullRandomReqCount": 10000}, "FallBackBlenderPos": 2, "ModelSource": "fast_data"}* 

Регистрация: в model_list.txt дописываем *news_tr_touch_b30_lr01*.

#### Использование RTMR в качестве источника данных
В секции ApplyModels нужно указать *"ModelSource": "rtmr"*, регистрировать модель в fast_data не нужно.


#### Обучение модели поверх сторонних сборов
В секции ApplyModels не указываем RandomizeParams, в секции TrainModels указываем  *"UseLocalRandom" : 1*.

#### Применение модели без обучения
Необходимо использовать только секцию ApplyModels, RandomizeParams указывать не надо. Для применения этого варианта модель должна быть не только зарегистрирована в model_lists.txt, но и существовать в fast_data, т.к. не обновляемые (не обучаемые) модели удаляются из rtmr в соответствии с [настройками](https://a.yandex-team.ru/arc/trunk/arcadia/rtmapreduce/config/user_tasks/blender_online_learning.py) времени жизни   

#### Дополнительные параметры критичные для работоспособности схемы
**Наличие блендерной модели**

Для того, чтобы заработала блендерная рандомизация, обязательно наличие какой-либо модели для интента, она может быть установлена так: 
*&rearr=scheme_Local/BlenderFmls/FmlConfig/images/universe/\"1\"/\"10000\"/fml=pos_always_five*
Или в некоторых сложных случаях (когда в Vertical установлен фиксрованный вес интента или позиция) так:
*&rearr=scheme_blender/fml/WIZMEDCONSULT={name:always_zero,update:1}*
Предикт формулы не влияет только на оценку текущего продакшена в метриках по скользящему окну, опорная позиция для рандомизации определяется по предикту онлайн формулы, т.к. переранжирование передает ее в блендер с большим приоритетом, чем у стандартных формул.

#### Миниблендер
Для взаимодействия с миниблендером (источник fastres2) была реализована возможность задавать настройки обучения и применения моделей в EasyBlend. Для этого используются методы блендера SetFastModelToTrain и SetFastModelToApply.
Чтобы включить онлайн обучение, необходимо в vertical_settings на стороне бэкенда миниблендера настроить узлы FastModelsToApply и FastModelsToTrain. Обязательно указать IntentWeightFml (произвольную формулу заглушку) и удалить узлы Pos и IntentWeight.
Также необходимо отключить интентный фильтр: *"system": {"intent_filter": 0}*
Пример полного конфига: https://paste.yandex-team.ru/1000344/text

# Отладка и мониторинги
#### Кука релевантности
В куку дампится некоторая отладочная и служебная информация. Применение модели выглядит так: https://nda.ya.ru/3UWDGW. 
В случае срабатывания рандомизации или использования внешнего рандома в search_props дампится запись BlenderOnlineLearning.request_data, которая используется для построения пулов в rtmr процессе. Выглядит это так: https://nda.ya.ru/3UWDGY
Под флагом *rearr=BlenderOnlineLearning_dbg* можно увидеть human-readable представление request_data, а так же некоторую дополнительную отладочную информацию в куке и в eventlog. 

#### Онлайн оценка качества
В процессе обучения модели на rtmr также считаются метрики качества по скользящему окну (размера EvaluationWindowSize). Метрики прямо из rtmr процесс пишутся в соломон: https://solomon.yandex-team.ru/?project=blender&cluster=production&service=rtmr_online_learning
# Обучение
### Типы моделей
Доступные типы моделей перечислены [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/kernel/blender/online_learning/model/model_type.h). 
На 2020/04/15 доступны следующие типы моделей:
* linear_softmax - полная поддержка, модель описана [здесь](https://clubs.at.yandex-team.ru/blender/190)
* linear_winloss_bin - частичная поддержка (реализовано обучение в rtmr, но не реализовано применение в noapache), модель представляет собой набор бинарных классификаторов для каждого класса показа, классификация "положительный профицит против отрицательного"
* linear_winloss_mc - частичная поддержка (реализовано обучение в rtmr, но не реализовано применени в noapache), реализация текущего продакшен подхода к обучению больших блендерных моделей, детали [тут](https://clubs.at.yandex-team.ru/blender/139)

### Оффлайн эксперименты
С помощью программы [offline_emulator](https://a.yandex-team.ru/arc/trunk/arcadia/yweb/blender/online_learning/bin/offline_emulator) можно ставить оффлайн эксперименты по обучению моделек.
Так можно собрать пул для обучения: *./offline_emulator collect_pool -d 20200201 -p //home/blender/orepin/online_learning/pool -b ~/data/blockstat.dict*
В пул попадут записи для всех моделей, которые обучались в заданный период времени.
Поверх пула можно обучить одну из моделек, доступных в нем, с произвольным апдейтом параметров: *./offline_emulator local_train -p //home/blender/orepin/online_learning/pool/20200201 -o linear_winloss_bin_ -m video_all_locrnd_sp1_v2 --feat_nm 3301 --estimate_window_size 10000 --batch_size 300 -l 0.03 --class_nm 11 --max_lines 30000 --model_type linear_winloss_bin*
В процессе обучения в stdout будут выводиться метрики качества, точно такие же как при обучении в rtmr.

### Про подбор learning rate
Эксперименты показывают, что диапазоны оптимальных learning rate достаточно сильно отличаются для softmax и winloss_* моделей, для softmax модели стоит пробовать диапазон **0.01 - 0.1**, для winloss_* - **0.001 - 0.01**.
[Здесь](https://paste.yandex-team.ru/973399/text) собраны примеры запусков разных типов моделек на каком-то одном пуле, лучшие learning rate для batch_size=50:
* linear_softmax - lr=0.03
* linear_upper_mc и linear_upper_bin  - lr=0.003

### Предобучение/дообучение модели в оффлайне
Один из главных недостатков онлайн обучения - использование каждого примера ровно один раз, в условиях небольшого количества данных, это ограничение становится существенным. 
Смягчить его можно с помощью дополнительного обучения модели в оффлайне (например на суточных данных) и подкладыванием модели в rtmr для дальнейшего обучения. 
Пока такой возможности нет, тк rtmr не поддерживает нативную доставку данных в джобу. Возможные варианты решить эту проблему:
* подложить на вход trainer доплнительную табличку, в которую руками писать объекты TPoolItem с непустой моделью, и сделать обработку такого сценария в trainer (такая табличка уже есть, она называется train_param_updates, код обработки надо написать) 
* ходить из самой джобы за моделью во внешнюю систему (менне предпочтительный вариант, но вот пара примеров таких реализаций [1](https://a.yandex-team.ru/arc/trunk/arcadia/yweb/news/rank/rtmr_visits_exporter/lib/operations.cpp?rev=3641089), [2](https://a.yandex-team.ru/arc/trunk/arcadia/rtmapreduce/mrtasks/bs_fast_stat/lib/operations.cpp?rev=3641089))

# Развитие и доработки 
https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/blender/onlinelearning/improvements