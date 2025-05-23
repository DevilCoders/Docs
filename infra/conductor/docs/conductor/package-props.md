# Настройка {{ serviceName }}а

Для использования {{ serviceName }}а необходимо авторизоваться во внутреннем Я.Паспорте, выполнить [настройку параметров учетной записи](./task/users.md) и [запросить необходимые права](./task/admin-role.md). Для Passerby-пользователей требуется [настройка ограниченного доступа](./task/roles.md).

Для выкладки пакетов в {{ serviceName }}е должны быть определены объекты, влияющие на выкладку.

Основными объектами, определяющими свойства пакета и правила выкладки, являются:

- [Репозитории](#Repos).
- [Хосты](#Hosts).
- [Дата-центры](#DCs).
- [Воркфлоу](#workflows).
- [Проекты](#Projects).
- [Тесты](#Tests).
- [Сервисы](#Services).

## Репозитории {#Repos}

Пакеты, для распространения которых используется {{ serviceName }}, хранятся в _репозиториях_, расположенных (в основном) на `dist.yandex.ru`.

Каждый пакет может хранится в одном и более репозиториях. Так обеспечивается возможность отдельно собираться для разных архитектур (например, для Ubuntu Hardy и Ubuntu Lucid).

Для выкладки в {{ serviceName }}е должны быть [определены репозитории](./task/repos.md#new), в которых хранятся пакеты. Информация о пакетах обновляется ежеминутно (при опросе перечисленных репозиториев).

## Хосты {#Hosts}

В большинстве случаев сервисы запущены на нескольких серверах. Каждый из них однозначно идентифицируется _хостом_. Пакеты могут быть установлены только на те хосты, которые [зарегистрированы](./task/hosts.md#new) в {{ serviceName }}е.

Для удобства администрирования и гибкого управления хосты объединяются в _группы_. Каждая [группа](./task/groups.md#new) относится к одному из [проектов](#Projects). В некоторых случаях группы объединяются в [макросы](./task/macroses.md), которые в дальнейшем используются при настройке [свойств пакета](./task/packages.md#edit_deploy) и в API {{ serviceName }}а.

## Дата-центры {#DCs}

Надежность сервисов Яндекса обеспечивается установкой серверов в разных _дата-центрах_.

Поставить пакет с помощью {{ serviceName }}а можно только в тот дата-центр, информация о котором  [зарегистрирована](./task/datacenters.md#new).

## Воркфлоу {#workflows}

Пакеты выкладываются на тестовые и боевые [хосты](#Hosts) сервисов. Такие хосты объединяются в _деплой-группы_. Выкладка пакета в определенную [ветку](branches.md) возможна только в том случае, если для нее определена по крайней мере одна деплой-группа.

Множество веток, деплой-групп, соответствующих каждой из них, а также правил перехода пакета между ними образуют _воркфлоу_. Для выкладки пакету должен быть назначен по крайней мере один воркфлоу.

Каждый воркфлоу можно связать с одним и более пакетами.

## Проекты {#Projects}

Каждый проект хранит информацию о связанных с ним хостах, группах хостов, воркфлоу и администраторах проекта.

В {{ serviceName }}е отсутствует прямая связь между пакетом и проектом. Для ее вычисления используются данные о хостах, на которых установлен данный пакет. Каждый хост состоит в одной из групп, которая привязана к одному из проектов. Так вычисляется связь между пакетом и проектом.

## Тесты {#Tests}

Чтобы контролировать выкладку и воздействие пакетов на смежные сервисы, используются _тесты_. Реализация обеспечивается посредством интеграции с сервисом [AQuA](http://aqua.yandex-team.ru). Для каждой [ветки](branches.md), в которую выкладывается пакет, может быть определен независимый набор тестов.

Пакетам могут быть назначены только [определенные](./task/test_suites.md#new) в {{ serviceName }}е тесты.

## Сервисы {#Services}

Выкладка пакета может сопровождаться остановом/запуском/перезапуском связанных с данным пакетом сервисов. Для автоматизации данного процесса в {{ serviceName }}е предусмотрена возможность [создания скриптов](./task/services.md#new), регулирующих подобные действия — _сервисов_.
