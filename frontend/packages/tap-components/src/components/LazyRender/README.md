# LazyRender

Компонент для ленивой отрисовки блока.

Задерживает отрисовку компонента до момента первого появления в области видимости окна браузера.

## Пример использования

```typescript jsx
import React from 'react';
import { LazyRender } from '@yandex-int/tap-components/LazyRender';

import Skeleton from './my-component/Skeleton';
import Component from './my-component/Component';

const App: React.FC = () => {
    return  (
        <LazyRender skeleton={<Skeleton />} >
            <Component />
        </LazyRender>
    );
};

export { MyComponent };
```

## Свойства

| Свойство             | Тип                        | Описание                         |
| -------------------- | -------------------------- | -------------------------------- |
| children             | `React.ReactElement`       | Компонент для отрисовки          |
| intersectionOptions? | `IntersectionObserverInit` | Опции для `IntersectionObserver` |
| skeleton?            | `React.ReactElement`       | Заглушка                         |

## Когда использовать

Здесь перечислены случаи и примеры, в которых использование `LazyRender` дает прирост в производительности.

- Большие third-party-скрипты. Например, редакторы текста, скрипты новостей, встраиваемые видео и т. д.
- Тяжелые компоненты с большими объемами логики (сложные многофункциональные таблицы, большие формы оформлений заказов и т. д.).
- Компоненты, которые тянут с собой большое количество ресурсов (картинки, файлы и т. д.).

Не рекомендуется оборачивать в `LazyRender` элементы больших списков, т. к. это приведет к созданию инстанса `IntersectionObserver` на каждый элемент списка и его срабатыванию на каждый скролл, что может существенно снизить как скорость загрузки и инициализации приложения, так и скорость работы приложения в целом. Для отображения больших списков рекомендуется использовать виртуализированные списки (например, [react-window](https://github.com/bvaughn/react-window)).

### Пример из жизни

Погода в прямом эфире и новостные блоки в сервисе Яндекс.Погода реализованы в виде вставки `iframe` и подключения стороннего скрипта JS.
Такая инициализация, т. е. поход в сеть за скриптами, парсинг и т. д., на старте приложения могут сильно повлиять на [Time to Interactive](https://developers.google.com/web/tools/lighthouse/audits/time-to-interactive), [First Contentful Paint](https://developers.google.com/web/tools/lighthouse/audits/first-contentful-paint) и [другие метрики производительности](https://developers.google.com/web/tools/lighthouse/v3/scoring).

Для улучшения этих метрик был использован компонент `LazyRender`.

Блок новостей:<br/>
<img src="./assets/news.jpeg" width="320" alt="news">

```typescript jsx
<LazyRender skeleton={<ExternalScriptSkeleton />}>
    <ExternalScript src={'external-script-src'} />
</LazyRender>
```

Блок с погодой в прямом эфире:<br/>
<img src="./assets/camera.jpeg" width="320" alt="camera">

```typescript jsx
<LazyRender>
    <iframe src={'iframe-src'} />
</LazyRender>
```

Средние результаты замеров производительности **без использования** `LazyRender`:

|                        | Emulator x4 throttling Macbook Pro 13 | Samsung Galaxy J5 | Sony Xperia E5 |
| ---------------------- | ------------------------------------- | ----------------- | -------------- |
| Scripting              | 6106 ms                               | 5304 ms           | 5410 ms        |
| Rendering              | 547 ms                                | 512 ms            | 532 ms         |
| DomContentLoad Event   | 3018 ms                               | 2801 ms           | 2874 ms        |
| First Paint            | 4212 ms                               | 3821 ms           | 3912 ms        |
| First Contentful Paint | 4212 ms                               | 3823 ms           | 3912 ms        |
| Onload Event           | 5814 ms                               | 4920 ms           | 5012 ms        |
| Total                  | 8900 ms                               | 7101 ms           | 7213 ms        |

Средние результаты замеров производительности **с использованием** `LazyRender` на блоках камер и новостей:

|                        | Emulator x4 throttling Macbook Pro 13 | Samsung Galaxy J5 | Sony Xperia E5 |
| ---------------------- | ------------------------------------- | ----------------- | -------------- |
| Scripting              | 4684 ms                               | 4231 ms           | 4268 ms        |
| Rendering              | 475 ms                                | 375 ms            | 385 ms         |
| DomContentLoad Event   | 2992 ms                               | 2603 ms           | 2684 ms        |
| First Paint            | 4025 ms                               | 3301 ms           | 3312 ms        |
| First Contentful Paint | 4025 ms                               | 3303 ms           | 3312 ms        |
| Onload Event           | 3959 ms                               | 3265 ms           | 3287 ms        |
| Total                  | 7045 ms                               | 6323 ms           | 6387 ms        |

Видно, что использование `LazyRender` позволяет сократить время выполнения скриптов на 1.1 сек. и время отрисовки страницы на 200 мс.

Помимо перечисленных случаев применения `LazyRender`, рекомендуется исследовать пользу в реалиях конкретных приложений.

## Поддержка

Для работы в старых версиях браузера необходим [полифил](https://github.com/w3c/IntersectionObserver/tree/master/polyfill) для `IntersectionObserver`

Поддержка без полифила:

Safari >= 11 \
Chrome >= 52
