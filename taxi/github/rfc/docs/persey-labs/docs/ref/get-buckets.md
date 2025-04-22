# Получить список заявок

Заявки можно запрашивать только на определенный день. При этом заявки будут доступны не раньше, чем накануне вечером. 

## Формат запроса

Чтобы получить список заявок, отправьте запрос:

```http
GET https://labs-api.yandex.ru/lab/v1/buckets?date=<дата>&lab_id=<идентификатор лаборатории>
```

### Параметры запроса

| Query-параметр| Описание      |
| ------------- |--------------|
|  date *   | **Date**<br/> Дата в формате `YYYY-MM-DD`. |
|  lab_id  *  | **String**<br/> Строковый идентификатор лаборатории.|

*Обязательный параметр.

### HTTP-заголовки

В запросе необходимо передать заголовки:

```http
X-External-Service: <логин лаборатории>
X-External-Api-Key: <API-ключ>
Origin: https://labs-api.yandex.ru
```
Подробнее см. в разделе [Доступ к API](../concepts/authorization.md).

## Формат ответа {#response}

В ответ сервис присылает список заявок на заданную дату. Заявки сгруппированы по сумкам. Одна сумка — это один выезд. 

```json
{
    "buckets":  [{
        "id": "10001",
        "owner_login": "ivan",
        "orders": [{
            "id": "100",
            "patient": {
                "firstname": "Иван",
                "middlename": "Иванович",
                "surname": "Иванов",
                "birthday": "1980-10-10",
                "document": {
                    "type": "national_passport",
                    "number": "7777 123456",
                    "issue_date": "2010-10-10",
                    "issued_by": "Отделение в городе Москва ОУФМС"
                },
                "gender": "male"
            },
            "contacts": {
                "phone": "+71234567890",
                "email": "ivan@ivanov.ru"
            },
            "address": {
                "text": "Россия, Москва, Садовническая улица, д. 81",
                "position": [38.55, 55.3],
                "apartment": "4",
                "floor": "5",
                "entrance": "5",
                "comment": "домофон"
            },
            "workplace": {
                "organization": "ОАО Организация",
                "job_position": "Менеджер",
                "address_text": "Россия, Москва, Садовническая улица, д. 81",
                "phone": "+7123456789"
            }
        }, {
            "id": "13456",
            "patient": {
                "firstname": "Екатерина",
                "middlename": "Васильевна",
                "surname": "Васильева",
                "birthday": "2010-10-10",
                "document": {
                    "type": "birth_certificate",
                    "number": "IV-123456"
                },
                "gender": "female"
            },
            "guardian": {
                "firstname": "Василий",
                "middlename": "Васильевич",
                "surname": "Васильев",
                "document": {
                    "type": "national_passport",
                    "number": "7777 123452",
                    "issue_date": "2010-10-10",
                    "issued_by": "Отделение в городе Москва ОУФМС",
                    "registration": "Россия, Москва, ул. Улица, д. 123, кв. 406"
                },
                "birthday": "1991-01-13",
                "gender": "male"
            },
            "contacts": {
                "phone": "+71234567893",
                "email": "vasya@vasya.ru"
            },
            "address": {
                "text": "Россия, Московская область, Балашиха, микрорайон Железнодорожный, Колхозная улица, 8",
                "position": [38.021949,  55.745275],
                "apartment": "4",
                "floor": "3",
                "entrance": "5",
                "comment": "консьерж"
            }
        }]            
    }, {
        "id": "10003",
        "owner_login": "gleb",
        "orders": [{
             ...
        }]
    }]
}
```

### Параметры ответа

