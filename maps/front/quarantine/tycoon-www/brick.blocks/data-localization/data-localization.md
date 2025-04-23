## Classes

<dl>
<dt><a href="#DataLocalization">DataLocalization</a></dt>
</dl>

## Constants

<dl>
<dt><a href="#fallbackList">fallbackList</a> : <code>Array.&lt;string&gt;</code></dt>
<dd><p>Список фолбеков языков перевода, на случай, если перевод в языке пользователя не найден</p>
</dd>
<dt><a href="#priorities">priorities</a> : <code>Object</code></dt>
<dd><p>Таблица приоритетов переводов, в зависимости от языка пользователя</p>
</dd>
</dl>

<a name="DataLocalization"></a>

## DataLocalization
**Kind**: global class  

* [DataLocalization](#DataLocalization)
    * [new DataLocalization(userLocale)](#new_DataLocalization_new)
    * _instance_
        * [.joinTranslations(translations)](#DataLocalization+joinTranslations) ⇒ <code>Array</code>
        * [.sortTranslations(translations)](#DataLocalization+sortTranslations) ⇒ <code>Array</code>
        * [.getTranslation(translations)](#DataLocalization+getTranslation) ⇒ <code>String</code>
        * [.getTranslations(translations)](#DataLocalization+getTranslations) ⇒ <code>Array.&lt;String&gt;</code>
        * [.getAllTranslations(translations)](#DataLocalization+getAllTranslations) ⇒ <code>Array.&lt;Object&gt;</code>
        * [.getTranslationByType(items, [type])](#DataLocalization+getTranslationByType) ⇒ <code>String</code>
        * [.getTranslationsByType(items, type)](#DataLocalization+getTranslationsByType) ⇒ <code>Array.&lt;String&gt;</code>
    * _static_
        * [.getTranslationsHash(translations)](#DataLocalization.getTranslationsHash) ⇒ <code>Object</code>

<a name="new_DataLocalization_new"></a>

### new DataLocalization(userLocale)

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| userLocale | <code>String</code> | <code>ru</code> | Локаль пользователя(en,ru etc.) |

<a name="DataLocalization+joinTranslations"></a>

### dataLocalization.joinTranslations(translations) ⇒ <code>Array</code>
Соединяет переводы по одинаковым локалям

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> | Перевод |

<a name="DataLocalization+sortTranslations"></a>

### dataLocalization.sortTranslations(translations) ⇒ <code>Array</code>
Сортирует переводы согласно установленному порядку @see this.getOrder

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization+getTranslation"></a>

### dataLocalization.getTranslation(translations) ⇒ <code>String</code>
Возвращает переводы основываясь языке пользователя
Объединяет переводы в одну строку

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization+getTranslations"></a>

### dataLocalization.getTranslations(translations) ⇒ <code>Array.&lt;String&gt;</code>
Возвращает переводы основываясь языке пользователя

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization+getAllTranslations"></a>

### dataLocalization.getAllTranslations(translations) ⇒ <code>Array.&lt;Object&gt;</code>
Возвращает отсортированные переводы, основываясь на языке пользователя

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization+getTranslationByType"></a>

### dataLocalization.getTranslationByType(items, [type]) ⇒ <code>String</code>
Возвращает переводы на языке страницы/пользователя по типу сущности одной строкой

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| items | <code>Array.&lt;Object&gt;</code> |  |
| items.type | <code>String</code> | тип сущности(main, synonym etc.) |
| items.value | <code>Array.&lt;Object&gt;</code> | массив переводов для сущности({ locale: 'en', value: 'trust' }) |
| [type] | <code>String</code> | тип сущности по которой фильтровать переводы. Default: main |

<a name="DataLocalization+getTranslationsByType"></a>

### dataLocalization.getTranslationsByType(items, type) ⇒ <code>Array.&lt;String&gt;</code>
Возвращает переводы на языке страницы/пользователя по типу сущности

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Default |
| --- | --- |
| items |  | 
| type | <code>main</code> | 

<a name="DataLocalization.getTranslationsHash"></a>

### DataLocalization.getTranslationsHash(translations) ⇒ <code>Object</code>
Получает хеш переводов по локалям.

**Kind**: static method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization"></a>

## DataLocalization
**Kind**: global class  

* [DataLocalization](#DataLocalization)
    * [new DataLocalization(userLocale)](#new_DataLocalization_new)
    * _instance_
        * [.joinTranslations(translations)](#DataLocalization+joinTranslations) ⇒ <code>Array</code>
        * [.sortTranslations(translations)](#DataLocalization+sortTranslations) ⇒ <code>Array</code>
        * [.getTranslation(translations)](#DataLocalization+getTranslation) ⇒ <code>String</code>
        * [.getTranslations(translations)](#DataLocalization+getTranslations) ⇒ <code>Array.&lt;String&gt;</code>
        * [.getAllTranslations(translations)](#DataLocalization+getAllTranslations) ⇒ <code>Array.&lt;Object&gt;</code>
        * [.getTranslationByType(items, [type])](#DataLocalization+getTranslationByType) ⇒ <code>String</code>
        * [.getTranslationsByType(items, type)](#DataLocalization+getTranslationsByType) ⇒ <code>Array.&lt;String&gt;</code>
    * _static_
        * [.getTranslationsHash(translations)](#DataLocalization.getTranslationsHash) ⇒ <code>Object</code>

<a name="new_DataLocalization_new"></a>

### new DataLocalization(userLocale)

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| userLocale | <code>String</code> | <code>ru</code> | Локаль пользователя(en,ru etc.) |

<a name="DataLocalization+joinTranslations"></a>

### dataLocalization.joinTranslations(translations) ⇒ <code>Array</code>
Соединяет переводы по одинаковым локалям

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> | Перевод |

<a name="DataLocalization+sortTranslations"></a>

### dataLocalization.sortTranslations(translations) ⇒ <code>Array</code>
Сортирует переводы согласно установленному порядку @see this.getOrder

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization+getTranslation"></a>

### dataLocalization.getTranslation(translations) ⇒ <code>String</code>
Возвращает переводы основываясь языке пользователя
Объединяет переводы в одну строку

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization+getTranslations"></a>

### dataLocalization.getTranslations(translations) ⇒ <code>Array.&lt;String&gt;</code>
Возвращает переводы основываясь языке пользователя

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization+getAllTranslations"></a>

### dataLocalization.getAllTranslations(translations) ⇒ <code>Array.&lt;Object&gt;</code>
Возвращает отсортированные переводы, основываясь на языке пользователя

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="DataLocalization+getTranslationByType"></a>

### dataLocalization.getTranslationByType(items, [type]) ⇒ <code>String</code>
Возвращает переводы на языке страницы/пользователя по типу сущности одной строкой

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| items | <code>Array.&lt;Object&gt;</code> |  |
| items.type | <code>String</code> | тип сущности(main, synonym etc.) |
| items.value | <code>Array.&lt;Object&gt;</code> | массив переводов для сущности({ locale: 'en', value: 'trust' }) |
| [type] | <code>String</code> | тип сущности по которой фильтровать переводы. Default: main |

<a name="DataLocalization+getTranslationsByType"></a>

### dataLocalization.getTranslationsByType(items, type) ⇒ <code>Array.&lt;String&gt;</code>
Возвращает переводы на языке страницы/пользователя по типу сущности

**Kind**: instance method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Default |
| --- | --- |
| items |  | 
| type | <code>main</code> | 

<a name="DataLocalization.getTranslationsHash"></a>

### DataLocalization.getTranslationsHash(translations) ⇒ <code>Object</code>
Получает хеш переводов по локалям.

**Kind**: static method of <code>[DataLocalization](#DataLocalization)</code>  

| Param | Type | Description |
| --- | --- | --- |
| translations | <code>Array.&lt;Object&gt;</code> |  |
| translations.locale | <code>String</code> | Ключ локали |
| translations.value | <code>String</code> &#124; <code>Array.&lt;String&gt;</code> | Перевод или список переводов |

<a name="fallbackList"></a>

## fallbackList : <code>Array.&lt;string&gt;</code>
Список фолбеков языков перевода, на случай, если перевод в языке пользователя не найден

**Kind**: global constant  
<a name="priorities"></a>

## priorities : <code>Object</code>
Таблица приоритетов переводов, в зависимости от языка пользователя

**Kind**: global constant  
