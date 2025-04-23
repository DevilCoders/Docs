# Экран уточнения точки А и Б

В этом RFC будут технические детали новой фичи.

Продуктовое описание тут - https://st.yandex-team.ru/TAXIPROJECTS-1836

### Дизайн

![drive-discovery](https://jing.yandex-team.ru/files/pavelnekrasov/clarify_points.png "Уточнение точек после саммари")


### Клиентский флоу
 
 Предлагается сделать ручку `/4.0/persuggest/v1/clarify-points`.
 Ручка принимает на вход `state` - такой же как в ручках саджеста, но с 
 расширением `state.fields[]` полями `metrica_action, metrica_method, method`, а 
 также `summary_state` с информацией из последнего ответа `routestats`:
 ```json5
{
    "state": {
      ...
      "fields": [
        {
          "type": "a",
          "metrica_action": "xxx", <- новое поле 
          "metrica_method": "yyy", <- новое поле
          "finalsuggest_method": "zzz", <- новое поле (из ответа persuggest - results[0].method)
          ...
        },
        ...
      ]
    },
    "summary_state": {
      "offer_id": "...", // <- id оффера из последнего ответа routestats
      "has_alternatives": true //<- флаг наличия альтернативных точек посадки в последнем ответе routestats
    }
}
```

Ручка вызывается сразу после `routestats` - после каждого вызова routestats на саммари клиент 
ходит в ручку `clarify-points`. Если по нажатию 
кнопки `Забронировать` на саммари не был получен ответ на последний запрос 
`clarify-points`, то экраны уточнения не показываются, а событие о том, 
 что не был получен ответ  `clarify-points` логируется в апп-метрику. 
 На экранах уточнения точек, которые открываются после summary ручка 
 `clarify-points` **не дергается**. 
Ручка дергается с тайм-аутом 4 секунды без ретраев. Каждый новый запрос routestats 
инвалидирует последний ответ ручки `clarify-points`.


Ручка `/4.0/persuggest/v1/clarify-points` возвращает список `clarify_points`:
```json5
{
    "clarify_points": [
        {
            "type": "a",  //обязательное поле
            "completion_timeout_ms": 1000,
            "text": "Уточните место подачи" //обязательное поле
        },
        {
            "type": "b",  //обязательное поле
            "text": "Уточните место назначения" //обязательное поле
            // "completion_timeout_ms": 2000 - если не указан, значит не должно быть 
            // прогресс-бара
        },
        // точек mid* не будет!
    ]
}
```

Если список `clarify_points` отсутствует (не был получен ответ ручки) или пустой, 
то нужно сразу перейти к заказу. Иначе для каждой точки по порядку из списка 
clarify_points нужно:
1. Показать текст `text`.
2. Показать прогресс бар, если задан `completion_timeout_ms`.
3. Если нет `completion_timeout_ms`, то просто отображается кнопка `Далее`.

#### Клиентский эксперимент
Заводим клиентский эксп `clarify_points` в zoneinfo со следующей схемой:

```json5
{
  "enabled": true,
}
```
Если эксперимент выключен, то запросы clarify-points не делаются.
