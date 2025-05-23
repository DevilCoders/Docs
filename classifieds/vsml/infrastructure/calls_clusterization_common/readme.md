# Кластеризация звонков

**Связанные тикеты:** VSML-1002, VSML-1003, VSML-700.

## Файлы

### Ноутбуки

- **notebooks/script_detection.ipynb** - обучение детектора скриптовых звонков, ссылки на данные для обучения лежат в тикете VSML-1002, VSML-1003.

- **notebooks/call_clusterization.ipynb** - ноутбук с кластеризацией, подбор параметров, визуализация.


### Скрипты

- **scripts/call_processing_functions.py** - функции обработки звонков: препроцессинг текста, вычисление расстояний, сбор информации о кластерах.

- **scripts/script_detection.py** - разметка звонков на скриптовость (общение по шаблону, обзвон), принимает на вход таблицу, векторайзер и классификатор (подготовлены в **script_detection.ipynb**), на выходе выдаёт таблицу, размеченную на скриптовость.

- **scripts/call_clustering.py** - кластеризация звонков, принимает на вход таблицу, json с брендами, на выходе выдаёт размеченную таблицу, разметку кластеров, векторайзер.

- **scripts/call_classification.py** - классификация звонков, принимает на вход таблицу, json с брендами, разметку кластеров, векторайзер, на выходе выдаёт размеченную таблицу.


### YQL запросы

- **YQL/collect_calls_for_clustering.yql** - сбор звонков для кластеризации.

- **YQL/collect_calls_for_classification.yql** - сбор звонков для инференса.



# Общее описание алгоритмов

## Кластеризация звонков

**Граф:** https://nirvana.yandex-team.ru/flow/1217c136-6cd2-4d16-b7d9-bec3af7af253/1efedef2-f8fb-4efc-8d79-f41e0199d007/graph

**Реакция:** https://reactor.yandex-team.ru/reaction?id=10536334&mode=instances


### Пайплайн кластеризации

В общих чертах кластеризация происходит следующим образом: 

1. Собираются звонки и транскрипции звонков, они базово фильтруются (не пустые, дольше 10 секунд и т.д.).
2. Полученная MR-таблица переводится в TSV и к ней дописывается **header** (если есть возможность сделать так, чтобы **header** добавлялся автоматически, лучше это сделать).
3. Звонки из таблицы фильтруются на скриптовость/нескриптовость, с помощью бинарников разово положенных в **s3** (обучение модели в ноутбуке **script_detection.ipynb**, модель не переобучается и выборка не очень большая, в этом месте, возможно, стоит что-то сделать).
4. Нескриптовые звонки отсекаются.
5. При кластеризации тексты звонков предобрабатываются: лемматизация, исправление брендов по словарю, копирование брендов в начало текста, обрезание до определённой длинны.
6. Кластеризация происходит с помощью **DBSCAN** по **TI-IDF** векторам. Для **DBSCAN** оптимальный параметр **eps** 0.84-0.88 в этих значениях наилучшие результаты. Я проводил эксперименты с различными параметрами на разных выборках и получилось следующее: для больших выборок (в данном случае 7 дней) данные получаются довольно "шумными" из-за чего кластера начинают "склеиваться", при этом параметр **eps** не помогает, кластера перестают образовываться раньше, чем начинают "расклеиваться"; на небольших выбороках такой проблемы вроде не наблюдается (может зависеть от дней недели). Если придётся уменьшить период кластеризации меньше 3, то стоит отключить перерасчёт кластеров в выходные, чтобы не терять обзвонщиков, которые звонят только по будним дням.
7. По кластерам собирается информация: центроид, [среднее расстояние до центроида, стандартное отклонение в расстояниях,] ключевые слова (слова, которые используются в кластере чаще, чем в среднем по звонкам), имя кластера (проставляется, если среди ключевых слов есть бренд). ([] - не используются на данный момент)
8. По результатам кластеризации в **s3** заливаются её артефакты (информация о кластерах, векторайзер). Текущая версия кластеризации перезаписывается, и дублируется с пометкой версии, для возможности вернутся к старой версии. После этого информация о текущей версии обновляется.


## Классификация звонков

**Граф:** https://nirvana.yandex-team.ru/flow/fa6945ee-f936-49b3-bbfb-9591d1b1f710/137f3089-9bce-4501-b863-abdcd5ec3fc8/graph

**Реакция:** -

Исходные данные: https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/test/warehouse/dust/nirvana_clustering/1h 

Будут появляться чанки данных для теста. Колонки timestamp, id, clustering_payload, clustering_type.

Пример с форматом: https://yql.yandex-team.ru/Operations/Ya3nLlZ1O3Wlf41S8Ib4xZP8nqc53NiZX6oWoedJRMA= 

В проде тоже скоро будут: https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/dust/nirvana_clustering/1h


Результаты: https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/dust/clustering_results 

Складывать результаты кластеризации в поддериктории для теста и прода соответственно. При этом тут нужно использовать cluster_type из input-а (он сейчас везде одинаковый) и писать в папку **../clustering_results/{test/prod}/$cluster_type/**.


### Пайплайн классификации

В общих чертах классификация происходит следующим образом: 

1. Достаётся последняя таблица из папки, из неё отдельно достаётся текст звонка.
2. Полученная MR-таблица переводится в TSV и к ней дописывается **header** (если есть возможность сделать так, чтобы **header** добавлялся автоматически, лучше это сделать).
3. Звонки из таблицы фильтруются на скриптовость/нескриптовость, с помощью бинарников разово положенных в **s3** (обучение модели в ноутбуке **script_detection.ipynb**, модель не переобучается и выборка не очень большая, в этом месте, возможно, стоит что-то сделать).
4. Нескриптовые звонки отсекаются.
5. При кластеризации тексты звонков предобрабатываются (аналогично кластеризации): лемматизация, исправление брендов по словарю, копирование брендов в начало текста, обрезание до определённой длинны.
6. Рассчитывается расстояние до центроидов, если расстояние меньше порога (в ноутбуке получалось, что оптимальный 0.81, но лучше ставить немного больше, до 0.95), то звонок относится к ближайшему кластеру, -1 иначе.
7. Звонкам проставляется информация о кластерах и версии кластеризации.
8. Полученная таблица выгружается в YT.


Более подробно в тикете VSML-1003.
