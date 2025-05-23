# Rubick - конструктор форм добавления и редактирования

Решает следущие задачи:
- Представляет черновик или объявление в виде набора лейаутов для формы добавления или редактирования соответственно.
- Определяет количество (зависит от категории) и порядок лейаутов на форме.
- Определяет текущий и последний шаги формы добавления.
- Предоставляет апи для работы с текущей формой добавления пользователя.
- Предоставляет апи для редактирования существующего объявления через форму редактирования.
- Пописывает и раздает url-ы для загрузки фотографии в черновик или объявление.
- Валидирует принадлежность телефонов пользователю.

Не решает следущие задачи:
- Прокачка картинок (этим занимается uploader).
- Валидация значений полей черновика: атрибутов, цены, описания и т.д. (этим занимается gost).

## Сущности

`Control/Контрол` - лейаут, элемент формы, отвечающий за ввод определенного параметра объявления.
Каждый контрол имеет тип и количество [типов контролов ограничено](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/rubick/add_form_model.proto#L24-L36). Предполагаем, что фронт заранее знает список всех возможных контролов.
Контрол содержит в себе все для его отображения на клиенте:
- Значение поля (если есть)
- Настройки поля(например для атрибутов)
- Ограничения, накладываемые на поле
- Ошибку валидации (если есть)

`Section/Секция` - шаг формы, состоящий из нескольких контролов.

`Draft/Черновик` - неопубликованное объявление, находящееся на стадии заполнения полей.
Может содержать невалидную информацию.
У пользователя может быть только один текущий черновик, который он может изменять через форму добавления.

`Add form/Форма добавления` - форма для работы с черновиками.

`Offer/Объявление` - опубликованное объявление.

`Edit form/Форма редактирования` - форма для редактирования оферов.


## Этапы реализации

В первой реализации rubick строит форму по следующей схеме:
1. Секция категории:
    1. Контрол категории
2. Секция описания:
    1. Контрол названия объявления
    2. Контрол текстового описания объявления
    3. Контрол фотографий
    4. Контрол видео
3. Секция атрибутов - содержит по контролу на каждый атрибут категории объявления.
4. Секция цены:
    1. Контрол цены
5. Секция контактов:
    1. Контрол контактов
6. Секция адресов
    1. Контрол адресов
 

На втором этапе (вероятно, уже после запуска серсива) предполагаем разработку хранилища конструторов форм и админки к нему, 
для того, чтобы контент менеджеры могли менять внешний вид формы добавления для определенных категорий, не привлекая разработку.

## Компоненты

### Публичное апи формы добавления

Предоставляет пользователю апи для работы с текущим церновиком. [Описание gRPC сервиса](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/rubick/add_form_api.proto#L10).

##### Плоский список контролов
При передаче специального флага все методы апи формы добавления возвращают форму в виде плоского списка контролов, то есть в каждой секции по 1 контролу. (Нужно для тача)

##### Текущая секция
Апи позволяет клиенту сохранять порядковый номер текущего контрола формы добавления (считая все секции по порядку). Если контрол не передан, в апи, считается, что текущий - самый первый.
Текущая секция вычисляется из номера текущего контрола и передается ответе формы добавления.

#### Запрос черновика
1. Клиент запрашивает текущий черновик пользователя через gateway.
2. Gateway посылает запрос в rubick, а тот идет в gost.
3. Gost достает черновик из базы (создает, если его не было) и валидирует его. Ошибки валидации и ограничения на атрибуты отдаются в rubick плоским списком.
4. Далее rubick раскладывает значение полей черновика и ошибки по контролам. Порядок контролов зависит от категории, а также существует порядок по умолчанию.
5. Контролы объединяются в секции. При этом rubick помечает последнюю и текущую секции.

#### Обновление черновика
1. Клиент присылает частично заполненный черновик.
2. Gateway посылает запрос в rubick, а тот пытается обновить черновик через gost, получая ошибки валидации.
Далее как в пунктах 4 и 5 запроса черновика.

#### Публикация черновика
Если в черновике присутствуют ошибки валидации - логика идентична обновлению черновика. При отсутствии ошибок валидации черновик публикуется через gost, rubick возвращает id опубликованного объявления.

### Публичное апи формы редактирования

Предоставляет пользователю апи для изменения офера. [Описание gRPC-сервиса](https://github.com/YandexClassifieds/schema-registry/blob/701bc8a8edeb241a69bc1275b8ded4b1018d31de/proto/general/rubick/edit_form_api.proto#L12)

#### Получение офера в виде формы
Логика идентична получению текущего черновика апи формы добавления, но при этом работа идет с объявлением, и rubick не помечает текущую и последнюю секции.

#### Валидация обновленного офера
Логика идентична обновлению черновика апи формы добавления, но при этом работа идет с объявлением, а гост не сохраняет объявление после валидации.

#### Сохранение обновлений объявления
Логика идентична объявлению черновика апи формы добавления, но при этом работа идет с объявлением, а сохранение происходит только при отсутствии ошибок валидации.
