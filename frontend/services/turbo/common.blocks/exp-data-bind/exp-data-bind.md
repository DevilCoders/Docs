## Динамические поля

Блок работает вместе с блоком **exp-external-request**, расположенным вверх по дереву.  
Блок миксуется через пустую моду ко всем блокам, у которых есть в контексте `dyn`.  

[Схема данных](../exp-data-bind/exp-data-bind.schema.json)

Примеры и варианты использования блока см. в [документации к блоку **exp-external-request**](../exp-external-request/README.md)

Пример в данных:
```json
{
    "dyn": [
        {
            "type": "class",
            "key": "class_name_prop"
        }
    ]
}
```
