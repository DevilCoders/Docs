# ImageSlider

Просмотрщик изображений

{{%story::imageslider-touch-phone--5-images%}}

## Использование

```js
import { ImageSlider } from '../ImageSlider';

<ImageSlider
    images={[
        '//avatars.mds.yandex.net/get-mpic/1859063/img_id9069574831100159221.jpeg/6hq',
        '//avatars.mds.yandex.net/get-mpic/1382936/img_id2827011941376083753.jpeg/6hq',
        '//avatars.mds.yandex.net/get-mpic/1539743/img_id1676880599374605783.jpeg/6hq',
        '//avatars.mds.yandex.net/get-mpic/1544149/img_id3615248753094624341.jpeg/6hq',
        '//avatars.mds.yandex.net/get-mpic/1365202/img_id3244104323139602333.jpeg/6hq',
    ]}
    width={250}
    height={250}
/>
```

## Свойства
<table>
    <thead>
        <tr>
            <td><b>Свойство</b></td>
            <td><b>Тип</b></td>
            <td><b>Описание</b></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>images</td>
            <td><code>string[]</code></td>
            <td>Массив URLов изображений</td>
        </tr>
        <tr>
            <td>width?</td>
            <td><code>number</code></td>
            <td>Ширина просмотрщика</td>
        </tr>
        <tr>
            <td>height?</td>
            <td><code>number</code></td>
            <td>Высота просмотрщика</td>
        </tr>
    </tbody>
</table>
