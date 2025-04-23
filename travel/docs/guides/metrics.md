---
title: Работа с метриками
---

## Цель

Декларировать общие подходы к работе с техническими метриками в рамках Путешествий.
Предметы унификации:
  - бэкенд (используем [Solomon tool](https://docs.yandex-team.ru/travel/ops/tools/solomon_tool) ) 
  - таксономия метрик
  - решения для сбора метрик
  - утилиты для конфигурирования

## Минимальный набор метрик и алертов

Кроме здравого смысла - наборы метрик основаны на:
 - [RED](https://www.weave.works/blog/the-red-method-key-metrics-for-microservices-architecture/).
 - [Four Golden Signals (by google)](https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/)

### Общие принципы определения необходимости алерта

(перевод из статьи Four Golden Signals)

При заведении нового правила для мониторинга имеет смысл ответить на следующие вопросы. Это позволит снизить количество false positives и, как следствие pager burnout.
  - Определяет ли это правило какое то, ранее не определяемое, состояние, которое является: срочным, видимым (сейчас или в скором времени) пользователям? И есть ли возможность предпринять какие то действия по этому поводу?
  - Можем ли мы при каких бы то ни было условиях проигнорировать этот алерт? Когда и почему мы можем проигнорировать этот алерт?    
  - Определяет ли этот алерт, что пользователи ТОЧНО страдают? Есть ли какие то ситуации (определимые), в которых пользователи не пострадают?
  - Есть ли какие то действия, которые мы можем предпринять в качестве реакции на алерт? Являются ли эти действия срочными или могут подождать до утра? Можно ли их автоматизировать? Если можно - будет это долговременное решение или временный костыль-подорожник?
  - Будут ли уведомлены об инциденте другие люди (кроме непосредственно ответственного)?

И из этих вопросов следует фундаментальная философия уведомлений:
  - Каждый раз, когда ответственный получает уведомление, он должен быть способен отреагировать на него, причем срочно. Но при этом человек может оперативно реагировать всего лишь несколько раз в день. Если событий больше - он скорее всего устанет.
  - Каждое уведомление должно быть actionable.
  - Каждое уведомление должно требовать человеческих мозгов. Если это не так - уведомления не должно быть вовсе.
  - Каждое уведомление должно подсвечивать новую проблему, т.е. не должно быть дублирующихся уведомлений.


### Общий набор

Все метрики с аггрегацией по DC.


| Метрика | Мониторинг | Комментарий |
|---------|------------|-------------|
| Потребляемая память | да | Мониторинг выставляем по trashold от общей памяти (~80%) |
| CPU | нет | |
| Диск | да | Мониторинг выставляем по trashold от общей емкости диска (~80%) |
| Количество живых инстансов | да | trashold - зажигаем если осталась 1/3 или меньше от общего числа инстансов |

### http service

Все метрики с аггрегацией по DC.

| Метрика | Мониторинг | Комментарий |
|---------|------------|-------------|
| rps общий | нет | |
| rps 200 Ok | нет | |
| rps 3xx | нет | |
| rps 4xx | нет | |
| rps 5xx | да | % от успешных |
| timeouts | да | % от успешных, но пока не понятно как мерять без nginx |
| timings | да | 90/95/99 квантили |

### grpc service

Все метрики с аггрегацией по DC.

| Метрика | Мониторинг | Комментарий |
|---------|------------|-------------|
| rps общий | нет | |
| rps успешных ответов | нет | |
| rps ошибок | да | % от успешных |
| timings | да | 90/95/99 квантили |

### background task

Какая то задача, запускающаяся по cron'у - разовому событию.
  - факт запуска
  - факт успешного завершения
  - факт ошибок

### event/task/job queue

Приложение, которое слушает некую очередь и обрабатывает приходящие события / задания.
Все метрики с аггрегацией по DC.

| Метрика | Мониторинг | Комментарий |
|---------|------------|-------------|
| длина очереди | да | |
| количество публикуемых сообщение | нет | |
| количество подтвержденных сообщений | нет | |
| количество inflight | нет | |
| длина dead-letter queue | да |  |
| latency обработки сообщений | нет | 75/90/95/99 квантили |

## Таксономия метрик

В терминах Solomon метрика описывается следующими аттрибутами.

**project**
Проект в solomon - некая логическая сущность, объединяющая метрики относящиеся к терминам условно одной команды. 
Например:
  * https://solomon.yandex-team.ru/admin/projects/rasp/
  * https://solomon.yandex-team.ru/admin/projects/travel/
  * https://solomon.yandex-team.ru/admin/projects/trains/
Предполагается гранулярность проектов в соответствии с направлениями: rasp/trains/buses/hotels/avia. 
Наличие общего проекта travel не очень вписывается в эту схему, но можно приближенно считать что travel=hotels+orders.

**service**
Сервис это в общем случае некий executable. Например если мы имеем сервис offer_storage, то ему должен соответствовать сервис offer_storage (предлагается именовать проекты так же, как в Аркадии).

Исключения:
  - python проект со сбором метрик через nginx. Тогда сервис для сбора nginx_logs метрик должен называться {service_name}_nginx
  - системные метрики (cpu/mem/etc). {service_name}_sys (или sys ?)
  - sandbox - здесь сервис называется sandbox

**cluster**
Это совокупность машин (контейнеров), на которых запускается service. Обычно каждому сервису соответствует как минимум два кластера: testing/production.
Пример кластеров для сервиса offer_storage:
offer_storage_production
offer_storage_testing

Почему не использовать один общий кластер production на все сервисы?
Во первых из-за того, что в solomon есть понятие шард и шард это сервис+кластер. И существует ограничение <[рекомендуется в одном шарде количество метрик < 1000000. Если вы хотите превысить это количество, то нужно обращаться к команде Соломона;]> (см [тут](https://wiki.yandex-team.ru/solomon/userguide/metricsnamingconventions/#kolichestvometrik) ).
Во вторых - в случае если мы скидаем все сервисы в один кластер - появится риск забыть добавить окружение нового сервиса в этот кластер.

**sensor**
Имя сенсора. Это строка определяющая тип метрик.
При определении имени сенсора рекомендуется использовать пространства имен.
Пример:
```
grpc.errors_count
app.billing.errors_count
```

Подробнее про именование метрик: https://wiki.yandex-team.ru/solomon/userguide/metricsnamingconventions/#names

**tags**
Это произвольные метки, по которым можно выбирать и/или аггрегировать метрики. 

## Решения для сбора метрик

### python

Сбор метрик осуществляется через solomon-agent. 
Для сбора http метрик используется соответствующие модули:
  - https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/library/docker/docker_images/base/solomon/modules/nginx_log_parser.py
  - https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/library/docker/docker_images/base/solomon/modules/nginx_log_normalize_functions.py

Для сбора произвольных application метрик следует использовать [Solomon PUSH API](https://wiki.yandex-team.ru/solomon/api/push/#python). Над ним есть [библиотека](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/solomon).
``TODO:`` Примеры, возможно более высокоуровневая библиотека, аналог [deprecated yasmutil](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/library/python/common/utils/yasmutil.py).

**deprecated**
Для сбора кастомных метрик используется https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/infra/tools/unistat_aggregator в который из кода можно ходить так: https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/library/python/common/utils/yasmutil.py


**

### go

В go все метрики должны собираться напрямую из приложения (не используем nginx). 
Библиотека:
  - базовая https://a.yandex-team.ru/arc/trunk/arcadia/library/go/core/metrics
  - набор хэлперов поверх базовой: https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/go/metrics
  - для grpc: https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/go/grpcutil/metrics

В схеме может участвовать solomon-agent в том случае, если необходимо собирать системные метрики.

## Утилиты для конфигурирования

**Для конфигурирования графиков, дашбордов и алертов в solomon** 
solomon-tool.
Утилита: https://a.yandex-team.ru/arc/trunk/arcadia/travel/devops/solomon
Пример конфигов: ((https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/solomon раз)) и ((https://a.yandex-team.ru/arc/trunk/arcadia/travel/trains/devops/solomon два))

**Для конфигурирования алертов в juggler**
Для создания проверок в juggler на данный момент используется sandbox задача ANSIBLE_JUGGLER.
Конфиги testenv: 
https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/rasp/ApplyJugglerChecksRasp.yaml
https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/rasp/ApplyJugglerChecksTrains.yaml
Конфиги juggler: 
https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/trains/configs/juggler
https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/configs/juggler

**deprecated утилита для конфигурирования solomon алертов**
Утилита deprecated потому что не поддерживает custom чеки и не умеет конфигурировать графики и дашборды. В отличие от solomon-tool.
Код утилиты: https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/infra/tasks/solomon/alert_updater.py
Код sb задачи: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/rasp/infra/GenerateAlerts
Конфиги:
https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/configs/solomon
https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/trains/configs/solomon
