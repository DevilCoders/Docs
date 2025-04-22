# Bunker

Данные в стейте:
```js
{
    nodes: {
        beru: {
            tanker: {
                branch: 'dev-i18n',
                keysets: {
                    SomeKeySet: {
                        keys: {
                            'some.key.from.keyset': {
                                info: {
                                    context: '',
                                    is_plural: false,
                                    references: '',
                                },
                                translations: {
                                    ru: {
                                        status: 'approved',
                                        translator_comment: '',
                                        author: 'mikeron',
                                        change_date: '18:48:56 04.07.2019',
                                        form: 'Для экономии не нужен повод, поэтому мы каждый день даём вам скидки',
                                    },
                                    en: {
                                        status: 'requires_translation',
                                        translator_comment: '',
                                        author: 'tanker',
                                        change_date: '18:48:43 04.07.2019',
                                        form: 'You don\'t need a reason to save money, that\'s why we give you discounts every day',
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```

Сокращённая форма, рекомендуемая к использованию в тестах:
```js
{
    nodes: {
        beru: {
            tanker: {
                keysets: {
                    SomeKeySet: {
                        keys: {
                            'some.key.from.keyset': {
                                translations: {
                                    ru: {
                                        form: 'Для экономии не нужен повод, поэтому мы каждый день даём вам скидки'
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```

Для нод */*/keysets/* описана схема и работает генерация фейков. Остальные ноды отдаются, как есть.
Отдача разных версий пока не имплементирована, все запросы работают, как будто передано version=latest

## Метод cat
Выводит содержимое ноды. Для примера выше:
- http://bunker-api-dot.yandex.net/v1/cat?node=%2Fberu%2Ftanker
- http://bunker-api-dot.yandex.net/v1/cat?node=%2Fmarket-partner%2Fheader-banners&version=latest

## Метод ls
Выводит список нод в проекте. Например, http://bunker-api-dot.yandex.net:80/v1/ls?node=beru&version=latest
