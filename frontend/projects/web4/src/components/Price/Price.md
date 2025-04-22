# Price

```js
import { Price } from '@components/Price';
```

## Базовый вариант

Обычное отображение — со знаком рубля.

```js
<Price value={100} currency="RUB" rurSymbolFont />
```

{{%story::desktop:serp-components-price--default%}}

## Иностранные валюты

Чтобы было привычнее и проще читать, мы ставим знаки валют после суммы. Пятизначные и выше цифры нужно разделять неразрывными пробелами, чтобы быстро считывалось число.

```js
<Price value={100} currency="USD" />
<Price value={1000} currency="EUR" />
<Price value={10000} currency="KZT" />
<Price value={100000} currency="UAH" />
<Price value={1000000} currency="BYN" />
<Price value={10000000} currency="TRY" />
```

{{%story::desktop:serp-components-price--foreign-currency%}}

## Без знака рубля

В Поиске не нужно использовать такой вариант. Только, если дизайнер может объяснить зачем это нужно.

```js
<Price value={1000} currency="RUB" showAbbr />
```

{{%story::desktop:serp-components-price--without-sign%}}

## Символ рубля не из шрифта

Символ рубля отображается не во всех браузерах. Если для вас не так важна поддержка браузерами, можно взять вариант без шрифта.

```js
<Price value={1000} currency="RUB" />
```

{{%story::desktop:serp-components-price--without-font%}}

## Отображение копеек

```js
<Price value={10000.25} currency="RUB" withCents />
```

{{%story::desktop:serp-components-price--with-cents%}}

## Отображение старого ценника

```js
<Price value={100.25} oldValue={200.30} currency="RUB" withCents />
```

{{%story::desktop:serp-components-price--with-old-value%}}

## Свойства

<table>
    <thead>
        <tr>
            <td>Свойство</td>
            <td>Тип</td>
            <td>По умолчанию</td>
            <td>Описание</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>value</td>
            <td><code>number</code></td>
            <td><code>0</code></td>
            <td>Значение суммы. Округляется до целого значения</td>
        </tr>
        <tr>
            <td>currency</td>
            <td><code>PriceCurrencyCode</code></td>
            <td></td>
            <td>Код валюты. Может быть <code>RUB</code>, <code>USD</code>, <code>EUR</code>, <code>KZT</code>, <code>UAH</code>, <code>BYN</code>, <code>TRY</code>, <code>RUR</code> или <code>BYR</code></td>
        </tr>
        <tr>
            <td>showAbbr?</td>
            <td><code>boolean</code></td>
            <td>false</td>
            <td>Показывать аббревиатуру валюты вместо её символа</td>
        </tr>
        <tr>
            <td>rurSymbolFont?</td>
            <td><code>boolean</code></td>
            <td>false</td>
            <td>Показывать символ рубля — ₽</td>
        </tr>
        <tr>
            <td>withCents?</td>
            <td><code>boolean</code></td>
            <td>false</td>
            <td>Показывать копейки</td>
        </tr>
        <tr>
            <td>oldValue?</td>
            <td><code>number</code></td>
            <td></td>
            <td>Добавляет старый перечеркнутый ценник справа от основного</td>
        </tr>
    </tbody>
</table>
