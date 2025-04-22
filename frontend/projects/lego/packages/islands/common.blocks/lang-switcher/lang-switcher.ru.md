# lang-switcher

Используется для создания переключателя языков интерфейса.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [noflags](#mods-noflags) | `'yes'` | `BEMJSON`, `JS` | Скрывает иконки флагов. |

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [lang](#field-lang) (req) | `Object` | Текущий язык интерфейса. |
| [retpath](#field-retpath) (req) | `String` | Адрес для редиректа (перенаправления) после переключения языка. |
| [secretKey](#field-secretkey) (req) | `String` | Секретный ключ для [Lang API](https://wiki.yandex-team.ru/tune/api/#langapi). |
| [tld](#field-tld) (req) | `String` | Текущий домен. |
| [tune](#field-tune) | `String` | Хост сервиса `tune`. |
| [moreText](#field-moretext) | `String` | Содержимое ссылки для перехода на `tune`. |
| [noMore](#field-nomore) | `Boolean` | Возможность скрыть ссылку для перехода на `tune`. |
| [moreRetpath](#field-moreretpath) | `Boolean` | Возможность редиректа после смены языка на `tune`, если задан `retpath`. |
| [setLangUrl](#field-setlangurl) | `String` | Адрес сервиса для смены языка. |
| [content](#field-content) | `BEMJSON` | Список языков. |

req — обязательное поле.

<a name="elems"></a>

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| [lang](#elem-lang) | Язык. |
| [flag](#elem-flag) | Иконка c флагом страны. Формируется блоком [country-flag](../country-flag/country-flag.ru.md). |
| [all](#elem-all) | Ссылка для перехода на `tune`. |
| [popup-content](#elem-popup-content) | Содержимое блока `popup`. |

## Подробное описание

### Модификаторы блока

<a name="mods-noflags"></a>

#### Модификатор `noflags`

Отвечает за скрытие иконок флагов.

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['без _noflags_yes', 'с  _noflags_yes'],
    body: [
        [false, 'yes'].map(function(val) {
            return {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'lang-switcher',
                    lang: { lang: 'ru', name: 'Ru' },
                    retpath: 'https://lego.yandex-team.ru',
                    tld: 'ru',
                    mods: { noflags: val },
                    secretKey: 'oh-my-secret',
                    content: [
                        {
                            elem: 'lang',
                            lang: { lang: 'be', name: 'Be' }
                        },
                        {
                            elem: 'lang',
                            elemMods: { selected: 'yes' },
                            lang: { lang: 'ru', name: 'Ru' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'en', name: 'En' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'kk', name: 'Kk' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'tr', name: 'Tr' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'tt', name: 'Tt' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'uk', name: 'Uk' }
                        }
                    ]
                }
            };
        })
    ]
}
```

### Поля блока

<a name="field-lang"></a>

#### Поле `lang`

Определяет текущий язык интерфейса. **Обязательное**.

Добавляет элемент [lang](#elem-lang) визуально представленный кнопкой раскрывающегося списка.

Тип: `Object`.

> **Примечание.** Язык интерфейса выражается двухбуквенным кодом и соответствующим названием `lang: { lang: 'ru', name: 'Ru' }`. Коды соответствуют стандарту [ISO 639-1](https://ru.wiktionary.org/wiki/Викисловарь:ISO_639).

```js
{
    block: 'x-table',
    head: ['Русский', 'Английский', 'Турецкий'],
    body: [
        [{ lang: 'ru', name: 'Ru' }, { lang: 'en', name: 'En' }, { lang: 'tr', name: 'Tr' }].map(function(lang) {
            return {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'lang-switcher',
                    lang: lang,
                    retpath: 'https://lego.yandex-team.ru',
                    tld: 'ru',
                    secretKey: 'oh-my-secret',
                    content: [
                        {
                            elem: 'lang',
                            lang: { lang: 'be', name: 'Be' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'ru', name: 'Ru' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'en', name: 'En' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'kk', name: 'Kk' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'tr', name: 'Tr' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'tt', name: 'Tt' }
                        },
                        {
                            elem: 'lang',
                            lang: { lang: 'uk', name: 'Uk' }
                        }
                    ]
                }
            };
        })
    ]
}
```

<a name="field-retpath"></a>

#### Поле `retpath`

Определяет адрес для редиректа (перенаправления) после переключения языка. **Обязательное**.

Тип: `String`.

> **Примечание.** Значение по умолчанию: `i-global.rethpath`.

```js
{
    block: 'x-table',
    head: ['Поле retpath'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://www.yandex.com.tr',
                tld: 'com.tr',
                secretKey: 'oh-my-secret',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'kk', name: 'Kk' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tr', name: 'Tr' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tt', name: 'Tt' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'uk', name: 'Uk' }
                    }
                ]
            }
        }
    ]
}
```

<a name="field-secretkey"></a>

#### Поле `secretKey`

Определяет секретный ключ для [Lang API](https://wiki.yandex-team.ru/tune/api/#langapi). **Обязательное**.

Тип: `String`.

> **Примечание.** Используется для защиты форм. Значение по умолчанию: `i-global.secret-key`.

```js
{
    block: 'x-table',
    head: ['Поле secretKey'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://lego.yandex-team.ru',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'kk', name: 'Kk' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tr', name: 'Tr' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tt', name: 'Tt' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'uk', name: 'Uk' }
                    }
                ]
            }
        }
    ]
}
```

<a name="field-tld"></a>

#### Поле `tld`

Определяет текущий домен. **Обязательное**.

Тип: `String`.

> **Примечание.** Используется для формирования списка языков. Значение по умолчанию: `i-global.tld`.

```js
{
    block: 'x-table',
    head: ['Поле tld'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://lego.yandex-team.ru',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'kk', name: 'Kk' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tr', name: 'Tr' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tt', name: 'Tt' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'uk', name: 'Uk' }
                    }
                ]
            }
        }
    ]
}
```

<a name="field-tune"></a>

#### Поле `tune`

Определяет хост сервиса `tune`.

Тип: `String`.

> **Примечание.** Значение по умолчанию: `https://yandex.$TLD/tune`.

