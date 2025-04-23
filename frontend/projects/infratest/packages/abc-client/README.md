# Клиент для работы с ABC API

[Документация по API](https://wiki.yandex-team.ru/intranet/abc/api/)

## Установка

```bash
npm install @yandex-int/si.ci.abc-client
```

## API

### abc(options)

Возвращает объект с набором методов.

#### В options

##### token

* Type: string

OAuth токен от Staff.

##### host

* Type: string

По умолчанию `abc-back.yandex-team.ru`.

##### port

* Type: string

`https:` или `http:`. По умолчанию `https:`.

## Методы

* services [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/services/)
* service [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/services/id/)
* servicesResponsibles [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/services/responsibles/)
* servicesMembers [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/services/members/)
* servicesContacts [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/services/contacts/)
* roles [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/roles/)
* resourcesTypesCategories [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/resources/types/categories)
* resourcesTypes [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/resources/types)
* resourcesTagsCategories [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/resources/tags/categories)
* resourcesTags [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/resources/tags)
* resourcesConsumers [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/resources/consumers)
* resources [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/resources)
* intranetPersons **(ВНУТРЕННЕЕ API)** [Описание](https://wiki.yandex-team.ru/Intranet/abc/api/#get/api/v3/intranet/personsvnutrenneeapi)

## Пример использования

```js
const abc = require('@yandex-int/si.ci.abc-client')({
  token: '<token>'
});

abc.service(1)
  .then(console.log);

abc.services({
    id__in: '1,2'
}).then(console.log);

abc.roles({
    service__slug: 'infraspeed'
}).then(console.log);
```
