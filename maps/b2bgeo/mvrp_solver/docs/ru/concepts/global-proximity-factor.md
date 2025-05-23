# Географически сгруппированные маршруты

Параметр `options.global_proximity_factor` позволяет увеличить кучность маршрутов. С этой опцией алгоритм строит маршруты так, чтобы точки доставки были более географически сгруппированными.

Возможные значения параметра — от `0.0` до `10.0`, где:

- `0.0` — указание не делать маршруты кучными (значение по умолчанию);
- `10.0` — указание обеспечить максимальную кучность.

Рекомендуемые значения лежат в пределах от `0.0` до `1.0`.

Использование `global_proximity_factor` может ухудшать метрики решения. Величину параметра следует подбирать индивидуально: начать с `0.5` и постепенно повышать значение (с шагом 0,5) до получения нужного результата.

**Пример 1**

Значение опции `global_proximity_factor` установлено в `0.0`. Географическая близость локаций минимально влияет на результат.

[Запрос API (JSON)](https://courier.yandex.ru/vrs/api/v1/log/request/7f6345f7-c3a77cde-35119196-e3870dee) ⋅ [Ответ API](https://courier.yandex.ru/vrs/api/v1/result/7f6345f7-c3a77cde-35119196-e3870dee) ⋅ [Открыть на карте](https://courier.yandex.ru/mvrp-map#7f6345f7-c3a77cde-35119196-e3870dee)

**Пример 2**

В исходных данных одно отличие от предыдущего примера: `global_proximity_factor` задан равным `1.0`. Маршруты построены более кучно, но увеличился пробег.

[Запрос API (JSON)](https://courier.yandex.ru/vrs/api/v1/log/request/8330ce4d-a635aa1a-423e0434-72b0b739) ⋅ [Ответ API](https://courier.yandex.ru/vrs/api/v1/result/8330ce4d-a635aa1a-423e0434-72b0b739) ⋅ [Открыть на карте](https://courier.yandex.ru/mvrp-map#8330ce4d-a635aa1a-423e0434-72b0b739)
