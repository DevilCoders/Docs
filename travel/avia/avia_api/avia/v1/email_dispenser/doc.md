# Терминология
* **id** - идентификатор подписчика. Выдается, например, ручкой `subscribe`, `user_subscription`
* **passportuid** - идентификатор залогиненого пользователя, например `36972065`
* **passportuid_hashed** - sha256 хеш от passportuid. Если не хочется считать руками, то такой хеш должен приходить в письме на подтверждение (2opt-in), спрятан в ссылке на главное кнопке (смотри параметр `p`)
* **qkey** - идентификатор подписки.
Структура <точка отправления>\_<точка прибытия>\_<дата в ту сторону YYYY-MM-DD>\_<дата в обратную сторону или 'None'>\_<тип билета (например economy)>\_<кол-во взрослых>\_<кол-во детей>\_<кол-во младенцев>_<нац версия (например ru)>.
Например `c213_c2_2017-12-19_None_economy_2_1_0_ru`
* **session** - любая сессионная кука
* **sessions_hashed** - sha256 хеш от сессии. Также как и *passportuid_hashed* приходит в письмо 2opt-in (смотри параметр `s`)

# API
## Подписка
### По email
#### С паспортом

`curl 'https://<API_HOST>/email_subscription/v1.0/subscribe?email=<email>&passportuid=<passportuid>&qkey=c213_c2_2018-04-01_None_economy_1_0_0_ru&email_source=VALERA'`

#### Без паспорта (по сессии)

`curl 'https://<API_HOST>/email_subscription/v1.0/subscribe?email=<email>&session=<session>&qkey=c213_c2_2018-04-01_None_economy_1_0_0_ru&email_source=VALERA'`

### Только по passportuid

`curl 'https://<API_HOST>/email_subscription/v1.0/subscribe?passportuid=<passportuid>&qkey=c213_c2_2018-04-10_None_economy_1_0_0_ru&email_source=VALERA'`

### Ответы
#### Если подтверждение не нужно

```json
{
    "status": "success",
    "data": {
        "required_double_opt_in": false,
        "id": "54f62277-efdb-4839-a3e2-bcfad309c7e5",
        "pending": false
    }
}
```

#### Если подтверждение нужно

```json
{
    "status": "success",
    "data": {
        "required_double_opt_in": true,
        "id": "54f62277-efdb-4839-a3e2-bcfad309c7e5",
        "pending": false
    }
}
```

#### Если подтверждение нужно и мы его уже отправляли, но пользователь ещё не подтвердил

```json
{
    "status": "success",
    "data": {
        "required_double_opt_in": true,
        "id": "54f62277-efdb-4839-a3e2-bcfad309c7e5",
        "pending": true
    }
}
```


## Подписка с фильтрами

Работает также как и предыдущие ручки подписок, но кроме стандартных параметров нужно передавать фильтр в формате json.
Фильтр передаётся как form-data поле filter в виде строчки.

### Формат фильтров

```json
{
    "withBaggage": true, // Фильтр багажа
    "airlines": [1,2,5,7,15], // Фильтр авиалиний
    "transfer" : { // Фильтры пересадок
        "count": 3, // Максимально допустимое количество пересадок
        "minDuration": 4, // Минимальная продолжительность. Не имплементировано из-за отсутствия поддерживающего кода на фронте
        "maxDuration": 6, // Максимальная продолжительность. Не имплементировано из-за отсутствия поддерживающего кода на фронте
        "hasAirportChange": false, // Запрет смены аэропорта
        "hasNight": false // Запрет ночных пересадок
    },
    "time":{ // Фильтры времени
        "forwardArrival": 1, // Время суток прилёта туда
        "forwardDeparture": 1, // Время суток вылета туда
        "backwardArrival": 3, // Время суток прилёта обратно
        "backwardDeparture" : 4 // Время суток вылета обратно
    },
    "airport" : { // Фильтры аэропортов
        "forwardDeparture": [1, 2], // Разрешенные аэропорты вылета туда
        "forwardArrival": [3, 4], // Разрешенные аэропорты прилета туда
        "forwardTransfers": [5, 6], // Разрешенные аэропорты пересадок туда
        "backwardDeparture": [3, 4], // Разрешенные аэропорты вылета обратно
        "backwardArrival": [1, 2], // Разрешенные аэропорты прилета обратно
        "backwardTransfers": [5, 6] // Разрешенные аэропорты пересадок обратно
    },
    "filter_url_postfix" : "#tt=1,0,0,0,0,0&bg=1&t=f|d|3b|d|" // Постфикс url для формирования фильтрованной выдачи
}
```
#### Фильтр багажа
**withBaggage** Два валидных значения: true - вариант только с багажом, null - не фильтруется. 
#### Фильтр авиалининй
**airlines** Разрешенный список кодов (id) авиакомпаний. 
Валидные варианты: список с кодами - отбрасывает варианты перелётов с авиакомпаниями, которых нет в списке; 
null - нет фильтра ( не путать с пустым списком ).
#### Фильтр пересадок
**count** Валидные значения - целое число больше нуля, обозначающее количество пересадок на маршруте. Применяется как к сегментам "туда", так и к сегментам "обратно". null - отсутствие фильтрации.

