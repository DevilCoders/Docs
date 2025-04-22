# Формы фидбека

Для отправки фидбека используется [feedback-api](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api)

Содержание:

-   [Точки входа](#entry-points)
-   [Параметры форм](#params):
    -   [Общие параметры всех форм](#common-params)
    -   [Разводящая страница на добавление/редактирование](#map-edit)
    -   [Добавление объекта (разводящая форма)](#object-add)
    -   [Добавление объекта: адрес](#address-add)
    -   [Добавление объекта: подъезд](#entrance-add)
    -   [Добавление объекта: дорога](#road-add)
    -   [Добавление объекта: шлагбаум](#barrier-add)
    -   [Добавление объекта: парковка](#parking-add)
    -   [Добавление объекта: остановка](#stop-add)
    -   [Добавление объекта: забор](#fence-add)
    -   [Добавление объекта: калитка](#gate-add)
    -   [Добавление объекта: пешеходный переход](#crosswalk-add)
    -   [Добавление объекта: провайдер](#provider-add)
    -   [Добавление объекта: организация](#organization-add)
    -   [Добавление объекта: другое](#other-add)
    -   [Редактирование объекта: выбор объекта](#object-select)
    -   [Редактирование объекта: организация (разводящая форма)](#organization/edit)
    -   [Редактирование объекта: организация закрыта (разводящая форма)](#organization/closed)
    -   [Редактирование объекта: изменение информации об организации](#organization/edit-info)
    -   [Редактирование объекта: изменение входов и местоположения организации](#organization/location/edit)
    -   [Редактирование объекта: доступность организации для людей с инвалидностью](#organization/edit-accessibility)
    -   [Редактирование объекта: топоним (разводящая форма)](#object-edit)
    -   [Редактирование объекта: другое](#other-edit)
    -   [Редактирование объекта: удалить объект с карты](#other-not-found)
    -   [Редактирование объекта: изменение местоположения](#object-location-edit)
    -   [Редактирование объекта: изменение наименования](#object-name-edit)
    -   [Редактирование входа в здание: выбор входа (разводящая форма)](#entrance-select)
    -   [Редактирование входа в здание (разводящая форма)](#entrance-edit)
    -   [Редактирование здания: исправление имени входа в здание](#entrance-name-edit)
    -   [Редактирование здания: неверное расположение входа в здание](#entrance-location-edit)
    -   [Редактирование здания: входа в здание здесь нет](#entrance-not-found-edit)
    -   [Редактирование здания: неверный адрес](#address-edit)

    -   [Редактирование ОТ (разводящая форма)](#transit-stop-edit)
    -   [Редактирование ОТ: Остановки здесь нет](#transit-stop-not-found)
    -   [Редактирование ОТ: Изменить название остановки](#transit-stop-name-edit)
    -   [Редактирование ОТ: Остановка в другом месте](#transit-stop-location-edit)
    -   [Редактирование ОТ: Неправильный набор маршрутов](#transit-stop-route-incorrect)
    -   [Редактирование ОТ: Другое](#transit-stop-other)

    -   [Редактирование метро (станция/выход) (разводящая форма)](#subway-edit)
    -   [Редактирование метро (станция/выход): Объекта здесь нет](#subway-not-found)
    -   [Редактирование метро (станция/выход): Изменить название объекта](#subway-name-edit)
    -   [Редактирование метро (станция/выход): Объект в другом месте](#subway-location-edit)
    -   [Редактирование метро (станция/выход): Другое](#subway-other)

    -   [Редактирование маршрута (разводящая форма)](#route-edit)
    -   [Редактирование маршрута: нельзя проехать по маршруту (разводящая форма)](#route-incorrect)
    -   [Редактирование маршрута: конечные формы](#route-edit-forms)
    -   [Быстрая форма фидбека](#spot-other)
-   [Проброс авторизации из мобильного клиента](#mobile-auth)
-   [Возвращение в мобильный клиент](#mobile-back)
-   [Аналитика](#analytics)
-   [Точки входа в формы фидбека](#contexts)

<div id=entry-points></div>

## Точки входа

| env        | url                                                                                       |
| ---------- | ----------------------------------------------------------------------------------------- |
| testing    | https://l7test.yandex.ru/maps/feedback/<br/>https://l7test.yandex.com/maps/feedback/<br/> |
| production | https://yandex.ru/maps/feedback/<br/>https://yandex.com/maps/feedback/                    |

<div id=params></div>

## Параметры форм

<div id=common-params></div>

### Общие параметры всех форм

#### БЯК

| query arg             | type                                                                              | required | description                                                                                                                                                                                                                                                                                                |
| --------------------- | --------------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| client_id             | [client_id](https://wiki.yandex-team.ru/maps/feedback/newfeedback/clientid/)      | ✔        | Идентификатор клиента форм фидбека.                                                                                                                                                                                                                                                                        |
| context               | [context](https://wiki.yandex-team.ru/maps/feedback/newfeedback/clientcontextid/) |          | Идентификатор точки входа в формы фидбека на стороне клиента.                                                                                                                                                                                                                                              |
| uuid                  | string                                                                            |          | uuid пользователя из AppMetrika. Только для мобильных клиентов.                                                                                                                                                                                                                                            |
| deviceid              | string                                                                            |          | deviceid пользователя из AppMetrika. Только для мобильных клиентов.                                                                                                                                                                                                                                        |
| lang                  | string                                                                            |          | Язык или локаль пользователя. От этого параметра зависит язык интерфейса форм и отображение подложки на карте. Если параметр передан не будет, то будет использовано автоматическое определение локали с помощью [langdetect](https://doc.yandex-team.ru/lib/lang-detect/concepts/lang-detect-descr.html). |
| webview               | true                                                                              |          | Для мобильных клиентов.                                                                                                                                                                                                                                                                                    |
| theme                 | dark                                                                              |          | Тема интерфейса. Используется только в WebView.                                                                                                                                                                                                                                                            |
| safearea_inset_top    | number                                                                            |          | Отступ контента сверху для отображения в SafeArea в WebView.                                                                                                                                                                                                                                               |
| safearea_inset_bottom | number                                                                            |          | Отступ контента снизу для отображения в SafeArea в WebView.                                                                                                                                                                                                                                                |
| application_version   | string                                                                            |          | Версия мобильного приложения.                                                                                                                                                                                                                                                                              |

<div id=map-edit></div>

### Разводящая страница на добавление/редактирование

#### БЯК

| query arg | type     | required |
| --------- | -------- | -------- |
| type      | map/edit | ✔        |
| ll        | string   | ✔        |
| z         | number   | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=map/edit&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true_**

<div id=object-add></div>

### Добавление объекта (разводящая форма)

#### БЯК

| query arg | type       | required |
| --------- | ---------- | -------- |
| type      | object/add | ✔        |
| ll        | string     | ✔        |
| z         | number     | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=object/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true_**

<div id=address-add></div>

### Добавление объекта: адрес

#### БЯК

| query_arg | value       | required |
| --------- | ----------- | -------- |
| type      | address/add | ✔        |
| ll        | string      | ✔        |
| z         | number      | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=address/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | toponym    | ✔        |

<div id=entrance-add></div>

### Добавление объекта: подъезд

#### БЯК

| query_arg | value        | required |
| --------- | ------------ | -------- |
| type      | entrance/add | ✔        |
| ll        | string       | ✔        |
| z         | number       | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=entrance/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | entrance   | ✔        |

<div id=road-add></div>

### Добавление объекта: дорога

#### БЯК

| query_arg | value    | required |
| --------- | -------- | -------- |
| type      | road/add | ✔        |
| ll        | string   | ✔        |
| z         | number   | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=road/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | road       | ✔        |

<div id=barrier-add></div>

### Добавление объекта: шлагбаум

#### БЯК

| query_arg | value       | required |
| --------- | ----------- | -------- |
| type      | barrier/add | ✔        |
| ll        | string      | ✔        |
| z         | number      | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=barrier/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | barrier    | ✔        |

<div id=parking-add></div>

### Добавление объекта: парковка

#### БЯК

| query_arg | value       | required |
| --------- | ----------- | -------- |
| type      | parking/add | ✔        |
| ll        | string      | ✔        |
| z         | number      | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=parking/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | parking    | ✔        |

<div id=stop-add></div>

### Добавление объекта: остановка

#### БЯК

| query_arg | value            | required |
| --------- | ---------------- | -------- |
| type      | transit/stop/add | ✔        |
| ll        | string           | ✔        |
| z         | number           | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=transit/stop/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | stop       | ✔        |

<div id=fence-add></div>

### Добавление объекта: забор

#### БЯК

| query_arg | value     | required |
| --------- | --------- | -------- |
| type      | fence/add | ✔        |
| ll        | string    | ✔        |
| z         | number    | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=fence/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | fence      | ✔        |

<div id=gate-add></div>

### Добавление объекта: калитка

#### БЯК

| query_arg | value    | required |
| --------- | -------- | -------- |
| type      | gate/add | ✔        |
| ll        | string   | ✔        |
| z         | number   | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=gate/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | gate       | ✔        |

<div id=crosswalk-add></div>

### Добавление объекта: пешеходный переход

#### БЯК

| query_arg | value         | required |
| --------- | ------------- | -------- |
| type      | crosswalk/add | ✔        |
| ll        | string        | ✔        |
| z         | number        | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=crosswalk/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | crosswalk  | ✔        |

<div id=provider-add></div>

### Добавление объекта: провайдер

#### БЯК

| query_arg | value                     | required |
| --------- | ------------------------- | -------- |
| type      | provider/add              | ✔        |
| ll        | string                    | ✔        |
| z         | number                    | ✔        |
| context   | toponym.add_object_to_map |

**_Пример: https://yandex.ru/maps/feedback/?type=provider/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value                     | required |
| ----------- | ------------------------- | -------- |
| form_id     | toponym                   | ✔        |
| question_id | add_object                | ✔        |
| answer_id   | provider                  | ✔        |
| context_id  | toponym.add_object_to_map |

<div id=organization-add></div>

### Добавление объекта: организация

#### БЯК

| query_arg | value            | required |
| --------- | ---------------- | -------- |
| type      | organization/add | ✔        |
| ll        | string           | ✔        |
| z         | number           | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=organization/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value        | required |
| ----------- | ------------ | -------- |
| form_id     | organization | ✔        |
| question_id | add_object   | ✔        |
| answer_id   | organization | ✔        |

<div id=other-add></div>

### Добавление объекта: другое

#### БЯК

| query_arg | value     | required |
| --------- | --------- | -------- |
| type      | other/add | ✔        |
| ll        | string    | ✔        |
| z         | number    | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=other/add&ll=37.597381,55.745915&z=15&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.add_object_to_map&webview=true_**

#### feedback-int

| query_arg   | value      | required |
| ----------- | ---------- | -------- |
| form_id     | toponym    | ✔        |
| question_id | add_object | ✔        |
| answer_id   | other      | ✔        |

<div id=object-select></div>

### Редактирование объекта: выбор объекта

#### БЯК

| query arg | type          | required |
| --------- | ------------- | -------- |
| type      | object/select | ✔        |
| ll        | string        | ✔        |
| z         | number        | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=object/select&ll=37.597381,55.745915&z=15&client_id=desktop-maps_**

<div id=organization/edit></div>

### Редактирование объекта: организация (разводящая форма)

#### БЯК

| query_arg | value             | required |
| --------- | ----------------- | -------- |
| type      | organization/edit | ✔        |
| uri       | string            | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=organization/edit&uri=ymapsbm1%3A%2F%2Forg%3Foid%3D4709482929&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=organization.footer&webview=true_**

<div id=organization/closed></div>

### Редактирование объекта: организация закрыта (разводящая форма)

#### БЯК

| query_arg | value               | required |
| --------- | ------------------- | -------- |
| type      | organization/closed | ✔        |
| uri       | string              | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=organization/closed&uri=ymapsbm1%3A%2F%2Forg%3Foid%3D4709482929&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=organization.footer&webview=true_**

<div id=organization/edit-info></div>

### Редактирование объекта: изменение информации об организации

#### БЯК

| query_arg | value                  | required |
| --------- | ---------------------- | -------- |
| type      | organization/edit-info | ✔        |
| uri       | string                 | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=organization/edit-info&uri=ymapsbm1%3A%2F%2Forg%3Foid%3D4709482929&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=organization.footer&webview=true_**

#### feedback-int

| query_arg   | value              | required |
| ----------- | ------------------ | -------- |
| form_id     | organization       | ✔        |
| question_id | wrong_information  | ✔        |
| answer_id   | report_information | ✔        |

<div id=organization/location/edit></div>

### Редактирование объекта: изменение входов и местоположения организации

#### БЯК

| query_arg | value                      | required |
| --------- | -------------------------- | -------- |
| type      | organization/location/edit | ✔        |
| uri       | string                     | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=organization/location/edit&uri=ymapsbm1%3A%2F%2Forg%3Foid%3D4709482929&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=organization.footer&webview=true_**

<div id=organization/edit-accessibility></div>

### Редактирование объекта: доступность организации для людей с инвалидностью

#### БЯК

| query_arg | value                           | required |
| --------- | ------------------------------- | -------- |
| type      | organization/edit-accessibility | ✔        |
| uri       | string                          | ✔        |

**_Пример: https://yandex.ru/maps/feedback/?type=organization/edit-accessibility&uri=ymapsbm1%3A%2F%2Forg%3Foid%3D4709482929&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=organization.footer&webview=true_**

<div id=object-edit></div>

### Редактирование объекта: топоним (разводящая форма)

#### БЯК

| query arg | type        | required                                                      |
| --------- | ----------- | ------------------------------------------------------------- |
| type      | object/edit | ✔                                                             |
| uri       | string      | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string      | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number      | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=object/edit&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true_**
<br />**_Пример: https://yandex.ru/maps/feedback/?type=object/edit&ll=37.588100%2C55.734055&z=20&client_id=web_**

<div id=other-edit></div>

### Редактирование объекта: другое

#### БЯК

| query_arg | value        | required                                                      |
| --------- | ------------ | ------------------------------------------------------------- |
| type      | object/other | ✔                                                             |
| uri       | string       | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string       | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number       | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=object/other&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.building&webview=true_**

#### feedback-int

| query_arg   | value   | required |
| ----------- | ------- | -------- |
| form_id     | toponym | ✔        |
| question_id | other   | ✔        |
| answer_id   | comment | ✔        |

<div id=object-not-found></div>

### Редактирование объекта: удалить объект с карты

#### БЯК

| query_arg | value            | required                                                      |
| --------- | ---------------- | ------------------------------------------------------------- |
| type      | object/not-found | ✔                                                             |
| uri       | string           | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string           | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number           | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=object/not-found&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.building&webview=true_**

#### feedback-int

| query_arg   | value         | required |
| ----------- | ------------- | -------- |
| form_id     | toponym       | ✔        |
| question_id | remove_object | ✔        |
| answer_id   | toponym       | ✔        |

<div id=object-location-edit></div>

### Редактирование объекта: изменение местоположения

#### БЯК

| query_arg | value                | required                                                      |
| --------- | -------------------- | ------------------------------------------------------------- |
| type      | object/location/edit | ✔                                                             |
| uri       | string               | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string               | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number               | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=object/location/edit&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.588%252C55.734%26spn%3D0.009%252C0.005%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D0%25A6%25D0%25B5%25D0%25BD%25D1%2582%25D1%2580%25D0%25B0%25D0%25BB%25D1%258C%25D0%25BD%25D1%258B%25D0%25B9%2520%25D0%25B0%25D0%25B4%25D0%25BC%25D0%25B8%25D0%25BD%25D0%25B8%25D1%2581%25D1%2582%25D1%2580%25D0%25B0%25D1%2582%25D0%25B8%25D0%25B2%25D0%25BD%25D1%258B%25D0%25B9%2520%25D0%25BE%25D0%25BA%25D1%2580%25D1%2583%25D0%25B3%252C%2520%25D1%2580%25D0%25B0%25D0%25B9%25D0%25BE%25D0%25BD%2520%25D0%25A5%25D0%25B0%25D0%25BC%25D0%25BE%25D0%25B2%25D0%25BD%25D0%25B8%25D0%25BA%25D0%25B8%252C%2520%25D0%25BA%25D0%25B2%25D0%25B0%25D1%2580%25D1%2582%25D0%25B0%25D0%25BB%2520%25D0%259A%25D1%2580%25D0%25B0%25D1%2581%25D0%25BD%25D0%25B0%25D1%258F%2520%25D0%25A0%25D0%25BE%25D0%25B7%25D0%25B0&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.default&webview=true_**

#### feedback-int

| query_arg   | value           | required |
| ----------- | --------------- | -------- |
| form_id     | toponym         | ✔        |
| question_id | wrong_entrance  | ✔        |
| answer_id   | report_location | ✔        |

<div id=object-name-edit></div>

### Редактирование объекта: изменение наименования

#### БЯК

| query_arg | value            | required                                                      |
| --------- | ---------------- | ------------------------------------------------------------- |
| type      | object/name/edit | ✔                                                             |
| uri       | string           | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string           | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number           | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=object/name/edit&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.588%252C55.734%26spn%3D0.009%252C0.005%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D0%25A6%25D0%25B5%25D0%25BD%25D1%2582%25D1%2580%25D0%25B0%25D0%25BB%25D1%258C%25D0%25BD%25D1%258B%25D0%25B9%2520%25D0%25B0%25D0%25B4%25D0%25BC%25D0%25B8%25D0%25BD%25D0%25B8%25D1%2581%25D1%2582%25D1%2580%25D0%25B0%25D1%2582%25D0%25B8%25D0%25B2%25D0%25BD%25D1%258B%25D0%25B9%2520%25D0%25BE%25D0%25BA%25D1%2580%25D1%2583%25D0%25B3%252C%2520%25D1%2580%25D0%25B0%25D0%25B9%25D0%25BE%25D0%25BD%2520%25D0%25A5%25D0%25B0%25D0%25BC%25D0%25BE%25D0%25B2%25D0%25BD%25D0%25B8%25D0%25BA%25D0%25B8%252C%2520%25D0%25BA%25D0%25B2%25D0%25B0%25D1%2580%25D1%2582%25D0%25B0%25D0%25BB%2520%25D0%259A%25D1%2580%25D0%25B0%25D1%2581%25D0%25BD%25D0%25B0%25D1%258F%2520%25D0%25A0%25D0%25BE%25D0%25B7%25D0%25B0&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.default&webview=true_**

#### feedback-int

| query_arg   | value       | required |
| ----------- | ----------- | -------- |
| form_id     | toponym     | ✔        |
| question_id | wrong_name  | ✔        |
| answer_id   | report_name | ✔        |

<div id=entrance-select></div>

### Редактирование входа в здание: выбор входа (разводящая форма)

#### БЯК

| query_arg | value           | required                                                      |
| --------- | --------------- | ------------------------------------------------------------- |
| type      | entrance/select | ✔                                                             |
| uri       | string          | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string          | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number          | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=entrance/select&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.building&webview=true_**

<div id=entrance-edit></div>

### Редактирование входа в здание (разводящая форма)

#### БЯК

| query_arg | value         | required                                                      |
| --------- | ------------- | ------------------------------------------------------------- |
| type      | entrance/edit | ✔                                                             |
| uri       | string        | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string        | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number        | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=entrance/edit&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8%252C%2520%25D0%25BF%25D0%25BE%25D0%25B4%25D1%258A%25D0%25B5%25D0%25B7%25D0%25B4%25201%2520%257B3940017220%257D&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.building&webview=true_**

<div id=entrance-name-edit></div>

### Редактирование здания: исправление имени входа в здание

#### БЯК

| query_arg | value              | required                                                      |
| --------- | ------------------ | ------------------------------------------------------------- |
| type      | entrance/name/edit | ✔                                                             |
| uri       | string             | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string             | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number             | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=entrance/name/edit&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8%252C%2520%25D0%25BF%25D0%25BE%25D0%25B4%25D1%258A%25D0%25B5%25D0%25B7%25D0%25B4%25201%2520%257B3940017220%257D&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.building&webview=true_**

#### feedback-int

| query_arg   | value       | required |
| ----------- | ----------- | -------- |
| form_id     | toponym     | ✔        |
| question_id | wrong_name  | ✔        |
| answer_id   | report_name | ✔        |

<div id=entrance-location-edit></div>

### Редактирование здания: неверное расположение входа в здание

#### БЯК

| query_arg | value                  | required                                                      |
| --------- | ---------------------- | ------------------------------------------------------------- |
| type      | entrance/location/edit | ✔                                                             |
| uri       | string                 | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string                 | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number                 | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=entrance/location/edit&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8%252C%2520%25D0%25BF%25D0%25BE%25D0%25B4%25D1%258A%25D0%25B5%25D0%25B7%25D0%25B4%25201%2520%257B3940017220%257D&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.building&webview=true_**

#### feedback-int

| query_arg   | value           | required |
| ----------- | --------------- | -------- |
| form_id     | toponym         | ✔        |
| question_id | wrong_entrance  | ✔        |
| answer_id   | report_location | ✔        |

<div id=entrance-not-found-edit></div>

### Редактирование здания: входа в здание здесь нет

#### БЯК

| query_arg | value              | required                                                      |
| --------- | ------------------ | ------------------------------------------------------------- |
| type      | entrance/not-found | ✔                                                             |
| uri       | string             | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string             | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number             | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=entrance/not-found&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8%252C%2520%25D0%25BF%25D0%25BE%25D0%25B4%25D1%258A%25D0%25B5%25D0%25B7%25D0%25B4%25201%2520%257B3940017220%257D&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.building&webview=true_**

#### feedback-int

| query_arg   | value          | required |
| ----------- | -------------- | -------- |
| form_id     | toponym        | ✔        |
| question_id | wrong_entrance | ✔        |
| answer_id   | not_found      | ✔        |

<div id=address-edit></div>

### Редактирование здания: неверный адрес

#### БЯК

| query_arg | value        | required                                                      |
| --------- | ------------ | ------------------------------------------------------------- |
| type      | address/edit | ✔                                                             |
| uri       | string       | ✔ (взаимоисключающий с парой ll и z)                          |
| ll        | string       | ✔ (взаимоисключающий с uri, используется только вместе с z)   |
| z         | number       | ✔️ (взаимоисключающий с uri, используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/feedback/?type=address/edit&uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.589%252C55.734%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D0%25BA8&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&context=toponym.building&webview=true_**

#### feedback-int

| query_arg   | value          | required |
| ----------- | -------------- | -------- |
| form_id     | toponym        | ✔        |
| question_id | wrong_address  | ✔        |
| answer_id   | report_address | ✔        |

<div id=transit-stop-edit></div>

### Редактирование ОТ: (разводящая форма)

#### БЯК

| query_arg           | value              | required                                                                     |
| ------------------- | ------------------ | ---------------------------------------------------------------------------- |
| type                | transit/stop/edit  | ✔                                                                            |
| masstransit[stopId] | string             | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string             | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number             | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=transit%2Fstop%2Fedit&masstransit%5BstopId%5D=stop__9858755&ll=37.652147%2C55.739373&z=17**

<div id=transit-stop-not-found></div>

### Редактирование ОТ: Остановки здесь нет

#### БЯК

| query_arg           | value                  | required                                                                     |
| ------------------- | ---------------------- | ---------------------------------------------------------------------------- |
| type                | transit/stop/not-found | ✔                                                                            |
| masstransit[stopId] | string                 | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string                 | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number                 | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=transit%2Fstop%2Fnot-found&masstransit%5BstopId%5D=stop__9858755&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value          | required |
| ----------- | -------------- | -------- |
| form_id     | toponym        | ✔        |
| question_id | remove_object  | ✔        |
| answer_id   | toponym        | ✔        |

<div id=transit-stop-name-edit></div>

### Редактирование ОТ: Изменить название остановки

#### БЯК

| query_arg           | value                  | required                                                                     |
| ------------------- | ---------------------- | ---------------------------------------------------------------------------- |
| type                | transit/stop/name/edit | ✔                                                                            |
| masstransit[stopId] | string                 | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string                 | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number                 | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=transit%2Fstop%2Fname%2Fedit&masstransit%5BstopId%5D=stop__9858755&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value       | required |
| ----------- | ----------- | -------- |
| form_id     | toponym     | ✔        |
| question_id | wrong_name  | ✔        |
| answer_id   | report_name | ✔        |

<div id=transit-stop-location-edit></div>

### Редактирование ОТ: Остановка в другом месте

#### БЯК

| query_arg           | value                      | required                                                                     |
| ------------------- | -------------------------- | ---------------------------------------------------------------------------- |
| type                | transit/stop/location/edit | ✔                                                                            |
| masstransit[stopId] | string                     | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string                     | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number                     | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=transit%2Fstop%2Flocation%2Fedit&masstransit%5BstopId%5D=stop__9858755&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value           | required |
| ----------- | --------------- | -------- |
| form_id     | toponym         | ✔        |
| question_id | wrong_location  | ✔        |
| answer_id   | report_location | ✔        |

<div id=transit-stop-route-incorrect></div>

### Редактирование ОТ: Неправильный набор маршрутов

#### БЯК

| query_arg           | value                        | required                                                                     |
| ------------------- | ---------------------------- | ---------------------------------------------------------------------------- |
| type                | transit/stop/route/incorrect | ✔                                                                            |
| masstransit[stopId] | string                       | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string                       | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number                       | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=transit%2Fstop%2Froute%2Fincorrect&masstransit%5BstopId%5D=stop__9858755&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value        | required |
| ----------- | ------------ | -------- |
| form_id     | toponym      | ✔        |
| question_id | wrong_lines  | ✔        |
| answer_id   | report_lines | ✔        |

<div id=transit-stop-other></div>

### Редактирование ОТ: Другое

#### БЯК

| query_arg           | value              | required                                                                     |
| ------------------- | ------------------ | ---------------------------------------------------------------------------- |
| type                | transit/stop/other | ✔                                                                            |
| masstransit[stopId] | string             | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string             | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number             | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=transit%2Fstop%2Fother&masstransit%5BstopId%5D=stop__9858755&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value   | required |
| ----------- | ------- | -------- |
| form_id     | toponym | ✔        |
| question_id | other   | ✔        |
| answer_id   | comment | ✔        |

---------------------------------------------
<div id=subway-edit></div>

### Редактирование метро (станция/выход): (разводящая форма)

#### БЯК

| query_arg           | value              | required                                                                     |
| ------------------- | ------------------ | ---------------------------------------------------------------------------- |
| type                | subway/edit        | ✔                                                                            |
| masstransit[stopId] | string             | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string             | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number             | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=subway%2Fedit&masstransit%5BstopId%5D=exit__22994&ll=37.652147%2C55.739373&z=17_**

<div id=subway-not-found></div>

### Редактирование метро (станция/выход): Объекта здесь нет

#### БЯК

| query_arg           | value                  | required                                                                     |
| ------------------- | ---------------------- | ---------------------------------------------------------------------------- |
| type                | subway/not-found       | ✔                                                                            |
| masstransit[stopId] | string                 | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string                 | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number                 | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=subway%2Fnot-found&masstransit%5BstopId%5D=exit__22994&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value          | required |
| ----------- | -------------- | -------- |
| form_id     | toponym        | ✔        |
| question_id | wrong_subway   | ✔        |
| answer_id   | not_found      | ✔        |

<div id=subway-name-edit></div>

### Редактирование метро (станция/выход): Изменить название объекта

#### БЯК

| query_arg           | value                  | required                                                                     |
| ------------------- | ---------------------- | ---------------------------------------------------------------------------- |
| type                | subway/name/edit       | ✔                                                                            |
| masstransit[stopId] | string                 | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string                 | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number                 | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=subway%2Fname%2Fedit&masstransit%5BstopId%5D=exit__22994&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value         | required |
| ----------- | -----------   | -------- |
| form_id     | toponym       | ✔        |
| question_id | wrong_subway  | ✔        |
| answer_id   | report_subway | ✔        |

<div id=subway-location-edit></div>

### Редактирование метро (станция/выход): Объект в другом месте

#### БЯК

| query_arg           | value                      | required                                                                     |
| ------------------- | -------------------------- | ---------------------------------------------------------------------------- |
| type                | subway/location/edit       | ✔                                                                            |
| masstransit[stopId] | string                     | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string                     | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number                     | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=subway%2Flocation%2Fedit&masstransit%5BstopId%5D=exit__22994&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value           | required |
| ----------- | --------------- | -------- |
| form_id     | toponym         | ✔        |
| question_id | wrong_subway    | ✔        |
| answer_id   | report_subway   | ✔        |

<div id=subway-other></div>

### Редактирование метро (станция/выход): Другое

#### БЯК

| query_arg           | value              | required                                                                     |
| ------------------- | ------------------ | ---------------------------------------------------------------------------- |
| type                | subway/other       | ✔                                                                            |
| masstransit[stopId] | string             | ✔ (взаимоисключающий с парой ll и z)                                         |
| ll                  | string             | ✔ (взаимоисключающий с masstransit[stopId], используется только вместе с z)  |
| z                   | number             | ✔️ (взаимоисключающий с masstransit[stopId], используется только вместе с ll) |

**_Пример: https://yandex.ru/maps/213/moscow/?feedback=subway%2Fother&masstransit%5BstopId%5D=exit__22994&ll=37.652147%2C55.739373&z=17_**

#### feedback-int

| query_arg   | value        | required |
| ----------- | ------------ | -------- |
| form_id     | toponym      | ✔        |
| question_id | wrong_subway | ✔        |
| answer_id   | other        | ✔        |

<div id=route-edit></div>

### Редактирование маршрута (разводящая форма)

#### БЯК

| query_arg    | value                                                     | required | description                                                                                         |
| ------------ | --------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------- |
| type         | route/edit                                                | ✔        |
| uri          | string                                                    | ✔        |
| travel_mode  | `auto`, `masstransit`, `pedestrian`, `bicycle`, `scooter` | ✔        | Bместе с `travel_mode=auto` можно использовать [параметры грузовиков](#vehicle-restrictions-params) |
| way_points   | string                                                    | ✔        | lat,lon~lat,lon                                                                                     |
| via_points   | string                                                    |          | lat,lon~lat,lon                                                                                     |
| traffic_jams | true                                                      |          |

**_Пример: https://yandex.ru/maps/feedback/?type=route/edit&uri=ymapsbm1%3A%2F%2Froute%2Fdriving%2Fv1%2FCswCCmCAiu0jD78dnw6PHe8dzzigKtAY-Asg2BLIF_gW4BfIDJAEpwW_BtcP11rPEbA6gDvgXrBpwEuoG-Ak0A5I3xDvCIcR-ASvLqcUhwzHAcc_lzvwKHfXDLdi5zeXEecbQF8SYeDTkzW_CscvnwPADbgS0Cl33w-HEBDvA4cPzwOQJ-ga0AGnC48KiAGAIoAFtxiPFO8d7yHPFt8DtwG3A88DzwHoAj__GN8Uj0OvJhj4C-gLuCnQAfcGj0LHGq8E_wvgCWAaVYYBxgHkAbACtwLBAjCJAYoBMzOJAY4BExAVecwBgQKuArICwwF7d3Z4bWNYnAHYAaMCkALQAY8CuwHAAZsCmwKhAqACEKMC2wHcAbcC7wGvAscCxwIiCggmEgYIARAJGBciCggAEgYQxQUYmQMiCggxEgYQmzYYuBgiCggKEgYQqAIYzwESABoAIIRL&travel_mode=auto&way_points=55.735327%2C37.593373~55.734127%2C37.588731~55.718604%2C37.586964&via_points=55.735403999999996%2C37.593929&traffic_jams=true&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true_**

<div id=route-incorrect></div>

### Редактирование маршрута: нельзя проехать по маршруту (разводящая форма)

#### БЯК

| query_arg    | value                                                     | required | description                                                                                         |
| ------------ | --------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------- |
| type         | route/incorrect                                           | ✔        |
| uri          | string                                                    | ✔        |
| travel_mode  | `auto`, `masstransit`, `pedestrian`, `bicycle`, `scooter` | ✔        | Bместе с `travel_mode=auto` можно использовать [параметры грузовиков](#vehicle-restrictions-params) |
| way_points   | string                                                    | ✔        | lat,lon~lat,lon                                                                                     |
| via_points   | string                                                    |          | lat,lon~lat,lon                                                                                     |
| traffic_jams | true                                                      |          |

**_Пример: https://yandex.ru/maps/feedback/?type=route/incorrect&uri=ymapsbm1%3A%2F%2Froute%2Fdriving%2Fv1%2FCswCCmCAiu0jD78dnw6PHe8dzzigKtAY-Asg2BLIF_gW4BfIDJAEpwW_BtcP11rPEbA6gDvgXrBpwEuoG-Ak0A5I3xDvCIcR-ASvLqcUhwzHAcc_lzvwKHfXDLdi5zeXEecbQF8SYeDTkzW_CscvnwPADbgS0Cl33w-HEBDvA4cPzwOQJ-ga0AGnC48KiAGAIoAFtxiPFO8d7yHPFt8DtwG3A88DzwHoAj__GN8Uj0OvJhj4C-gLuCnQAfcGj0LHGq8E_wvgCWAaVYYBxgHkAbACtwLBAjCJAYoBMzOJAY4BExAVecwBgQKuArICwwF7d3Z4bWNYnAHYAaMCkALQAY8CuwHAAZsCmwKhAqACEKMC2wHcAbcC7wGvAscCxwIiCggmEgYIARAJGBciCggAEgYQxQUYmQMiCggxEgYQmzYYuBgiCggKEgYQqAIYzwESABoAIIRL&travel_mode=auto&way_points=55.735327%2C37.593373~55.734127%2C37.588731~55.718604%2C37.586964&via_points=55.735403999999996%2C37.593929&traffic_jams=true&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true_**

<div id=route-edit-forms></div>

### Редактирование маршрута: конечные формы

#### БЯК

| query_arg    | value                                                                                                                                                                     | required | description                                                                                                                                                                                                                                                                                                                                |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type         | route/edit/better</br>route/incorrect/road-closed</br>route/incorrect/poor-condition</br>route/incorrect/prohibiting-sign</br>route/incorrect/obstruction</br>route/other | ✔        | route/edit/better - форма `Есть маршрут лучше`</br>route/incorrect/road-closed - форма `Дороги здесь нет`</br>route/incorrect/poor-condition - форма `Неровная дорога`</br>route/incorrect/prohibiting-sign - форма `Запрещающая разметка или знак`</br>route/incorrect/obstruction - форма `Препятствие`</br>route/other - форма `Другое` |
| uri          | string                                                                                                                                                                    | ✔        |
| travel_mode  | `auto`, `masstransit`, `pedestrian`, `bicycle`                                                                                                                            | ✔        | Bместе с `travel_mode=auto` можно использовать [параметры грузовиков](#vehicle-restrictions-params)                                                                                                                                                                                                                                        |
| way_points   | string                                                                                                                                                                    | ✔        | lat,lon~lat,lon                                                                                                                                                                                                                                                                                                                            |
| via_points   | string                                                                                                                                                                    |          | lat,lon~lat,lon                                                                                                                                                                                                                                                                                                                            |
| traffic_jams | true                                                                                                                                                                      |          |

**_Пример: https://yandex.ru/maps/feedback/?type=route/edit/better&uri=ymapsbm1%3A%2F%2Froute%2Fdriving%2Fv1%2FCswCCmCAiu0jD78dnw6PHe8dzzigKtAY-Asg2BLIF_gW4BfIDJAEpwW_BtcP11rPEbA6gDvgXrBpwEuoG-Ak0A5I3xDvCIcR-ASvLqcUhwzHAcc_lzvwKHfXDLdi5zeXEecbQF8SYeDTkzW_CscvnwPADbgS0Cl33w-HEBDvA4cPzwOQJ-ga0AGnC48KiAGAIoAFtxiPFO8d7yHPFt8DtwG3A88DzwHoAj__GN8Uj0OvJhj4C-gLuCnQAfcGj0LHGq8E_wvgCWAaVYYBxgHkAbACtwLBAjCJAYoBMzOJAY4BExAVecwBgQKuArICwwF7d3Z4bWNYnAHYAaMCkALQAY8CuwHAAZsCmwKhAqACEKMC2wHcAbcC7wGvAscCxwIiCggmEgYIARAJGBciCggAEgYQxQUYmQMiCggxEgYQmzYYuBgiCggKEgYQqAIYzwESABoAIIRL&travel_mode=auto&way_points=55.735327%2C37.593373~55.734127%2C37.588731~55.718604%2C37.586964&via_points=55.735403999999996%2C37.593929&traffic_jams=true&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345_**

#### feedback-int

| query_arg   | value        | required |
| ----------- | ------------ | -------- |
| form_id     | route        | ✔        |
| question_id | wrong_route  | ✔        |
| answer_id   | report_route | ✔        |

<div id=vehicle-restrictions-params></div>

### Параметры грузового автотранспорта

#### БЯК

| query arg           | type    | required | description                    |
| ------------------- | ------- | -------- | ------------------------------ |
| vehicle_width       | number  |          | Ширина                         |
| vehicle_height      | number  |          | Высота                         |
| vehicle_length      | number  |          | Длина                          |
| vehicle_weight      | number  |          | Фактическая масса (с грузом)   |
| vehicle_max_weight  | number  |          | Разрешённая максимальная масса |
| vehicle_axle_weight | number  |          | Нагрузка на ось                |
| vehicle_payload     | number  |          | Грузоподъемность               |
| vehicle_eco_class   | number  |          | Экологический класс            |
| vehicle_has_trailer | boolean |          | Движение с прицепом            |

<div id=spot-other></div>

### Быстрая форма фидбека

#### БЯК

| query_arg | value      | required | description |
| --------- | ---------- | -------- | ----------- |
| type      | spot/other | ✔        |             |
| uri       | string     |          |             |

**_Пример: https://yandex.ru/maps/feedback/?type=spot/other&uri=ymapsbm1%3A%2F%2Froute%2Fdriving%2Fv1%2FCswCCmCAiu0jD78dnw6PHe8dzzigKtAY-Asg2BLIF_gW4BfIDJAEpwW_BtcP11rPEbA6gDvgXrBpwEuoG-Ak0A5I3xDvCIcR-ASvLqcUhwzHAcc_lzvwKHfXDLdi5zeXEecbQF8SYeDTkzW_CscvnwPADbgS0Cl33w-HEBDvA4cPzwOQJ-ga0AGnC48KiAGAIoAFtxiPFO8d7yHPFt8DtwG3A88DzwHoAj__GN8Uj0OvJhj4C-gLuCnQAfcGj0LHGq8E_wvgCWAaVYYBxgHkAbACtwLBAjCJAYoBMzOJAY4BExAVecwBgQKuArICwwF7d3Z4bWNYnAHYAaMCkALQAY8CuwHAAZsCmwKhAqACEKMC2wHcAbcC7wGvAscCxwIiCggmEgYIARAJGBciCggAEgYQxQUYmQMiCggxEgYQmzYYuBgiCggKEgYQqAIYzwESABoAIIRL&client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345_**

#### feedback-int

| query_arg   | value   | required |
| ----------- | ------- | -------- |
| form_id     | toponym | ✔        |
| question_id | other   | ✔        |
| answer_id   | comment | ✔        |

<div id=mobile-auth></div>

## Проброс авторизации из мобильного клиента

Для проброса авторизации из мобильного клиента необходимо устанавливать куки через метод `requestCookieAuthURLWithAccount` в AccountManager.
Подробнее можно прочитать в [документации](https://wiki.yandex-team.ru/yandexmobile/accountmanager/help/ios/lastapi/#yalcookieexchangerobmenxtokenanaavtorizacionnyekuki).

<div id=mobile-back></div>

## Возвращение в мобильный клиент

При использовании через webview после завершения отправки фидбэка необходимо закрыть это webview.
Для этого внутри БЯК осуществляется переход на специальный технический урл вида `/maps/feedback/completed`. Например, для production-окружения на домене ru, полный урл перехода выглядит как: https://yandex.ru/maps/feedback/completed.
Мобильный клиент должен "слушать" изменение урла в webview и закрывать его в случае совпадения.

<div id=analytics></div>

## Логирование

### Логирование ФФ для дашбордов

Для логирования событий показа и сокрытия форм используются `show` и `hide` события соответственно c полем `type == form`.
Для логирования событий показа, сокрытия и клика кнопок отправки используются `show`, `hide` и `click` события соответственно c полем `type == submit_button`.
В метадате событий используются следующие поля:

| field name      | type                                     | description                                                                                                                                         |
| --------------- | ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| type            | `form`<br/>`submit_button`               | Тип логируемого объекта. Используется в новом формате логирования.                                                                                  |
| formType        | string                                   | Тип формы фидбека. [Посмотреть весь список](../src/feedback/common/types/feedback-common.ts#L1-L133). |
| formContextId   | string                                   | [Точка входа](#form-contexts) в фидбек в UI БЯКа.                                                                                                   |
| clientContextId | string                                   | [Точка входа](#client-contexts) в фидбек на стороне клиента (например, пуши из приложения).                                                         |
| clientId        | string                                   | [Идентификатор клиента](https://wiki.yandex-team.ru/maps/feedback/newfeedback/clientid/).                                                           |
| formId          | `toponym`<br/>`organization`<br/>`route` | Идентификатор формы.                                                                                                                                |

Реализация контракта, описывающего метадату событий, представлена в интерфейсе `ContractAnalyticsWrapperNodeState`.

#### Пример использования в ФФ

Логирование ФФ:

```jsx
<FeedbackContractAnalyticsWrapper isForm name="form" config={props.config} feedback={props.feedback}>
    <AddObjectFeedbackView />
</FeedbackContractAnalyticsWrapper>
```

Логирование кнопки отправки в ФФ:

```jsx
<FeedbackContractAnalyticsWrapper name="submit" isSubmitButton feedback={props.feedback} config={props.config} logClick>
    <FeedbackLoadableButton text={i18n('feedback', 'submit')} onClick={this._onSubmitClick} />
</FeedbackContractAnalyticsWrapper>
```

### Логирование активных элементов ФФ

В метадате событий используются следующие поля:

| field name | type   | description                                                                                                                                                                       |
| ---------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| formType   | string | Тип формы фидбека. [Посмотреть весь список](../src/feedback/common/types/feedback-common.ts#L1-L133).                               |
| openForm   | string | Тип формы фидбека, которую открывает пункт меню. [Посмотреть весь список](../src/feedback/common/types/feedback-common.ts#L1-L133). |

#### Пример использования в ФФ

Логирование любой кнопки ФФ:

```jsx
<FeedbackAnalyticsWrapper name="back_to_map" formType="other/add" logClick>
    <Button view="secondary-blue" size="medium" onClick={this.setMobileViewState('mini')}>
        {i18n('feedback', 'show-map')}
    </Button>
</FeedbackAnalyticsWrapper>
```

Логирование пункта меню:

```jsx
<FeedbackAnalyticsWrapper name="menu-item" formType="object/add" openForm="other/add" logClick>
    <CardFeatureView view="dark" iconUrl={icon} onClick={this._onClick(type)}>
        {i18n('feedback', 'menu-item-other-add')}
    </CardFeatureView>
</FeedbackAnalyticsWrapper>
```

<div id=form-contexts></div>

## Точки входа в фидбек в UI БЯКа

| formContextId                                            | place description                                                                          |
| -------------------------------------------------------- |--------------------------------------------------------------------------------------------|
| `feedback.common.error_in_geo_object_menu`               | Пункт "Ошибка в организации или географическом объекте" формы "Сообщить от ошибке"         |
| `feedback.common.add_object_to_map`                      | Пункт "Добавить объект на карту" формы "Сообщить от ошибке"                                |
| `feedback.spot_other.finish`                             | Пункт "Исправить еще" на финальной странице быстрой формы фидбека                          |
| `feedback.finish_form.edit_status_carousel`              | Карусель с заданиями на организации на финальной странице формы фидбека                    |
| `toponym.add_finish`                                     | Пункт "Добавить еще" на финальной страницы добавления топонима                             |
| `toponym.edit_finish`                                    | Пункт "Исправить еще" на финальной страницы редактирования топонима                        |
| `organization.add_finish`                                | Пункт "Добавить еще" на финальной страницы добавления организации                          |
| `organization.edit_finish`                               | Пункт "Исправить еще" на финальной странице редактирования организации                     |
| `ugc_profile.feedbacks_footer`                           | Пункт "Редактировать карту" в десктопе из вкладки UGC "Исправления"                        |
| `ugc_profile.feedbacks_footer.edit_map`                  | Пункт на тачах "Редактировать карту" из вкладки UGC "Исправления"                          |
| `ugc_profile.feedbacks_footer.add_object`                | Пункт на тачах "Добавить объект на карту" из вкладки UGC "Исправления"                     |
| `ugc_profile.feedbacks_placeholder`                      | Пункт "Редактировать карту" из вкладки UGC "Исправления" без исправлений                   |
| `ugc_profile.feedbacks_drafts.feedbacks_draft`           | "Редактирование черновика" из вкладки UGC "Исправления" в режиме "Черновки"                |
| `ugc_profile.assignments_placeholder.add_object`         | Пункт "Добавить объект на карту" из вкладки UGC "Задания" без заданий                      |
| `ugc_profile.assignments_push_placeholder.edit_object`   | Пункт "Исправить неточность" из вкладки UGC "Задания" без заданий из пуша                  |
| `ugc_profile.organization_edit_status_assignment.edit`   | Форма редактирования задания на статус организации из вкладки UGC "Задания"                |
| `ugc_profile.organization_edit_status_assignment.submit` | Кнопка "Да, она открыта" в карточке задания на статус организации из вкладки UGC "Задания" |
| `ugc_profile.gate_assignment.edit`                       | Форма редактирования задания на калитку из вкладки UGC "Задания"                           |
| `ugc_profile.barrier_assignment.edit`                    | Форма редактирования задания на шлагбаум из вкладки UGC "Задания"                          |
| `ugc_profile.add_address_assignment.edit`                | Форма редактирования задания на добавление адреса из вкладки UGC "Задания"                 |
| `ugc_profile.settlement_scheme_assignment.edit`          | Форма редактирования задания на схемы СНТ из вкладки UGC "Задания"                         |
| `ugc_profile.entrances_assignment.edit`                  | Форма редактирования задания на подъезды из вкладки UGC "Задания"                          |
| `ugc_profile.review_impression.closed`                   | Кнопка "не работает" в карточке впечатления на отзыв в UGC                                 |
| `map.context`                                            | Пункт "Редактировать карту" из контекстного меню карты                                     |
| `map.controls`                                           | Пункт "Редактировать карту" из контрола карты "троеточие"                                  |
| `organization.footer`                                    | Пункт "Редактировать информацию об организации" из карточки организации                    |
| `organization.search_result`                             | Плейсхолдер "Добавьте организацию ..." из результата поиска                                |
| `organization.features`                                  | Пункт "Редактировать" в особенностях карточки организации                                  |
| `toponym.search_results`                                 | Плейсхолдер "Добавьте организацию или объект ..." из результата поиска                     |
| `toponym.default`                                        | Пункт "Редактировать информацию об объекте" из карточки топонима                           |
| `toponym.building`                                       | Пункт "Редактировать информацию об объекте" из карточки здания                             |
| `toponym.building_without_address`                       | Карточка здания без адреса                                                                 |
| `toponym.add_object`                                     | Кнопка "Добавить объект" в карточке топонима                                               |
| `route.routes_list`                                      | Кнопка "Исправить" из списка доступных маршрутов                                           |
| `route.detailed_info`                                    | Кнопка "Исправить маршрут" в подробной информации о маршруте                               |
| `user_profile.edit_map`                                  | Кнопка "Исправить карту" в карусели профиля пользователя                                   |
| `masstransit.default`                                    | Карточка остановки                                                                         |
| `masstransit.subway`                                     | Карточка станции или выхода метро                                                          |
| `organization.card_actions`                              | [OLD] Форма редактирование организации из экшен кнопок организации                         |
| `ugc_profile.organization_edit_status_assignment`        | [OLD] Карточка организации из вкладки UGC "Задания"                                        |
| `ugc_profile.organization_edit_status_assignment.reject` | [OLD] Пункт "Нет" карточки организации из вкладки UGC "Задания"                            |
| `ugc_profile.gate_assignment`                            | [OLD] Карточка на задaние на калитку из вкладки UGC "Задания"                              |
| `ugc_profile.gate_assignment.submit`                     | [OLD] Пункт "Да" из задания на калитку из вкладки UGC "Задания"                            |
| `ugc_profile.gate_assignment.reject`                     | [OLD] Пункт "Ее тут нет" из задания на калитку из вкладки UGC "Задания"                    |
| `ugc_profile.barrier_assignment`                         | [OLD] Карточка на задaние на шлагбаум из вкладки UGC "Задания"                             |
| `ugc_profile.barrier_assignment.submit`                  | [OLD] Пункт "Да" из задания на шлагбаум из вкладки UGC "Задания"                           |
| `ugc_profile.barrier_assignment.reject`                  | [OLD] Пункт "Ее тут нет" из задания на шлагбаум из вкладки UGC "Задания"                   |
| `ugc_profile.add_address_assignment`                     | [OLD] Карточка на "Добавить адрес" из вкладки UGC "Задания"                                |
| `ugc_profile.add_address_assignment.submit`              | [OLD] Пункт "Добавить адрес" карточки топонима из вкладки UGC "Задания"                    |
| `ugc_profile.settlement_scheme_assignment.submit`        | [OLD] Пункт "Добавить схему" задания на схемы СНТ из вкладки UGC "Задания"                 |

<div id=client-contexts></div>

## Точки входа в фидбек на стороне клиента

### Точки входа в PUSH-уведомлениях

| clientContextId                      | push description                                  |
| ------------------------------------ | ------------------------------------------------- |
| `organization.push_notifications`    | Пуш на актуализацию статусов организаций          |
| `toponym.push_notifications`         | Пуш на добавление адреса                          |
| `ugc.org_status.push_notifications`  | Пуш в ЛК с приоритезацией карточки на организации |
| `ugc.address_add.push_notifications` | Пуш в ЛК с приоритезацией карточки на адреса      |

### Точки входа из МЯКа

**Просьба, при добавлении нового контекста, воспользоватья шаблоном `app.<context>`.**

| clientContextId                      | push description                                           |
| ------------------------------------ | ---------------------------------------------------------- |
| `app.user_profile.ugc`               | Кнопка "Отзывы, фото и исправления" в профиле пользователя |
| `app.user_profile.add_object_to_map` | Кнопка "Добавить объект на карту" в профиле пользователя   |

* Формы фидбека в МЯКе открываются по ссылке ```https://yandex.ru/maps/feedback``` с дополнительными параметрами урла. В таком случае внутри вебвью загружается полная версия веб-карт для тачей.
* Для работы с webview фидбека нужно просто поднять мобильную сборку<br/>
```ENTRIES=mobile make dev```<br/>
И добавить в урл следующие параметры: ```feedback-metadata[client_id]```, ```feedback-metadata[device_id]```, ```feedback-metadata[uuid]```, ```feedback-webview=1```, ```webview=true```. Например: <br/>
https://yandex.ru/maps/213/moscow/?feedback=map/edit&feedback-metadata[client_id]=ru.yandex.yandexmaps&feedback-metadata[device_id]=12345&feedback-metadata[uuid]=38c285c4-777e-a5d6-7caf-a169df3bce6a&feedback-webview=1&ll=37.597381,55.745915&webview=true&z=15<br/>

Внутри форм фидбека, фичи, которые должны быть доступны только для вебвью, лежат за флагом [feedbackDataUtils.isWebview(props.config)](../src/feedback/common/utils/feedback-data-utils.ts?rev=r9539511#L119)
