# index-page

```js
{
    block: 'index-page',
    content: [
        {
            elem: 'websearch',
            content: {
                block: 'form',
                content: {
                    block: 'control-group',
                    content: [
                        {
                            block: 'input',
                            mods: {
                                theme: 'islands',
                                size: 'xl'
                            },
                            name: 'big_attr',
                            placeholder: 'Начните свою работу с поиска'
                        },
                        {
                            block: 'button',
                            mods: {
                                theme: 'islands',
                                size: 'xl',
                                view: 'action',
                                type: 'submit'
                            },
                            text: 'Найти'
                        }
                    ]
                }
            }
        },
        {
            block: 'modal',
            mods: {
                theme: 'islands',
                'has-close': true
            },
            mix: {
                block: 'index-page',
                elem: 'search-modal'
            },
            content: [
                {
                    block: 'heading',
                    mods: {
                        level: 2
                    },
                    content: 'Расширенный поиск'
                },
                {
                    block: 'search-form',
                    mix: [
                        {
                            mods: {
                                type: ''
                            }
                        }
                    ],
                    content: {
                        block: 'form',
                        content: {
                            block: 'table',
                            content: [
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-names',
                                            content: 'Название'
                                        },
                                        {
                                            elem: 'cell',
                                            mix: {
                                                block: 'search-form',
                                                elem: 'cell',
                                                elemMods: {
                                                    type: 'name'
                                                }
                                            },
                                            content: [
                                                {
                                                    block: 'plural-value',
                                                    elem: 'section',
                                                    js: {
                                                        data: [
                                                            {
                                                                block: 'input',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    width: 'available',
                                                                    'has-clear': true
                                                                },
                                                                val: '',
                                                                id: 'search-names',
                                                                name: 'search-names'
                                                            },
                                                            {
                                                                block: 'select',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    mode: 'check'
                                                                },
                                                                text: 'Тип',
                                                                val: '',
                                                                name: 'search-names_type',
                                                                options: [
                                                                    {
                                                                        val: 'main',
                                                                        text: 'Название'
                                                                    },
                                                                    {
                                                                        val: 'synonym',
                                                                        text: 'Альтернативное'
                                                                    },
                                                                    {
                                                                        val: 'short',
                                                                        text: 'Короткое'
                                                                    }
                                                                ]
                                                            }
                                                        ]
                                                    },
                                                    content: [
                                                        {
                                                            block: 'input',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                width: 'available',
                                                                'has-clear': true
                                                            },
                                                            val: '',
                                                            id: 'search-names',
                                                            name: 'search-names'
                                                        },
                                                        {
                                                            block: 'select',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                mode: 'check'
                                                            },
                                                            text: 'Тип',
                                                            val: [],
                                                            name: 'search-names_type',
                                                            options: [
                                                                {
                                                                    val: 'main',
                                                                    text: 'Название'
                                                                },
                                                                {
                                                                    val: 'synonym',
                                                                    text: 'Альтернативное'
                                                                },
                                                                {
                                                                    val: 'short',
                                                                    text: 'Короткое'
                                                                }
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'name'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-rubrics',
                                            content: 'Рубрика'
                                        },
                                        {
                                            elem: 'cell',
                                            content: [
                                                {
                                                    block: 'plural-value',
                                                    elem: 'section',
                                                    js: {
                                                        data: [
                                                            {
                                                                block: 'suggest',
                                                                js: {
                                                                    dataType: '',
                                                                    lang: 'ru'
                                                                },
                                                                mods: {
                                                                    mode: 'main',
                                                                    type: 'edit-rubrics',
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    'has-dataprovider': true,
                                                                    width: 'available',
                                                                    'has-clear': true
                                                                },
                                                                id: 'search-rubrics',
                                                                name: 'search-rubrics',
                                                                val: '',
                                                                placeholder: 'Введите id или название',
                                                                dataprovider: {}
                                                            }
                                                        ]
                                                    },
                                                    content: {
                                                        block: 'suggest',
                                                        js: {
                                                            dataType: '',
                                                            lang: 'ru'
                                                        },
                                                        mods: {
                                                            mode: 'main',
                                                            type: 'edit-rubrics',
                                                            theme: 'islands',
                                                            size: 'm',
                                                            'has-dataprovider': true,
                                                            width: 'available',
                                                            'has-clear': true
                                                        },
                                                        id: 'search-rubrics',
                                                        name: 'search-rubrics',
                                                        val: '',
                                                        placeholder: 'Введите id или название',
                                                        dataprovider: {}
                                                    }
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'rubric'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-formatted',
                                            content: 'Адрес'
                                        },
                                        {
                                            block: 'suggest',
                                            js: {
                                                dataType: '',
                                                lang: 'ru'
                                            },
                                            mods: {
                                                mode: 'main',
                                                type: 'edit-address',
                                                theme: 'islands',
                                                size: 'm',
                                                'has-dataprovider': true,
                                                width: 'available',
                                                'has-clear': true
                                            },
                                            id: 'search-formatted',
                                            name: 'search-formatted',
                                            val: '',
                                            dataprovider: {}
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'address'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-region_code',
                                            content: 'Страна'
                                        },
                                        {
                                            block: 'suggest',
                                            js: {
                                                dataType: 'country',
                                                lang: 'ru'
                                            },
                                            mods: {
                                                mode: 'main',
                                                type: 'default',
                                                theme: 'islands',
                                                size: 'm',
                                                'has-dataprovider': true,
                                                width: 'available',
                                                'has-clear': true
                                            },
                                            id: 'search-region_code',
                                            name: 'search-region_code',
                                            val: '',
                                            dataprovider: {}
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'country'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-geo_id',
                                            content: 'Регион'
                                        },
                                        {
                                            block: 'suggest',
                                            js: {
                                                dataType: 'region',
                                                lang: 'ru'
                                            },
                                            mods: {
                                                mode: 'main',
                                                type: 'default',
                                                theme: 'islands',
                                                size: 'm',
                                                'has-dataprovider': true,
                                                width: 'available',
                                                'has-clear': true
                                            },
                                            id: 'search-geo_id',
                                            name: 'search-geo_id',
                                            val: '',
                                            dataprovider: {}
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'region'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-feature_id',
                                            content: 'Признак'
                                        },
                                        {
                                            elem: 'cell',
                                            mix: {
                                                block: 'search-form',
                                                elem: 'cell',
                                                elemMods: {
                                                    type: 'feature'
                                                }
                                            },
                                            content: [
                                                {
                                                    block: 'plural-value',
                                                    elem: 'section',
                                                    js: {
                                                        data: [
                                                            {
                                                                block: 'input',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    width: 'available',
                                                                    'has-clear': true
                                                                },
                                                                mix: {
                                                                    block: 'search-form',
                                                                    elem: 'feature-id'
                                                                },
                                                                placeholder: 'ID признака',
                                                                val: '',
                                                                id: 'search-feature_id',
                                                                name: 'search-feature_id'
                                                            },
                                                            {
                                                                block: 'input',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    width: 'available',
                                                                    'has-clear': true
                                                                },
                                                                mix: {
                                                                    block: 'search-form',
                                                                    elem: 'feature-value'
                                                                },
                                                                placeholder: 'Значение признака',
                                                                val: '',
                                                                id: 'search-feature_value',
                                                                name: 'search-feature_value'
                                                            }
                                                        ]
                                                    },
                                                    content: [
                                                        {
                                                            block: 'input',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                width: 'available',
                                                                'has-clear': true
                                                            },
                                                            mix: {
                                                                block: 'search-form',
                                                                elem: 'feature-id'
                                                            },
                                                            placeholder: 'ID признака',
                                                            val: '',
                                                            id: 'search-feature_id',
                                                            name: 'search-feature_id'
                                                        },
                                                        {
                                                            block: 'input',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                width: 'available',
                                                                'has-clear': true
                                                            },
                                                            mix: {
                                                                block: 'search-form',
                                                                elem: 'feature-value'
                                                            },
                                                            placeholder: 'Значение признака',
                                                            val: '',
                                                            id: 'search-feature_value',
                                                            name: 'search-feature_value'
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'feature'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-chain_parent_companies',
                                            content: 'Сеть'
                                        },
                                        {
                                            block: 'suggest',
                                            js: {
                                                dataType: 'chain',
                                                lang: 'ru'
                                            },
                                            mods: {
                                                mode: 'main',
                                                type: 'default',
                                                theme: 'islands',
                                                size: 'm',
                                                'has-dataprovider': true,
                                                width: 'available',
                                                'has-clear': true
                                            },
                                            id: 'search-chain_parent_companies',
                                            name: 'search-chain_parent_companies',
                                            val: '',
                                            placeholder: 'Введите id или название',
                                            dataprovider: {}
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'chain'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-export_id',
                                            content: 'Пермалинк'
                                        },
                                        {
                                            block: 'input',
                                            mods: {
                                                theme: 'islands',
                                                size: 'm',
                                                width: 'available',
                                                'has-clear': true
                                            },
                                            placeholder: 'Введите значения через запятую',
                                            val: '',
                                            id: 'search-export_id',
                                            name: 'search-export_id'
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'permalink'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-providers',
                                            content: 'Provider id'
                                        },
                                        {
                                            elem: 'cell',
                                            mix: {
                                                block: 'search-form',
                                                elem: 'cell',
                                                elemMods: {
                                                    type: 'provider'
                                                }
                                            },
                                            content: [
                                                {
                                                    block: 'plural-value',
                                                    elem: 'section',
                                                    js: {
                                                        data: [
                                                            {
                                                                block: 'suggest',
                                                                js: {
                                                                    dataType: 'provider',
                                                                    lang: 'ru'
                                                                },
                                                                mods: {
                                                                    mode: 'main',
                                                                    type: 'default',
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    'has-dataprovider': true,
                                                                    width: 'auto',
                                                                    'has-clear': true
                                                                },
                                                                mix: {
                                                                    block: 'search-form',
                                                                    elem: 'providers'
                                                                },
                                                                id: 'search-providers',
                                                                name: 'search-providers',
                                                                val: '',
                                                                dataprovider: {}
                                                            },
                                                            {
                                                                block: 'form',
                                                                elem: 'label',
                                                                for: 'search-original-id',
                                                                content: 'Original id'
                                                            },
                                                            {
                                                                block: 'input',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    width: 'auto',
                                                                    'has-clear': true
                                                                },
                                                                mix: {
                                                                    block: 'search-form',
                                                                    elem: 'original-id'
                                                                },
                                                                val: '',
                                                                id: 'search-original-id',
                                                                name: 'search-original-id'
                                                            },
                                                            {
                                                                block: 'form',
                                                                elem: 'label',
                                                                for: 'search-feed-id',
                                                                content: 'Feed id'
                                                            },
                                                            {
                                                                block: 'input',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    width: 'auto',
                                                                    'has-clear': true
                                                                },
                                                                mix: {
                                                                    block: 'search-form',
                                                                    elem: 'feed-id'
                                                                },
                                                                val: '',
                                                                id: 'search-feed-id',
                                                                name: 'search-feed-id'
                                                            }
                                                        ]
                                                    },
                                                    content: [
                                                        {
                                                            block: 'suggest',
                                                            js: {
                                                                dataType: 'provider',
                                                                lang: 'ru'
                                                            },
                                                            mods: {
                                                                mode: 'main',
                                                                type: 'default',
                                                                theme: 'islands',
                                                                size: 'm',
                                                                'has-dataprovider': true,
                                                                width: 'auto',
                                                                'has-clear': true
                                                            },
                                                            mix: {
                                                                block: 'search-form',
                                                                elem: 'providers'
                                                            },
                                                            id: 'search-providers',
                                                            name: 'search-providers',
                                                            val: '',
                                                            dataprovider: {}
                                                        },
                                                        {
                                                            block: 'form',
                                                            elem: 'label',
                                                            for: 'search-original-id',
                                                            content: 'Original id'
                                                        },
                                                        {
                                                            block: 'input',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                width: 'auto',
                                                                'has-clear': true
                                                            },
                                                            mix: {
                                                                block: 'search-form',
                                                                elem: 'original-id'
                                                            },
                                                            id: 'search-original-id',
                                                            name: 'search-original-id'
                                                        },
                                                        {
                                                            block: 'form',
                                                            elem: 'label',
                                                            for: 'search-feed-id',
                                                            content: 'Feed id'
                                                        },
                                                        {
                                                            block: 'input',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                width: 'auto',
                                                                'has-clear': true
                                                            },
                                                            mix: {
                                                                block: 'search-form',
                                                                elem: 'feed-id'
                                                            },
                                                            id: 'search-feed-id',
                                                            name: 'search-feed-id'
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'provider'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-id',
                                            content: [
                                                [
                                                    {
                                                        block: 'search-form',
                                                        elem: 'id-label',
                                                        elemMods: {
                                                            type: 'chain'
                                                        },
                                                        content: 'chain'
                                                    },
                                                    {
                                                        block: 'search-form',
                                                        elem: 'id-label',
                                                        elemMods: {
                                                            type: 'company'
                                                        },
                                                        content: 'company'
                                                    }
                                                ],
                                                ' id'
                                            ]
                                        },
                                        {
                                            block: 'input',
                                            mods: {
                                                theme: 'islands',
                                                size: 'm',
                                                width: 'available',
                                                'has-clear': true
                                            },
                                            placeholder: 'Введите значения через запятую',
                                            val: '',
                                            id: 'search-id',
                                            name: 'search-id'
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'company-id'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-internal_name',
                                            content: 'Backa id'
                                        },
                                        {
                                            block: 'input',
                                            mods: {
                                                theme: 'islands',
                                                size: 'm',
                                                width: 'available',
                                                'has-clear': true
                                            },
                                            placeholder: 'Введите значения через запятую',
                                            val: '',
                                            id: 'search-internal_name',
                                            name: 'search-internal_name'
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'backa-id'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-urls',
                                            content: 'Сайт'
                                        },
                                        {
                                            elem: 'cell',
                                            mix: {
                                                block: 'search-form',
                                                elem: 'cell',
                                                elemMods: {
                                                    type: 'urls'
                                                }
                                            },
                                            content: [
                                                {
                                                    block: 'plural-value',
                                                    elem: 'section',
                                                    js: {
                                                        data: [
                                                            {
                                                                block: 'input',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    width: 'available',
                                                                    'has-clear': true
                                                                },
                                                                val: '',
                                                                id: 'search-urls',
                                                                name: 'search-urls'
                                                            },
                                                            {
                                                                block: 'select',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    mode: 'check'
                                                                },
                                                                text: 'Тип',
                                                                val: '',
                                                                name: 'search-urls_type',
                                                                options: [
                                                                    {
                                                                        val: 'main',
                                                                        text: 'Основной'
                                                                    },
                                                                    {
                                                                        val: 'alternative',
                                                                        text: 'Альтернативный'
                                                                    },
                                                                    {
                                                                        val: 'attribution',
                                                                        text: 'Поставщик'
                                                                    },
                                                                    {
                                                                        val: 'booking',
                                                                        text: 'Бронирование'
                                                                    },
                                                                    {
                                                                        val: 'mirror',
                                                                        text: 'Зеркало'
                                                                    },
                                                                    {
                                                                        val: 'showtimes',
                                                                        text: 'Расписания'
                                                                    },
                                                                    {
                                                                        val: 'social',
                                                                        text: 'Соц.сеть'
                                                                    },
                                                                    {
                                                                        val: 'mining',
                                                                        text: 'Источник данных'
                                                                    }
                                                                ]
                                                            },
                                                            {
                                                                block: 'checkbox',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    checked: false
                                                                },
                                                                name: 'search-urls_hide',
                                                                text: 'Скрыт'
                                                            }
                                                        ]
                                                    },
                                                    content: [
                                                        {
                                                            block: 'input',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                width: 'available',
                                                                'has-clear': true
                                                            },
                                                            val: '',
                                                            id: 'search-urls',
                                                            name: 'search-urls'
                                                        },
                                                        {
                                                            block: 'select',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                mode: 'check'
                                                            },
                                                            text: 'Тип',
                                                            val: [],
                                                            name: 'search-urls_type',
                                                            options: [
                                                                {
                                                                    val: 'main',
                                                                    text: 'Основной'
                                                                },
                                                                {
                                                                    val: 'alternative',
                                                                    text: 'Альтернативный'
                                                                },
                                                                {
                                                                    val: 'attribution',
                                                                    text: 'Поставщик'
                                                                },
                                                                {
                                                                    val: 'booking',
                                                                    text: 'Бронирование'
                                                                },
                                                                {
                                                                    val: 'mirror',
                                                                    text: 'Зеркало'
                                                                },
                                                                {
                                                                    val: 'showtimes',
                                                                    text: 'Расписания'
                                                                },
                                                                {
                                                                    val: 'social',
                                                                    text: 'Соц.сеть'
                                                                },
                                                                {
                                                                    val: 'mining',
                                                                    text: 'Источник данных'
                                                                }
                                                            ]
                                                        },
                                                        {
                                                            block: 'checkbox',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                checked: false
                                                            },
                                                            name: 'search-urls_hide',
                                                            text: 'Скрыт'
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'url'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-phones',
                                            content: 'Телефон'
                                        },
                                        {
                                            elem: 'cell',
                                            mix: {
                                                block: 'search-form',
                                                elem: 'cell',
                                                elemMods: {
                                                    type: 'phones'
                                                }
                                            },
                                            content: [
                                                {
                                                    block: 'plural-value',
                                                    elem: 'section',
                                                    js: {
                                                        data: [
                                                            {
                                                                block: 'input',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    width: 'available',
                                                                    'has-clear': true
                                                                },
                                                                val: '',
                                                                id: 'search-phones',
                                                                name: 'search-phones'
                                                            },
                                                            {
                                                                block: 'select',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    mode: 'check'
                                                                },
                                                                text: 'Тип',
                                                                val: '',
                                                                name: 'search-phones_type',
                                                                options: [
                                                                    {
                                                                        val: 'phone',
                                                                        text: 'Тел'
                                                                    },
                                                                    {
                                                                        val: 'fax',
                                                                        text: 'Факс'
                                                                    },
                                                                    {
                                                                        val: 'phone_fax',
                                                                        text: 'Тел/Факс'
                                                                    },
                                                                    {
                                                                        val: 'short',
                                                                        text: 'Кор'
                                                                    }
                                                                ]
                                                            },
                                                            {
                                                                block: 'checkbox',
                                                                mods: {
                                                                    theme: 'islands',
                                                                    size: 'm',
                                                                    checked: false
                                                                },
                                                                name: 'search-phones_hide',
                                                                text: 'Скрыт'
                                                            }
                                                        ]
                                                    },
                                                    content: [
                                                        {
                                                            block: 'input',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                width: 'available',
                                                                'has-clear': true
                                                            },
                                                            val: '',
                                                            id: 'search-phones',
                                                            name: 'search-phones'
                                                        },
                                                        {
                                                            block: 'select',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                mode: 'check'
                                                            },
                                                            text: 'Тип',
                                                            val: [],
                                                            name: 'search-phones_type',
                                                            options: [
                                                                {
                                                                    val: 'phone',
                                                                    text: 'Тел'
                                                                },
                                                                {
                                                                    val: 'fax',
                                                                    text: 'Факс'
                                                                },
                                                                {
                                                                    val: 'phone_fax',
                                                                    text: 'Тел/Факс'
                                                                },
                                                                {
                                                                    val: 'short',
                                                                    text: 'Кор'
                                                                }
                                                            ]
                                                        },
                                                        {
                                                            block: 'checkbox',
                                                            mods: {
                                                                theme: 'islands',
                                                                size: 'm',
                                                                checked: false
                                                            },
                                                            name: 'search-phones_hide',
                                                            text: 'Скрыт'
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'phone'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-actualized',
                                            content: 'Дата актуализации'
                                        },
                                        {
                                            elem: 'cell',
                                            mix: {
                                                block: 'search-form',
                                                elem: 'cell',
                                                elemMods: {
                                                    style: 'flex'
                                                }
                                            },
                                            content: [
                                                {
                                                    block: 'input',
                                                    id: 'search-actualized',
                                                    name: 'search-actualized',
                                                    mods: {
                                                        'has-calendar': true,
                                                        size: 'm',
                                                        theme: 'islands',
                                                        width: 'available'
                                                    },
                                                    val: '',
                                                    weekdays: [
                                                        'пн',
                                                        'вт',
                                                        'ср',
                                                        'чт',
                                                        'пт',
                                                        'сб',
                                                        'вс'
                                                    ],
                                                    months: [
                                                        'Январь',
                                                        'Февраль',
                                                        'Март',
                                                        'Апрель',
                                                        'Май',
                                                        'Июнь',
                                                        'Июль',
                                                        'Август',
                                                        'Сентябрь',
                                                        'Октябрь',
                                                        'Ноябрь',
                                                        'Декабрь'
                                                    ]
                                                },
                                                {
                                                    block: 'search-form',
                                                    elem: 'separator',
                                                    content: '–'
                                                },
                                                {
                                                    block: 'input',
                                                    id: '',
                                                    name: 'search-actualized',
                                                    mods: {
                                                        'has-calendar': true,
                                                        size: 'm',
                                                        theme: 'islands',
                                                        width: 'available'
                                                    },
                                                    val: '',
                                                    weekdays: [
                                                        'пн',
                                                        'вт',
                                                        'ср',
                                                        'чт',
                                                        'пт',
                                                        'сб',
                                                        'вс'
                                                    ],
                                                    months: [
                                                        'Январь',
                                                        'Февраль',
                                                        'Март',
                                                        'Апрель',
                                                        'Май',
                                                        'Июнь',
                                                        'Июль',
                                                        'Август',
                                                        'Сентябрь',
                                                        'Октябрь',
                                                        'Ноябрь',
                                                        'Декабрь'
                                                    ]
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'actualize'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        {
                                            block: 'form',
                                            elem: 'label',
                                            for: 'search-publishing_status',
                                            content: 'Статус публикации'
                                        },
                                        {
                                            elem: 'cell',
                                            mix: {
                                                block: 'search-form',
                                                elem: 'cell',
                                                elemMods: {
                                                    style: 'flex',
                                                    type: 'status'
                                                }
                                            },
                                            content: [
                                                {
                                                    block: 'select',
                                                    mods: {
                                                        theme: 'islands',
                                                        size: 'm',
                                                        mode: 'check'
                                                    },
                                                    text: '–',
                                                    name: 'search-publishing_status',
                                                    options: [
                                                        {
                                                            val: 'publish',
                                                            text: 'публиковать'
                                                        },
                                                        {
                                                            val: 'temporarily_closed',
                                                            text: 'временно закрыто'
                                                        },
                                                        {
                                                            val: 'geo_spam',
                                                            text: 'геоcпам'
                                                        },
                                                        {
                                                            val: 'duplicate',
                                                            text: 'дубль'
                                                        },
                                                        {
                                                            val: 'apartment',
                                                            text: 'квартира'
                                                        },
                                                        {
                                                            val: 'not_answered',
                                                            text: 'недозвон'
                                                        },
                                                        {
                                                            val: 'legal_address',
                                                            text: 'юр.адрес'
                                                        },
                                                        {
                                                            val: 'denied_publishing',
                                                            text: 'отказ от предоставления информации'
                                                        },
                                                        {
                                                            val: 'spam',
                                                            text: 'спам'
                                                        },
                                                        {
                                                            val: 'closed',
                                                            text: 'фирма закрылась'
                                                        },
                                                        {
                                                            val: 'moved',
                                                            text: 'фирма переехала'
                                                        },
                                                        {
                                                            val: 'unchecked',
                                                            text: 'непроверенные данные'
                                                        },
                                                        {
                                                            val: 'unknown',
                                                            text: 'распубликовать'
                                                        },
                                                        {
                                                            val: 'obsolete',
                                                            text: 'устаревший (тех.статус)'
                                                        }
                                                    ]
                                                },
                                                {
                                                    block: 'form',
                                                    elem: 'label',
                                                    for: 'search-type',
                                                    content: 'Тип'
                                                },
                                                {
                                                    block: 'select',
                                                    mods: {
                                                        theme: 'islands',
                                                        size: 'm',
                                                        mode: 'radio'
                                                    },
                                                    mix: {
                                                        block: 'search-form',
                                                        elem: 'type-select'
                                                    },
                                                    text: '–',
                                                    val: 'ordinal',
                                                    name: 'search-type',
                                                    options: [
                                                        {
                                                            val: 'ordinal',
                                                            text: 'Компания'
                                                        },
                                                        {
                                                            val: 'chain',
                                                            text: 'Сеть'
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: 'status'
                                        }
                                    }
                                },
                                {
                                    elem: 'row',
                                    content: [
                                        '',
                                        {
                                            elem: 'cell',
                                            mix: {
                                                block: 'search-form',
                                                elem: 'cell',
                                                elemMods: {
                                                    type: 'actions'
                                                }
                                            },
                                            content: [
                                                {
                                                    block: 'button',
                                                    mods: {
                                                        theme: 'islands',
                                                        view: 'action',
                                                        size: 'l',
                                                        type: 'submit'
                                                    },
                                                    text: 'Найти'
                                                },
                                                {
                                                    block: 'button',
                                                    mods: {
                                                        theme: 'islands',
                                                        size: 'l',
                                                        type: 'clear'
                                                    },
                                                    text: 'Очистить'
                                                }
                                            ]
                                        }
                                    ],
                                    mix: {
                                        block: 'search-form',
                                        elem: 'field',
                                        elemMods: {
                                            type: ''
                                        }
                                    }
                                }
                            ]
                        }
                    }
                }
            ]
        }
    ]
}
```
