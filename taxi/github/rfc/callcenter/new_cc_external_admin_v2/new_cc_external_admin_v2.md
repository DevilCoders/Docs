# Переход на метаочереди в интерфейсах

## Основная цель
- Удаление сабкластеров из отчетов и админки управления операторов
- Создание базовых ручек, отдающих информацию об очередях (тэги, имя, номер, привязки к сабам)

## Доработки по разделам

### Новая ручка /cc/v1/callcenter-queues/v1/system/list
Отдает информацию по метаочередям внешним потребителям (пр. новой админке).
- Имя метаочереди
- тэги метаочереди
- номер метаочереди
- список кластеров метаочереди 

Кластера отдаются в виде обычного списка строк (без доп. информации) и используются для отображения в фильтрах админки и т.д.
На бэке список кластеров формируется исходя из условия {enabled: True} (параметр кластера, отвечающий за "включенность", "видимость").

Ручка имеет фильтр по метаочередям.
Для админки в ручке нужно поддержать опциональное поле проект и завести под каждый проект вычислимый пермишн, который будет проверять проект.

Ручка дергается при запуске админки.

**PS**:  старую ручку */cc/v1/callcenter-queues/v1/system/list* нужно переименовать в *v1/system/list*. Она нужна лишь внутри cc-operators при выводе на очередь. Аналогично можно сразу перименовать другие внутренние ручки.

### Раздел "Звонки"
Ручка /cc/v1/callcenter-stats/v2/calls/history.
Отличие от v1 ручки - принимает фильтр по метаочередям.

### Раздел "Дашборд по очередям"
Ручка /cc/v1/callcenter-stats/v2/statistics/short_term_report
Отличие от v1 ручки - принимает фильтр по метаочередям. Отдает инфо в разбивкой по метаочередям. 
Разбивку по сабкластерам не нужна.

### Раздел "Дашборд по дисциплине"
Ручка /cc/v1/callcenter-stats/v2/dashboards/operators/discipline.
Отличие от v1 ручки - принимает фильтр по метаочередям.

### Раздел "Отчет по часам"
Ручка /cc/v1/callcenter-stats/v2/statistics/hour_report
Отличие от v1 ручки - принимает фильтр по метаочередям. Отдает информацию по метаочередм.
Разбивки по сабкластерам нет.

### Раздел "Задачи операторов"
Ручка /cc/v1/callcenter-stats/v2/statistics/short_term_report (см. выше).

Ручка /cc/v1/callcenter-stats/v2/dashboards/operators.
Принимает фильтр по метаочередям.
Лимиты не меняем.

В этом разделе используется информация из ручки /cc/v1/callcenter-queues/v1/system/list, для списка сабкластеров.

### Раздел "Таймлайн операторов КЦ"
Остается без изменений.

## Пермишены
Пермишены на ручки не меняются. Добавляется несколько новых пермишна под /cc/v1/callcenter-queues/v1/system/list.
Один пермишн для технического проекта, и по 1 пермишну на каждый существующий проект.

**PS**: Нужно добавить новые пермишны в документацию на вики.
***
# Доработки в разделе "Матрица очередей"
- Перейти на ручки v2, где есть фильтр по метаочередям и сабкластерам.
- *Tech duty*: После выпиливания старой балансировки из cc-stats, заполнить конфиг CALLCENTER_METAQUEUES allowed_clusters.
- *Future plans*: Так же в них поддержан проект, чтобы этот раздел можно было размножить из Технического в остальные проекты.

