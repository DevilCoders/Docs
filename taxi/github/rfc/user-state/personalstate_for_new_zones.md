# Тарифы по умолчанию для новых зон

## Что хотим сделать
Сейчас пользователю, который хочет куда-то уехать из геозоны, в которой он первый раз, personalstate возвращает пустой ответ, соответственно берётся тариф из локального хранилища (LS) на клиенте (сохраняется последний выбранный тариф). Если LS пусто, либо сохранённый тариф недоступен в зоне, то выбирается is_default=True тариф из ответа zoneinfo
Необходимо улучшить механизм выбора дефолтного тарифа
https://st.yandex-team.ru/TAXIBACKEND-34361

## Сценарии
Выделим 2 основных сценария:
- совершенно новая зона
- зона была в поездке в качестве точки Б

Для первого случая предлагается следующее решение: присылать в launch массив с упорядоченными наборами тарифов. Если сохранённый в LS тариф недоступен в зоне, то берётся следующий (предыдущий в зависимости от сортировки) тариф из набора, в котором он присутствует  
Массив можно хранить в конфиге

Пример:
```yaml
...
new_zone_default_tariff_settings:
    groups: [
      [econom, comfort, comfort+],
      [business, ultima],
      [express, courier]
    ]
    is_ascending: true
...
```

Для второго случая можно при завершении заказа асинхронно (stq) сохранять в personalstate тариф точки А. Сначала смотрим есть ли для пользователя, зоны, бренда сохранённый personalstate. Если нет - то создаём его с переданными параметрами  

```yaml
name: user_state_update_point_b_personalstate
arguments:
  - name: point_b
    required: true
    schema:
        $ref: 'geometry/definitions.yaml#/definitions/PositionAsArray'  # https://github.yandex-team.ru/taxi/uservices/blob/7f5748714a45ac03b8341877a3d71d2e3236254c/libraries/geometry/docs/yaml/definitions.yaml#L22
  - name: yandex_uid
    required: true
    schema:
        type: string
  - name: application  # нужно для определения бренда
    required: true
    schema:
        type: string
  - name: selected_class
    required: true
    schema:
        type: string
```

