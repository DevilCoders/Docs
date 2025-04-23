# Описание json-a с параметрами


    // Группы параметров
    {
        "task_id": некоторый уникальный идентификатор конкретной модели, аналог task_id в ml-engine
        "log_processing": Все, что относится к подготовке логов для линейной модели
        "dmlc_learn_params": Параметры dmlc (регуляризация, тип модели (линейная модель или факторизационная машина), тип функции потерь)
        "namespaces": Список факторов для линейной модели
        "target_field": Поле с ответом
        "group_loss_keys": Список ключей, по которым мы будем группировать объекты для ранжирования (обычно тут просто 'HitLogID')
        "ffm_product_rules": Зарезервировано для модели FFM (в онлайне пока что не допилена)
        "nirvana_workflow": Здесь все поля для самого графа в Нирване (память, ttl и пр.)
    }

## log_processing
Здесь находится все, что относится к предебработке таблиц для обучения модели.

    // log_processing
    {
        "type": маска, по которой ищутся логи
        "start_date": Первая дата (обязательно выставляется)
        "end_date": Последняя дата. Если None, возьмет все доступные логи, начиная от start_date
        "preprocessors": список препроцессоров для логов (подробнее ниже)
        "begin": Legacy
        "exec": Legacy
        "arcadia_patch_libraries": Список дополнительных библиотек, которые нужно подхватить при сборке бинаря для препроцессора.
        Нужен, если вы используете препроцессор в списке preprocessors, который лежит в какой-то аркадийной библиотеке
        "num_parts_per_log": // Разрежет каждую входную табличку на n частей по ShowTime
    }

Логи ищутся так:
from yabs.logconfig import get_logs_regexp_time
logs_list = get_logs_regexp_time(type, start_date, end_date)

### Preprocessors

Список препроцессоров - это список строк, который передается в кубик нирваны в качестве параметров. При получении над ними делается eval,
так что эни должны представлять собой валидный питонячий код
В списке препроцессоров можно указывать следующие классы:
1. Mapper
2. Reducer
3. Любые классы, отнаследованные от BasicPreprocessor (лежит в ads/libs/py_ml_factors/ml-factors/py-modules/matrixnet/learn_preprocessors.py, импортируется по yabs.matrixnet.learn_preprocessors)
4. YTSpecContext

Если подряд указано несколько Mapper'ов или Reducer'ов, то они сгруппируются в одну операцию.
Каждый препроцессор - это отдельная YT операция.
YTSpecContext - нужен, чтобы задавать свои YtSpec на блоки операций. Из самых важных применений:
1. Можно выставить пул YT
2. Можно выставить data_size_per_job. Выставление правильного data_size_per_job может в несколько раз ускорить обработку логов.
Работает это следующим образом: работы YT джобы складывается из инициализации, собственно работы и уничтожения. Если работа сверхбыстрая
(Grep, к примеру), то 90% работы джобы будет заполнять оверхед самого YT.


    // Пример списка препроцессоров:
    [
        "YTSpecContext({\"data_size_per_job\": 8 * 2 ** 32, \"pool\": \"robot-online-learning-rtb\"})",
        "Grep('r.FraudBits == 0 or  (r.CounterType == 1 and r.FraudBits == 1)')",
        "Grep('r.SelectType not in (0, 5, 17)')",
        "Grep('r.IsClickedHit == 1 or r.HitLogID % 107 == 0')",
        "Mapper('r.NegativeFraudBits = -r.FraudBits')",
        "Mapper('r.IsClick = r.CounterType - 1', add_fields=[('IsClick', int)])",
        "Mapper('r.ProductType = {\"\": 0,u\"direct\": 1,u\"media-creative\": 4,u\"media-image\": 3,u\"media-smart\": 2,u\"video-smart\": 5}.get(r.ProductType, 0)', add_fields=[('ProductType', int)])",
        "Mapper('r.QueryID = r.QueryID if r.QueryID is not None else 0')",
        "YTSpecContext({\"data_size_per_job\": 4 * 2 ** 32, \"pool\": \"robot-online-learning-rtb\"})",
        "JoinBannerToTextsPreprocessor(\"stat/BannerToTexts\", joinType='outer')",
        "YTSpecContext({\"data_size_per_job\": 2 ** 32, \"pool\": \"robot-online-learning-rtb\"})",
        "RSYAFactors(factors_to_compute=[\"BannerTitleLemmaH\", \"BannerBMCategoryID\", \"QueryH\", \"QueryLemmaH\"])",
    ]

Что здесь происходит:
1. Выставляем большой data_size_per_job. При запуске на JoinedEFH логах уменьшает время работы блока с grep и map с ~30 часов до ~8 часов.
2. Грепаем логи и считаем нужные нам поля. Все три грепа и 4 маппера объединяются в один mr_do_map
3. Выставляем data_size поменьше
4. Вызываем JoinBannerToText, чтобы довезти тексты баннеров и тексты привязок, все, что нужно для текстовых факторов
5. Выставляем дефолтный data_size_per_job, поскольку RSYAFactors - тяжелая медленная операция.
6. Считаем недостающие в логе факторы для линейной модели