```js
{
    block: 'x-table',
    head: ['Поле tune'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://yandex.ru/',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                tune: 'https://yandex.ru/tune',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    }
                ]
            }
        }
    ]
}
```

<a name="field-moretext"></a>

#### Поле `moreText`

Определяет содержимое ссылки для перехода на `tune`.

Тип: `String`, `BEMJSON`.

> **Примечание.** Значение по умолчанию: «Ещё».

```js
{
    block: 'x-table',
    head: ['Поле moreText'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://yandex.ru/',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                moreText: '⨁',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    }
                ]
            }
        }
    ]
}
```

<a name="field-nomore"></a>

#### Поле `noMore`

Позволяет скрыть ссылку для перехода на `tune`.

Тип: `Boolean`.

> **Примечание.** Значение по умолчанию: `false`. Приоритет поля `noMore` выше, чем у поля `moreText`.

```js
{
    block: 'x-table',
    head: ['Поле noMore'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://yandex.ru/',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                moreText: '⨁',
                noMore: true,
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    }
                ]
            }
        }
    ]
}
```

#### Поле `moreRetpath`

Позволяет сделать редирект после изменения языка на `tune`.

Тип: `Boolean`.

> **Примечание.** Значение по умолчанию: `false`.

```js
{
    block: 'x-table',
    head: ['Поле moreRetpath'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://yandex.ru/',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                moreRetpath: true,
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    }
                ]
            }
        }
    ]
}
```

<a name="field-setlangurl"></a>

#### Поле `setLangUrl`

Определяет адрес сервиса для смены языка.

Тип: `String`.

> **Примечание.** Значение по умолчанию: `https://www.yandex.$TLD/portal/set/lang`.

```js
{
    block: 'x-table',
    head: ['Поле setLangUrl1'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://lego.yandex-team.ru',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                setLangUrl: 'https://www.yandex.com.tr/portal/set/lang',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'kk', name: 'Kk' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tr', name: 'Tr' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tt', name: 'Tt' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'uk', name: 'Uk' }
                    }
                ]
            }
        }
    ]
}
```

<a name="field-content"></a>

#### Поле `content`

Определяет список языков.

Тип: `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['Поле content'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://www.yandex.com.tr',
                tld: 'com.tr',
                secretKey: 'oh-my-secret',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'kk', name: 'Kk' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tr', name: 'Tr' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tt', name: 'Tt' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'uk', name: 'Uk' }
                    }
                ]
            }
        }
    ]
}
```

### Элементы блока

<a name="elem-lang"></a>

#### Элемент `lang`

Определяет язык c соответствующим флагом и произвольным названием.

**Поля элемента**

| Поле    | Тип      | Описание                                    |
| ------- | -------- | ------------------------------------------- |
| lang    | `String` | Язык выражается двухбуквенным кодом и соответствующим названием `lang: { lang: 'ru', name: 'Ru' }`.      |
| url     | `String` | URL с набором параметров для смены языка.   |

```js
{
    block: 'x-table',
    head: ['lang-switcher__lang'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://yandex.ru',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'kk', name: 'Kk' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tr', name: 'Tr' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tt', name: 'Tt' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'uk', name: 'Uk' }
                    }
                ]
            }
        }
    ]
}
```

**Модификаторы элемента**

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [selected](#elem-mods-selected) | `'yes'` | `BEMJSON`, `JS` | Определяет выбранный пункт списка. |

<a name="elem-mods-selected"></a>

**Модификатор `selected`**

Определяет выбранный пункт списка.

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['lang-switcher__lang_selected'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'lang-switcher',
                lang: { lang: 'ru', name: 'Ru' },
                retpath: 'https://lego.yandex-team.ru',
                tld: 'ru',
                secretKey: 'oh-my-secret',
                content: [
                    {
                        elem: 'lang',
                        lang: { lang: 'be', name: 'Be' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'ru', name: 'Ru' },
                        elemMods: { selected: 'yes' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'en', name: 'En' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'kk', name: 'Kk' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tr', name: 'Tr' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'tt', name: 'Tt' }
                    },
                    {
                        elem: 'lang',
                        lang: { lang: 'uk', name: 'Uk' }
                    }
                ]
            }
        }
    ]
}
```

<a name="elem-flag"></a>

#### Элемент `flag`

Определяет иконку с флагом страны.

Формируется блоком [country-flag](../country-flag/country-flag.ru.md).

**Модификаторы элемента**

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| `icon` | `'be'`, `'en'`, `'kk'`, `'ru'`, `'tr'`, `'uk'` | `BEMJSON`, `JS` | Определяет иконку страны. |

<a name="elem-all"></a>

#### Элемент `all`

Определяет ссылку для перехода на `tune`.

> **Примечание.** Микс пункта меню `menu__item`.

<a name="elem-popup-content"></a>

#### Элемент `popup-content`

Определяет содержимое выпадающего списка.

Формируется блоком [popup2](../popup2/popup2.ru.md).
