# Получить список отделений

Лаборатория может запросить список своих отделений, которые участвуют в программе тестирования.

## Формат запроса

Чтобы получить список отделений, отправьте запрос:

```http
GET https://labs-api.yandex.ru/lab/v1/labs
```

### HTTP-заголовки

В запросе необходимо передать заголовки:

```http
X-External-Service: <логин лаборатории>
X-External-Api-Key: <API-ключ>
Origin: https://labs-api.yandex.ru
```

Подробнее см. в разделе [Доступ к API](../concepts/authorization.md).

## Формат ответа {#response}

В случае успеха сервер возвращает статус 200 OK. В теле ответа будет содержаться список лабораторий.

```json
{
    "labs": [{
        "id": "lab_1",
        "name": "Лаборатория Выхино",
        "address": {
            "position": [37.810809, 55.700212],
            "text": "Россия, Москва, улица Ташкентская, дом 25, корп. 1"
        },
        "bucket_owners": [{
             "login": "lab_med_1",
             "fullname": "Петров Петр Петрович"
        }, {
             "login": "lab_med_2",
             "fullname": "Иванова Татьяна Васильевна"
        }]
    }, {
        "id": "lab_2",
        "name": "Лаборатория Академическая",
        ...
    ]}
```

### Параметры ответа

| Параметр | Описание      |
| ------------- |:-------------|
| labs * | **Array[Object]** <br/> Список отделений лаборатории. |
| labs[].id * | **String** <br/> Идентификатор, который был присвоен отделению.|
| labs[].name * | **String** <br/> Название отделения.|
| labs[].address * | **Object** <br/> Адрес отделения.|
| labs[].address.position *| **Array[Number]** <br/> Географические координаты.|
| labs[].address.text *| **String** <br/> Полный адрес.|
| labs[].bucket_owners * | **Array[Object]** <br/> Информация о медработниках, которые будут выполнять выезды к пациентам.|
| labs[].bucket_owners[].login * | **String** <br/> Логин медработника в приложении «Помощь рядом». |
| labs[].bucket_owners[].fullname *| **String** <br/> ФИО медработника. |

*Обязательное поле

## Пример
```curl
curl 'https://labs-api.yandex.ru/lab/v1/buckets?lab_id=my_lab&date=2020-08-09' \
 -H 'X-External-Service: msk_lab' \
 -H 'X-External-API-Key: Njrgku45vmklf34gffgft44saafvvvqqnrfmgl9h' \
 -H 'Origin: https://labs-api.yandex.ru'
```