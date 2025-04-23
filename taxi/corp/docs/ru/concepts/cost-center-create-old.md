# Создание кост-центров клиента в старом формате

{% note warning %}

Если вы продолжаете работать с кост-центрами в старом формате, вы можете перейти на [новую форму кост-центров](cost-center-create.md). Перейти обратно на старый формат нельзя.

{% endnote %}


Запрос позволяет добавить информацию о кост-центрах клиента.

## Синтаксис запроса

```
PUT https://business.taxi.yandex.ru/api/1.0/client/{идентификатор клиента}/cost_centers
```

{% include [order-create-headers-p](../_includes/concepts/order-create/id-order-create/headers-p.md) %}


#### Authorization
OAuth-токен. Процесс получения токена описан в разделе [Начало работы](quickstart.md).

Запросов отправляется с типом содержимого `multipart/form-data`. Это означает, что при отправке запроса необходимо указывать заголовок `Content-Type: multipart/form-data`.

В теле запроса необходимо передать `.xls`-файл с информацией о кост-центрах. Значения кост-центров должны находиться в первом столбце `.xls`-файла.

## Описание полей ответа

В случае успеха вернется пустой ответ с кодом 200.

## Пример запроса

```
PUT https://business.taxi.yandex.ru/api/1.0/client/a2...09/cost_centers
...
Authorization: <OAuth-токен>


--Asde457BGe4h
Content-Disposition: form-data; name="cost_centers_file"; filename="cost_centers.xls"

(двоичное содержимое .xls файла)
--Asde457BGe4h--


```

## Возможные коды ответа

{% include [cost-center-create-possible-answers-code](../_includes/concepts/cost-center-create/id-cost-center-create/possible-answers-code.md) %}


- `200` — запрос выполнен успешно.
- `400` — в запросе был передан неизвестный параметр или параметр с недопустимым значением.
- `401` — был передан неверный [OAuth-токен](quickstart.md).
- `403` — у клиента не хватает прав на выполнение данного запроса.
- `404` — запрашиваемая запись не найдена.
- `415` — указан неподдерживаемый тип содержимого запроса.

