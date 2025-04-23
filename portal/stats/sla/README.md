# SLA

**Оглавление**:
- [Обзор](#обзор)
- [Конфиг сервиса](#конфиг-сервиса)
- [Добавление нового сервиса](#добавление-нового-сервиса)
- [Разовый пересчёт](#разовый-пересчёт)

## Обзор

[Дашборд](https://dash.yandex-team.ru/2toxz2sid1noy)
[ABC-сервис](https://abc.yandex-team.ru/services/portal_zbp_and_stats/)

Сбор SLA-метрик запускается каждую ночь в 01:30 мск [задачей в Sandbox](https://sandbox.yandex-team.ru/schedulers?owner=PORTAL_STATS&limit=20).

Метрики собираются для сервисов, конфиги готорых находятся в папке `projects`.

## Конфиг серивса

Конфиг сервиса задается в yml-формате:

```yml
name: home                  # код сервиса латинскими буквами
title: Морда                # название сервиса
filters:                    # список фильтров для сбора метрик
-                           # фильтр 1)
  filter: 'Queue: HOME
    and Resolution: !Некорректный
    and Resolution: !Дубликат
    and Resolution: !"Не воспроизводится"
    and Resolution: !"Не будет исправлено"'
  sla:                      # список SLA, которые нужно мониторить
    691: Ревью              # в формате ID: название
    1975: Тестирование
    2022: Кейсы для асессоров
-                           # фильтр 2)
  filter: 'Queue: SPI Tags: "service:MORDA"'
  sla:
    2019: SPI
```

Идентификатор SLA можно взять из урла, если перейти в раздел Администрирование › SLA:

`https://st.yandex-team.ru/admin/queue/_YOUR_QUEUE_/sla`

и кликнуть на нужный SLA, чтобы он развернулся. В урле появится id:

`https://st.yandex-team.ru/admin/queue/_YOUR_QUEUE_/sla#691`

## Добавление нового сервиса

Чтобы добавить новый сервис нужно:
1. Выдать доступ __на чтение__ очереди АВС-группе __Виртуальные сотрудники (ZBP сервисов портала и пр. статистика)__

    ![add_access_to_st](https://jing.yandex-team.ru/files/robot-portal-stats/add_access_to_st.jpeg)

    ![access_to_st](https://jing.yandex-team.ru/files/robot-portal-stats/access_to_st.jpeg)
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

На [дашборде](https://dash.yandex-team.ru/2toxz2sid1noy) данные серивса появятся на следующий день.

## Разовый пересчёт

Запустить пересчёт можно и по необходимости. Для этого нужно зайти в список [Sandbox-тасков](https://sandbox.yandex-team.ru/schedulers?owner=PORTAL_STATS&limit=20) и нажать кнопку [Run once] для таска "SLA stats mainer to ClickHouse".

> ![sb_run_once](https://jing.yandex-team.ru/files/robot-portal-stats/sb_run_once.jpeg)
