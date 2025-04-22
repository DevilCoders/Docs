## Новый экран отмен

В рамках проекта делаем окно из скрина ниже

![image](static/modal_window.png)

Зачем - снижение колличества отказов от поездки пользователями за счет новой коммуникации.

## Техническая реализация

### Клиент

Для статусов заказа `driving` и `assigned` в ответе ручки `3.0/taxiontheway` будет приходить в т.ч. и информация по
модальному окну, которое необходимо показать клиенту в случае тапа на кнопку отмены.

Логика показа - если приходит объект нового экрана отмены - показываем его - если нет - старый экран. Все эксперименты,
связанные с логикой показа, будут жить целиком на бэкенде.

В качестве API предлагается частично переиспользовать компонент, реализованный в рамках СБП:

```yaml
ModalWindow:
    type: object
    additionalProperties: false
    description: Модальное окно с информацией об отмене
    required:
        - id
        - title
        - text
        - buttons
    properties:
        id:
            type: string
            description: Идентификатор окна
        title:
            type: string
            description: Заголовок. В примере выше "Водитель Михаил уже едет к вам"
        text:
            type: string
            description
        icon:
            type: object
            additionalProperties: false
            description: |
                Картинка в верхнем углу
                Из image_tag/image_url приходит что-то одно
            properties:
                image_tag:
                    type: string
                image_url:
                    type: string
                badge_text:
                    type: string
                    description: Текст в шильдике
        buttons:
            type: object
            required:
                - orientation
                - items
            properties:
                orientation:
                    type: string
                    description: Ориентация кнопок в модальном окне
                    enum:
                        - horizontal
                        - vertical
                items:
                    type: array
                    description: |
                        Массив кнопок, показываемый слева на право или сверху вниз в зависимости от ориентации
                    items:
                        $ref: '#/components/schemas/ModalWindowButton'


ModalWindowButton:
    type: object
    additionalProperties: false
    required:
        - text
        - color
        - action
    properties:
        text:
            type: string
        color:
            type: string
            example: 'HEX'
        action:
            oneOf:
                - $ref: '#/components/schemas/CancelAction'
                - $ref: '#/components/schemas/TypedDoNothingAction'

CancelAction:
    type: object
    additionalProperties: false
    required:
        - type
    properties:
        type:
            type: string
            enum:
                - cancel

TypedDoNothingAction:
    type: object
    additionalProperties: false
    required:
        - type
    properties:
        type:
            type: string
            enum:
                - do_nothing
```

Пример ответа `3.0/taxiontheway`:

```json
{
    // ...
    "notifications": {
        "order_cancel_notification": {
            "id": "r9wB4RkEv6",
            "title": "Водитель Михаил уже едет к вам",
            "icon": {
                "image_url": "https://icon.url"
            }
            "text": "Если отменить сейчас, поиск новой машины может быть дольше",
            "buttons": {
                "orientation": "horizontal",
                "items": [
                    {
                        "text": "Отменить заказ",
                        "color": "#HEX",
                        "action": {
                            "type": "cancel"
                        }
                    },
                    {
                        "text": "Подождать водителя",
                        "color": "#HEX",
                        "action": {
                            "type": "do_nothing"
                        }
                    }
                ]
            }
        }
    }
}
```

В случае, если с бэкенда не пришло изображение, или клиенту не удалось его загрузить - ничего не отображаем. Так же в
этом случае игнорируем поле `badge_text`.

Если с бэкенда приходит тип отображения кнопок `horizontal`, и количество кнопок более 2,
в приложении они должны отображаться вертикально.

При нажатии пассажиром на кнопку с типом `CancelAction` по аналогии с текущей отменой клиентом отправляется информация
об отмене в `/totw`.

### Бэкенд

Потребуются доработки в двух компонентах:

* **api-proxy-critical**

  Необходимо будет добавить дополнительный объект к ответу ручки, получаемый из сервиса inapp-communication. В случае
  недоступности ресурса, или каких-либо ошибок, никакой информации возвращаться не должно.

* **inapp-communications**

  Для ручки `promos-on-the-way` добавляем новую коммуникацию, информация в которой кастомизируется экспериментом, и
  зависит в т.ч. от текущего статуса заказа.

## Ограничения решения

* В шильдике над фото водителя показываем только текст
* Если захотим показывать динамическую информацию в тексте модалки (например, оставшееся время), могут быть сложности
  из-за кэширования запросов на бэкенде, и потребуется доп проработка
