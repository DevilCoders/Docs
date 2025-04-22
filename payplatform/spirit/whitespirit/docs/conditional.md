### Пример **make_receipt**
```
{
"receipt_content": {

},
"conditional": {
    "dialect": "hy",
    "conditions": [
        {
            "condition": "before",
            "expression": "10"
        },
        {
            "condition": "accept_device",
            "expression": "(= (int (or (. device sn) 0)) 00000003820034331902)"
        }
    ]
    }
}
```

+ condition **before** и **after**: вернуть количество секунд ожидания до и после пробития чека соответственно
+ condition **after_select_device**: вернуть количество секунд ожидания после выбора кассы для пробития чека
+ condition **accept_device**: вернуть true для выбора устройства для пробития чека, false или исключение -- для отклонения
    - Поля в переменной **device**:
        * sn -- заводской номер кассы
        * groups -- группы кассы
+ [Докментация по Hy](http://docs.hylang.org/en/stable/index.html)
