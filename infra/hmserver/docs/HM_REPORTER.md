# HM Reporter

> ca.key, db_user, db_password хранятся в
>
> https://yav.yandex-team.ru/secret/sec-01efy99nzq5n09n2bnq0pb599t

## Репорты

### Структура репорта описаная в [hmserver.proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/proto/hmserver.proto):
```protobuf
message Report {
    string node = 1;
    string name = 2;
    string version = 3;
    string stage = 4;
    string kind = 5;
    Ready ready = 6;
    google.protobuf.Timestamp last_transition = 7;
    google.protobuf.Timestamp report_time = 8;
}
```
* Name - имя юнита
* Kind - Package-Set или PortoDaemon
* Node - hostname
* Stage - `testing|production|prestable`
* Version - версия выбраная пользователем
* LastTransition - время последнего изменения юнита
* ReportTime - время репорта
* Ready

### API
* [grpc](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/proto/hmserver.proto)
* [go](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/pkg/reporter/client/client.go)

## UI
В ui можно смотреть на репорты в разрезах:
* Список юнитов по локациям: `http://hm-sas.in.yandex.net:8998/units`
* Страница юнита в локации для sas: `http://hm-sas.in.yandex.net:8998/units/<unit-name>`
* Список репортов в локации с фильтрами для sas: `http://hm-sas.in.yandex.net:8998/`

## Развернут в 5 локациях
* PRESTABLE [UI](http://hm-prestable.in.yandex.net:8998)
  - hm-prestable-1.sas.yp-c.yandex.net
  - hm-prestable-2.vla.yp-c.yandex.net
  - hm-prestable-3.man.yp-c.yandex.net
* SAS [UI](http://hm-sas.in.yandex.net:8998)
  - stout21.search.yandex.net
  - stout22.search.yandex.net
  - stout23.search.yandex.net
  - stout24.search.yandex.net
  - stout25.search.yandex.net
* VLA [UI](http://hm-vla.in.yandex.net:8998)
  - vla1-0474.search.yandex.net
  - vla1-1451.search.yandex.net
  - vla1-2999.search.yandex.net
* MAN [UI](http://hm-man.in.yandex.net:8998)
  - man1-9003.search.yandex.net
  - man1-9004.search.yandex.net
  - man1-9005.search.yandex.net
  - man1-9006.search.yandex.net
  - man1-9007.search.yandex.net
* MSK [UI](http://hm-msk.in.yandex.net:8998)
  - myt1-0074.search.yandex.net
  - myt1-0075.search.yandex.net
  - myt1-0088.search.yandex.net