**hasAirportChange** Валидные значения - false запрещает сменять аэропорт, null - отсутствие фильтра.

**hasNight** Валидные значение - false запрещает ночную пересадку, null - отсутствие фильтра.
#### Фильтры времени
Фильтруют время суток вылета и прилёта. 1 - утро, 2 - день, 3 - вечер, 4 - ночь. null - отсутствие фильтра.

#### Фильтры аэропортов
По смыслу такие же как фильтры авиалиний. 
При наличии списка кодов (id) аэропортов убирает все варианты, которых нет в списке; null - отсутствие фильтра.

Все поля опциональны, так же как и в price index. Вместо null можно просто не передавать ключ фильтра.
Это касается фильтров на любом уровне. Например, мы можем передать фильтр вида
```json
{
    "withBaggage": true, // Фильтр багажа
    "transfer" : { // Фильтры пересадок
        "count": 3, // Максимально допустимое количество пересадок
        "hasAirportChange": false, // Запрет смены аэропорта
        "hasNight": null // Запрет ночных пересадок
    },
    "time": null,
    "airport": null,
    "filter_url_postfix" : "#tt=1,0,0,0,0,0&bg=1&t=f|d|3b|d|" // Постфикс url для формирования фильтрованной выдачи
}
```
Здесь фильтр airlines не был передан, можно было вместо этого передать `"airlines": null`. в фильтре transfer передан hasNigh:null, значит фильтроваться ночные пересадки не будут. И так далее...
 
## Подтверждения согласия на получения писем
### По паспорту

`curl 'https://<API_HOST>/email_subscription/v1.0/confirm?id=54f62277-efdb-4839-a3e2-bcfad309c7e5&p=<passportuid_hashed>'`

### По email

`curl 'https://<API_HOST>/email_subscription/v1.0/confirm?id=54f62277-efdb-4839-a3e2-bcfad309c7e5&s=<session_hashed>'`



```json
{
  "status":"success",
  "data":{
    "id":"54f62277-efdb-4839-a3e2-bcfad309c7e5"
  }
}
```
## Получить список подписок пользователя 
### По паспорту

`curl 'https://<API_HOST>/email_subscription/v1.0/user_subscriptions/list?passportuid=<passportuid>'`

### По email

`curl 'https://<API_HOST>/email_subscription/v1.0/user_subscriptions/list?email=<email>'`

### Ответы

```json
{  
  "status":"success",
  "data":{  
    "id":"b6860403-b7f0-4cf2-9a16-d229c15ed0b3",
    "subscriptions":[  
      "c213_c54_2017-12-21_2018-01-05_economy_1_0_0_ru",
      "c213_c2_2017-12-19_None_economy_2_1_0_ru"
    ]
  }
}
```

## Проверить подписан ли пользватель на направление
### По пасспорту:

`curl 'https://<API_HOST>/email_subscription/v1.0/user_subscriptions?passportuid=<passportuid>&qkey=c213_c54_2017-12-21_2018-01-05_economy_1_0_0_ru'`

### По email:

`curl 'https://<API_HOST>/email_subscription/v1.0/user_subscriptions?email=<email>&qkey=c213_c54_2017-12-21_2018-01-05_economy_1_0_1_ru'`


### Ответы
#### Если подписан

```json
{  
  "status":"success",
  "data":{  
    "id":"b6860403-b7f0-4cf2-9a16-d229c15ed0b3",
    "subscribed":true,
    "filter": "#tt=1,0,0,0,0,0&bg=1",
    "qkey": "c213_c54_2017-12-20_2018-01-04_economy_1_0_1_ru",
    "date_range": 2
  }
}
```

