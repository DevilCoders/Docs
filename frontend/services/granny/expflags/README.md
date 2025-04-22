# Список экспериментальных флагов

Директория с флагами экспериментов. Один флаг — один файл.

**пример:**

Имя флага: `disable_promo_logo`

Имя файла: `disable_promo_logo.json`

Содержимое файла:

```json
{
  "date": "04.04.2017",
  "description": "SERP-32658: Праздничный логотип на серпе",
  "manager": "vtenity",
  "dataDependent": false,
  "values": {
    "Включить функциональность": 1
  },
  "platforms": [
    "desktop",
    "touch-phone"
  ],
  "validation_type": "json"
}
```

Поле `dataDependent` показывает, является ли функциональность под флагом зависимой от данных, которые также включаются флагом.

Флаг может иметь несколько значений:

```json
  "values": {
    "Включить функциональность": 1,
    "Включить функциональность в режиме отладки": 2
  }
```

Отнеситесь серьезно к заполнению поля `validation_type`. Ошибка может привести к инциденту [SEARCHPRODINCIDENTS-3213](https://st.yandex-team.ru/SEARCHPRODINCIDENTS-3213#1519643483000)

**Возможные значения**

| validation_type | пример       | 
| ----------------|:-------------| 
| json            | `"json_attr": "some json value"` 
| str             | `"string_attr": "строка"` 
| int             | `"int_attr": 42` 
| float           | `"float_attr": 3.14` 
| bool            | `"boolean_attr": true` 
| 01              | `"01_attr": 1` 
| list_of_str     | `"list_of_str_attr": ["value1", "value2", "value3"]` 

## Тулза для создания новых флагов

Файлы можно создавать через консольную утилиту, где в интерактивном режиме можно задать все необходимые поля. Запускается из корня проекта:

```bash
tools/expflags
```
