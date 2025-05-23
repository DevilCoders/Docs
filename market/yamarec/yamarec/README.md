# Рекомендации Маркета 

Здесь развивается основная кодовая база нашей команды:

- [Разработка](#Разработка)
- [Ревью](#Ревью)
- [Документация](#Документация)
- [Развертывание](#Развертывание)
- [Поддержка](#Поддержка)
- [FAQ](#faq)

## Разработка

### Стиль

При написании кода мы используем [руководство по стилю кода](https://wiki.yandex-team.ru/devrules/python/#styleguide) Аркадии.

### Подготовка окружения

Для запуска тестов и демона необходимо предварительно заэкспортировать роботные токены  в переменные окружения `YT_TOKEN` и `YQL_TOKEN` (не храним их в коде из соображений безопасности).
Токены робота `robot-yamarec-jr` можно найти в своей [Секретнице](https://yav.yandex-team.ru).
Если ты их не видишь, то тебя не включили в группу рекомендаций Маркета на [Стаффе](https://staff.yandex-team.ru/departments/yandex_monetize_market_marketdev_index_search_rec).

### Тесты

Если ты фиксишь баг, то постарайся сначала воспроизвести его в тестах.
Если ты добавляешь новый функционал, то сначала продумай сценарии его использования и напиши к ним тесты.
Если ты добавляешь новые задачи, то к ним тоже нужны тесты, но особые (не pytest, об этом в следующих разделах).

Базовые тесты пишем с помощью [pytest](https://wiki.yandex-team.ru/yatool/test/#python), прогоняем через
[ya m -A](https://wiki.yandex-team.ru/yatool/make/#testirovanie):
```bash
ya m -A market/yamarec/yamarec/bin/
```

Среди прочих эта команда запускает проверки импорта.

Юнит-тесты проверяют функционал, не требующий доступа вовне, и отрабатывают очень быстро.
Живут они в `tests/unit`.

Интеграционные тесты проверяют корректность взаимодействия с внешними сервисами и могут работать дольше.
Живут они в `tests/integration`.

Для задач есть свои тесты, они определяются в поле `tests` каждой из задач.
Запуск производится из директории `tests/functional`
См. [Запуск тестов на задачи](#запуск-тестов-на-задачи)

Все фикстуры мы для единообразия и удобства выносим в файлы `conftest.py`.

### Настройки

Клиенты для работы с чем-либо всегда реализуются в отдельном модуле и не должны использовать глобальную конфигурацию пакета.
Для настройки клиентов и их инстанциирования "on demand" мы запилили механизм бинов (beans), отдалённо похожий на Spring в Java.
Работает это просто: нужен клиент - определи класс Bean в модуле подпакете `beans` (см. примеры) и используй так:
```python
from yamarec1.beans import my_awesome_client
```
Бины автоматически пересоздаются после форка.

Основной бин пакета - это `settings`, он хранит конфигурацию для всех остальных бинов.
Мы обзавелись собственным форматом конфига.
Он внешне похож на YAML, но поддерживает произвольные Python-выражения в качестве значений.
На то, откуда конфигурация берётся и что в ней в итоге появляется, влияют переменные окружения (см. код бина).

### Задачи

Вся оффлайновая работа по сути сводится к выполнению определённых задач в правильной последовательности в несколько процессов на разных машинах.
За это отвечает движок [edera](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/edera).
Нам остается корректно определить классы задач, их цели, зависимости между ними и сценарии тестирования.

У задач зачастую бывают параметры, например, пути к ресурсам или порог в алгоритме.
И у нас есть два способа передачи параметров: через конфигурацию `settings.tasks` и через `edera.Parameter`.
Второй нужно использовать только в тех случаях, когда в наших воркфлоу могут потенциально жить несколько инстансов одного класса задач с разными значениями параметров (например, расчет величины X за несколько дней подразумевает, что `day` стоит передать через `edera.Parameter`).

Прежде чем приступить к определению новой задачи:
- выясни, каковы входные данные и какие задачи их готовят;
- выясни, где правильнее хранить выходные данные, например:
  - в inlet мы загружаем внешнюю информацию в сыром виде;
  - в items мы храним всю внешнюю информацию о категориях/моделях/офферах/...;
  - в events мы храним обработанные логи с различными событиями;
  - в features мы складываем все фичи, т.е. вычисленные числовые характеристики;
  - в sets мы складываем разного рода подборки (candidate sets, feature sets, data sets);
  - в outlet мы складываем подготовленные выгрузки вовне (обычно в TSV);
- сконфигурируй недостающие штуки (например, через `banks.config`).

#### Добавление задачи

Все задачи лежат в `yamarec1/tasks`.
Аналогично, все условия лежат в `yamarec1/conditions`, а общие сценарии - в `yamarec1/scenarios`.

Классы задач и сценариев называются в честь действия, которое они выполняют, поэтому обычно начинаются с глагола.
Классы условий должны описывать эти условия на естественном языке.

Начать добавление новой задачи можно с поиска похожей и методологии "copy and paste".
Не забудь опубликовать класс задачи в `__init__.py` (то же касается условий и сценариев).
***При этом все зависимости задачи должны быть объявлены в файле `__init__.py` выше объявления самой задачи, инача будет ошибка импорта***.
Теперь напиши минимальный рабочий код - он должен просто не падать и не обязан правильно решать задачу.

Пришла пора придумать простейший сценарий тестирования для новой задачи.
По умолчанию, у задачи есть один тест - запустить себя с дефолтными заглушками для всех зависимостей и не упасть.
Дефолтные заглушки для некоторых задач просто не определены, поэтому тебе либо придется совсем отказаться от тестов (очень плохо), либо описать свой сценарий тестирования.
Специфичный для задачи сценарий тестирования можно определять в одном файле с задачей.
Он должен описывать ограничения на используемые заглушки зависимостей через `restrictions` и описывать процесс тестирования (например, запуск и проверку результата) через `execute`.
Новоиспечённый сценарий можно подключить к задаче через свойство `tests`.
Можно заодно, если это имеет смысл, определить и дефолтную заглушку для новой задачи через свойство `stub`.

#### Конфигурирование демона

Теперь включи новую задачу в воркфлоу (ориентированный ациклический граф задач).
В `yamarec1.beans.pool` ты найдешь все доступные "точки входа" (задачи, задающие воркфлоу).
Либо встройся в один из существующих воркфлоу, либо создай новый и включи его в `daemon.config` (там же можно определить параметры запуска, вроде количества процессов или задержки между запусками).

И мы готовы к запуску!

#### Запуск тестов на задачи

В папке market/yamarec/yamarec/tests/functional находятся тесты, которые поднимают локальный экземпляр YQL/YT и запускают тесты для задач из файла `task_list.py`.

Время выполнения тестов для всех задач занимает продолжительное время и не укладывается в отведенный для LARGE тестов час.
Поэтому, можно запускать локально тесты с флагом `--test-disable-timeout` или явно указать какие тесты прогонять через `--test-param test_subject="DoMyThing"`
Также нужно включить запуск тестов, помеченных тегами `ya:fat+ya:manual`


Пример запуска:
```
ya make -ttt --test-tag ya:fat+ya:manual --test-disable-timeout --test-stdout --test-stderr --test-log-level info --test-param test_subject="DoMyThing"
```

Тесты запускаются параллельно батчами, размер можно задать с помощью `--test-param parallel_pool_size=4` (по умолчанию 16).

Если есть необходимость посмотреть результаты тестов в YT, можно передать флаг `--test-param pause_on_exit=1`.
После выполнения тестов функция не завершится сразу и можно будет посмотреть данные через yt клиент (порт для локального прокси будет указан в логах тестов, чтобы увидеть их включите `--test-stderr` и `--test-log-level info`):

```
yt list //home/market/development/yamarec --proxy 127.0.0.1:36541
```

#### Запуск демона

По умолчанию демон начнет прогонять все доступные тесты для всех воркфлоу (долго):
```bash
$ cd market/yamarec/yamarec/maintenance
$ ./launch.sh
```

Чаще всего в деве ты хочешь прогнать тесты лишь для некоторых задач.
Это можно сделать, передав регулярку на полное имя целевой задачи:
```bash
$ cd market/yamarec/yamarec/maintenance
$ YAMAREC_TEST_SUBJECT=DoMyThing ./launch.sh
```

Ещё нужно учесть, что иногда окружение портится.
Например, в нём кэшируется неверно выполненная задача.
В этом случае можно сменить окружение, указав директиву `new`:
```bash
$ cd market/yamarec/yamarec/maintenance
$ YAMAREC_TEST_SUBJECT=DoMyThing ./launch.sh new
```

Далее смотри на монитор, а в крайнем случае - непосредственно в лог.
Если всё идёт хорошо, то можно взглянуть на результат работы новых заглушек и тестов (скажем, в YT).
В общем, находи ошибки, вноси правки и перезапускай.

#### Запуск кода в окружении из Аркадии

Чтобы руками позапускать библиотечный код yamarec, можно запустить ipython с нашим окружением:
```bash
export YAMAREC_ENVIRONMENT_TYPE=development
ya py -t market/yamarec/yamarec/yamarec1/
```

## Ревью

Старайся выкладывать код на ревью небольшими законченными частями (это сильно упростит процесс ревью).
В заголовке PR укажи тикет и commit-like описание изменений на английском, вроде такого:

> MARKETRECOM-666 Summon a demon from the outworld

В комментарии к PR предоставь ревьюверу стартовую информацию об изменениях на русском.

## Документация

После каждого ревью проверь актуальность этой документации.

В `README.md` мы размещаем основную информацию для разработчиков.
Более детальную информацию мы размещаем в отдельной директории `docs` в файлах вида `CamelCaseName.md` и ссылаемся на них из `README.md`.

## Развертывание

Развёртывание yamarec1 автоматизировано через [Arcanum CI](https://a.yandex-team.ru/projects/marketrecommend/ci/releases/timeline?dir=market%2Fyamarec&id=yamarec-release).

После выкладки в testing следи за [монитором](http://yamarec1.tst.vs.market.yandex.net/monitor).
В идеале там не должно быть ничего красного.
При падениях смотри лог, примонтированный на logview.market.yandex.net в директорию `yandex/yandex-yamarec1/info.log`.
Всё ещё? открыта вакансия героя, который автоматизирует приёмку!

С проблемами в production разбирается [дежурный](#Поддержка).
Конечно же, его основной инструмент - это [монитор](http://yamarec1.vs.market.yandex.net/monitor).

## Поддержка

Каждая неделя становится звёздным часом одного разработчика - дежурного.
Его долг (по убыванию приоритета):
- не отвлекаться на проектные задачи;
- оперативно отвечать на вопросы в [хотлайне](https://t.me/joinchat/ACIuBkEA9clN3S3frZje7w);
- реагировать на [лампочки](https://t.me/joinchat/BbgvTERXHp-_ugLrIpafKg);
- разгребать очередь поддержки (раздел Support [дашборда](https://st.yandex-team.ru/dashboard/8284));
- обновлять [инструкцию](../docs/Support.md) для дежурных.

## FAQ

#### Исчезли зависимости задачи! Что произошло?

Почти наверное, ты добавил адхок, который выпилил результат работы задачи X, но оставил результаты какой-то другой задачи Y, зависящей от X. И теперь edera вправе считать X выполненной, несмотря на отсутствие реальных результатов, на что будут жаловаться все невыполненные задачи, зависящие от X.

Либо выпили всё, что зависит от X (если это действительно нужно), либо запили адхок для отдельного запуска X.

#### Ошибка при импорте из `yamarec1`

Пример стэк трейса из `.home/yamarec.std`:
```
Traceback (most recent call last):
  File "<string>", line 2, in <module>
  File "library/python/runtime/importer.pxi", line 265, in __res.ResourceImporter.run_main
    self.load_module(entry_point, fix_name='__main__')
  File "library/python/runtime/importer.pxi", line 236, in __res.ResourceImporter.load_module
    exec code in mod.__dict__
  File "market/yamarec/yamarec/bin/daemon/__main__.py", line 3, in <module>
    from yamarec1.beans import daemon
  File "market/yamarec/yamarec/yamarec1/kit/helpers/bean_bag.py", line 35, in __setattr__
    object.__setattr__(self, name, LazyProxy[getattr(value, "Bean")]())
AttributeError: 'NoneType' object has no attribute 'Bean'
```

Чтобы получить больше информации, можно запустить интерпретатор в окружении `yamarec1` (запускать из корня аркадии или подправить путь)
```
./ya py -t market/yamarec/yamarec/yamarec1
```
и уже в нём выполнить импорт подозрительной таски. Например, так:
```
In [1]: from yamarec1.tasks import CookMostOftenBought
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
contrib/python/ipython/py2/IPython/__init__.py in <module>()
----> 1 from yamarec1.tasks import CookMostOftenBought

library/python/runtime/importer.pxi in __res.ResourceImporter.load_module()
    234
    235         try:
--> 236             exec code in mod.__dict__
    237             old_mod = sys.modules[mod_name]
    238         finally:

market/yamarec/yamarec/yamarec1/tasks/__init__.py in <module>()
    268 from .cook_reason_to_buy_tech_spec import CookReasonToBuyTechSpec  # noqa
    269 from .cook_reason_to_buy_viewed_n_times import CookReasonToBuyViewedNTimes  # noqa
--> 270 from .cook_most_often_bought import CookMostOftenBought  # noqa
    271 from .cook_most_recommended import CookMostRecommended  # noqa
    272 from .cook_tsv_data_from_sandbox_resource import CookTsvDataFromSandboxResource  # noqa

library/python/runtime/importer.pxi in __res.ResourceImporter.load_module()
    234
    235         try:
--> 236             exec code in mod.__dict__
    237             old_mod = sys.modules[mod_name]
    238         finally:

market/yamarec/yamarec/yamarec1/tasks/cook_most_often_bought.py in <module>()
     33
     34
---> 35 class CheckResult(Scenario):
     36
     37     subject = edera.Parameter(edera.qualifiers.Instance[Task])
NameError: name 'Scenario' is not defined
```
