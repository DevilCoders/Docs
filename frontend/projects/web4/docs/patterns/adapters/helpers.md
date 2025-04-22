# Хелперы

- [Пример #1](#функции-обработки-картинок)
- [Пример #2](#настройки-колдунщика)

## Функции обработки картинок

В адаптерах ["Картинок"](../../../src/features/Images) нужен код для работы с картинками внутри колдунщика:

- вычисление размера картинки по параметрам
- генерация различных частей URLа для картинки
- работа с настройками обрезки картинок
- работа с кукой szm

Этот общий код вынесен в [Images.helpers](../../../src/features/Images/Images.helpers). Разные подтипы адаптеров используют разные хелперы.

Например, так:

``` ts
import { Helpers } from ‘./Images.helpers’;

export class AdapterImages extends Adapter<IImagesSnippet> {
    protected helpers = Helpers;

    protected szm = this.helpers.getSzmCookie(this.context);
    protected screenSize = this.helpers.getScreenSize(this.szm);
}
```

## Настройки колдунщика

Настройки адаптеров ["Здоровья"](../../../src/features/HealthArticles) выделены в отдельную [сущность и разложены по платформам](../../../src/features/HealthArticles/Options).

Настройки возвращаются абстрактным методом `getOptions`:

``` ts
export abstract class AdapterHealthDiseases extends Adapter<IAdapterHealthDiseases> {
    protected abstract getOptions(): IAdapterHealthOptions;

    thumb(): Construct.IThumb {
        const { imageUrl, url } = this.snippet;
        const { imageSize, imageHdSize } = this.getOptions();

        return {
            block: 'thumb',
            url,
            image: imageUrl + imageSize,
            imageHd: imageUrl + imageHdSize,
        };
    }

    // ...
}
```

Пример подключения настроек в эксперименте:

``` ts
import {
    AdapterHealthArticles_multiple as Base,
} from '../../../../../features/HealthArticles/_multiple/HealthArticles_multiple@desktop';
import { options } from '../../../../../features/HealthArticles/Options/HealthArticlesOptions@desktop';

export function adapterHealthArticles_multiple() {
    return class AdapterHealthArticles_multiple extends Base {
        getOptions() {
            return options();
        }
    };
}
```
