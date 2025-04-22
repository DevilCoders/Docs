# Pahom

## Что это такое

Pahom - это анализатор реалтайм состояний BGP сессий с быстрым HTTP API

api:

 - `yttl_network_blacklist`: список сетей `ToR`-ов у которых неполная связность
 - `x_d_status`: список линков `X<=>D` где есть проблемы (где не все `BGP` сессии живы)

## Где что искать
- fqnd VS'a: [прод](https://pahom.yandex-team.ru/)
- api [документация](https://pahom.yandex-team.ru/api/doc)
- рилы: [прод](https://racktables.yandex-team.ru/index.php?page=macros&macro_name=_C_NOCDEV_PAHOM_)
- графички: [дашборд](https://grafana.yandex-team.ru/d/pLF6U_fMk/pahom-prod), [все метрики](https://solomon.yandex-team.ru/?project=pahom&cluster=prod&service=*)
- juggler: [события](https://juggler.yandex-team.ru/raw_events/?query=tag%3Dnoc%20%26%20tag%3Dpahom), [аггрегат](https://juggler.yandex-team.ru/project/noc/aggregate?host=pahom&service=pahom_business_logic&project=noc)
- код [arcadia/noc/pahom](https://a.yandex-team.ru/arc/trunk/arcadia/noc/pahom), [конфиги](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/files/nocdev-pahom)
- [катается через arc.ci](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fpahom&id=pahom-release) + [conductor](https://c.yandex-team.ru/packages/yandex-pahom)
- логи надо смотреть на рилах, `/var/log/pahom/*.log`

## Если зажёгся алерт

У пахома один основной аггрегат который говорит "всё хорошо" или "всё плохо" это
[pahom-business-logic](https://juggler.yandex-team.ru/project/noc/aggregate?host=pahom&service=pahom_business_logic&project=noc).
Если он загорелся нужно уже смотреть подробнее почему:

 - `pahom.sink.bgp_session.delay_seconds/vendor.*` - загорается если информация о статусе `bgp` сессий для данного
вендора (`huawei`, `arista` и тп) стала слишком старой. Это может быть, например, если информация о сессиях
с `grad`-а стала по каким-то причинам отставать от реальности, или, например, если `db` pahom-а начала тормозить.
Когда тормозит `db`, то обычно загорается сразу куча проверок, а не только одна.
 - `pahom.sync.delay_seconds` - загорается если сбор всего `mesh`-а с `racktables`+`ann` начал отставать (должен собираться каждые 2 часа)
 - `pahom.sicktor.delay_seconds` - загорается, если информация о `ToR`-ах с неполной связностью перестала обновляться

Сейчас из известных проблем у `pahom`-а бывает затуп с `db`. В этом случае база начинает очень сильно тормозить,
не получается просчитывать метрики и это заставляeт тормозить `db` ещё больше. До конца непонятно почему такое
происходит, случается раз в несколько месяцев. Лечится это выключением всех сервисов `pahom`-а кроме `pahom-apid`
до тех пор пока нагрузка на бд не нормализуется. Нагрузку на бд смотреть тут
[YC PostgreSQL - Pahom](https://yc.yandex-team.ru/folders/foosk13mu0ib9qrjkh8a/managed-postgresql/cluster/mdb7pduggnq6knpq4gjq?section=monitoring)

Сервисы которые нужно выключить:

```
   pahom-analyzerd.service         Pahom Analyzed Daemon
   pahom-confsyncd.service         Pahom Confsync Daemon
   pahom-grad-rmq-sinkd.service    Pahom Grad RMQ Sink Daemon
   pahom-metricsd.service          Pahom Metrics Daemon
   pahom-update-tags.service       Pahom UpdateTags Daemon
```

При этом сервис апи трогать не нужно, он будет продолжать отдавать последние просчитанные данные:

```
   pahom-apid.service              Pahom API Daemon
```

Если есть возможность - лучше всегда прийти к [mocksoul@](https://staff.yandex-team.ru/mocksoul) с этим до каких-либо действий, т.к. до сих пор эта проблема
в стадии "ловим" и каждый случай подробно разглядывается перед лечением.

### pahom.sync.delay_seconds

**Причина проблемы**
Загорается если сбор всего mesh-а с racktables+ann начал отставать (должен собираться каждые 2 часа), например, по причине недоступности InvApi.

**Решение** 

Рестартим сервис. Это безопасное действие

Если настроен ycg|psh
```
ycg nocdev-pahom | psh sudo systemctl restart pahom-confsyncd.service
```

Через executer
```
p_exec %nocdev-pahom sudo systemctl restart pahom-confsyncd.service
```

Руками на хостах:
- <sas-pahom1.net.yandex.net>
- <vla-pahom1.net.yandex.net>
