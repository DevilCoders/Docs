# Буллеты в карточке тарифа

## Что хотим

Для некоторых тарифов возникает желание делать буллеты в карточке тарифа на саммари с некоторым описанием.
Напрмиер уже сделано через клиентский эксп в тарифе Шаттл и будет сделано в новом тарифе Комбо.


![combo](combo_example.png)


Кажется, что пора делать нормальное решение, чтобы не плодить клиентские экспы.

## Что добавим

Добавляем поле `tariff_card`, в котором для начала описываем буллеты в простом виде.
Эти буллеты отображаются сверху вниз друг за другом.
Располагаются ниже requirements и промоплашек, показываемых в картчоке тарифа:
1. Промоплашки
2. Комментарий к заказу, заказать другому
3. requirements
4. буллеты с описанием


```yaml
    TariffCardBullet:
        type: object
        additionalProperties: false
        properties:
            title:
                $ref: "extended-template/definitions.yaml#/definitions/AttributedText"
            subtitle:
                $ref: "extended-template/definitions.yaml#/definitions/AttributedText"
            icon_tag:
                type: string
        required:
          - title

    TariffCard:
        type: object
        additionalProperties: false
        properties:
            bullets:
                type: array
                items:
                    $ref: "#/definitions/TariffCardBullet"

    ServiceLevel:
        type: object
        additionalProperties: false
        properties:
            tariff_card:
                $ref: "#/definitions/TariffCard"
```

```json
{
  "tariff_card": {
    "bullets": [
      {
        "title": {
          "items": [
            {
              "type": "text",
              "text": "Подача такси займет ~10 мин",
              "font_size": 13
            }
          ]
        },
        "subtitle": {
          "items": [
            {
              "type": "text",
              "text": "Ищем, кому с вами по пути",
              "font_size": 10,
              "color": "#9E9B98"
            }
          ]
        },
        "icon_tag": "clocks_icon_tag"
      }
    ]
  }
}
```
