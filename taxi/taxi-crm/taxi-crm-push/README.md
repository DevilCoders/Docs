# Каналы коммуникаций в Нирване и realtime_notifications*

https://github.yandex-team.ru/eantyshev/realtime-notifications

## Описание и архитектура
Асинхронные сервисы для отправок разных коммуникаций: пуши, смс, Лента, пр.
(channel/base.py:AsyncSender)
Поддерживаются batch ручки для coupons, Ленты (channel/base.py:BatchSender)
(в этом случае только один запрос выполняется в конкретный момент)
могут запускаться в качестве сервиса, тогда входные данные поступают
по ZMQ порту в виде потока json объектов (services/push_service.py).
Второй вариант: one-shot процесс в окружении Нирваны,
читает входные данные из YT таблицы.
Результаты отправки сохраняются либо в YT либо в PG (log).
Чтение входных данных, отправка и логгирование в таблицу
являются корутинами, обрабатывающих локальную очередь событий (а-ля каналы Го)
В случае терминальной ошибки в любой точке
чтение и отправка прекращаются, уже сделанные отправки логгируются.

## Артефакты и процессы в Нирване

Операция состоит из описания входов, выходов и параметров:
в частности, скрипта запуска и porto слоя с окружением и кодом проекта.
Все операции и слои имеют семантическое версионирование, главное правило состоит в том,
чтобы увеличивать PATCH каждый раз при обновлении 
параметров, скрипта-обертки или базового слоя. 

### pg2yt
Операция для перекладывания лога отправок из PG на YT Hahn.
Запущена через hitman cron в 2х экземплярах для пользователей и водителей.  
[операция](https://nirvana.yandex-team.ru/operation/4d1f1a36-89d5-4e34-bc8f-738d458ce65d)

[исходный граф](https://nirvana.yandex-team.ru/flow/afa758a6-4dcd-4e09-a3ee-aa8983459f20/d2ec7b8d-e526-47bc-8d2f-03fdd85b9a23/graph)

Проекты в Hitman (cron сервис для запуска графов)
[user_push_pg2yt](https://hitman.yandex-team.ru/projects/realtime_notifications_logging/user_push_pg2yt)  
[driver_push_pg2yt](https://hitman.yandex-team.ru/projects/realtime_notifications_logging/driver_push_pg2yt)

## Базовый porto образ и обновление операций

Указывается в job-layer параметрах операций.  
При изменении исходников, котрые используются в операции,
следует склонировать последнюю актуальную операцию, обновить версию
и сделать предыдущую deprecated (такой слой может продолжать 
использоваться в других операциях, все операции обновлять необязательно).
Последняя версия: 1.4.10  
[taxi-crm-push 1.4.10](https://nirvana.yandex-team.ru/layer/e8d9554b-5a8f-4986-9197-7d6660876ca3)

## Актуальные операции
* [driver_push 1.4.10](https://nirvana.yandex-team.ru/operation/77c3b56f-fe67-41dc-846d-cf395af20950/overview)
* [promotions 1.4.8](https://nirvana.yandex-team.ru/operation/14000dce-9e85-415b-8d3a-eb9c6eea2528) *с поддержкой YQL сегмента*
* [promotions 1.4.5dev](https://nirvana.yandex-team.ru/operation/d111ee9d-8574-43e7-adf9-77cce1c858f3)
* [taxi_upload 1.4.8](https://nirvana.yandex-team.ru/operation/973369b2-2eee-454f-8558-dee3c5204986)
* [taxi_exp 1.4.6](https://nirvana.yandex-team.ru/operation/f4ad4dd7-241e-435a-9663-5019264e1998)
* [coupons_activate 1.4.4](https://nirvana.yandex-team.ru/operation/0e9eadd9-d922-4c1c-ab3b-ed62c95b7c66)
* [pg2yt 1.4.1](https://nirvana.yandex-team.ru/operation/4d1f1a36-89d5-4e34-bc8f-738d458ce65d)
* [user_push 1.3.0](https://nirvana.yandex-team.ru/operation/c6612248-58a6-4407-a26d-e6752f5e0322)
* [taximeter_wall 1.2.10](https://nirvana.yandex-team.ru/operation/9e97ab97-87f5-4553-afef-0eb9178a1c5b)

## Операции с кодом вне этого репозитория
эти операции были созданы очень давно и основаны на небольшом
скрипте поверх слоя по умолчанию. Они просто работают и почти
не нуждаются в поддержке. Некоторые даже внесены в библиотеку Нирваны.
Если код операции существует в git ссылка указана в её описании.

* [YT cleanup old tables 2.0](https://nirvana.yandex-team.ru/operation/3c7cb2f5-163e-4e43-b7a6-095759726ba0) очистка поддерева в YT
* [MR YQL from Jinja2 template 1.2.1](https://nirvana.yandex-team.ru/operation/6679bbc8-8a73-4be5-a3bb-5fb238c8585a)
* [YQL validate and share 1.0](https://nirvana.yandex-team.ru/operation/446da597-c582-437b-a68c-f6f9817a1172) *вспомогательная, идея Ильи Торчинского*
* [Download YQL operation info by id|url](https://nirvana.yandex-team.ru/operation/a73441be-85c7-42c9-bc44-589a3e31c95b)
* [drivers sms 0.0.3](https://nirvana.yandex-team.ru/operation/3f5b3402-4c09-4268-8e4c-eca654076640)