## dmlc_learn_params
    // Параметры dmlc для обучения модели

    "dmlc_learn_params": {

        // Параметры регуляризации (читайте статью https://www.eecs.tufts.edu/~dsculley/papers/ad-click-prediction.pdf)
        "lambda_l1": 4,
        "lambda_l2": 0,
    
        // Инкрементальная l1-регуляризация. что это такое читаем тут https://arxiv.org/pdf/1403.3465.pdf
        "lambda_l2_incremental": 0,
    
        // Параметры learning rate для AdaGrad. lr_eta стоит подбирать, lr_beta можно оставить
        "lr_eta": 0.1,
        "lr_beta": 1,
    
        // Размер минибатча
        "minibatch": 100,
    
        // Оставляем равным 1
        "max_data_pass": 1,
    
        // Инкрементальная l1-регуляризация для уменьшения размеров модели (читать https://arxiv.org/pdf/1403.3465.pdf)
        // В отличие от lambda_l2_inc, применяется после каждого часа
        "l1_inc_on_save": 0,
    
        // Эвристика для порезки learning rate (не дает adagrad убывать слишком быстро)
        "adjust_learning_rate_after_l1_inc": "true",
    
        // Тип алгоритма (для линейной модели пока есть только FTRL_ADAGRAD_W)
        "algo_w": "FTRL_ADAGRAD_W",
    
        // Использовать во всех алгоритмах вместо обычного стохастического градиента его svrg вариант (про svrg читаем тут
        https://papers.nips.cc/paper/4937-accelerating-stochastic-gradient-descent-using-predictive-variance-reduction.pdf)
        "use_svrg": "false",
    
        // Тип модели. Может быть:
        // 1. GLM - Generalized Linear Model
        // 2. FMG - Factorization Machine Grouped
        // 3. FFM - Field-Aware Factorization Machine
        // Все типы моделей умеют работать с svrg
        "model_type": "GLM",
    
        // Параметры для embedding'ов для FMG и FFM, аналогичны уже указанным выше
        "embedding": {
            "algo_v": "FTRL",
            "dim": 10,
            "threshold": 10,
            "lambda_l2": 10,
            "lambda_l1": 0,
            "lr_eta": 0.01,
            "lr_beta": 1,
            "dropout": 0
        },
    
        // Эвристика для сохранения памяти: если w = 0, то и вектор равен 0 и память под него не выделяется
        "l1_shrk": "true",
    
        // Конфигурация функции потерь. Функции потерь могут быть:
        a) Для непрерывного y:
            1. SQUARED - линейная регрессия
        б) Для классификации:
            1. LOGISTIC_BINARY - обычный logloss
            2. SHARDED_BINARY_RANK - logloss между разностями прогнозов (известен как CRR, читать http://www.decom.ufop.br/menotti/rp122/sem/sem2-alex-pres.pdf)
            3. LLMAX_BINARY - llmax ранжирование как в матрикснете
        "loss" : [
            {"type": "LOGISTIC_BINARY", "coefficient": 1}
        ]
    }

Все функции потерь взвешиваются с коэффициентами, которые вы указываете. За нормировку (чтобы их сумма = 1)
отвечаете вы сами.

### group_loss_keys
Если вы указали хотя бы один loss из [SHARDED_BINARY_RANK, LLMAX_BINARY], то необходимо также указать ключ, по которому объекты будут группироваться.
Внутри этих групп и будет считаться ранжирование. По умолчанию в РСЯ можно ставить
group_loss_keys = ['HitLogID']


## nirvana_workflow
    // Параметры workflow в Нирване. 
    
    {
        "basic_workflow_id": "3fb6955d-0af7-11e7-a873-0025909427cc", // Базовый workflow для production
        "dst-path": "dst_path", // Legacy
        "mapping_table": // Папочка (!), куда положится вспомогательная табличка. Табличка весит очень немного
        (одна запись с 5 полями на каждый час), так что можно положить куда-нибудь в хомяк и забыть про нее.
        "slaves": 10, // Число слейвов для dmlc. Качество модели, как правило, обратно пропорционально числу слейвов
        "protomapper_name": "ProtoMapperWrapper",
        "proto_sharded_reducer_name": "ProtoShardedReducer",
        "sandbox_token": "robot-ml-engine-v-nirvane-sandbox", // Sandbox-токен (имя секрета в нирване) для отгрузки дампов на sandbox
        "max_graphs_to_launch": 5, // Максимальное число графов, запускаемых graph_launcher'ом за раз (можно не трогать)
        "first_model": "ahaha_fake_task", // Если у вас уже есть дамп dmlc, то можно начать обучение с него.
        "mr_do_map_max_ram": 3000, // Память для бинаря препроцессора. Если кубик упал по MAX_RAM - увеличьте
        "master_max_ram": 5000, // Память для dmlc-master, в принципе, можно не трогать - на мастере ничего не считается
        "mr_do_map_ttl": 3000, // ttl для препроцессинга логов
        "slave_max_ram": 5000, // Память для dmlc-slave, если упало по MAX RAM - нужно увеличить
        "num_threads_sandbox_upload": 3, // Лучше не трогать, а то ребята из sandbox будут ругаться
        "yt_pool": "ml-engine" // Legacy
    }
