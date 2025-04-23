# Пакет для выбора случайного сотрудника из нескольких источников

В качестве источников могут быть указаны список логинов или сервисы ABC.

## Установка

```bash
npm install @yandex-int/si.ci.staff-chooser
```

## Пример использования

```js
const staffChooserClient = require('@yandex-int/si.ci.staff-chooser')({
  token: '<token>'
});

// Выведет в консоль одного из участников ABC сервиса infraspeed.
staffChooserClient.choose({
  abcServices: ['infraspeed']
}).then(console.log);
```

## API

### staffChooserClient(options)

Возвращает объект с набором методов.

#### В options

##### token

* Type: `string`

Портальный OAuth токен (ABC, Gap).

## Методы

### choose(options)

#### В options

##### date

* Type: `string`

Дата в формате "YYYY-MM-DD", на которую происходит выбор.

##### members

* Type: `string[]`

Участвующие логины сотрудников.

##### abcServices

* Type: `string[]`

Участвующие ABC сервисы.

##### includeGapWorkflows

* Type: `string[]`

Включаемые типы отсутствий.

##### excludeGapWorkflows

* Type: `string[]`

Исключаемые типы отсутствий. По умолчанию: `["trip"]`

##### includeAbcRoles

* Type: `string[]`

Включаемые роли из ABC сервисов.

##### excludeAbcRoles

* Type: `string[]`

Исключаемые роли из ABC сервисов. По умолчанию: `["robot"]`

#### Возвращает

Логин выбранного сотрудника или null, если нет свободных сотрудников (к примеру все в отпуске).
