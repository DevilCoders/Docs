# Отображение времени окончания предложения по скидке на саммари

Клиентская проработка сделана в [discounts_on_summary.md](https://github.yandex-team.ru/taxi/rfc/blob/6f27d808ee7eb9a02fec30ab8dfea415c0463e7c/discount-notifications/discounts_on_summary.md).

Скидки на саммари реализованы на основе [случайных скидок](https://github.yandex-team.ru/taxi/rfc/blob/6f27d808ee7eb9a02fec30ab8dfea415c0463e7c/discount-notifications/random_discounts.md).

### Расширение ответа ручек roll и status

Согласно клиентcкой проработке в ответ ручек roll и status добавим поля:
```(json)
{
    "show_runaway_discout": true|false,
    "expire_at": "2016-02-07T19:45:00.922+00:00", // optional
    "discount_ttl_min": 6 // время жизни промокода в минутах, optional
    "supported_classes": ["econom"] // optional
    
    "button_info": {
        "title_message": "Заказать со скидкой 10%",
        "description_message": "Истекает через $TIMER$"
        "background_color": "#00CA50",
        "clip_color": "#00CA50"
    }
}
```

Для этого расширим схему эксперимента `random_discounts` следующими полями
```yaml
properties:
    is_runaway_discount:
        type: boolean
        description: признак того, что в эксперименте разыгрываются убегающие скидки
    promocode_ttl_for_user_min:
        type: integer
        description: |
            Отображаемое пользователю время жизни промокода.
            Значение должно быть немного меньше promocode_ttl,
            чтобы не возникло проблем при заказе на последних секундах.
            (если значение поля не задано, тогда пользователю показывается значение promocode_ttl)
        x-taxi-cpp-type: std::chrono::minutes
        minimum: 0
    supported_classes:
        type: array
        items:
            type: string
        description: |
            Список поддерживаемых данной скидкой тарифов.
            Если поле не заполнено, значит скидка действует для всех классов.
    button_info:
        $ref: '#/definitions/ButtonInfo'


definitions:
    ButtonInfo:
        type: object
        additionalProperties: false
        description: Описание скидки на кнопке тарифа на саммари
        required:
            - title_message_key
            - description_message_key
            - background_color
            - clip_color
        properties:
            title_message_key:
                type: string
                description: Танкерный ключ заголовка
            description_message_key:
                type: string
                description: Танкерный ключ описания
            background_color:
                type: string
                pattern: '^#[0-9A-Z]{6}'
            clip_color:
                type: string
                pattern: '^#[0-9A-Z]{6}'
```

Некоторые детали заполнения полей в ответе:
- expire_at: вычисляется как время создания промокода + его ttl отображаемый для пользователя
- discount_ttl_min: используется значение promocode_ttl_for_user_min, если его нет -- promocode_ttl
- button_info.title_message/button_info.description_message: 
  локализуется ключ из соответствующего поля эксперимента, для локализации передаются дополнительные параметры:
  - percent: процент скидки у выигранного промокода, 


### Синхронизация отображения скидки из ручки status c фактом выдачи промокода

В текущей реализаци случайных скидок возможна следующая ситуация:
в ручке roll успешно разыгрался промокод, запись в БД об этом была сделана,
но сам промокод получить не удалось из-за недоступности сервиса купонов. 
В таком случае ручка roll будет отдавать 500, но если клиентское приложение вызовет ручку status,
то она вернёт информацию о выигрыше (хотя фактически промокода у пользователя нет)

Для решения этой проблемы предлагается
расширить таблицу `random_discounts.random_discounts` новым полем `coupon_code`.

Ручка roll после генерации купона записывает в это поле полученный промокод.

Так как промокод привязан к конкретному пользователю, для которого он был сгенерирован,
то его значение безопасно писать в БД с точки зрения антифрода
(другие люди не смогут им воспользоваться).

Ручка status считывает значение этого поля, и если там будет null,
то в ответе выставляет `show_runaway_discout = false`, таким образом клиенты поймут,
что скидку отображать не нужно.
