# Клиент для работы с Staff Gap API

[Документация по API](https://wiki.yandex-team.ru/staff/pool/gap2/api/)

## Установка

```bash
npm install @yandex-int/si.ci.gap-client
```

## API

### gap(token, [host, protocol])

Возвращает объект с набором методов.

#### token

* Type: string

OAUTH токен от STAFF.

#### host

* Type: string

По умолчанию `staff.yandex-team.ru`.

#### port

* Type: string

`https:` или `http:`. По умолчанию `https:`.

## Методы

* fetch [Описание](https://wiki.yandex-team.ru/staff/pool/gap2/api/#poiskotsutstvijapoid)
* find [Описание](https://wiki.yandex-team.ru/staff/pool/gap2/api/#poiskotsutstvijjpofiltru)
* create [Описание](https://wiki.yandex-team.ru/staff/pool/gap2/api/#sozdanieotsutstvija)
* edit [Описание](https://wiki.yandex-team.ru/staff/pool/gap2/api/#redaktirovanieotsutstvija)
* confirm [Описание](https://wiki.yandex-team.ru/staff/pool/gap2/api/#podtverzhdenieotsutstvija)
* sign [Описание](https://wiki.yandex-team.ru/staff/pool/gap2/api/#podpisotsutstvija)
* cancel [Описание](https://wiki.yandex-team.ru/staff/pool/gap2/api/#otmenaotsutstvija)
* workflows [Описание](https://wiki.yandex-team.ru/staff/pool/gap2/api/#spisoktipovotsutstvijj)

## Пример использования

```js
const gap = require('@yandex-int/si.ci.gap-client')('token');

gap.fetch(1).then(console.log);

gap.find({
    person_login: ['test_person', 'another_person'],
    date_from: '01.01.2017',
    date_to: '01.02.2018'
}).then(console.log);

gap.create({
    workflow: "illness",
    person_login: "test_person",
    date_from: "2015-01-01T10:20:00",
    date_to: "2015-01-02T11:30:00",
    work_in_absence: true,
    comment: "И пусть весь мир подождёт.",
    to_notify: ["a@yandex-team.ru", "b@gmail.com"],
    full_day: true
}).then(console.log);
```
