# Колдунщик/Факт контрагента

## Схема данных


```json
{
    "docs_right": [
        {
            {
                "title": "Сторожев Максим Геннадьевич",
                "active": true,
                "short": { // ключи -- любые строки
                    "ИНН": "352512565818",
                    "ОГРНИП": "500512080556"
                },
                "additional": [{
                    "title": "Информация об организации",
                    "content": { // опциональный, ключи -- любые строки
                        "Юридический адрес": "119021, г Москва, улица Льва Толстого, дом 16"
                    }
                }],
                // плюс что-то про орагнику (тайтл, гринурл, etc)
            }
        }
    ]
}
```