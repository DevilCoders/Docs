# Contribution
## Терминология
Приложение — вертикаль вашего сервиса в Многомордии и в Турбо.

Компоненты — набор визуальных блоков, которые реиспользуются между Приложениями.

## Как начать

```sh
git clone git@github.yandex-team.ru:serp/turbo.git
cd turbo
make
npm start
```

## Что делать, чтобы добавить новое приложение
```sh
npx turbo create myAppName --app
```
* В результате в platform/applications появится директория приложения (название директории === название сервиса)
* По команде `npm start` будет поднят сервер, доступный на `https://$USER-1-ws1.si.yandex.ru`.
* Вызвать требуемое приложение можно передав его имя в `text`, `https://$USER-1-ws1.si.yandex.ru/turbo?text=https://example.layout.ru`

### Структура приложения
* Каждое приложение должно содержать:
  * `layout.ts` —  корневой компонент
  * `fetcher.ts` — загрузчик данных
  * `brand.ts` — способ брендирования шапки и футера стандартных турбо-страниц (опционально)
  * `fallback.ts` — документ для отображения, либо url для редиректа в случае если layout вернет null или упадет (опционально)
  * `error.ts` — документ для отображения страницы с ошибкой (опционально)
  * `owners.yml` - информация о владельце приложения

Для примера можно смотреть на [`example.layout.ru`](/platform/applications/example.layout.ru).

`fetcher.ts` должен экспортировать функцию, принимающаю на вход [oбъект вида `IRequest`](/platform/core/types/fetcher-params.ts) и возвращать [oбъект вида `IFetchOptions`](/platform/core/types/fetcher-params.ts)

`layout.ts` должен экспортировать функцию, принимающаю на вход данные из целевого сервиса и возвращать json для турбо-страницы.

`brand.ts` должен экспортировать объект, который в поле `components` содержит поля с названиями блока и значениями - функциями, которые принимают на вход turbo-json стандартного блока и должны вернуть заменяющий turbo-json.

`fallback.ts` должен экспортировать функцию, возвращающую json как в `layout`, либо объект с полем `fallbackUrl` - на этот url будет сделан редирект. В функцию будут передаваться те же данные, что и в `layout`

```
applications/
└── example.layout.ru
    ├── brand.ts
    ├── fetcher.ts
    ├── layout.ts
    └── owners.yml
```

### Fallback
Можно использовать для отображения страницы ошибки, либо для редиректа на оригинальную страницу.

В случае если `layout.ts` упадет с ошибкой или вернет null, или вернет объект, в котором отсутствует либо пустое поле `content`, для приложения будет вызван код из `fallback.ts`, если таковой имеется. Результатом выполнения должен быть либо обычный turbo-json, как в `layout`, либо объект вида:
```typescript
return { fallbackUrl: 'http://yandex.ru' }
```
В случае turbo-json - он просто отобразится на странице, в случае `fallbackUrl` - на указанный url будет сделан редирект. В функцию, которая должна экспортироваться в `fallback.ts`, будут  передаваться те же параметры, что и в `layout`.

**Также** можно в самом `layout.ts` вернуть объект с пустым полем `content` и полем `fallbackUrl`, в этом случае тоже будет сделан редирект.

Пример можно посмотреть в _тестовом приложении_ [`fallback.layout.ru`](/platform/applications/fallback.layout.ru). Для запуска:
```bash
/turbo?text=https://fallback.layout.ru
```
Чтобы тестовое приложение падало, нужно добавить параметр `&fail=1` либо `&fail=random`. В первом случае ошибка в `layout` будет выбрасываться всегда, во втором - случайно.

По умолчанию тестовое приложение будет редиректить на `yandex.ru`, но можно передать свой url в параметре `&url=https://ya.ru`. Для остальных приложений никакого url по умолчанию нет.

Параметр `&content=1` отображает контент вместо редиректа.

Также можно указать параметр `&no-fallback=1`, чтобы отображалась стандартная ошибка.

