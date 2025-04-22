# Работа с флагами

Описание флага должно быть добавлено в проектный уровень `allowed.flags.json`

Для удобного создания описания флага рекомендуется использовать команду: `fiji expflags <project>`

```bash
# Создание флага в Картинках
npm run expflags:create:images

# Создание флага в Видео
npm run expflags:create:video

# Создание флага в Сахалине
npm run expflags:create:sakhalin
```

Пример:

```json
    {
        "name": "enable_super_feature_flag",
        "date": "12.12.2012",
        "description": "SAKHALIN-12345: Включает супер фичу",
        "manager": "reganam",
        "projects": [
            "images3",
            "images_touch_pad",
            "images_touch_phone",
            "video3",
            "video_touch_phone"
        ],
        "expire": "12.12.2022",
        "validation_type": "str",
        "default": {
            "images3" : 1,
            "video_touch_phone" : 2
        }
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

Если флаг нужен на клиенте:

```json
"client": true
```

Если флаг для использования только во внутренней сети:

```json
"internal": true
```

Можно задать дефолтное значение флага для автотестов:
для всех платформ

```json
"default": 1
```

или выборочно

```json
"default": {
    "images3" : 1,
    "video_touch_phone" : 2
}
```
