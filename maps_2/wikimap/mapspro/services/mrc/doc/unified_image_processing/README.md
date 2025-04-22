### Введение

##### Уже унифицированные задачи обработки входящих снимков (image_analyzer_yt)

- оценка качества
- оценка ориентации
- нахождение лиц и номерных знаков (сохраняются в отдельной таблице)
- запрещенного контента, road_probability (not null соответствующих полей)

##### Задачи - кандидаты на унификацию (новый сервис)

- проверка требований gdpr
  - [ride_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/process_queue.cpp?rev=r8172207#L256)
- проверка вхождения фотографии в удаленный пользователем интервал
  - [ride_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/process_queue.cpp?rev=r8172207#L271)
- позиционирование снимков и выбор графа
  - [image_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/image_inspector/coverage.cpp?rev=r8172482#L163)
  - [ride_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/process_queue.cpp?rev=r8172490#L145)
- позиционирование по сенсорам
  - [image_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/image_inspector/coverage.cpp?rev=r8172503#L174)
  - [ride_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/process_queue.cpp?rev=r8172503#L155)
- определение camera_deviation
  - [image_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/image_inspector/camera_deviation.cpp?rev=r8172525#L28)
  - [ride_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/process_queue.cpp?rev=r8172525#L118)
- вычисление privacy
  - [image_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/image_inspector/share_images.cpp?rev=r8172552#L58)
  - [ride_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/process_queue.cpp?rev=r8172552#L177)
  - [onfoot-processor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/onfoot-processor/lib/worker.cpp?rev=r8172552#L121)
- принятие решения о публикации
  - [image_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/image_inspector/share_images.cpp?rev=r8172563#L66)
  - [ride_inspector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/process_queue.cpp?rev=r8172563#L184)  
  - [onfoot-processor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/onfoot-processor/lib/worker.cpp?rev=r8172563#L122)

### База данных

##### Изменения в таблице signals.feature

| Column       | Type                     | Nullable |
|--------------|--------------------------|----------|
| processed_at | timestamp with time zone |          |

processed_at:
- NULL -- снимок ожидает обработки новым сервисом
- '1970-01-01' -- legacy снимок
- 'время окончания обработки новым сервисом' -- снимок обработан

```
Indexes:
    "feature_id_not_processed_index" btree (feature_id) WHERE processed_at IS NULL
````

### Последовательность работ

- добавляем поле processed_at в БД
- в существующих сервисах (image_inspector, ride_inspector, onfoot-processor)
    - выполняем задачи для нового сервиса только если ```processed_at == NULL```
    - по окончанию выполнения задач для нового сервиса ставим ```processed_at = now()```
- всем старым снимкам ставим ```processed_at = '1970-01-01'```
- добавляем индекс в БД
- добавляем новый сервис
    - читает снимки по индексу ```WHERE processed_at IS NULL```
    - пропускает снимки на которых еще не отработал image_analyzer_yt
    - выполняет задачи-кандидаты
    - ставит ```processed_at = now()```
- в старых сервисах (image_inspector, ride_inspector, onfoot-processor)
    - удаляем код выполнения задач нового сервиса
    - не обрабатываем снимки пока ```WHERE processed_at IS NULL```
