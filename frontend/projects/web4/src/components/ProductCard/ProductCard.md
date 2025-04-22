# ProductCard

Товарная карточка Яндекс.Маркета

{{%story::productcard-sandbox-touch-phone--playground%}}

## Использование

```js
import { compose } from "@bem-react/core";
import {
    ProductCard as ProductCardBase,
    withTypeTop
} from '../../../../../components/ProductCard/ProductCard@touch-phone';

const ProductCard = compose(
    withTypeTop
)(ProductCardBase);

<ProductCard
    type='top'
    url='https://market.yandex.ru'
    image='http://avatars.mds.yandex.net/get-mpic/1750349/img_id8238090644423545057.jpeg/5hq'
    imageHd='http://avatars.mds.yandex.net/get-mpic/1750349/img_id8238090644423545057.jpeg/orig'
    titleText='Телевизор \u0007[Samsung\u0007] UE55 RU8000U 54.6" (2019)'
    greenUrlText='Яндекс.Маркет'
    priceCurrency='RUB'
    priceValue={100}
    ratingValue={0}
/>
```

## Модификаторы
<table>
    <thead>
        <tr>
            <td><b>Модификатор</b></td>
            <td><b>Допустимые значения</b></td>
            <td><b>Описание</b></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>type</td>
            <td>
                <table>
                    <tr>
                        <td><code>top</code></td>
                        <td>Вверху (Рекламная галерея Маркет+Директ)</td>
                    </tr>
                    <tr>
                        <td><code>center</code></td>
                        <td>Центральная врезка</td>
                    </tr>
                    <tr>
                        <td><code>right</code></td>
                        <td>Правая колонка</td>
                    </tr>
                </table>
            </td>
            <td>Тип, место использования карточки</td>
        </tr>
    </tbody>
</table>

## Свойства
<table>
    <thead>
        <tr>
            <td><b>Свойство</b></td>
            <td><b>Тип</b></td>
            <td><b>Описание</b></td>
            <td><b>Уточнение</b></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>url</td>
            <td><code>string</code></td>
            <td>Ссылка, по которой ведут все клики по карточке</td>
            <td></td>
        </tr>
        <tr>
            <td>image?</td>
            <td><code>string</code></td>
            <td>URL изображения для обычных дисплеев (см. так же <code>imageHd</code>)</td>
            <td></td>
        </tr>
        <tr>
            <td>imageHd?</td>
            <td><code>string</code></td>
            <td>
                URL изображения для Retina-дисплеев
            </td>
            <td>
                <uL>
                    <li>Для обычных и Retina-дисплеев показываются разные картинки</li>
                    <li>В случае, если Retina-картики нет – покажется обычная из поля <code>image</code></li>
                    <li>В случае, если картинки нет, показывается заглушка</li>
                    <li>Вытянутые горизонтально и вертикально картинки уменьшаются, сохраняя пропорции</li>
                </uL>
            </td>
        </tr>
        <tr>
            <td>titleText</td>
            <td><code>string</code></td>
            <td>Текст заголовка товара</td>
            <td></td>
        </tr>
        <tr>
            <td>greenUrlText</td>
            <td><code>string</code></td>
            <td>Текст для гринурла</td>
            <td></td>
        </tr>
        <tr>
            <td>priceCurrency?</td>
            <td><code>PriceCurrencyCode</code></td>
            <td>
                Код валюты
            </td>
            <td>
                <ul>
                    <li>Допустимые значения – <code>RUB</code>, <code>USD</code>, <code>EUR</code>, <code>KZT</code>, <code>UAH</code>, <code>BYN</code>, <code>TRY</code>, <code>RUR</code> или <code>BYR</code></li>
                    <li>По умолчанию – <code>RUB</code></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>priceValue?</td>
            <td><code>number</code></td>
            <td>
                Точная цена товара в указанной валюте
            </td>
            <td>
                <ul>
                    <li>В случае, если ни точной, ни граничной цены нет, она не отрисуется</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>priceFromValue?</td>
            <td><code>number</code></td>
            <td>
                Граничная (минимальная == "от") товара в указанной валюте
            </td>
            <td>
                <ul>
                    <li>В случае, если ни точной, ни граничной цены нет, она не отрисуется</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>priceToValue?</td>
            <td><code>number</code></td>
            <td>
                Граничная (максимальная == "до") товара в указанной валюте
            </td>
            <td></td>
        </tr>
        <tr>
            <td>ratingValue?</td>
            <td><code>number</code></td>
            <td>
                Рейтинг товара
            </td>
            <td>
                <ul>
                    <li>Отображается, если указано ненулевое значение</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>withAlice?</td>
            <td><code>withAliceType</code></td>
            <td>
                Добавляет значок Алисы и текст
            </td>
            <td>
                Допустимые значения –  <code>undefined</code>, <code>work-with</code>, <code>live-in</code>, <code>fake-alice</code>
                <ul>
                    <li><code>work-with</code> = Работает с Алисой</li>
                    <li><code>live-in</code> = Алиса живёт здесь</li>
                    <li><code>fake-alice</code> = Алисы нет, но размер карточки изменяется</li>
                </ul>
                По умолчанию – <code>undefined</code>
            </td>
        </tr>
        <tr>
            <td>service?</td>
            <td><code>'direct'</code></td>
            <td>
                Показывает источник карточки
            </td>
            <td>
                Допустимые значения –  <code>undefined</code>, <code>direct</code>
                <ul>
                    <li><code>direct</code> = источник карточки - Директ</li>
                </ul>
                По умолчанию – <code>undefined</code>
            </td>
        </tr>
        <tr>
            <td>oldPrice?</td>
            <td><code>number</code></td>
            <td>
                Добавляет перечеркнутый старый ценник правее от основого
            </td>
            <td>
            </td>
        </tr>
        <tr>
            <td>maxOldPriceSymbols?</td>
            <td><code>number</code></td>
            <td>
                Количество цифр в старом ценнике
                Используется только с oldPrice
            </td>
            <td>
                По умолчанию <code>undefined</code>
                <ul>
                    <li>Если меньше 5, то карточку не увеличиваем по ширине</li>
                    <li>Если 5, то увеличиваем ширину карточки</li>
                    <li>Если 6 и больше, то еще увеличиваем ширину карточки</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>onClick?</td>
            <td><code>React.MouseEventHandler</code></td>
            <td>
                Обработчик клика по ссылке
            </td>
            <td>
                Пробрасывается на клик по тумбу и на клик по сниппету
            </td>
        </tr>
    </tbody>
</table>
