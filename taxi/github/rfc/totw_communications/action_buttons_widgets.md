
## Задача: научиться получать в `/taxiontheway` промоблоки с виджетами action_buttons и обрабатывать нажатия

![image](static/action_button.png)

###Клиентская логика

-В totw добавляется новый тип виджетов - action_buttons
У action_button'ов может быть три типа экшена - "deeplink", "request_totw_with_key_and_value" и "pick_contact_for_totw"

-В случае с типом deeplink клиент проверяет, что диплинк не пустой и открывает его.
На андроиде поддержан тип диплинка(deeplink source), заводим новый - TOTW_PROMOTION,
необходимо для корректного прокидывания в web view 

-В случае с типом request_totw_with_key_and_value необходимо отправлять action с ключом и значением,
которые клиент считывает и отправляет user_actions в ручку taxiontheway 

-В случае с pick_contact поднимаем окно выбора контактов и отправляем в ручку taxiontheway
Например:
```
{
    ...
   "order_contact": {
        "name": "Никита", // Optional
        "phone": "+79340000000" // Required
   }

}
```

Пример ответа taxiontheway
```
{
    ...
    "promotions": {
      "promoblocks": {
        "items": [
            {
                "title": {
                    "items": [
                      {
                        "type": "text",
                        "text": "Добавить Никиту в семью?"
                      }
                    ]
                },
                "icon": {
                   "image_url": "..."
                 }
                ...
                "widgets": {
                    "action_buttons": [
				        { // deeplink action
				            "text": "Да",                       // Required
				            "color": "#fae436",      		    // Optional
				            "text_color": "#ffffff",  			// Optional
                            "action": {                         // Required
                               "type": "deeplink",       // Required
                               "deeplink": "https://yandex.ru", // Optional. Use with target deeplink
                            }
                        },
                        { // request totw action
                            "text": "Нет",                      // Required
                            "color": "#fae436",                 // Optional
                            "text_color": "#ffffff",            // Optional
                            "action": {                         // Required
                                "type": "request_totw_with_key_and_value",
                                "key": $$KEY$$,
                                "value": $$VALUE$$
                            }
                        },
                        {
                            "text": "Да",                       // Required
                            "color": "#fae436",      		    // Optional
                            "text_color": "#ffffff",  			// Optional
                            "action": {                         // Required
                                "type": "pick_contact_for_totw",       // Required
                                "title": "Выберите контакт для заказа другому",
                                "button_title": "Выбрать"
                            }
                        }
			      	]
                }
            }
        ]
      } 
    }
    ...
}
```

Пример запроса в taxiontheway

```
{
    ...
    "user_actions": {
    		"$$KEY$$": {
    			"value": $$VALUE$$
    		}
    	}
}
```

## Дополнение для action_buttons: action типа modal_view

Добавляем новый action для action_buttons. Он в первую очередь заиспользуется для флоу метода оплаты SBP, чтоб по кнопке "Как оплатить" можно было показывать окошко с пояснением. Пример на картинке ниже
![image](https://jing.yandex-team.ru/files/maxim-ivanov/Screen%20Shot%202022-04-08%20at%203.19.55%20PM.png)

```yaml
Color:
    type: string
    description: |
        возможно как точное значение типа '#FF00FF',
        так и цвет из палитр  control, bgMain и тд

Button:
    type: object
    additionalProperties: false
    properties:
        text:
            type: string
        color:
            $ref: '#/definitions/Color'
        text_color:
            $ref: '#/definitions/Color'
    required:
        - text
        - color
        - text_color

ModalViewAction:
    type: object
    additonalProperties: false
    properties:
        type:
            type: string
            enum:
              - modal_view
        icon_tag:
            type: string
        title:
            type: string
            description: Заголовок модалки
        attributed_text:
            $ref: 'где-то-там/#/definitions/AttributedText'
            description: как в /layers/attributed_text.md
        button:
            $ref: '#/definitions/Button'
    required:
      - type
      - title
      - attributed_text
      - button
        
```
