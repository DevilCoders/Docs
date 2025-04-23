# Оглавление
2. [Общее описание](#general)
1. [Базовые технологии](#base)
1. [YT](#yt)
2. [Рантайм (Sandbox)](#sandbox)
3. [Мониторинги](#monitorings)
4. [Квоты](#monitorings)

## Общее описание { #general }
Данная таска является частью промопроцесса https://docs.yandex-team.ru/marketpromo/components/

Реализует процесс заведения акции через трекер через регулярную sandbox таску.
Робот читает эксельки из тикетов, парсит, валидирует и результат складывает на YT

Очередь для заведения акция для прода https://st.yandex-team.ru/blueaction

Очередь для заведения акция для тестинга https://st.yandex-team.ru/blueactiontest

Слой бизнес логики хранится отдельно:
https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/promos/blue_gift_with_purchase

## Базовые технологии { #base }

**ОБЯЗАТЕЛЬНО К ПРОЧТЕНИЮ**

Рантайм робота - бинарная Sandbox задача
https://docs.yandex-team.ru/sandbox/dev/binary-task

Выполнение кода робота по расписанию
https://docs.yandex-team.ru/sandbox/schedulers

CI/CD
https://docs.yandex-team.ru/ci

Релизы Sandbox ресурсов
https://docs.yandex-team.ru/sandbox/dev/releases

Rollback
https://docs.yandex-team.ru/ci/release#rollback

## YT

Запись осуществляется в таблицы в зависимости от окружения:
- **PROD HAHN**: https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/stratocaster/promos/blue/in
- **PROD ARNOLD**: https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/gibson/promos/blue/in
Запись происходит в оба кластера.

В тестинге ДЦ-1 не поддержан:
- **TESTING ARNOLD**: https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/indexer/stratocaster/promos/blue/in

## Рантайм (Sandbox) { #sandbox }

### Schedulers

Непосредственные запуски робота:
- **TESTING** https://sandbox.yandex-team.ru/scheduler/15697/view
- **PROD**  https://sandbox.yandex-team.ru/scheduler/17417/view

Параметры запуска:
- `binary_executor_release_type` - берём исходники из тестинга (testing) или прода (stable)
- `idx_env` - окружение индексатора, куда кладём целевую табличку
- `yt_table_shopdsdat` - информация о магазинах, связка warehouse_id + supplier_id -> feed_id
- `yt_path_blue_in` - выходная таблица со списком акций
- `shop_id` - _deprecated_
- `st_filter_id` - id фильтра в стартреке для поиска актуальных акций
- `test_run` - тестовый прогон, без записи данных на yt
- `max_items_per_promo` - максимальное количество товаров в акции. Для товар+подарок, комплекты считаются основные и дополнительные товары
- `report_proxy` - ссылка на хост репорта, для формирования ссылки "счётчик" в ответе робота
- `working_threads` - количество потоков обработки парсинга экселек
- `force_update` - пройтись по всем активным акциям, даже если не было изменений

Шедулер устроены таким образом, что ищут ресурс бинарной задачи по двум критериям:
- тип ресурса `testing/stable`
- последний созданный

![image](https://jing.yandex-team.ru/files/eandreyf/binary_type.png)


### Разовый запуск

Зайти в нужный шедулер, нажать **Run Once**

![image](https://jing.yandex-team.ru/files/eandreyf/scheduler_run_once.png)

Для этого необходимо иметь доступ к токенам.

Достаточно состоять в https://abc.yandex-team.ru/services/marketpromo/

Или обратиться к @nickshevr для выдачи персонального доступа

### Остановка запусков

Зайти в нужный шедулер, нажать **Stop**

![image](https://jing.yandex-team.ru/files/eandreyf/scheduler_stop.png)

## Релизный процесс + CI/CD { #release}

### CI билд в PR

При изменении исходного кода робота создается `flow` следующего типа:

https://a.yandex-team.ru/ci/workflow/details/eab3264bd6e8c7f5b9bc6f18ed8bc167aed62f59be3a8b1e9d9d6c0962909457

В PR появляется дополнительная проверка `Build Binary BluePromoGwpXlsParser`

![image](https://jing.yandex-team.ru/files/eandreyf/pr.png)

**Данная проверка необходима должна быть зеленой перед мержом вашего кода в транк**

При нажатии на **details** можно перейти во `flow`:

![image](https://jing.yandex-team.ru/files/eandreyf/flow.png)

`flow` состоит из 3 кубиков:

#### build binary resource

собирает бинарный ресурс вашей задачи, а так же производит тестовый запуск:

- Задача сборки: https://sandbox.yandex-team.ru/task/1075656829/view
- Запущенная задача интеграционного тестирования: https://sandbox.yandex-team.ru/task/1075661679/view

#### resource into testing

Релизит собранный ресурс в `testing`, подробнее читай на https://docs.yandex-team.ru/sandbox/dev/releases

После данного кубика ресурс автоматом подхватится в тестовый шедулер и
тестинг будет работать на коде из вашего ПРа до тех пор, пока:
- его не займет кто-то другой более свежим ресурсом
- вы не нажмете на следующий кубик - `resource rollback`

Для мержа в транк необходимым условием является запуск тестового шедулера с бинарником из вашего `PR`.

#### resource rollback

После запуска шедулера с вашим ресурсом и получением реузльтатов - распубликовываем ресурс.

### Релизный пайплайн

Ознакомиться с интерфейсом `New CI`: https://docs.yandex-team.ru/ci/ui

Ссылка на релизный пайплайн Робота: https://a.yandex-team.ru/projects/marketpromo/ci/releases/timeline?dir=sandbox%2Fprojects%2Fmarket%2Fidx%2FBluePromoGwpXlsParser&id=release-binary-tasks

Релизный пайплайн похож на пайплайн в `CI/CD`, добавляется всего лишь один новый кубик - релиз в престейбл.

Алгоритм релиза:
- проверяем запуск тестового шедулера с вашим ресурсом (стартуем руками)
- деплоим ресурс в `stable`, самостоятельно проверяем функционал
- завершаем релиз

### Rollback

Алгоритм отката:
- выбрать нужный релиз
- нажать на `Rollback to`
- завершить созданный пайплайн (может понадобиться нажать на гендальфов)

![image](https://jing.yandex-team.ru/files/eandreyf/rollback.png)


### Полезные фишки

#### Список задач запущенных с бинарным ресурсом
![image](https://jing.yandex-team.ru/files/eandreyf/sb_tip.png)

#### Найти бинарный ресурс из запуска задачи
![image](https://jing.yandex-team.ru/files/eandreyf/sb_tip2.png)

#### Получить информацию из задачи сборки
![image](https://jing.yandex-team.ru/files/eandreyf/sb_tip3.png)


## Мониторинги { #monitorings }
Общая информация про мониторинги промопроцесса
https://docs.yandex-team.ru/marketpromo/stable/monitorings

Мониторинги работы тасок
https://arcanum.yandex-team.ru/arc_vcs/market/solo_monitorings/marketpromo/registry/alerts/sandbox/robot.py

Мониторинг раскатки релизов https://arcanum.yandex-team.ru/arc_vcs/market/solo_monitorings/marketpromo/registry/alerts/releases/new_ci.py

## Квоты { #quotas }
Общая информация про используемые квоты промопроцесса
https://docs.yandex-team.ru/marketpromo/quotas/

1. Ресурсы sandbox в квоте MARKETPROMO
https://sandbox.yandex-team.ru/admin/groups/MARKETPROMO/general
2. Ресурсы YT в квоте market-indexer-production
