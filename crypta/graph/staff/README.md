Выгрузка стафф-крипта
=====================

Директория выгрузки: [//home/crypta/public/ids_storage/staff][0]
Описание таблиц:

| tbl                     | descr |
| ----------------------- | ----- |
| [dump][2]               | Динамическая таблица выгрузки из api стаффа, фильтр по активным сотрудникам |
| [crypta_id][1]          | Соответсвие между логином на стаффе, и идентификатором крипты. Строится через джойн указанных на стаффе контактных passport_login/email/phone с таблицами склейки. |
| [login][6]              | Соответсвие между логином на стаффе, и логином в пасспорте. Строится как прямая выгрузка контактных passport_login/email. |
| [puid][7]               | Соответсвие между логином на стаффе, и puid в пасспорте. Строится как прямая выгрузка контактных passport_login/email - достраивается до пуида, по словарному супу паспорта. |
| [passport_userdata][3]  | Выгрузка пасспортных логинов с атрибутом `sid 669` |
| [puid_ext][4]           | Таблица без соответсвия, содержит puid'ы из `passport_userdata` и `crypta_id/puid` |
| [yandexuid_ext][5]`*`   | Таблица без соответсвия, содержит список всех yandxuid'ов входящих в crytpa_id, которые попали в затронутые стаффом криптаайди, как через дамп, так и через паспорт. |

`*` -- используется для выкатки экспериментов на стафф в АБ-шнице.

[0]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/ids_storage/staff
[1]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/ids_storage/staff/crypta_id
[2]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/ids_storage/staff/dump
[3]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/ids_storage/staff/passport_userdata
[4]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/ids_storage/staff/puid_ext
[5]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/ids_storage/staff/yandexuid_ext
[6]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/ids_storage/staff/login
[7]: https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/ids_storage/staff/puid
