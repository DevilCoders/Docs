# Сценарии

## Что это
Во время работы с Wall-e периодически возникают рутинные последовательности задач над группами хостов, которые необходимо выполнить в рамках одной бизнес-транзакции в определенном порядке. Для того, чтобы автоматизировать такие задачи были созданы сценарии.

## Краткое описание работы
Сценарии позволяют выбрать операцию из нескольких заранее созданных последовательностей действий (стейджей), добавить в него группу хостов (над которыми требуется выполнить некоторые задачи) и выполнить задачи над каждой группой хостов).

## Типы сценариев
* [Ввод хостов в RTC](https://wiki.yandex-team.ru/wall-e/Scenarii/Instrukcija-po-scenariju-vvoda-xostov/)
* [Быстрые NOC работы](https://docs.yandex-team.ru/wall-e/scenario/noc-soft)
* [Работы ITDC](https://docs.yandex-team.ru/wall-e/scenario/itdc-maintenance)
* [Долгие NOC работы](https://docs.yandex-team.ru/wall-e/scenario/noc-hard)
* [Быстрый ввод из резервов RTC](https://docs.yandex-team.ru/wall-e/scenario/reserved-hosts-transfer)

Для создания опредлённого типа сценария может понадобиться запросить доступ к нему через [IDM (система Wall-E)](https://idm.yandex-team.ru/#rf=1,rf-role=cTYH9Vus#walle/scenario(fields:()),f-status=all,sort-by=-updated,rf-expanded=cTYH9Vus)

## Авторизация
На данный момент, сценариями без ограничений разрешено пользоваться лишь админам wall-e. Однако, мы даем пользователям доступ к отдельным типам сценариев через явное указание их логина в конфиге.

В случае ввода хостов, право на отмену сценариев также дается пользователям, которые сдают хосты.

Доступ к использованию сценария выдаётся через IDM. Например, [вот так](https://nda.ya.ru/t/3_Bq166y3W9SPy) можно запросить доступ к использованию сценария ввода хостов.

Надо понимать, что сценарии это достаточно специализированная система, в ней нет сценариев общего пользования, и те, кому доступ нужен, уже его имеют.

## API
API для создания и управления сценариями доступно по https://api.wall-e.yandex-team.ru/ см. раздел "Scenario API"

## Валидация параметров
На сегодня мы валидируем все параметры на семантическую правильность (принадлежность по типу, длина, формат), а также:
* тикет в стартреке на существование. Требуется, чтобы тикет для сценария был доступен пользователю @robot-walle.
* switch (не даем создавать новые сценарии с указанным switch, если существуют незавершенные сценарии с ним же)

Все параметры, их тип и формат можно увидеть в документации, в разделе [Scenario API](https://api.wall-e.yandex-team.ru)

## Текущий статус сценария
На каком этапе выполнения находится сценарий можно определить по label `WORK_STATUS` у сценария.

Возможные значения:
* `created` - сценарий создан без опции `autostart` и ещё не выполняется. Надо его запустить вручную
* `started` - сценарий начал выполнение
* `approvement` - сценарий находится на этапе согласования. Ответственные люди должны подтвердить работы в соответствующих тикетах, прилинкованных к основному тикету сценария.
* `ready` - walle выполнил свою часть работы (подготовил сервера) и теперь смежные команды (ITDC/NOC) могут приступать к своим работам
* `finishing` - walle выполняет работы по возврату хостов в эксплуатацию
* `finished` - сценарий завершён

## UI Actions

| Action / Status | `created`    | `started` | `paused`  | `ready`   | `WOKS_STATUS - ready`  |
| --------------- | :----------: | :-------: | :-------: | :-------: | :--------------------: |
| Start           | &#9989;      | &#9989;   | &#128683; | &#128683; | &#128683;              |
| Pause           | &#128683;    | &#9989;   | &#128683; | &#128683; | &#128683;              |
| Skip            | &#128683;    | &#128683; | &#9989;   | &#128683; | &#128683;              |
| Cancel          | &#9989;      | &#9989;   | &#9989;   | &#9989;   | &#128683;              |
| Finish          | &#128683;    | &#128683; | &#128683; | &#128683; | &#9989;                |
