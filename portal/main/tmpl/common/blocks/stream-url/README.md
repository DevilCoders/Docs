# stream-url

Формирует ссылку на Эфир

### Описание

Используется для формирования ссылки на Эфир.

Из `stream-settings` забирает настройки протокола, домена и пр.

```javascript
execView('stream-url', { /* параметры ссылки */ })
```

Параметры ссылки:

```
{
    fromBlock,
    fromBlockPrefix,
    fromBlockCode,
    path,
    streamDefault,
    isSharing,
    isRetPath,
    isSportContent,
    isDRMContent,
    withHost,
    streamActive,
    streamId,
    streamChannel,
    streamCategory,
    streamPublisher,
    streamSearchText,
    source,
    from
}
```

#### fromBlock

Для аналитики ссылка на эфир должна содержать fromBlock, чтобы можно было узнать как пользователь попал на страницу.

Если fromBlock не был передан или не проходит валидацию, будет выведено сообщение с ошибкой.

fromBlock должен быть в формате `<block>_<elem>`.
В процессе формирования ссылки такой fromBlock будет дополнен префиксом.

Инициализация префикса происходит на соответствующем уровне. На common уровне префикс отсутствует.

#### fromBlockCode
Число, которое подставляем вместо from_block для урлов, которые видны пользователю (например шарилка).
Представляет из себя закодированный (сейчас простой маппинг) fromBlock. Он разворачивается на сервере в from_block, в логи прорастает строка.
Подставится в параметр ?f=...

Пример ?f=1 развернется в from_block=share_button и в логи смотрения прорастет с такой строкой.

# stream-url__fromblock-prefix

Определяется на уровнях, чтобы добавить префикс.

# stream-url__fromblock_default

Определяется на уровнях, чтобы задать дефолтное значение fromBlock.
Если `fromBlock === undefined`, но определено дефолтное значение , ошибка не выводится.