### Компоненты для приложения
* Компоненты для приложения надо хранить в директории [/turbo/platform/components](/platform/components).
* Компоненты надо разрабатывать так, чтобы они были легко реиспользуемы. Они должны быть абстрактными и принимать данные в удобном для них формате.
* В редких случаях допустимо создавать кастомный компонент для сервиса, добавив для него префикс, например `ZenFeed`.
* Каждый компонент должен содержать в корне файл `owners.yml`, с информацией о владельце.
* Чтобы стили компонента с адаптером (доступного из layout) стали приходить на клиент, необходимо:
  - создать бандлы в [`turbo/src/bundles`](https://github.yandex-team.ru/serp/turbo/tree/dev/src/bundles) согласно [`README`](https://github.yandex-team.ru/serp/turbo/blob/dev/src/bundles/README.md)
  - выполнить `make`.

### Информация о владельце
Все компоненты и приложения должны содержать `owners.yml` файл с основной информацией о владельце. Минимум надо указать v-team.
```
v-team: Turbo
```
Указание дополнительных контактов - по желанию. Так же основную информация о владельцах различных приложений и компонентов в турбо можно
найти [тут](https://wiki.yandex-team.ru/turbo/services/). Если ваша команда использует Турбо, но вас там нет - можно вписываться и поддерживать контакты актуальными.

## Что делать, чтобы добавить новый компонент
```sh
npx turbo create MyComponentName --component
```

Для разработки и отладки компонентов надо выполнить в консоли `npm run storybook:serve`

### Расположение story
```
platform
├── components
│   └── Link
│       ├── Link.scss
│       ├── Link.tsx
│       └── Link.story.tsx
```
### Пример story
```tsx
import * as React from 'react';
import { storiesOf } from '@storybook/react';
import { text } from '@storybook/addon-knobs';
import { Link } from './Link';

storiesOf('Link', module)
  .add('with text', () => (
    <Link text={text('text', 'Hello Button')} />
  ))
  .add('with url', () => (
    <Link text={text('text', 'text')} url={text('url', 'http://yandex.ru')}/>
  ));
```

## Tесты
Тесты необходимо располагать в директории `__tests__`.
Unit-test файлы должны иметь расширение `.spec.ts` или `.spec.tsx`.
Hermione файлы  должны иметь расширение `.hermione.js`.

```
components/
├── Link
│   ├── Link.scss
│   ├── Link.story.tsx
│   ├── Link.tsx
│   └── List.tests
│       └── Link.spec.tsx
│       └── link.hermione.js
```

### Запуск unit тестов

```sh
npm test
```

### Запуск hermione
[Документация](./README.md#Запуск-тестов)



## Иконки и картинки
Иконки и картинки складываем в директорию `assets` внутри компонента

```
components/
├── Link
│   ├── Link.scss
│   ├── Link.story.tsx
│   ├── Link.tsx
│   └── __tests__
│       └── Link.spec.tsx
│       └── link.hermione.js
└── assets
    └── icon.svg
```

Для запуска тестов необходимо выполнить команду `npm test`;

## Технологии
* В качестве языка используется [TypeScript](http://www.typescriptlang.org/)
* Как библиотека View используется [React](https://reactjs.org/)
* Для работы со State используется [Redux](https://redux.js.org/)
* Для отладки компонентов используется [StoryBook](https://storybook.js.org/)
* Для написания unit-тестов используется [jest](https://jestjs.io/) + [enzyme](https://airbnb.io/enzyme/)

## Архитектура
### Морда
Приложения из директории applications будут загружаться на Морду по средством специального загрузчика, после клика по вкладке сервиса.
Данные, получанные в fetcher, будут передаваться в layout.ts выбранного приложения.

### Турбо
В Турбо данные будут приходить внутри turbo-json и рендерится через корневой компонент.
turbo-json -- это bemjson с некоторым доп договоренностями.
В отличие от bemjson в turbo-json может быть задано поле slots.
В slots может быть передан объект, ключи этого объекста будут использованы для наименования props'ов, а значения должны быть turbo-json'ом.
Например,
```
{
  "block": "my-component",
  ...
  "slots": {
     "rightIcon": {
        "block": "my-another-component",
     }
  }
}
```
Тогда в метод element адаптера помимо props'ов, выбранных в transform, и children, будет добавлено свойство rightIcon,
в котором будет React.ReactNode, срендеренный по turbo-json'у
```
{
    "block": "my-another-component",
}
```


### Redux
В Турбо есть Redux. Store формируется и изменяется только на клиенте.
Для использования необходимо использвать hoc `withGlobalState`:

```tsx
import { withGlobalState } from '@yandex-turbo/components/withGlobalState/withGlobalState';

import { MyComponent } from '../MyComponent/MyComponeny';

export MyComponentGlobalState = withGlobalState()(MyComponent);
```

Все данные располагаются в общем reducer `global`;
Подключенный компонент получает в props следующее:
```tsx
this.props.state // Данные из global
this.props.dispatch // Функция для отправки action
```

Для изменения state необходимо отправить action, например:
```tsx
import { GlobalActions } from '@yandex-turbo/core/state/global/reducer';

// Код

this.props.dispatch({
    type: GlobalActions.UPDATE,
    payload: {
        someField: { ...nestedFields }
    }
});
```

Чтобы записать в state данные на сервере необходимо:
```tsx
// MyComponent.adapter.tsx
export class MyComponentAdapter extends Adapter<IScheme, IProps, AdapterContext> {
    public transform(data: IScheme): IProps {
        this.context.assets.pushStore({
            global: {
                myData: {
                    partOfDataKey: partOfDataValue
                }
            }
        });
    }
}

// MyComponent.tsx
import { withGlobalState } from '@yandex-turbo/components/withGlobalState/withGlobalState';

class MyComponnet extends React.PureComponent {
    public render() {
        const { partOfDataKey } = this.props.state.myData;

        return (
            ...
        );
    }
}

export MyComponentGlobalState = withGlobalState()(MyComponent);
```

### Переводы
Про переводы подробнее можно почитать [тут](../README.md#Переводы)

### CSS Константы
При написании CSS надо стараться использовать константные значения для таких стилей как color, margin, padding, etc.
Константы для Турбо лежат в `/platform/components/constants.scss`

Ввиду того, что в Турбо существует множество сервисов, предлагается располагать их собственные файлы с константами в директориях приложений, например:
`/platform/application/news/constants.scss`.

### Layouts
Иногда необходимо, чтобы один и тот же компонент имел несколько отображений. В таких случаях помогают Layouts.
Layouts необоходимо распологать в поддиректории с компонентом:

```
components/
├── MyGreatComponent
│   ├── Element1
│   │   ├── MyGreatComponent-Element1.scss
│   │   └── MyGreatComponent-Element1.tsx
│   ├── Element2
│   │   ├── MyGreatComponent-Element2.scss
│   │   └── MyGreatComponent-Element2.tsx
│   ├── MyGreatComponent.layout
│   │   └── default.tsx
│   ├── MyGreatComponent.scss
│   ├── MyGreatComponent.story.tsx
│   ├── MyGreatComponent.tsx
```

Где MyGreatComponeny.layout/default.tsx имеет вид:
```tsx
export function withDefaultLayout(Base: MyGreatComponent) {
    return function WithDefaultLayout(props: IProps) {
        return (
            <Base {...props}>
                <Element1/>
                <Element2/>
            </Base>
        );
    };
}
```

### HOC
Для использования Higher Order Components необходимо использовать compose, при этом первым hoc в композиции должен идти withDisplayName с именем компонента.
Это необходимо для правильного определения того, какой компонент соответствует элементу в turbojson.
Например:
```tsx
// MyComponent/MyComponent.tsx

import { compose } from '@yandex-turbo/core/hoc';
import { withDisplayName } from '@yandex-turbo/components/withDisplayName/withDisplayName';
import { withBaobab } from '@yandex-turbo/components/withBaobab/withBaobab';
import { withMyHOC } from '@yandex-turbo/components/withMyHOC/withMyHOC';

class MyComponentPresenter extends React.PureComponent {
    // Code
}

export const MyComponent = compose(
    withDisplayName('MyComponent'),
    withBaobab({ name: 'some-element' }),
    withMyHoc()
)(MyComponentPresenter);
```

### Флаги

#### Backend:

Чтобы пробросить флаги конкретного сервиса в турбо, необходимо во входной источник FLAGS_SOURCE отправить аппхостовый тип flags. Примерный его формат:
```
{
    "all": {
        "flag_name": "value"
    },
    "type": "flags",
    "testids": [],
    "test_buckets": {},
}
```

#### В адаптере или в layout

Общие флаги для всех сервисов хранятся и добавляются в ```expflags/```
Этим флагам можно доверять, они проходят в ```this.context.expFlags```
см. [cgidata.js](../core/utils/cgidata.js)

Флаги сервиса можно достать в адаптере ```this.context.data.reqdata.flags``` - это прокинутые во FLAGS_SOURCE флаги не
прошедшие фильтрацию.

### Метрики

Для добавления собственного счетчика, например, Яндекс.Метрики необходимо в результат основной функции `layout.ts` добавить поле `analytics`.

**Важно**! Для корректной отправки `hit` Яндекс.Метрики необходимо добавить поле `url`.

```js
// layout.ts
export default function(data: ISomeData, rrCtx: IApphostContext) {
    const someData = {/*...*/};
    const someMetrikaParams = {/*...*/};
    const url = data.url;

    return {
        ...someData
        analytics: [{
            type: 'Yandex',
            id: 'someMetrikaId',
            params: { ...someMetrikaParams }
        }],
        // url необходим для корректной отправки hit Яндекс.Метрики
        url,
    };
}
```