#### Если не подписан

```json
{  
  "status":"success",
  "data":{  
    "id":"b6860403-b7f0-4cf2-9a16-d229c15ed0b3",
    "subscribed":false,
    "filter": null,
    "qkey": null,
    "date_range": null
  }
}
```

####  Если такого пользователя нет:

```json
{  
  "status":"success",
  "data":{  
    "id":null,
    "subscribed":false,
    "filter": null,
    "qkey": null,
    "date_range": null
  }
}
```


## Отписка от всех направлений
`curl 'https://<API_HOST>/email_subscription/v1.0/unsubscribe?id=54f62277-efdb-4839-a3e2-bcfad309c7e5'`
```json
{  
  "status":"success",
  "data":{  
    "id":"54f62277-efdb-4839-a3e2-bcfad309c7e5"
  }
}
```

## Отписка от направления

`curl 'https://<API_HOST>/email_subscription/v1.0/unsubscribe/by_direction?id=54f62277-efdb-4839-a3e2-bcfad309c7e5&qkey=c213_c54_2017-12-21_2018-01-05_economy_1_0_1_ru'`

```json
{  
  "status":"success",
  "data":{  
    "id":"54f62277-efdb-4839-a3e2-bcfad309c7e5"
  }
}
```

# Команды для работы с сервисом подписок
для выполнения команды на сервере в тестинге или проде делаем так.
```bash
cd /app
source ./env/bin/activate
python manage.py <command_name>
```
Первые две строчки необходимо выполнить один раз после входа, чтобы активировать виртуальное окружение.
### Отправка писем
`python manage.py send_emails` Отправляет письмо об изменении цен всем пользователям

`python manage.py send_email_to vasya@pupkin.ru` Отправляет письмо об изменении цен только для vasya@pupkin.ru

### Прогрев

`python manage.py preheat_subscriptions`
Прогревает холодные за последние сутки подписки. Процесс долгий, может длиться несколько часов

### Обновление подписок

`python manage.py update_subscriptions`
Обновляет минимальные цены для подписок. Процесс долгий, на проде длиться около 40 минут

### Тестирование

`python manage.py set_test_min_price_for_direction c213_c2_2019-05-02_None_economy_1_0_0_ru` 
Устанавливает пару случайных минимальных цен за сегодня и вчера для направления `c213_c2...`. Не работает в проде.

`python manage.py set_test_min_price_for_filtered_direction c213_c2_2019-05-02_None_economy_1_0_0_ru` 
Устанавливает пару случайных минимальных цен за сегодня и вчера для фильтрованных подписок.


# Отправка писем. Расширеннные письма с блоком фильтров.
## Формат данных, приходящих в jinja шаблон
```json
{
    "content" : {
        "diff": 123.5, // Разница между старой и новой ценой
        "point_from": "Сансара", // Название пункта отправления и прибытия
        "point_to": "Нирвана",
        "date_forward": "12 мая", // Дата туда в родительном падеже
        "date_backward": "15 мая", // Дата обратно. Может отсутствовать если полёт только туда
        "price": 200.12, // Новая цена на направление
        "currency": "EUR", // Код валюты, в которой пришла цена
        "old_price": 76.62, // Старая цена на направление
        "old_currency": "EUR",
        "unsubscribe_by_direction_link": "https://avia.../unsubscribe?id=...", // Ссылка на отписку от направления
        "avia_search_link": "https://avia...",  // Ссылка на поиск
        "calendar_link": "https://avia...",  // Ссылка на календарь цен
        "min_price_variant_data": {// Данные по вариантам с минимальными ценами
            "forward": { // Данные по варианту вперёд
                "departure_time": "12:00",
                "arrival_time": "13:10",
                "departure_date": "15.02",
                "arrival_date": "15.02",
                "airlines": "Уральские Авиалинии, Победа",
                "airlines_count": 2,
                "airline_avatar": null or 'http://avatars.mds3...../orig', // Ссылка на png в аватарнице
                "connections": "2 пересадки"
            },
            "backward": {}, // Данные по варианту назад. Такой же формат как и у forward
            "price": 200.12,
            "currency": "EUR",
            "order_link": "https://...", // Ссылка на непротухающую покупку
        }, 
        "popular_section_variants_data": {}, // Данные по варинатам с популярными направлениями
        "other_data": {}, // Другие данные (Например, если популярные данные лежат под фильтрами, здесь будет нефильтрованная выдача)
    }
}

```
