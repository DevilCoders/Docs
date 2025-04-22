<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Общие концепции](#%D0%BE%D0%B1%D1%89%D0%B8%D0%B5-%D0%BA%D0%BE%D0%BD%D1%86%D0%B5%D0%BF%D1%86%D0%B8%D0%B8)
  - [YT-центричное обучение](#yt-%D1%86%D0%B5%D0%BD%D1%82%D1%80%D0%B8%D1%87%D0%BD%D0%BE%D0%B5-%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5)
  - [Arcadia-центричные пайплайны](#arcadia-%D1%86%D0%B5%D0%BD%D1%82%D1%80%D0%B8%D1%87%D0%BD%D1%8B%D0%B5-%D0%BF%D0%B0%D0%B9%D0%BF%D0%BB%D0%B0%D0%B9%D0%BD%D1%8B)
  - [model_yt_dir](#model_yt_dir)
  - [Главное правило](#%D0%B3%D0%BB%D0%B0%D0%B2%D0%BD%D0%BE%D0%B5-%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%BE)
  - [Директория эксперимента](#%D0%B4%D0%B8%D1%80%D0%B5%D0%BA%D1%82%D0%BE%D1%80%D0%B8%D1%8F-%D1%8D%D0%BA%D1%81%D0%BF%D0%B5%D1%80%D0%B8%D0%BC%D0%B5%D0%BD%D1%82%D0%B0)
  - [URI. UriCallback](#uri-uricallback)
- [Online learning](#online-learning)
  - [Концепция, зачем нужен](#%D0%BA%D0%BE%D0%BD%D1%86%D0%B5%D0%BF%D1%86%D0%B8%D1%8F-%D0%B7%D0%B0%D1%87%D0%B5%D0%BC-%D0%BD%D1%83%D0%B6%D0%B5%D0%BD)
  - [Что есть в онлайн обучении](#%D1%87%D1%82%D0%BE-%D0%B5%D1%81%D1%82%D1%8C-%D0%B2-%D0%BE%D0%BD%D0%BB%D0%B0%D0%B9%D0%BD-%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B8)
    - [Снапшоты](#%D1%81%D0%BD%D0%B0%D0%BF%D1%88%D0%BE%D1%82%D1%8B)
    - [Фильтрация эмбеддингов: ttl_filter](#%D1%84%D0%B8%D0%BB%D1%8C%D1%82%D1%80%D0%B0%D1%86%D0%B8%D1%8F-%D1%8D%D0%BC%D0%B1%D0%B5%D0%B4%D0%B4%D0%B8%D0%BD%D0%B3%D0%BE%D0%B2-ttl_filter)
    - [Train data](#train-data)
    - [Evaluation](#evaluation)
  - [Как сварить датасет](#%D0%BA%D0%B0%D0%BA-%D1%81%D0%B2%D0%B0%D1%80%D0%B8%D1%82%D1%8C-%D0%B4%D0%B0%D1%82%D0%B0%D1%81%D0%B5%D1%82)
    - [Формат хранения.](#%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%82-%D1%85%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)
    - [Как устроен код подготовки данных](#%D0%BA%D0%B0%D0%BA-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BD-%D0%BA%D0%BE%D0%B4-%D0%BF%D0%BE%D0%B4%D0%B3%D0%BE%D1%82%D0%BE%D0%B2%D0%BA%D0%B8-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85)
      - [Какие данные должны быть на входе](#%D0%BA%D0%B0%D0%BA%D0%B8%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5-%D0%B4%D0%BE%D0%BB%D0%B6%D0%BD%D1%8B-%D0%B1%D1%8B%D1%82%D1%8C-%D0%BD%D0%B0-%D0%B2%D1%85%D0%BE%D0%B4%D0%B5)
        - [Как подать текст в обучение](#%D0%BA%D0%B0%D0%BA-%D0%BF%D0%BE%D0%B4%D0%B0%D1%82%D1%8C-%D1%82%D0%B5%D0%BA%D1%81%D1%82-%D0%B2-%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5)
      - [Как комбинируем данные в батчи](#%D0%BA%D0%B0%D0%BA-%D0%BA%D0%BE%D0%BC%D0%B1%D0%B8%D0%BD%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5-%D0%B2-%D0%B1%D0%B0%D1%82%D1%87%D0%B8)
      - [Как колонки разных типов превращаются в тензоры](#%D0%BA%D0%B0%D0%BA-%D0%BA%D0%BE%D0%BB%D0%BE%D0%BD%D0%BA%D0%B8-%D1%80%D0%B0%D0%B7%D0%BD%D1%8B%D1%85-%D1%82%D0%B8%D0%BF%D0%BE%D0%B2-%D0%BF%D1%80%D0%B5%D0%B2%D1%80%D0%B0%D1%89%D0%B0%D1%8E%D1%82%D1%81%D1%8F-%D0%B2-%D1%82%D0%B5%D0%BD%D0%B7%D0%BE%D1%80%D1%8B)
    - [Структурирование данных внутри батча. Групповые лоссы](#%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%B2%D0%BD%D1%83%D1%82%D1%80%D0%B8-%D0%B1%D0%B0%D1%82%D1%87%D0%B0-%D0%B3%D1%80%D1%83%D0%BF%D0%BF%D0%BE%D0%B2%D1%8B%D0%B5-%D0%BB%D0%BE%D1%81%D1%81%D1%8B)
    - [Полный пример запуска](#%D0%BF%D0%BE%D0%BB%D0%BD%D1%8B%D0%B9-%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0)
  - [Использование нескольких таблиц в обучении](#%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BD%D0%B5%D1%81%D0%BA%D0%BE%D0%BB%D1%8C%D0%BA%D0%B8%D1%85-%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86-%D0%B2-%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B8)
    - [Идеальный inner join](#%D0%B8%D0%B4%D0%B5%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-inner-join)
    - [Джойн таблиц при варке в тензорный формат](#%D0%B4%D0%B6%D0%BE%D0%B9%D0%BD-%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86-%D0%BF%D1%80%D0%B8-%D0%B2%D0%B0%D1%80%D0%BA%D0%B5-%D0%B2-%D1%82%D0%B5%D0%BD%D0%B7%D0%BE%D1%80%D0%BD%D1%8B%D0%B9-%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%82)
    - [Джойн таблиц в обучении](#%D0%B4%D0%B6%D0%BE%D0%B9%D0%BD-%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86-%D0%B2-%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B8)
  - [Как запускать обучение](#%D0%BA%D0%B0%D0%BA-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0%D1%82%D1%8C-%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5)
    - [Настройка ```.vhrc```](#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-vhrc)
    - [Бинарь для запуска](#%D0%B1%D0%B8%D0%BD%D0%B0%D1%80%D1%8C-%D0%B4%D0%BB%D1%8F-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0)
  - [Как запускать локально](#%D0%BA%D0%B0%D0%BA-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0%D1%82%D1%8C-%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE)
    - [Устанавливаем окружение](#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%B0%D0%B2%D0%BB%D0%B8%D0%B2%D0%B0%D0%B5%D0%BC-%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5)
    - [Команда запуска](#%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

**ВАЖНО**: сначала прочтите два предыдущих туториала! На текущий момент вы уже должны понимать, как писать скрипт обучения!

{{toc}}

# Общие концепции
## YT-центричное обучение
Разработка пайплайнов поверх YT позволяет получить следующие плюшки:
1. Артефакты моделей разложены по распределенной файловой системе с удобным UI. Нет ничего более привычного для любого пользователя ЭВМ, чем файловая система
2. Транзакционная система позволяет делать атомарные изменения во всех частях пайплайна обучения.
3. Файловую систему в YT удобно очищать
4. Ванильный YT имеет кросс-дц кластеры с отличными гарантиями, что позволяет **один раз** написать общий код обучения и для экспериментов, и для продакшен дообучения с необходимой отказоустойчивостью. По сути, единственное, чем отличается продакшен обучение поверх ытя от обучения в экспериментах - реалтаймовой читалкой данных.

## Arcadia-центричные пайплайны
Код обучения и всего пайплайна - это просто код на любом языке программирования, в котором из коробки поддержаны:
1. Циклы, рекурсии, обработки исключений, декоратора, корутины, потоки и прочие достижение инженерной мысли
2. CI-тесты
3. Вкупе с предыдущим пунктом про YT-центричность - интеграционные тесты в той же аркадии благодаря наличию local yt
4. Кеши пайплайнов сделаны **тоже поверх YT**. На это ушло некоторое время разработки, однако, такие кеши работают как cache by value с кастомной логикой, позволяющей иногда экономить десятки или даже сотни терабайт потенциально лишних данных.

## model_yt_dir
Во всех пайплайнах обучения центральной точкой входа является ```model_yt_dir```. Это путь до директории модели в ыте. Директория должна быть уникальной для каждой модели. Рассмотрим пример model_yt_dir для онлайн обучения ((https://yt.yandex-team.ru/hahn/navigation?path=//home/ads/users/alxmopo3ov/bsdev_78621/multiseq_v2_try2/config_id_0_max_workers_24_lr_0_01 ссылка)). Директория модели состоит из четырех составляющих:
1. ```script.py``` и ```model_config.json```. Это тот скрипт и конфиг, с которыми запускались обучалки. Часто пользователи пишут собственные фабрики конфигов, так вот здесь - результат после всех фабрик. Можно брать ```as is``` и запускать, к примеру, локально
2. ```all_files``` - дополнительные файлы, использованные в обучении (здесь пустой, потому что дополнительных файлов нет)
3. ```external_stuff``` - специальная директория, куда разрешается складывать артефакты, приписываемые модели, но не насчитываемые непосредственно обучалкой. В данном примере здесь - метрики, насчитанные сторонней тулзой для соответствующей таблички из ```evaluation``` после обучения
4. Все остальные папки - артефакты, выплевываемые самой обучалкой

В будущем, возможно, досыпем бинарь, которым запускалось, и неаркадийные питонопакеты для 100% воспроизводимости. Пока заказчиков у этой фичи не было. Для продакшена в ```model_yt_dir``` полный набор артефактов для перезапуска лежит в директории.

## Главное правило
**Главное правило** работы с результатами экспериментов: все в первую очередь должно лежать в YT. Все обучалки/пайплайны складывают все свои артефакты **только на YT**. С YT они уже забираются в другие транспорты по необходимости.

## Директория эксперимента
Экспериментом называется высокоуровневый запуск пачки модели с последующим их применением на тестовом сете и расчетом метрик (как правило, потусторонними тулзятинами). Правила те же:
1. Пайплайны складывают все свои артефакты в первую очередь в ыть, а потом уже - в любые другие сервисы
2. Кеши работают в первую очередь поверх артефактов YT
3. Подчистка результатов, сброс кешей и тд - это уничтожение директорий эксперимента в YT

## URI. UriCallback
Заглянем немножко в кишочки библиотеки, а точнее, в ее хребет: основной цикл обучения. По традиции, взглянем сначала на [код](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/core/runner.py)

Мы тут видим два класса:
* ```BaseRunnerCallback``` - базовый интерфейс для подмешивания **любой дополнительной логики** в обучение
* ```Runner``` - Базовый цикл обучения. Любой пайплайн обучения концептуально выглядит так:
   1. Создаем модель, оптимайзер и лосс пользовательским кодом
   2. Собираем MinibatchWorkerPool - штука, которая принимает модель, оптимайзер и лосс и кушает батчи. Осуществляет непосредственно обучение
   3. Создаем всякие разные callback'и для дополнительной логики: подсчет лоссов на валидационных выборках, снепшоты, фильтрации модели и тд
   4. Засовываем все в runner, запускаем

```Runner``` работает следующим образом. Любой датасет представляется в виде **последовательности URI**.
* **URI** - это  [неделимая единица обучения](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/core/runner.py?rev=r7848845#L89): от начала обработки данных из URI и до конца мы не вызываем никакой дополнительной логики в основном цикле обучения.
* **UriCallback** - функтор, вызываемый между обработкой URI. **Гарантируется**, что при вызове любого callback'а обработчик батчей MinibatchWorkerPool завершит работу, а модель, оптимайзер и лосс не будут им меняться.

Правильное конструирование обучения - это вопрос того, как вы нарежете на URI свой датасет:
1. Онлайн обучение по сортированному по времени потоку нарезает датасет по timestamp'у. Как правило, один URI = один час логов.
2. Классическое обучение по датасету в несколько эпох (мы его называем оффлайн обучением) - нарезаем датасет сначала по границе эпох, а затем чанками по 4000 батчей. Выбор размеров чанка обусловлен оверхедом на синхронизацию обучалки между вызовами callback'ов

Отдельно отметим, что цикл обучения не накладывает никаких ограничений на то, как физически располагаются URI. Это могут быть чанки одной таблицы, нескольких таблиц, потенциально даже на разных кластерах. С точки зрения абстракций, за то, как читать любые URI и превращать их в последовательность батчей, отвечает DataLoader.

# Online learning
Самый продвинутый пайплайн обучения рекомендательных моделей. В рекламе все без исключения pytorch модели используют именно эту парадигму.

## Концепция, зачем нужен
В данном посте довольно дается довольно подробное описание концепции онлайн обучения и ее плюшек https://clubs.at.yandex-team.ru/machinelearning/2177

Если коротко, то онлайн обучение - это обучение на сортированном по времени бесконечном потоке данных. Не существует понятия **фиксированного датасета**: в модель постоянно досыпаются новые данные и она постоянно дообучается.

Рассмотрим сразу одно из важнейших отличий от обычного батч обучения: как применять модель и как мерить профит. Поскольку модель инкрементально дообучается, потоки данных на обучение и на применение должны быть сортированы по одному и тому же времени. При применении модели к validation логу нужно взять данные на validation из будущего с лагом, равным лагу модели в продакшене.

В рекламе, к примеру, лаг модели примерно 6 часов, это значит, что моделька за 2021-01-20T17:00:00 будет применяться к логу с датой 2021-01-20T23:00:00.

Второй важный момент - как делать train/validation split. Короткий ответ: **никак**. Для замера качества самой модели, можно мерить качество на train логе с лагом в будущее.

## Что есть в онлайн обучении

По традиции, давайте просто взглянем на "дефолтный" конфиг обучения:
```(json)
{
    "model_yt_dir": "//home/ads/users/alxmopo3ov/bsdev_78621/LTP_features_try4/try_profiler3",
    "model": {
        "my_model_description": "составлять эту часть конфига мы учились в двух предыдущих туториалах"
    },
    "train_data": {
        "datetime_format": "%Y%m%d%H%M",
        "start_date": "202012222100",
        "end_date": "202101180000",
        "table": "//home/ads/users/alxmopo3ov/bigkv/train_data/ad_search_try1_pos_embed_sequence_embed_right_shape_torch_mb1024",
        "targets": [
            "IsClick"
        ]
    },
    "evaluation": {
        "eval_confs": [
            {
                "name": "train",
                "keys": ["HitLogID", "BannerID", "FraudBits", "Position", "ShowTime"],
                "table": "//home/ads/users/alxmopo3ov/bigkv/train_data/ad_search_try1_pos_embed_sequence_embed_right_shape_torch_mb1024",
                "datetime_format": "%Y%m%d%H%M",
                "start_date": "202101110000",
                "end_date": "202101180000",
                "shifts": [1]
            }
        ]
    },
    "ttl_filter": {
        "frequency": 30
    },
    "snapshotter": {
        "frequency": 7200
    }
}
```

### Снапшоты
```(json)
"snapshotter": {
    "frequency": 7200
}
```
Снапшоты складываются в поддиректорию `snapshot`. Настройка всего одна - frequency: частота сохранения **в секундах**. Снапшоты полностью откатывают состояние модели, оптимайзера, **и всех артефактов в директории** на момент вызова. В целом, вам как пользователю про него больше ничего знать не нужно, все работает автоматом из коробки.

### Фильтрация эмбеддингов: ttl_filter
```(json)
"ttl_filter": {
    "frequency": 30
}
```

У всех без исключения алгоритмов оптимизации эмбеддингов есть параметр [ttl](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/hash_embedding/optim.py?rev=r7776308#L148). ttl - это unsigned int, обозначающий **максимально допустимый возраст неиспользуемой фичи**. Если фича не встречалась в течение ```ttl``` **URI**, то мы удаляем ее из хеш-таблицы.

Почему ```ttl``` в URI, а не в минибатчах? Потому что разрабатывалась специально для онлайн обучения, а там естественным условием чистки является "фича не встречалась в логах обучения Х часов".

А зачем здесь какой-то frequency? Это детали реализации очистки. Честная очистка хешмапы во время обучения - удаление пачки эмбеддингов из хеш-таблицы - дорогая операция, поэтому мы сделали оптимизацию: если обучалка поймет, что фича старая, она не удалит ее, а просто сбросит ее состояние (сброс весов и стейта оптимайзера) и пометит как "устаревшую". Физическая очистка произойдет в callback'е, который пройдется по всем хешмапам и удалит их. Если фича вдруг встретилась заново в логе до вызова callback'а, флаг сбросится и она снова будет учиться.

### Train data
Описание данных для обучения.
```(json)
"train_data": {
     "datetime_format": "%Y%m%d%H%M",
     "start_date": "202012222100",
     "end_date": "202101180000",
     "table": "//home/ads/users/alxmopo3ov/bigkv/train_data/ad_search_try1_pos_embed_sequence_embed_right_shape_torch_mb1024",
     "targets": [
         "IsClick"
     ]
}
```

Для начала посмотрим на ((//home/ads/users/alxmopo3ov/bigkv/train_data/ad_search_try1_pos_embed_sequence_embed_right_shape_torch_mb1024 пример таблицы)). В таблице для обучения лежат **батчи** - как их варить и почему батчи у нас в ыте, расскажем позднее. Обращаем внимание, что таблица сортирована по ```_online_learning_date_granular``` - это timestamp'ы, огрубленные до часа. Сейчас онлайн обучение всегда дробить датасет по часам.

```start_date``` и ```end_date```: даты начала и конца обучения. Можно учиться на любом непрерывном отрезке из таблицы.

```targets``` и ```features``` - поля, перечисляющие какие фичи брать. Если вы делаете модель через IDeployableModel + BaseEmbeddingModel, то ```features``` необязателен: можно переопределить [вот такой метод](https://a.yandex-team.ru/arc/trunk/arcadia/junk/alxmopo3ov/ad_transformer_v2/warmup_without_deep_part_long_cb/script.py?rev=r7960778#L200) и фичи автоматически будут выведены из модели.

### Evaluation
```(json)
    "evaluation": {
        "eval_confs": [
            {
                "name": "train",
                "keys": ["HitLogID", "BannerID", "FraudBits", "Position", "ShowTime"],
                "table": "//home/ads/users/alxmopo3ov/bigkv/train_data/ad_search_try1_pos_embed_sequence_embed_right_shape_torch_mb1024",
                "datetime_format": "%Y%m%d%H%M",
                "start_date": "202101110000",
                "end_date": "202101180000",
                "shifts": [1]
            },
            {
                "name": "catboost",
                "keys": ["HitLogID", "BannerID", "FraudBits", "Position", "ShowTime"],
                "table": "//home/ads/users/alxmopo3ov/bigkv/train_data/search_premium_profile_log_torch_mb1024",
                "datetime_format": "%Y%m%d%H%M",
                "start_date": "202101110000",
                "end_date": "202101180000",
                "shifts": [8]
            }
        ]
    }
```

Evalution - это конфигурирование того, к каким логами применяется ваша онлайн модель. Применение онлайн модели означает, что у вас на каждый час логов должна быть своя моделька. Такую схему можно реализовать "в лоб", сохраняя снепшоты моделей каждый час, но это будет приводить к огромным издержкам как по диску, так и по скорости. Вместо этого, мы применяем модель in-memory, прямо во время обучения: после обработки нужного часа замораживаем ее, применяем на логе, отгружаем предикшены в YT. Эти предикшены потом принято джойнить к более толстым табличкам.

В целом, тут есть тот же набор полей, что и в train_data, и добавляются новые:
* ```keys``` - это должны быть **однозначные категориальные фичи**. Они поедут в табличку с предикшенами, и по этим ключам потом можно будет приджойнить таблицу с предсказаниями к нужному логу
* ```shifts``` - сдвиги в будущее в часах. **Сейчас должен быть единственный shift**. shift=1 означает, что моделька применится с лагом в будущее в 1 час.

Также могут быть переопределены ```features``` и ```targets```. По дефолту, эти поля берутся из train лога.

## Как сварить датасет
Пара особенностей:
1. Мы выносим максимум обработки данных в YT. Концепция DSSM, когда мы читаем совсем сырые логи, здесь работает плохо: при multi-gpu обучении можно начать упираться в процессинг данных, плюс CPU нам нужно еще и на расчет эмбеддингов
2. В YT лежат **готовые батчи данных**. Одна строчка в YT содержит в себе один минибатч со всеми необходимыми тензорами. На размерности тензоров мы при этом не накладываем никаких ограничений

### Формат хранения.
Читалка читает данные в Skiff формате. Тензоры прожимаются в похожий бинарный skiff format. Данные тензоров жмутся каким-то алгоритмом сжатия, обычно это ZSTD5.

Проще всего понять устройство, почитав код:
1. [Сериализация](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/lib/pool/formatter/serializer.h?rev=r8155672#L333)
2. [Десериализация](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/cpp_lib/yt/single_record_parser.cpp?rev=r8133373#L157)

Такой формат, с одной стороны, очень хорошо пакует тензоры в YT и обеспечивает достойную скорость стриминга, с другой -  парсинг skiff элементарно программируется в неаркадийном C++ без необходимости тащить аркадийные .so.

### Как устроен код подготовки данных
#### Какие данные должны быть на входе
Варщик логов предполагает, что все нужны данные в YT хранятся **в числовом формате**. Варщик данных только берет числовые данные и собирает их в тензоры с нужным batch_size. Все парсинги, токенизации текстов и т.д. мы отдаем на откуп пользователям - пусть делают так, как они привыкли/считают нужным, здесь нет единого наилучшего для всех решения.

##### Как подать текст в обучение
Вынесем этот пункт в отдельную главу как наиболее часто задаваемый вопрос. Чтобы подать текстовое поле в ```ads_pytorch```, вам самим надо превратить в категориальную фичу, т.е. в последовательность uint64 хешей. Есть два классических подхода: токенизация и триграммы.

Токенизация:
1. Текст токенизируется
2. Опционально лемматизируется
3. Все токены/леммы подаются на вход в какую-то хеш функцию, получая на выход последовательность хешей

Триграммы:
1. Текст превращается в последовательность триграмм
2. Все триграммы подаются на вход в какую-то хеш функцию, получая на выход последовательность хешей

Дальше из них уже ручками можно сварить биграммы/биграммы слов и т.д.

#### Как комбинируем данные в батчи
Поскольку мы учимся на сортированных по времени данных, необходимо заранее выделенную колонку со временем в секундах. Назовем ее ```time_field```. Для обучения очень важно, чтобы батчи получались одинакового размера, иначе возникнет ситуация с неравномерностью шума в градиентах батчей. Градиент по батчу размера 10 намного шумнее градиента по батчу 1024, однако, если в лоссах стоит reduction='mean', то они будут иметь примерно одинаковый вес в стейте оптимайзера. Это может иметь довольно трудноотлавливаемые плохие последствия для обучения. Отметим, что это наверняка не единственная проблема с неравномерностью - это просто одна из основных, на которую мы обращали внимание.

Чтобы получать батчи консистентного размера, будем редьюсить данные по специальному ключу, чтобы гарантировать определенный размер данных в каждой джобе. В идеале, количество данных в ключе должно быть кратно размеру батча. Для онлайн обучения можно организовать такой специальный ключ, однако нам было лень и мы сделали более простую схему: мы заводим поле ```granularity```, в которое подаем число секунд, которое попадет в один ключ. На наших рекламных данных ```granularity=300``` отлично работает, обрезанными получается не более 0.3% батчей.

#### Как колонки разных типов превращаются в тензоры
Для автоматического создания функторов, парсящих ваши логи, есть магическая функция

```(python)
converters = infer_converters(
     table=intermediate_timesorted_table,
     categorical_factors=CATEGORICAL_FACTORS,
     realvalue_factors=REALVALUE_FACTORS,
     unravelled_categorical_factors=[],
     yt_client=yt_client
)
```

Вам нужно сгруппировать свои фичи по трем группам:
* ```categorical_factors``` - это могут быть колонки типов int, List[int], List[List[int]]. Будет проинтерпретирована как последовательность айдишников для кат фичи. Последняя размерность сворачивается как BoW
* ```realvalue_factors``` - могут быть колонки int, List[int], List[List[int]], double, List[double], List[List[double]]. Будет проинтрепретирована как просто тензор
* ```unravelled_categorical_factors``` - тоже категориальные фичи, но последняя размерность разворачивается в последовательность, а не в BoW

тут лучше всего будет рассмотреть пример

| BannerID | BannerText | BannerTextUnravelled | SearchQueryHistory | SearchQueryFeatures |
| ---- | ---- | ---- |
| ```124```| ```[67, 1937, 478]``` |  ```[67, 1937, 478]```| ```[[689, 1567, 398], [2176], [19, 79]]``` | ```[[0.1, 0.2], [0.3, 0.4], [0.5, 0.6]]``` |
| ```456```| ```[76, 197]``` | ```[76, 197]``` | ```[[], [1, 2, 3, 4, 5, 6], [81, 9387]]``` | ```[[1.1, 1.2], [1.3, 1.4], [1.5, 1.6]]``` |
| ```null```| ```[93, 2, 5, 6, 7, 1]``` | ```[93, 2, 5, 6, 7, 1]``` | ```null``` | ```null``` |

Варить будем вот так

```(python)
converters = infer_converters(
     table=intermediate_timesorted_table,
     categorical_factors=["BannerID", "BannerText", "SearchQueryHistory"],
     realvalue_factors=["SearchQueryFeatures"],
     unravelled_categorical_factors=["BannerTextUnravelled"],
     yt_client=yt_client
)
```

На выходе получим следующие категориальные фичи:
```(python)
{
        "BannerID": {
            "data":     np.array([124, 456]),
            "data_len": np.array([1, 1, 0])
        },
        "BannerText": {
            "data":     np.array([67, 1937, 478, 76, 197, 93, 2, 5, 6, 7, 1]),
            "data_len": np.array([3, 2, 6]),
        },
        "BannerTextUnravelled": {
            "data":     np.array([67, 1937, 478, 76, 197, 93, 2, 5, 6, 7, 1]),
            "data_len": np.array([[1, 1, 1, 0, 0, 0], [1, 1, 0, 0, 0, 0], [1, 1, 1, 1, 1, 1]]),
        },
        "SearchQueryHistory": {
            "data":     np.array([689, 1567, 398, 2176, 19, 79, 1, 2, 3, 4, 5, 6, 81, 9387]),
            "data_len": np.array([[3, 1, 2], [0, 6, 2], [0, 0, 0]]),
        },
        "SearchQueryFeatures": {
            np.array([
                [[0.1, 0.2], [0.3, 0.4], [0.5, 0.6]],
                [[1.1, 1.2], [1.3, 1.4], [1.5, 1.6]],
                [[0.0, 0.0], [0.0, 0.0], [0.0, 0.0]],
            ])
        }
    }
```

Как вы уже наверняка знаете из предыдущих туториалов, после BaseEmbeddingModel эти фичи превратятся в тензоры таких размерностей
```(python)
{
        "BannerID": [3, 10],
        "BannerText": [3, 20],
        "BannerTextUnravelled": [3, 6, 20],
        "SearchQueryHistory": [3, 3, 20],
        "SearchQueryFeatures": [3, 3, 2]
}
```

Отметим, что в данном примере рассматривается именно фабрика ```infer_converters```, которая по схеме таблице выводит вам правильные обработчики. Обработчики (конвертеры) - это [абстракции](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/lib/pool/formatter/converter.h?rev=r7983364#L39) вида "принимаю минибатч строчек из Ытя и отдаю сколько-то именованных тензоров". Однако, если вам зачем-то понадобилось в этом разбираться и вы пишете свой конвертер, вы с вероятностью 1 делаете что-то странное. Пожалуйста, пользуйтесь ```infer_converters```, либо напишите нам в сложных ситуациях - мы подскажем.

### Структурирование данных внутри батча. Групповые лоссы
Часто возникает ситуация, когда нужно объекты обучающей выборки группировать вместе и подавать в лосс-функции с группами
Сейчас есть возможность указать колонку типа int, по которой данные будут сортироваться внутри батчевалки, такая колонка подается в аргумент ```pivot_column``` (даже не спрашивайте, почему мы взяли именно такое название). Сортированность по значениям этой колонки означает, что в минибатче элементы одной и той же группы будут идти подряд, что значительно упрощает работу с групповыми лоссами.

Также дается гарантия, что одни и те же значения pivot_column не будут разрезаны между батчами. Если какая-то группа не влезает целиком в батч, размер батча будет расширен и группа целиком туда попадет. Поэтому, когда вы указываете pivot_column, фактический размер батча будет всегда ```>= batch_size```.

### Полный пример запуска
```(python)
import yt.wrapper as yt
from ads.pytorch.lib.online_learning.preprocess import (
    map_date_field,
    format_ads_pytorch_input_table
)
from ads.pytorch.lib.pool.py_formatter import SkiffTensorSerializer
from ads.pytorch.lib.preprocess.converter import *  # noqa
from ads.pytorch.lib.pool.py_formatter.inference import infer_converters
import os
from ads.libs.yql import get_yql_client


CATEGORICAL_FACTORS = [
    # Однозначные кат фичи, представлены как int
    "ShowTime",
    "HitLogID",
    "BannerID",
    "OrderID",

    # Многозначные кат фичи, представлены как int
    "BannerTextTokenLemma",
    "BannerTitleTokenLemma",
    "LandingPageTitleTokenLemma",
    "BannerURLParsed",
    "LandingURLParsed"
]


REALVALUE_FACTORS = [
    # int
    "IsClick",

    # List[double]
    "CountersAggregatedValues",

    # List[List[double]]
    "BigBQueryFactors",
]

if __name__ == '__main__':
    yql_client = get_yql_client()
    yt_client = yt.YtClient(token=os.environ["YT_TOKEN"], proxy="hahn")
    yt_pool = "ads-research"

    batch_size = 1024
    src_tables = ["//home/ads/users/alxmopo3ov/bigkv/AdGroupProfile_RSYA_2021-02-16_2021-02-24_parsed_prof"]
    intermediate_timesorted_table = "//home/ads/users/alxmopo3ov/bigkv/AdGroupProfile_RSYA_2021-02-16_2021-02-24_parsed_prof_intermediate2"
    torch_table = "//home/ads/users/alxmopo3ov/bigkv/train_data/ad_group_key_phrases_mb_{}".format(batch_size)

    pivot_column = "HitLogID"

    if not yt.exists(intermediate_timesorted_table, client=yt_client):
        # 1. Варит два поля: _online_learning_date и _online_learning_date_granular
        #    _online_learning_date_granular - это та самая колонка с учетом granularity
        #    по которой мы потом будем редьюсить
        # 2. Сортирует по (_online_learning_date_granular, _online_learning_date) если нет pivot_column;
        #    в противном случае по (_online_learning_date_granular, pivot_column)
        #    Не делаем сортировку по (_online_learning_date_granular, _online_learning_date, pivot_column),
        #    так как в "плохих" сценариях группы будут просто уничтожены
        map_date_field(
            yql_client=yql_client,
            src_table=src_tables,
            result_table=intermediate_timesorted_table,
            time_field="ShowTime",
            yt_pool=yt_pool,
            # !!!! ВАЖНО !!!!
            # Сейчас granularity должен быть делителем 3600
            # В будущем пофиксим и разрешим произвольные значения
            granularity=300,
            pivot_column=pivot_column
        )

    converters = infer_converters(
        table=intermediate_timesorted_table,
        categorical_factors=CATEGORICAL_FACTORS,
        realvalue_factors=REALVALUE_FACTORS,
        unravelled_categorical_factors=[],
        yt_client=yt_client
    )

    print(converters)

    # Варит итоговую таблицу с сериализованными pytorch тензорами
    format_ads_pytorch_input_table(
        serializer=SkiffTensorSerializer(),
        yt_client=yt_client,
        yt_pool=yt_pool,
        src_table=intermediate_timesorted_table,
        result_table=torch_table,
        converters=converters,
        batch_size=batch_size,
        pivot_column=pivot_column,
        cpp_backend=True  # ДОЛЖЕН быть True, False - легаси, до конца не отпилили
    )
```

## Использование нескольких таблиц в обучении
Начиная с некоторого момента, ваши логи для обучения становятся **настолько толстыми**, что джойн и добавление любой мелкой фичи к ним занимает по 3+ дня и годы вычислений в YT. Чтобы решить эту проблему, есть два механизма:
1. Сджойнить таблицы при варке в тензорный формат, а не заранее (экономит джойн сырых логов, но все равно больно)
2. Джойнить батчи разных тензорных таблиц прямо во время обучения

### Идеальный inner join
... является главным и единственным требованием по **обоим** пунктам.

Главная причина такой жесткости в том, что с помощью неаккуратного джойна можно легко получить $[0; +\infty)$ % метрик за счет хитрой утечки таргета (классика жанра - фича не джойнится к кликам при определенных условиях). Из-за этого мы требуем, чтобы пользователь сам свои фичи приджойнил к множеству событий, на которых происходит обучение, а нам осталось только склеить сортированные потоки.
В случае любых непроджойнов у пользователя будет возможность подебажить джойн в YT с помощью привычных инструментов вроде YQL, а не лезть в кишки C++ парсера, пытаясь разобраться где что пошло не так.

### Джойн таблиц при варке в тензорный формат
Пример - вместо тысячи слов. **Обратите внимание** на наличие stability_column и на комментарий к ней.

```python
def page_imps():
    table = "//home/ads-deep-learning/pageimps_2021-08-01_2021-10-28"
    converters = infer_converters(
        table=table,
        categorical_factors=[
            "PageID",
            "ImpID",
            "PageImp"
        ],
        realvalue_factors=[],
        unravelled_categorical_factors=[],
        yt_client=yt_client
    )
    return TableConfig(table=table, converters=converters)


def l1_targets():
    table = "//home/ads-deep-learning/l1_targets_2021-10-02_2021-10-28"
    converters = infer_converters(
        table=table,
        categorical_factors=[
            'EventTime',
        ],
        realvalue_factors=[
            'ABConversionCostCoef',
            'BidCorrection',
            'EventCost',
            'RealCost',
        ],
        unravelled_categorical_factors=[],
        yt_client=yt_client
    )
    return TableConfig(table=table, converters=converters)


if __name__ == '__main__':
    yt_client = yt.YtClient(token=os.environ["YT_TOKEN"], proxy="hahn")
    table_configs = [
        page_imps(),
        l1_targets()
    ]

    format_ads_pytorch_input_table(
        serializer=SkiffTensorSerializer(),
        source_table_configs=table_configs,
        yt_client=yt_client,
        yt_pool="ads-research",
        result_table="//tmp/torch_result_path",
        batch_size=1024,
        pivot_column="HitLogID",
        # For ads users: pay attention on additional stability column.
        # All tables are sorted by three columns:
        # _online_learning_date_granular, HitLogID, BannerID
        # This makes sorted order unique for any ad events log
        # If you don't use multitable data preparation, stability_column is not needed
        stability_column="BannerID",
        date_field="_online_learning_date_granular",
        cpp_backend=True,
        memory_limit=20
    )
```

### Джойн таблиц в обучении
<span style="color: red">!!!UPD от 2022.06.08: сейчас джойн таблиц во время обучения НЕ РАБОТАЕТ. Будет работать, когда ads_pytorch переедет на новую читалку из YT!!!</span>

Во **всех** таблицах должны быть указаны списки таргетов. Список фичей разрешается не указывать в **одной таблице** - тогда он попытается заинферить список фичей из фабрики модели из метода ```get_required_features_list``` и будет брать из этой таблицы все фичи, которые не были перечислены явно в других таблицах.

**ВАЖНО**: джойн в обучении делается **побатчово**. Это значит, что все батчи во всех тензорных таблицах должны быть одинакового размера и должны джойниться 1к1 к батчам другой таблицы. Звучит сложно, но на практике надо всего лишь

```json
{
    "evaluation": {
        "eval_confs": [
            {
                "name": "is_click_train",
                "merge_tables": {
                    "merge_keys": [
                        "HitLogID",
                        "BannerID"
                    ],
                    "tables": [
                        {
                            "table": "//home/ads/users/alxmopo3ov/pytorch_tensor_tables/multitarget_torch_train_mb1024_202108010000_202110010000",
                            "targets": [
                                "HitLogID",
                                "IsClick",
                                "GG",
                                "IsNotNullGG",
                                "ABConversionCostCoef",
                                "BidCorrection",
                                "EventCost",
                                "RealCost"
                            ],
                            "keys": [
                                "HitLogID",
                                "BannerID",
                                "ShowTime"
                            ]
                        },
                        {
                            "table": "//home/ads-deep-learning/pytorch_tensor_tables/pageimps_1024_202108010000_202110250000",
                            "features": [
                                "PageID",
                                "ImpID",
                                "PageImp"
                            ],
                            "targets": []
                        }
                    ]
                },
                "datetime_format": "%Y%m%d%H%M",
                "start_date": "202108050000",
                "end_date": "202110010000",
                "shifts": [
                    24
                ],
                "max_memory": 62949672960
            }
        ]
    },
    "train_data": {
        "merge_tables": {
            "merge_keys": [
                "HitLogID", "BannerID"
            ],
            "tables": [
                {
                    "table": "//home/ads/users/alxmopo3ov/pytorch_tensor_tables/multitarget_torch_train_mb1024_202108010000_202110010000",
                    "targets": [
                        "HitLogID",
                        "IsClick",
                        "GG",
                        "IsNotNullGG",
                        "ABConversionCostCoef",
                        "BidCorrection",
                        "EventCost",
                        "RealCost"
                    ]
                },
                {
                    "table": "//home/ads-deep-learning/pytorch_tensor_tables/pageimps_1024_202108010000_202110250000",
                    "features": [
                        "PageID",
                        "ImpID",
                        "PageImp"
                    ],
                    "targets": []
                }
            ]
        },
        "datetime_format": "%Y%m%d%H%M",
        "start_date": "202108040000",
        "end_date": "202110010000"
    }
}
```

* ```merge_keys``` - список ключей, по которым будем джойнить батчи

Каждая из этих таблиц может быть сварена обычным кодом подготовки выше (возможно, с использованием неск таблиц и джойном в одну тензорную).

## Как запускать обучение
### Настройка ```.vhrc```
Чтобы пайплайн хорошо работал из коробки, стоит завести себе волшебный файлик [vhrc](https://a.yandex-team.ru/arc/trunk/arcadia/nirvana/valhalla/docs/reference/about/vhrc.md).

Чтобы все хорошо работало, надо написать примерно такой конфиг:
```
--oauth-token <<YOUR_NIRVANA_OAUTH_TOKEN_VALUE>>
--secret=alxmopo3ov_nirvana_token=<<YOUR_NIRVANA_OAUTH_TOKEN_VALUE>>
--secret=alxmopo3ov_yt_token=<<YOUR_YT_TOKEN_VALUE>>
--secret=alxmopo3ov_sandbox_token=<<YOUR_SANDBOX_OAUTH_TOKEN_VALUE>>
--project=pytorch_online_learning
--yt-token <<YOUR_YT_TOKEN_VALUE>>
--quota=ads
--yt-proxy hahn
--yt-pool ads-research
--yt-token-secret alxmopo3ov_yt_token
-j 30
--api-retries 10000
--api-retry-delay 2
--api-retry-delay-multiplier 1.1
--verbose
```

Только просьба заполнить все своими настройками, от начала до ```-j 30```. Все что после, оставьте как есть.
### Бинарь для запуска
https://a.yandex-team.ru/arc/trunk/arcadia/junk/alxmopo3ov/ad_online_and_metric_eval - финальный запускаемый пример

**ВАЖНО**: стрипайте бинарь перед запуском, иначе могут быть проблемы с отгрузкой бинарника в Нирвану. Можно делать двумя способами:

1. ```ya make -r && strip ./ad_online_and_metric_eval```
2. ```ya make -r -DSTRIP=yes```


## Как запускать локально
Локальный запуск нужен, чтобы быстро подебажить обучение. Как правило, 90% простых багов в модели падают сразу и их можно отловить быстрым запуском.

### Устанавливаем окружение
1. Ставим компилятор
```
apt-get install -y --force-yes g++-8
export CXX=/usr/bin/g++-8  # or update-alternatives, if you have your own container
```
2. Устанавливаем anaconda3 со свежим 3-м питоном
3. Устанавливаем следующие библиотеки в pip конды
```
pip install torch aiohttp uvloop requests tqdm termcolor numpy brotli tensorboard pyyaml jsonschema
pip install -i https://pypi.yandex-team.ru/simple/ yandex-yt
pip install -i https://pypi.yandex-team.ru/simple/ yandex-yt-yson-bindings

```
4. Устанавливаем ninja в анаконду
```
wget https://github.com/ninja-build/ninja/releases/download/v1.8.2/ninja-linux.zip
unzip ninja-linux.zip
mv ninja $PWD/anaconda3/bin/ninja
```
5. Проставляем все пакеты из ads/pytorch/packages в ```PYTHONPATH```, чтобы локальный дебаг работал. Ну и всякую всячину для сборки C++. Как-то так:

```shell script
# necessary for ads/pytorch/packages/cpp_extension_tools to build arcadia code via ya.make
export ARCADIA_ROOT=$HOME/arcadia

# to import packages from arcadia without installing them in virtualenv
export PYTHONPATH=$ARCADIA_ROOT/ads/pytorch/packages/ads_pytorch:$ARCADIA_ROOT/ads/pytorch/packages/dynamic_isometry:$ARCADIA_ROOT/ads/pytorch/packages/offline_learning_v1:$ARCADIA_ROOT/ads/pytorch/packages/deploy:$ARCADIA_ROOT/junk/alxmopo3ov/bsdev_78621/bsdev_78261_architectures:$ARCADIA_ROOT/ads/pytorch/packages/densenet_tsar_query_attention:$ARCADIA_ROOT/ads/pytorch/packages/densenet_tsar_query_attention_v2:$ARCADIA_ROOT/ads/pytorch/packages/ltp:$ARCADIA_ROOT/dj/research/pytorch_dssm/pytorch_cpp:$ARCADIA_ROOT/dj/torch/djtorch:$ARCADIA_ROOT/ads/yacontext/lib/dssm/train:$ARCADIA_ROOT/ads/pytorch/packages/avazu_online_learning:$ARCADIA_ROOT/ads/pytorch/packages/pytorch_embedding_model:$ARCADIA_ROOT/ml/tensorflow/models/userbert:$ARCADIA_ROOT/ads/pytorch/packages/cpp_extension_tools:$ARCADIA_ROOT/ads/pytorch/packages/ads_pytorch_unitednn

export ADS_PYTORCH_BUILD_DIR=$HOME/torch_build_dir
export PYTORCH_EMBEDDING_PYTHON_INCLUDE_PATH=$HOME/anaconda3/include/python3.9  # !! replace with your anaconda !!
export CACHED_CPP_EXTENSION_BUILD_DIR=$HOME/nonarc_build_cache
export TORCH_EXTENSIONS_DIR=$HOME/torch_extensions_dir
```

6. (временный фикс) Свежий ```yt.wrapper``` из pip не дружит со свежим brotli. Можно удалить ```brotlipy``` из анаконды и все заработает. Падает примерно вот так
```(python)
File "/home/alxmopo3ov/anaconda3/lib/python3.8/site-packages/yt/wrapper/common.py", line 295, in forbidden_inside_job
    return func(*args, **kwargs)
File "/home/alxmopo3ov/anaconda3/lib/python3.8/site-packages/yt/wrapper/http_driver.py", line 254, in make_request
    data = get_compressor(content_encoding)(data)
File "/home/alxmopo3ov/anaconda3/lib/python3.8/site-packages/yt/wrapper/compression.py", line 53, in get_compressor
    return _CODECS[codec_name]()
File "/home/alxmopo3ov/anaconda3/lib/python3.8/site-packages/yt/wrapper/compression.py", line 69, in _create_brotli_compressor
    return _Compressor(inner_compressor.process, inner_compressor.finish)
AttributeError: 'Compressor' object has no attribute 'process'
```
7. Смотрим настройки shared memory  ```sysctl -a | grep shm```. Если ее мало, прописываем в ```/etc/sysctl.conf```
```
# blah-blah-blah, cropped
kernel.shmall=18446744073692774399
kernel.shmmax=18446744073692774399
kernel.shmmni=4096
```
8. Убираем лимит открытых файлов. Каждый блоб в /dev/shm имеет свой файловый дескриптор, и их в обучении может быть много. ```cat /etc/security/limits.conf```
```
# bla-bla-bla, output is cropped
# Increase limit of open files to train PyTorch
alxmopo3ov hard nofile 165536
alxmopo3ov soft nofile 165536
```
проверить можно командой ```ulimit -n```


### Команда запуска
```ADS_PYTORCH_BUILD_DIR=~/torch_build_dir/ python ~/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/nirvana/wrapper.py ./script.py --files model_config=./config.json --entry_point ads_pytorch.yt.online_learning_entry_point```

Что тут происходит?
1. ```ADS_PYTORCH_BUILD_DIR``` - сюда будут высыпаться артефакты сборки C++ кода библиотеки
2. ```~/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/nirvana/wrapper.py``` - специальная обертка над любым скриптом, проводящая общую настройку
