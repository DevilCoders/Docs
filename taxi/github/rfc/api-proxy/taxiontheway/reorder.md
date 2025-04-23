## Бизнесовая задача

Сервис отвечат за перезаказы.
Сейчас в нем только ручки для taxiontheway, но в него можно забрать все наши перезаказы. Сейчас это функционал, который понимают только очень опытные сотрудники, а так может получше станет.

## Архитектура

### API

Ручка `GET /v1/suggest_reorder`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
  "reorder": {
    "cancel_button_title": "Отмена",
    "message": "Цена выросла до 214 $SIGN$$CURRENCY$",
    "notification_message": "Спрос на такси увеличился — сейчас мы не можем найти машину по старой цене.",
    "options": [
      {
        "button_title": "Подтвердить",
        "decision_id": "8b1c547bcd731ad498b31aef65d7bf41"
      }
    ],
    "price_description": "Спрос на такси увеличился — сейчас мы не можем найти машину по старой цене. \\n\\nВы согласны на повышение цены?"
  },
  "surge": {}
}
```

Ручка `GET /v1/autoreorder`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
  "autoreorder": {
    "text": "К сожалению, водитель не смог выполнить заказ. Мы уже ищем замену"
  }
}
```


### v1/suggest_reorder
Смотрит на `order_proc["reorder"]["suggestions"]` и в зависимости от этого готовит или поле reorder или поле surge. В проде примеров с полем surge не нашел.
####  Fallback
Сложно сказать. Если реордер реально есть и его нужно показать, то это нельзя игнорировать. Но как при фейле ручки понять, есть ли реордер - непонятно. Вероятно, можно пока просто игнорировать фейлы. 


### v1/autoreorder
Если мы автоматически начали искать нового водителя, выдаст соответствующий текст. Инфу об этом грузит из `order_proc["order_info"]["statistics"]`. Подробнее тут Order::BuildDataAutoreordered
#### Fallback
Можно не показывать.


### Технические детали и ограничения
1. Если сделаем сервис и он действительно будет отвечать за перезаказ, нужно посмотреть на корпов, они хотели свой функционал по реордеру. Подробности тут https://st.yandex-team.ru/TAXICORP-1928
2. Даня Бровцев в задаче https://st.yandex-team.ru/TAXIBACKEND-21097 неплохо разобрал имеющиеся механизмы реордера. Главное:
Судя по всему сейчас есть 3 похожих вещи в такси, связанные с перезаказами.
Реордер: ((https://github.yandex-team.ru/pages/taxi/schemas/Taxi_Documentation/Backend-cpp%20services/protocol/protocol/reorder/ ручка протокола)) ((https://github.yandex-team.ru/taxi/backend-cpp/blob/e037f84d74811bf92fe34a0c064a6f7290adf547/protocol/lib/src/handlers/reorder.cpp backend-cpp)) - используется для показа формы в мобильном приложении пассажиру с предложением перезаказать такси. Работает через отмену старого заказа (%%order.status: reordered%%) и создание нового заказа с такими же или изменёнными требованиями. В новом заказе будет ссылка на старый заказ.
Автореордер из админки: ((https://github.yandex-team.ru/taxi/backend/blob/9658819e4b5c8924e653655a21ac65714256ef3e/taxi/internal/dbh/order_proc.py#L2380 backend)) - используется для ручного перезаказа оператором из админки. Код находится в общем коде 2 питона, перезаписывает прок, стирая первую версию некоторых полей, добавляет в прок поле с причиной отказа (%%order_proc.autoreorder.decisions%%) и переводит заказ снова в статус "pending". Не заметен для пользователя.
Автореордер в ручке requestconfirm: ((https://github.yandex-team.ru/taxi/backend-cpp/blob/develop/protocol/lib/src/views/taxi_requestconfirm.cpp#L2612 backend-cpp)) - на первый взгляд делает тоже самое что автореордер из админки, однако находится в плюсах и вызывается автоматически в ((https://github.yandex-team.ru/pages/taxi/schemas/Taxi_Documentation/Backend-cpp%20services/protocol/protocol/requestconfirm/ protocol/requestconfirm)). Условия для авореордера проверяются там же.

