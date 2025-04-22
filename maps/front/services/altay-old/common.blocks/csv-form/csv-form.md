# csv-form

Блок, который запрашивает файлы csv в ручке поиска.
Используется на страницах с результатами поиска (компаний, рубрик).

```javascript
{
    block: 'csv-form',
    params: {
        searchRequest: {
            object_type: 'company',
            query: {
                and: [
                    {
                        field_name: 'names',
                        values: [
                            'кафе'
                        ],
                        mode: 'equals'
                    },
                    {
                        field_name: 'type',
                        values: [
                            'ordinal'
                        ],
                        mode: 'equals'
                    }
                ]
            }
        },
        total: 50084,
        hasAutoCoordinate: true
    },
    content: {
        block: 'control-group',
        content: [
            {
                block: 'button',
                mods: {
                    theme: 'islands',
                    size: 'm',
                    type: 'submit'
                },
                mix: {
                    block: 'csv-form',
                    elem: 'button',
                    js: {
                        login: 'robot-altay-reporter',
                        searchRequest: {
                            object_type: 'company',
                            query: {
                                and: [
                                    {
                                        field_name: 'names',
                                        values: [
                                            'кафе'
                                        ],
                                        mode: 'equals'
                                    },
                                    {
                                        field_name: 'type',
                                        values: [
                                            'ordinal'
                                        ],
                                        mode: 'equals'
                                    }
                                ]
                            }
                        },
                        total: 50084,
                        hasAutoCoordinate: true
                    }
                },
                text: 'CSV'
            },
            {
                block: 'select',
                mods: {
                    theme: 'islands',
                    size: 'm',
                    mode: 'radio'
                },
                name: 'lang',
                val: 'RU',
                options: [
                    {
                        val: 'RU',
                        text: 'ru'
                    },
                    {
                        val: 'UK',
                        text: 'uk'
                    },
                    {
                        val: 'EN',
                        text: 'en'
                    },
                    {
                        val: 'TR',
                        text: 'tr'
                    },
                    {
                        val: 'FR',
                        text: 'fr'
                    }
                ]
            },
            {
                block: 'checkbox',
                mods: {
                    theme: 'islands',
                    size: 'm',
                    type: 'button'
                },
                name: 'auto-coords',
                text: 'Авто-координата'
            }
        ]
    }
}
```
