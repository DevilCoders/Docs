# ZBP Портала

**Оглавление**:
- [Обзор](#обзор)
- [Конфиг сервиса](#конфиг-сервиса)
- [Изменение конфига](#изменение-конфига)
- [Добавление целей на следующий квартал/полугодие](#добавление-целей-на-следующий-квартал-полугодие)
- [Добавление нового сервиса](#добавление-нового-сервиса)
- [Разовый пересчёт](#разовый-пересчёт)

## Обзор

[Дашборд](https://dash.yandex-team.ru/8tq941sqba665)
[ABC-сервис](https://abc.yandex-team.ru/services/portal_zbp_and_stats/)

Сбор ZBP-метрик запускается каждую ночь в 02:00 мск [задачей в Sandbox](https://sandbox.yandex-team.ru/schedulers?owner=PORTAL_STATS&limit=20).

Метрики собираются для сервисов, конфиги готорых находятся в папке `projects`.

## Конфиг серивса

Конфиг сервиса задается в yml-формате:

```yml
name: home                  # код сервиса латинскими буквами
title: Морда                # название сервиса
st_queue: '(
  (Queue: HOME and Tags: !stream) or
  (Queue: ZEN and Assignee: "Denis Sebeldin")
)'                          # фильтр всех тикетов по очереди, компонентам, тегам и т.п.
st_queue_bugs: '(
  (Queue: HOME and Tags: !stream) or
  (Queue: ZEN and Tags: morda, morda_lib)
)'                          # опциональный фильтр для багов
bugs: 'Type: Bug'           # + доп.фильтр багов по типу тикета
tasks: 'Type: Task, Improvement, Bug, Refactoring, "New Feature"'   # доп.фильтр задач
sla_id: 390                 # идентификатор SLA для багов
sla_ids:                    # список идентификаторов SLA,
- 390                       # если сбор идёт по нескольким очередям
- 467
goals:                      # список целей по периодам
-                           # формат: [год-квартал, цифра]
  from: [2019-Q2, 382]      #   на начало Q2 фиксируем CrashID = 382
  to:   [2019-Q2, 272]      #   цель: снизить CrashID до конца Q2 до 272
-
  from: [2019-Q3, 270]      # или
  to:   [2019-Q3, 270]      #   держать CrashID в Q3 не выше 270
-
  from: [2019-Q4, 282]      # или
  to:   [2020-Q1, 232]      #   цель на два квартала
```

Идентификатор SLA можно взять из урла, если перейти в раздел Администрирование › SLA:

`https://st.yandex-team.ru/admin/queue/_YOUR_QUEUE_/sla`

и кликнуть на нужный SLA, чтобы он развернулся. В урле появится id:

`https://st.yandex-team.ru/admin/queue/_YOUR_QUEUE_/sla#390`

## Изменение конфига

Изменить конфиг можно прямо в интерфесе Арканума:
1. Заходим в папку `projects`
1. Открываем нужный конфиг и спарва от названия файла жмём карандашик

    ![edit_config](https://jing.yandex-team.ru/files/robot-portal-stats/edit_config@1x.png)

1. Редактируем конфиг и посылаем на ревью

    ![send_to_review](https://jing.yandex-team.ru/files/robot-portal-stats/send_to_review@1x.jpeg)

    1. Кратко описываем изменения
    1. Указываем, нужно ли сделать ревью изменений (будет призван кто-то из g:portal_zbp_and_stats)
    1. Если правка небольшая и вы в ней уверены, жмите `commit without checks`, правка сразу будет смерджена и при переходе в папку `projects` вы увидете уже изменённый конфиг
    1. Иначе жмите `Send` — будет сформирован пулл-реквест с изменениями, который будет автоматически смерджен после прохождения тестов

        ![pr](https://jing.yandex-team.ru/files/robot-portal-stats/pr@1x.png)

## Добавление целей на следующий квартал/полугодие

Чтобы добавить новую цель, нужно проделать шаги из раздела [изменение конфига](#изменение-конфига) и в список `goals` добавить запись вида

```yml
-
  from: [2020-Q2, 175]
  to:   [2020-Q3, 140]
```

Подробнее смотри в [описании конфига сервиса](#конфиг-сервиса).

## Добавление нового сервиса

Чтобы добавить новый сервис нужно:
1. Выдать доступ __на чтение__ очереди АВС-группе __Виртуальные сотрудники (ZBP сервисов портала и пр. статистика)__

    ![add_access_to_st](https://jing.yandex-team.ru/files/robot-portal-stats/add_access_to_st@1x.jpeg)

    ![access_to_st](https://jing.yandex-team.ru/files/robot-portal-stats/access_to_st@1x.jpeg)
1. Добавить yml-конфиг в папку `projects`
1. Добавить ссылку на конфиг в файл `ya.make` в раздел `RESOURCE` в виде:
    ```ya.make
    RECOURCE(
        ...
        projects/name.yml       config_name
        ...
    )
    ```
1. Закоммитить изменения :)

На [дашборде](https://dash.yandex-team.ru/8tq941sqba665) данные серивса появятся на следующий день.

## Разовый пересчёт

Запустить пересчёт можно и по необходимости. Для этого нужно зайти в список [Sandbox-тасков](https://sandbox.yandex-team.ru/schedulers?owner=PORTAL_STATS&limit=20) и нажать кнопку [Run once] для таска "ZBP stats mainer to ClickHouse".

> ![sb_run_once](https://jing.yandex-team.ru/files/robot-portal-stats/sb_run_once@1x.jpeg)
