# Интеграция с облаком

## Описание

В данный момент плагин интеграции с облаком осуществляет импорт и синхронизацию железа облака из [netbox](https://netbox.cloud.yandex.net/) в RT.

Каждый час запускается cron который:

 - импортирует в `RT` объекты, у которых в bot-е указан сервис `YC Network Infrastructure`.
 - вешает на них тег `{Cloud Netbox}`
 - для всех `{Cloud Netbox}` синхронизирует из `netbox`-a имена, fqdn, mgmt ip и др. Так же развешиваются аттрибуты
`role` и `tenant`.

Нюансы:

 - Если у объекта есть порты и нет тега `{CloudNetbox}` - то тег навешиваться не будет. Смысл этого в том, что если
объект был заведён руками до импорта этим плагином - то перевод на автоматическую синхронизацию должен требовать
ручного решения и вмешательства.
 - Плагин запускается каждый час на 32-й минуте.
 - Плагин `dns` будет для всех объектов `{CloudNetbox}` управлять `PTR` записями. Прямые записи в `.yndx.net` тоже
создаются/удаляются, но они не являются основными (основные - `*.netinfra.cloud.yandex.net` и ими управляет само
облако).

## Алерты

### [rt-cloud-import](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Drt-cloud-import)

Статус импорта из bot-а. Это аггрегат над сырыми событиями, для каждой железки есть отдельное сырое событие по
успешному/не успешному импорту.

### [rt-cloud-sync](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Drt-cloud-sync)

Аггрегат над `rt-cloud-sync-role-ct` и `rt-cloud-sync-role-cx`. Только эти 2 роли мониторятся активно (так, это
есть в [nocdev dashboard](https://juggler.yandex-team.ru/dashboards/nocdev)).

### [rt-cloud-sync-role-*](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Drt-cloud-sync-role-*)

Аггрегаты над сырыми событиями объектов, сгруппированных по ролям (`-ct`, `-cx` и тп).

Обычно в описании алерта будет человекочитаемое объяснение что пошло не так, например:

`Unable to get device software type/version (id: 63757, fqdn: gov-d-1ct9.netinfra.cloud.yandex.net)`.

Для разбирательств с проблемами могут помочь логи `/var/log/rtcloud/netbox_sync.log`.

Если совсем непонятно что происходит и что сломалось - [mocksoul@](https://staff.yandex-team.ru/mocksoul)
