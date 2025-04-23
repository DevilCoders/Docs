# Инфраструктура дежурств Геосервисов

[Документация Sedem](https://docs.yandex-team.ru/sedem/duty)

[Sandbox shedulers](https://sandbox.yandex-team.ru/schedulers?tags=duty&task_type=MAPS_BINARY_TASK%2CMAPS_SWITCH_DUTY_PHONE_TASK&limit=100)

[ABC дежурных выходного дня](https://abc.yandex-team.ru/services/maps-duty)

[Расписание дежурств выходного дня](https://abc.yandex-team.ru/services/maps-duty/duty)

## Основные компоненты

dutypayer - поиск смен выходного дня и заведение тикетов на оплату

generator - генерация смен дежурств

phone_switcher - обновление статуса текущего дежурного с оповещением  в Telegram/Slack чатики и переключением общего телефонного номера 1721

### Робот и его доступы

Дежурства генерирует [робот Хеви Дьюти](https://staff.yandex-team.ru/robot-heavy-duty).

Он использует следующие доступы:

#### Общие доступы для генерации дежурств и dutypayer

+ OAuth Скоупы — [новое OAuth-приложение](https://oauth.yandex-team.ru/client/ddc2f0186c164a93a00ebd23ce2d7daf) с правами:
    + ABC — Доступ к ABC
    + staff.yandex-team.ru — Чтение данных со Стаффа
    + Duty — Использование API Duty
    + YT — Использование API YT
    + (скоупы для dutypayer см. в соответствующем разделе ниже)

+ IDM:
    + YT:
      [Использование yt-аккаунта maps-core-duty](https://idm.yandex-team.ru/system/yt-cluster-hahn#role=75954420,f-role-id=75954420)
      [Доступ к директории //home/maps/core/duty добавлен вручную мимо IDM](https://yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//home/maps/core/duty)
      ~~[Роль не используется, так как директория `//home/maps/core/infra/duty` не используется](https://idm.yandex-team.ru/system/yt-cluster-hahn#role=75929917,f-role-id=75929917)~~


#### Доступы для генерации дежурств

+ IDM:
    + Staff Gap API:
      https://idm.yandex-team.ru/system/staff#role=75323492,f-role-id=75323492

+ Роли Duty Manager в ABC для всех сервисов, дежурствами которых робот управляет в ABC. Робот прописывается прямо в ABC. [Пример ABC, где роботу выдана роль](https://abc.yandex-team.ru/services/maps-duty-infra). [Пример выданной ему роли в IDM](https://idm.yandex-team.ru/system/abc#role=75662317,f-role-id=75662317)

#### Доступы для dutypayer

+ OAuth:
    + Стартрек — Запись в Стартреке

+ IDM:
    + Staff API:
      https://idm.yandex-team.ru/system/staffapi#role=76383365,f-role-id=76383365
      https://idm.yandex-team.ru/system/staffapi-test#role=76515041,f-role-id=76515041

+ Доступы в Startrek (запрошены [в тикете](https://st.yandex-team.ru/HRANALYTICS-18468))
    + к очереди SALARY
    + к компоненте 29814 «РПД»
