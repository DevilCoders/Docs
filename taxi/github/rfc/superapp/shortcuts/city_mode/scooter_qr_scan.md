# Action для сканирования QR-кода самоката

## Задача

Уметь переходить в режим сканирования QR-кода для бронирования самоката по нажатию на кнопку самокатов.

![Screenshot](static/scooter_qr_scan.png)

## Предложение

### Новый action

Добавляем новый action следующего вида:
#### Вариант 1 (отклоняем)
```yaml
TypedScooterQRScanAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - scooter_qr_scan
    required:
      - mode
```

Пример:
```json
"action": {
    "type": "scooter_qr_scan",
}
```
