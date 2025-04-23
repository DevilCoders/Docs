## Сажаем React фичи на Табурет
У нас есть фича `AwesomeFeature` на реакте, и мы хотим использовать её совместно с Табуретом для платформы desktop.

Пусть корневой компонент - это `./src/features/AwesomeFeature/AwesomeFeature.tsx`:
```ts
import React, { FC } from 'react';

interface IAwesomeFeatureProps {
    name: string;
}

export const AwesomeFeature: FC<IAwesomeFeatureProps> = props => (<p>Give me AwesomeFeature, {props.name}</p>)
```

### Подготовка фичи для отправки на клиент
#### Создание entrypoint для фичи
Необходимо сделать возможным работу компонента в двух режимах: на сервере - шаблонизация, а на клиенте - гидрация. Для этого мы привязываем фичу к специальному компоненту `Root`. Это можно сделать через вспомогательную функцию createApp.
Создаём файл `src/features/AwesomeFeature/AwesomeFeature.entries/desktop.ts` с таким содержимым:
```ts
import { createApp } from '...';
import { AwesomeFeature } from '../AwesomeFeature.tsx';

const AwesomeFeatureApp = createApp('awesome-feature')(AwesomeFeature);
```

Компонент `Root` на сервере помогает шаблонизировать нашу фичу, а на клиенте её гидрирует. Его необходимо имплементировать самостоятельно, учитывая специфику вашего сервиса. Базовый вариант компонента `Root` выглядит примерно так:
```ts
export function createApp(featureId: string) {

    return function<P>(Component: React.ComponentType<P>) {
        const canUseDom = (
            typeof window !== 'undefined' &&
                window.document &&
                window.document.createElement
        );

        if (canUseDOM) {
            const init = (selector?: string) => {

                const root = document.querySelector(selector || '.Root');

                ReactDOM.hydrate(<Component {...initialState} />, root);
            };

            init();
        }

        return (props: P) => {

            return React.createElement(
                'div', { className: 'Root', id: `${featureId}-${Math.random()}`, },
                <Component {...props} />,
            );
        };
    };
}
```

#### Сборка статики фичи
Cтатика [собирается](./static-building.md) в чанки с помощью webpack, при этом генерируется assets.json в котором указаны все пути до чанков. Полученный файл с путями ассетов передаётся в Runtime, который отправляет нужные ассеты фичам.
**На этом этапе надо проверить, что entries в конфиге webpack'а содержит правильный путь до entrypoint'а вашей фичи.**
В нашем случае это `src/features/AwesomeFeature/AwesomeFeature.entries/desktop.ts`.

### Шаблонизация на сервере
Чтобы код нашей фичи шаблонизировался на сервере необходимо настроить адаптер и Runtime;

В адаптер надо добавить метод `render`, который возвращает нашу фичу. **Необходимо возвращать entrypoint, создание которого было описано ранее:**
```ts
import { Adapter } from '...';
import { AwesomeFeatureApp } from 'src/features/AwesomeFeature/AwesomeFeature.entries/desktop.ts'

export class AdapterAwesomeFeature extends Adapter {

    render() {
        const props: IAwesomeFeatureProps = { ... };

        return (<AwesomeFeatureApp {...props} />);
    }
}
```

В `Runtime` нужно доопределить `tryRender` так, чтобы он вызывал рекатовый `renderToString` из библиотеки `ReactDOM`. Родительский метод сделает все базовые манипуляции и позовет метод `render` адаптера:
```ts
tryRender(instance) {
    const renderResult = super.tryRender(instance);
    return ReactDOM.renderToString(renderResult);
}
```
В результате цепочка вызовов Runtime.select → AdapterAwesomeFeature.render → ReactDOM.renderToString вернет объект с React фичей отрендеренной в строку `{ data: 'react-rendered-to-html', meta... }`.
### Как извлекать фичи из Runtime
Чтобы выполнить код адаптера нужно воспользоваться методом `select` экземпляра Runtime:
```ts
    runtime.select({
        context,
        snippet
    });
```
Подробнее описано [тут](./quick-start.md).

Чтобы получить статику, нужную на странице, достаточно вызвать метод `getAssets`, в нужном вам месте, который вернет информацию о статике в массиве ассетов, описанном в интерфейсе [IAsset](../adapters/typings/assets.ts).
```ts
    runtime.getAssets();
```

### Как доставить на клиент сам React/ReactDOM
Если нужно доставить на клиент дополнительные библиотеки, то тогда нужно переопределить метод `getAssets` в классе унаследованном от Runtime:
```ts
getAssets(): IAsset[] {
    const assets = super.getAssets();
    if (assets.length === 0) return [];

    return [{ name: 'react', url: '/* ссылка на react-with-dom-and-polyfills */' }].concat(assets);
}
```
