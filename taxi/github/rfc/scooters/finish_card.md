## Цели
- После окончания поездки показываем пользователю карточку с информацией о прошедшей поездке (детализация поездки и тарифом)
- Даем возможность поставить оценку и написать комментарий
- Если в клиентском эксперименте `scooters` карточка включена, то заменяем ей нотификацию 

### Дизайн
https://www.figma.com/file/UpZCx2kivSrdisuzfbnFL2/Scooters?node-id=17884%3A521896

### API
Сейчас при завершении поездки когда заказ пропадает из ответа `/sessions/current` клиенты ходят в `/sessions/history`
за итоговой стоимостью поездки для нотификации.

Предлагаю расширить `sessions[].segment` ответа `/session/history`,
добавив поля `finish_info`, `scale_size`, `discount`. Также в корень добавляется `currency_rules` для правильного отображения текстов из `finish_info`. Также же необходимо добавить в хедере апитег.
```json
{
    ...
    "sessions": [{
        ...
        "segment": {
            "start": 1657511536,
            "total_price": 6190, // полная стоимость поездки (уже используем для нотификации)
            "offer_name": "Забронировать [msk]",
            "diff": { ... },
            "insurance_type": "standart",
            "events": { ... },
            "total_duration": 39,
            "finish": 1657511575,
            "session_id": "2d6c4c69-1a5d-4a47-9b71-f99ff062282e",
            "finish_info": [{ // пункты с информацией о поездке (детализация)
                "title": { // Attributed text
                    ... "Waiting" ...
                },
                "value": { // Attributed text
                    ... "10$SIGN$$CURRENCY$" ...
                }
            }, {
                "title": {
                    ... "Start" ...
                },
                "value": {
                    ... "50$SIGN$$CURRENCY$" ...
                }
            }, {
                "title": {
                    ... "En route" ...
                },
                "value": {
                    ... "40 mins, 50$SIGN$$CURRENCY$" ...
                }
            }, { // только для поминутного тарифа
                "title": {
                    ... "Fare" ...
                    ... "Pay as you go" ...
                },
                "value": {
                    ... "4$SIGN$$CURRENCY$ / min" ...
                }
            }, {
                "title": {
                    ... "Total" ...
                },
                "value": {
                    ... "220$SIGN$$CURRENCY$" ...
                }
            }],
            "scale_size": 5, // максимальное количество звезд в шкале
            "discount": 1000 { // суммированая скидка в абсолютном значении (актуально для таларии)
        },
        ...
    }, {
        ... 
    }, { 
        ...
    }],
    "currency_rules": { ... },
    ...
}
```

После того как пользователь проставил оценку (и/или) написал комментарий необходимо уведомить бекенд. Предлагаю сделать новую ручку `POST 4.0/scooters/v1/feedback` c телом.
Также добавить в хедере апитег.

```json
{
    "session_id": "2d6c4c69-1a5d-4a47-9b71-f99ff062282e",
    "rating": 5, // Количество проставленных пользователем звезд (0 - без оценки)
    "comment": "The ride was awesome!!!"
}
```

Расширение клиенского эксперимента `scooters`:
```json
{
    ...
    "finish_card": {
        "enabled": true,
        "rating_enabled": true,
        "comment_enabled": true
    }
    ...
}
```
