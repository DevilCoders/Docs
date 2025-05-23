# Семейность 2.0, ЛК

## Цели

* Вырастить частотность пользователей, использующих семейный аккаунт Яндекс Такси
* Вырастить количество поездок через семейный аккаунт
* Пересадить пользователей на Плюс Мульти

### Предпосылки

* 3.2 млн пользователей с семейным такси (1.1 млн c >2 членов семьи)
* 1.3 млн. пользователей с Плюс Мульти, пересечение с семейным такси – 3-4%
* Доля «заказов другому» – 1.5% (оценка снизу)
* Поделиться поездкой (на waiting, driving) – 0.2%
* Слабый продукт текущего семейного аккаунта:
    * Нет лимитов на оплаты
    * Нет связи с Плюсом
    * Единственная ценность аккаунта – только шэринг банковской карты

### Доки

* [Figma](https://www.figma.com/file/JOZJKgQcQkyISf3XBqPnYd/%F0%9F%91%A8%E2%80%8D%F0%9F%91%A8%E2%80%8D%F0%9F%91%A6%E2%80%8D%F0%9F%91%A6-%D0%A1%D0%B5%D0%BC%D0%B5%D0%B9%D0%BD%D0%BE%D1%81%D1%82%D1%8C-%D0%B2-Go?node-id=831%3A89314)
* [Project](https://st.yandex-team.ru/TAXIPROJECTS-2387)

## Экраны

### Главное меню

![image](static/profile.png)

#### Как работает

На старте договорились реализовать функцинал без отображения участников, т.к. это позволяет сильно срезать углы на
разработке клиентской части. Кнопка "Моя Семья" будет отображаться при следующих условиях:

* Пользователь состоит в эксперименте `family_group_v2`
* В ответе `/3.0/paymentmethods` не вернулась информация о семейном
  аккаунте (`!coop_account.accounts[].type == 'family'`)

ИЛИ

* Пользователь состоит в эксперименте `family_group_v2`
* В ответе `/3.0/paymentmethods` для семейного аккаунта вернулась дополнительная информация о том, что акк переехал в
  паспорт (`coop_account.accounts[].type == 'family' && coop_account.accounts[].details.passport_account == true`)

Эксперимент будет приходить в ответе ручки `/launch` со значением `{"enabled": true}`

При этом если показывается новое меню семейного кабинета, старый должен быть скрыт. Текст для загловока кнопки и
сабтайтла будет приходить в эксперименте `coop_account` с учетом локализации.

После нажатия на кнопку клиентское приложение открывает главную страницу вебвью (url??).

### Стартовая страница семейного ЛК

### Как работает

После открытия главной страницы, клиент должен будет выполнить запрос бэкенда в ручку GET `/4.0/family/launch`. Ответ
эндпоинта будет содержать стартовую информацию о состоянии семейного аккаунта + список экспериментов участника аккаунта.
На основании этой информации клиентская часть определит, какой именно экран необходимо показывать в данный момент.

Более детальная логика формирования будет описана ниже.

Пример отвера эндпоинта:

```json
{
  // Информация о семейном аккаунте пользователя
  "family": {
    "id": "f1234",
    "name": "Моя семья",
    "role": "owner",
    "description": "2 участника",
    "has_invite": false,
    "members": [
      {
        "id": "12345",
        "name": "Никита",
        "avatar": ""
      }
    ]
  },
  // Выбранный платежный метод
  "payment_methods": [
    {
      "payment_system": "VISA",
      "card_number": "543219********1234"
    }
  ],
  // Список экспериментов, доступных пользователю
  "typed_experiments": {
    "version": 783039,
    "items": [
      {
        "name": "family_create_fullscreen",
        "cache_status": "no_cache",
        "value": {
          "enabled": true,
          "screen": {
            "srctions": []
          }
        }
      }
    ]
  }
}
```

В случае возникновения ошибок в сервисе family, будет возвращен 500 код ответа. Клиент в этом случае должен будет
показать заглушку с информацией о том, что ЛК временно недоступен.

#### Создание семейного аккаунта.

![image](static/create_account.png)

##### Условие показа

В ответе стартового эндпоинта вернулся пустой объект с информацией о семье пользователя (`family == {} || !family`). В
этом случае необходимо показать страницу создания аккаунта. При этом информация о шорткатах будет возвращаться в
эксперименте `family_create_fullscreen`.

Пример ответа API:

```json
{
  "typed_experiment": {
    "version": 783039,
    "items": [
      // ...
      {
        "name": "family_account_create_fullscreen",
        "cache_status": "cache",
        // информацию об эксперименте можно кэшировать на клиенте
        "value": {
          "enabled": true,
          "l10n": {
            "create_family_title": "Моя семья",
            "lookup_ride_info": "Просмотр поездки",
            "in_real_time": "В реальном времени",
            "rides_history": "История поездок"
          },
          "screen": {
            "sections": [
              {
                // Шорткаты должны показыаться в порядке, указанном в массиве
                "shortcut_ids": [
                  "family_create:1",
                  "family_create:2"
                ],
                "title": "create_family_title"
              }
            ],
            "offers": [
              {
                "shortcut_id": "family_create:1",
                // По дефолту считаем ширину экрана = 6. Если следующий элемент не помещается, 
                // его необходимо переносить на другую стоку  
                "width": 4,
                "height": 2,
                "icon": "icon_tag",
                "background": {
                  "color": "#F1F0ED"
                },
                "text_style": {
                  "color": "#000000"
                },
                // Значения для title/subtitle берутся из корневого объекта l10n
                "title": "lookup_ride_info",
                "subtitle": "in_real_time",
                "action": {
                  "type": "deeplink",
                  "deeplink": "yataxi://some_page"
                }
              },
              {
                "shortcut_id": "family_create:2",
                "width": 2,
                "height": 2,
                "background": {
                  "color": "#F1F0ED"
                },
                "text_style": {
                  "color": "#000000"
                },
                "title": "Просмотр поездки",
                "action": {
                  "type": "deeplink",
                  "deeplink": "yataxi://some_page"
                }
              }
            ]
          }
        }
      }
    ]
  }
}
```

Шорткаты необходимо отображать в том же порядке, в котором они обозначены в объекте sections. В дальнейшем для этой
страницы возможно наличие нескольких секций, как например, сделано для самокатов, из-за этого объект отдается массивом.

Значение текстовок для всех ключей, с названием `title||subtitle` хранятся в корне эксперимента, ключе `l10n`. Это
сделано из-за ограничений возможности локализации экспов - локализованными могут быть только ключи, находящиеся в корне
значений эксперимента. Если по каким-то причинам ключ отсутствует в объекте `l10n`, текст не должен быть показан на
клиенте.

Определение размеров шорткатов предлагается расчитывать на клиенте из следующих вводных:

* Суммарная максимальная ширина шорткатов, которые можно уместить на строке - 6 абстрактных единиц (параметр `width` в
  инфе по шорткату)
* Расстояние между шорткатами == 0.2 абстрактные единицы
* Расстояние до границ == 0.2 абстрактные единицы

Потенциально есть вероятность того, что эксперимент с шорткатами не придет в случае недоступности сервиса экспериментов.
Клиент в этом случае должен показать пустой экран с кнопкой "Создать семью". Бэкап текстов должен быть зашит на клиенте.

Текст для кнопки создания и блока условий политики конфиденциальности будет приходить в отдельном эксперименте
family_account. Пример экспа в ответе ручки:

```json
{
  // ...
  "typed_experiment": {
    "version": 1234,
    "items": [
      {
        "name": "family_account",
        "cache_status": "cache",
        "value": {
          "enabled": true,
          "l10n": {
            "create_account_button_text": "Создать аккаунт и выбрать участников",
            "privacy_policy_agreement": "Принимая приглашение вы соглашаетесь с политикой конфиденциальности"
            // Остальные ключи, используемые для локализации
          }
        }
      }
    ]
  }
}
```

Кнопка должна быть задизейблена до тех пор, пока клиент не нажмет на чекбокс с условиями конфиденциальности. После
нажатия на кнопку создания семьи мобильным клиентом должен быть отправлен запрос на бэкенд POST `4.0/family/create` с
объектом `{"user_agreement_accepted": true}`. В случае, если пользовательское соглашение не было принято, или при
наличии ошибок на стороне паспорта на клиента будет возвращена ошибка с детализированной информацией о причинах. Формат
и текст ошибок будет детализирован в рамках задачи по созданию эндпоинта.

После получения успешного ответа о том, что семья создана, клиент должен быть переброшен на нативную страницу с выбором
контактов для добавления в семейный аккаунт. После того, как контакт будет выбран, необходимо отправить запрос на бэкенд
в ручку `/4.0/family/v1/invite` с телом запроса

```json
{
  "phone": "89651447572"
}
```

В этот момент бэкенд создаст инвайт в семейный аккаунт на стороне Паспорта, и сохранит в локальной базе связку phone_id
+ invite_id для показа пользователю на старте приложения.

#### Создание семейного аккаунта при отсутствии карты

##### Условие показа

Сценарий - пользователь нажал на создание семьи, но закрыл ЛК на моменте выбора карты. Бэкенд в этот момент уже создаст
семью в паспорте, но на кнопке создания должна быть другая текстовка. Логика показа - в ответе стартовой ручке пришла
информация о семье, но ответ paymentmethods пустой.

Текстовка для кнопки будет лежать в эксперименте `family_account`, ключе `add_account_payment_method`.

#### Создание семейного аккаунта при наличии карты

![image](static/create_account_with_card.png)

##### Условие показа

В ответе стартового эндпоинта вернулся объект с информацией о семье пользователя, но в нем отсутствуют участники. Так же
в объекте `payment_methods` присутствует информация о добавленной карточке.

Пример ответа API:

```json
{
  // Информация о семейном аккаунте пользователя
  "family": {
    "id": "f1234",
    "name": "Моя семья",
    "role": "owner",
    "description": "2 участника",
    "has_invite": false,
    "members": []
  },
  // Выбранный платежный метод
  "payment_methods": [
    {
      "type": "card",
      "payment_method_id": "card-12345",
      "payment_system": "VISA",
      "card_number": "543219********1234"
    }
  ],
  // Список экспериментов, доступных пользователю
  "typed_experiments": {
    // ...
  }
}
```

В этом случае информация о шорткатах так же будет получаться из объекта экспериментов, как в примере выше.

Иконки для платежных систем предлагается зашить на клиенте. Возможные варианты будут описаны в рамках реализации задачи
по добавлению эндпоинта. После нажатия на кнопку клиент должен будет открыть нативный экран со списком контактов.

Текстовка для кнопки будет лежать в эксперименте `family_account`, ключе `add_account_members`.

#### Приглашение в семью

![image](static/account_invite.png)

##### Условие показа

В ответе стартовой ручки возвращается объект `family.has_invite` == true.

Информация о шорткатах будет приходить в эксперименте `family_account_invite_fullscreen`. Структура ответа аналогична
структуре шорткатов на старте.

Тексты для кнопок будет лежать в эксперименте `family_account`, ключах `agree_family_invite` и `decline_family_invite`.
Текст пользовательского соглашения будет приходить в том же ключе, что и при создании аккаунта.

При нажатии на кнопку "В другой раз" клиент должен отправить запрос на бэк в ручку
POST `4.0/family_account/member/invite/declined`, и после получения ответа закрыть вебвью. Более детальный API, а так же
информация об ошибках будет описана в рамках отдельных задач на реализацию эндпоинта.

При нажатии на кнопку "Принять приглашение" отправляется запрос в ручку `4.0/family_account/member/invite/agree` с телом
`{"user_agreement_accepted": true}`. В случае ошибки на бэкенде будет возвращен 500 статус ответа - в этом случае
необходимо показать пользователю экран с информацией о недоступности семейного ЛК. Более детальное описание API
аналогично предыдущему кейсу будет осуществлено в рамках задачи по разработке эндпоинта.

#### Изменение семейного аккаунта

##### Условия показа

В ответе стартового эндпоинта вернулся не пустой объект с информацией о семье пользователя (`family`). Менять данные о семье может только администратор семьи.

Тело запроса на PUT `/4.0/family/v1/<family_id>/update` должно содержать следующие значения:

```json
{
  "name": "Новое имя семьи"
}
```

В случае успешного выполнения API возвращает пустое тело с кодом `204 No Content`.

Если пользователь не является частью указанной семьи или не является администратором, то возвращается `403 Forbidden`.