| Параметр | Описание      |
| ------------- |:-------------|
|  buckets *   | **Array[Object]**<br/> Список сумок. |
|  buckets[].id *   | **Number**<br/> Идентификатор сумки. |
|  buckets[].owner_login *        | **String**<br/> Логин медработника, который будет выполнять выезды по адресам из текущей сумки. Этот логин используется в мобильном приложении «Помощь рядом».|
|  buckets[].orders *    | **Array[Object]**<br/> Список заявок в сумке. |
|  buckets[].orders[].id *        | **Number**<br/> Идентификатор заявки. |
|  buckets[].orders[].patient *   | **Object**<br/> Данные о пациенте. |
|  buckets[].orders[].patient.name *      | **String**<br/> Имя пациента. |
|  buckets[].orders[].patient.middlename | **String**<br/> Имя отчества. |
|  buckets[].orders[].patient.surname *   | **String**<br/> Фамилия пациента.|
|  buckets[].orders[].patient.birthday *     | **Date**<br/> Дата рождения в формате `YYYY-MM-DD`. |
|  buckets[].orders[].patient.document *     | **Object**<br/> Данные документа, удостоверяющего личность. |
|  buckets[].orders[].patient.document.type *     | **Enum(String)**<br/> Тип документа. Доступные значения: `birth_certificate` (свидетельство о рождении), `national_passport` (внутрироссийский паспорт), `international_passport` (заграничный паспорт), `any_passport` (другой вид паспорта).|
|  buckets[].orders[].patient.document.number *     | **String**<br/> Номер документа. |
|  buckets[].orders[].patient.document.issue_date      | **Date**<br/> Дата выдачи (только для паспорта). |
|  buckets[].orders[].patient.document.issued_by      | **Date**<br/> Кем выдан (только для паспорта). |
|  buckets[].orders[].patient.document.registration    | **String**<br/> Адрес прописки (только для паспорта). |
|  buckets[].orders[].patient.gender *     | **Enum(String)**<br/> Пол пациента. Доступные значения: `male`, `female`.|
|  buckets[].orders[].guardian      | **Object**<br/> Данные попечителя. Поле присутствует, если тест проводится у несовершеннолетних пациентов. |
|  buckets[].orders[].guardian.name *      | **String**<br/> Имя попечителя. |
|  buckets[].orders[].guardian.middlename | **String**<br/> Имя отчества попечителя. |
|  buckets[].orders[].guardian.surname *   | **String**<br/> Фамилия попечителя.|
|  buckets[].orders[].guardian.document *     | **Object**<br/> Данные документа, удостоверяющего личность. |
|  buckets[].orders[].guardian.birthday *     | **Date**<br/> Дата рождения попечителя в формате `YYYY-MM-DD`. |
|  buckets[].orders[].guardian.gender *     | **Enum(String)**<br/> Пол попечителя. Доступные значения: `male`, `female`.|
|  buckets[].orders[].contacts *     | **Object**<br/> Контакты пациента или попечителя. |
|  buckets[].orders[].contacts.phone *     | **String**<br/> Телефон. |
|  buckets[].orders[].contacts.email *     | **String**<br/> Электронная почта. |
|  buckets[].orders[].address *   | **Object**<br/> Информация об адресе проживания пациента. |
|  buckets[].orders[].address.text *      | **String**<br/> Полный адрес. |
|  buckets[].orders[].address.position *  | **Array[Number]**<br/> Географические координаты. |
|  buckets[].orders[].address.apartment |  **String**<br/> Номер дома. |
|  buckets[].orders[].address.floor      | **Number**<br/> Этаж. |
|  buckets[].orders[].address.entrance   | **Number**<br/> Подъезд. |
|  buckets[].orders[].address.comment    | **String**<br/> Дополнительная информация (наличие домофона, консьерж). |
|  buckets[].orders[].workplace    | **Object**<br/> Информация об организации, где работает пациент. |
|  buckets[].orders[].workplace.organization    | **String**<br/> Название организации. |
|  buckets[].orders[].workplace.job_position    | **String**<br/> Должность. |
|  buckets[].orders[].workplace.address_text   | **String**<br/> Адрес организации. |
|  buckets[].orders[].workplace.phone    | **String**<br/> Рабочий телефон. |

*Обязательное поле.

## Пример
```curl
curl 'https://labs-api.yandex.ru/lab/v1/buckets?lab_id=my_lab&date=2020-08-09' \
 -H 'X-External-Service: msk_lab' \
 -H 'X-External-API-Key: Njrgku45vmklf34gffgft44saafvvvqqnrfmgl9h' \
 -H 'Origin: https://labs-api.yandex.ru'
```