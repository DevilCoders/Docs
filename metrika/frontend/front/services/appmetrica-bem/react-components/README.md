Первоначально проект был создан с использованием [create-react-app-typescript](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fwmonk%2Fcreate-react-app-typescript), потом был сделан `eject` для добавления своих лоадеров

# Структура проекта

`config` - конфиги сборки и тестов (сейчас это [jest](https://h.yandex-team.ru/?https%3A%2F%2Ffacebook.github.io%2Fjest%2F)). Основной файл - `webpack.config.js`;

`docs` - `md` файлы;

`scripts` - скрипты-хелперы, например для запуска тестов;

`src` - исходники.

## Структура src

`src/components` - `view` компоненты;

`src/containers` - контейнеры. Используются для связи `redux`-стора и `view`-компонентов;

`src/icons` - иконки, наследуются от `src/icons/BaseIcon.ts`. Использование отдельной компоненты на каждую иконку вместо пропса `type` позволяет лучше их типизировать (у разных иконок могут быть разные пропсы). Кроме того, в итоговый бандл попадают только те иконки, которые в нём используются;

`src/lego` - реэкспорт из `lego-on-react`. Зачем:

* Для компонента нужно подключать ещё и стили. То есть, при `import { Button } from 'lego-on-react'` в сборку попадёт только `js`-код компонента. Стили нужно подключать так - `import 'lego-on-react/src/components/button/button.css';`. Теперь это лежит в одном месте, пример подключения компонента - `import Button from 'lego/Button';`. С каждым компонентом экспортируются и интерфейс с его пропсами - `import Button, { ButtonProps } from 'lego/Button';`;
* Переопределение стилей. Теперь это можно сделать в одном месте;
* Типизация. В начале в `lego-on-react` её не было совсем, сейчас она неполная. Наша типизация `lego`-компонентов описана в `typings/lego`;
* `Tree Shaking`. В данный момент `lego-on-react` экспортируется как `CommonJS` модуль, соответственно подключение одного компонента вида `import { Button } from 'lego-on-react';` тянет за собой **_всю_** библиотеку.

`tslint-rules` - кастомные правила для `tslint`;

`typings` - тайпинги для наших компонент из bem и для `lego-on-react`;

`index.tsx` - главный файл, `entrypoint`, с него начинается сборка. В него нужно добавить компоненты, которые нужно использовать в `bem`-мире. Компоненты добавлять в `window._reactAppmetrica`; props, которые являются функциями нужно добавить в массив handlers, они будут триггерить события на БЭМ элементе. В БЭМ компоненты можно использовать, через компонент `i-react`, передав имя компонента через параметр reactElem и props через параметр props.

### !!! Важно !!! ###

Пути до модулей по умолчанию вычисляются относительно директории `src`:

```diff
- import { ControlsList } from 'src/components/';
- import { Button } from 'src/lego/';
+ import { ControlsList } from 'components';
+ import { Button } from 'lego';
```

**_Не нужно_** писать относительных путей:

```diff
- import { ControlsList } from '../../components/';
+ import { ControlsList } from 'components';
```

При написании компонента необходимо добавить его реэкспорт в `index.ts` родительской директории:
```typescript
// src/components/YourComponent/YourComponent.tsx
export interface YourComponentProps {}
export default class YourComponent extends React.PureComponent<YourComponentProps>


// src/components/index.ts
// ...other reexports
export { default as YourComponent, YourComponentProps } from './YourComponent/YourComponent';
```

Это позволит писать так
```diff
- import YourComponent from 'components/YourComponent/YourComponent';
- import AnotherComponent from 'components/AnotherComponent/AnotherComponent';
+ import { YourComponent, AnotherComponent } from 'components';
```

## Файлы
`.babelrc` - настройки [babel](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbabel%2Fbabel)

`.browserslistrc` - настройка [browserslist](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fai%2Fbrowserslist). Список поддерживаемых браузеров. По ним [babel](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbabel%2Fbabel) и [postcss](https://h.yandex-team.ru/?http%3A%2F%2Fpostcss.org%2F) решают, какие фичи стоит "транспайлить", а какие нет.

`styleguide.config.js` - конфиг для [react-styleguidist](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fstyleguidist%2Freact-styleguidist)

`tsconfig.json` и `tsconfig.test.json` - конфиг для [typescript](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2FMicrosoft%2FTypeScript)

`tslint.json` - конфиг для [tslint](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fpalantir%2Ftslint)

## Описание сборки
[Typescript](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2FMicrosoft%2FTypeScript) используется только для проверки типов. Для `транспайлинга` (деградации) кода используется [babel](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbabel%2Fbabel). Кажется, что такой подход более гибкий, т.к. у [babel](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbabel%2Fbabel) большая экосистема плагинов (например для оптимизации jsx). Между плагинами передается один раз составленное `AST`-дерево, не нужно думать про `sourcemaps`.

## Команды

Нужно запускать из корня проекта. Эти команды вынесены в `GNUMakefile` в корне проекта, т.к. запускаются в основном на дев-сервере, где нужна правильная версия `node.js`

`make react-build` - соберет бандл в `react-components/build/js/_main_{lang}.js`. В `production` сборке так же будет собран `css` файл - `react-components/build/css/_main.css`;

`make react-watch` - соберет, будет следить за изменениями файлов и пересобирать бандл;

`make react-watch-dev` - отличие в том, что сборка происходит только для двух последних версий `Chrome` и `Firefox` - почти весь `es6` используется нативно. Если нужна работа в более старых браузерах - используй `make react-watch`.

### !!!Важно!!!
В перечисленных выше командах можно и нужно задать переменную окружения `BUILD_LANGS`, передав ей список языков через запятую, например

    BUILD_LANGS=ru make react-watch-dev

По умолчанию будут собраны 2 бандла (en, ru)

### Остальные команды

можно посмотреть в `package.json` (поле `scripts`) в текущей директории. Запускать их можно локально с помощью команды `npm run {command_name}`, прежде убедившись, что установлена правильная версия `node.js` (6 или выше). Например:

`make styleguide` - запустить [styleguidist](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fstyleguidist%2Freact-styleguidist) в режиме слежения за файлами и возможностью редактировать код примеров прямо в браузере;
(после запуска styleguidist'a нужно пробросить порт 6060 командой `ssh appmetrika-dev-trusty.mtrs.yandex.ru -N -L 6060:localhost:6060` и ввести `localhost:6060` в браузере)

`npm run test:watch` - запустить тесты [jest](https://h.yandex-team.ru/?https%3A%2F%2Ffacebook.github.io%2Fjest%2F) в режиме слежения за изменениями файлов. (Можно так же запускать тесты при помощи команды make test-react. Передать параметры можно как JEST_OPTS="-- TristateCheckBox")

Кроме того, в `package.json` есть поля с настройками [prettier](https://h.yandex-team.ru/?https%3A%2F%2Fprettier.io%2F), [stylelint](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fstylelint%2Fstylelint), [jest](https://h.yandex-team.ru/?https%3A%2F%2Ffacebook.github.io%2Fjest%2F) и `precommit`-хуков.

## Договорённости и code-style

### Договорённости об именовании props для React-компонентов

Если prop является компонентом, prop следует называть с большой буквы

```jsx
<Component TheComponent={AnotherComponent} />
```

Если prop является элементом, prop следует называть с маленькой буквы

```jsx
<Component theElement={<Component />} />
```

### Договорённости о написании стилей при помощи styled-components

Стилизация тегов:

```jsx
    export const Component = styled.div<PlaceholderProps>``
```

Стилизация react-компонентов:

```jsx
    export const Component = styled(AnotherComponent)<PlaceholderProps>``
```

## Переводы

Для подстановки переводов используется webpack плагин i18n-webpack-plugin

Для добавления параметра в перевод укажите его в названии ключа в фигурных скобках и используейте как параметр в содержимом перевода:

```jsx
    __(`from-date-${fromDate}`) // keyset = { 'from-date-{fromDate}': 'начиная с {fromDate}' }
```

Для склонения используйте зарезервированный параметр `count` (добавляйте переводы в танкере при помощи опции "склонять"):

```jsx
    __(`${count}-apples`) // keyset = { '{count}-apples': [ '{count} яблоко', '{count} яблока', '{count} яблок' ] }
```