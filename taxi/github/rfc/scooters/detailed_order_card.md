## Задача
[TAXIPROJECTS-2652](https://st.yandex-team.ru/TAXIPROJECTS-2652)

## Новый экран
Детальная карточка поездки будет показываться на ``screen: totw`` и ``mode: scooters``. Чтобы не ограничиваться одним заказом, предлагается сразу указать сессию, по которой нужно получить детальную информацию, сделать это можно, отправив ``session_id`` в запросе к ``layers``:
```(python)
request["state"]["scooters"] = {
    "session_id": "SESSION_ID"
}
```
В ответе клиенту приходит самокат по указанной сессии, а также парковки.

## Новый action
Для того, чтобы клиенты могли отобразить баббл построения маршрута, нужно вернуть им ``BubbleAction`` с типом ``show_navigation``. Возвращать его будем только на парковки на ``screen: totw`` и ``mode: scooters`` (управляется экспериментом)
```(yaml)
BubbleAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
                - show_navigation
        attributed_text:
            $ref: "#/definitions/AttributedText"
        buttons:
            items:
                type: object
                additionalProperties: false
                properties:
                    type: 
                        type: string
                        enum: 
                            - confirm
                            - reject
                    attributed_text:
                        $ref: "#/definitions/AttributedText"
                required:
                    - type
                    - attributed_text
    required:
        - type
        - attributed_text
        - buttons
```