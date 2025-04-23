<h1 align="center" style="border-bottom: none;">:rocket: :package: @metrika/components :heart_eyes_cat:</h1>
<h3 align="center">Общие компоненты для проектов Метрики</h3>
<h3 align="center">:lollipop: <a href="https://github.yandex-team.ru/pages/Metrika/frontend/components">Демостенд</a></h3>

## :cool: Установка :free:

```bash
npm i --save --registry=https://npm.yandex-team.ru @metrika/components react react-dom [typescript and @types]
```

## :muscle: Использование :metal:

```jsx
import {
    FormRow,
    HelpHint,
    IconToggle,
    Button,
    TextInput,
} from '@metrika/components';
...
<FormRow size={Size.S}>
    <FormRow.Label>
        это label с иконкой <IconToggle />
    </FormRow.Label>
    <FormRow.Control>
        <ControlsBar size="s">
            <TextInput size="s" theme="normal" placeholder="а это контрол" />
            <Button size="s" theme="normal">say hi</Button>
            <HelpHint>Подсказка</HelpHint>
        </ControlsBar>
    </FormRow.Control>
</FormRow>
```

Пакет можно использовать в двух сборках, с `commonjs` и `es6` модулями соответственно. Webpack автоматически будет использовать `es6` версию, а node.js или webpack < 2 - `commonjs`. В `commonjs` версии удалёны импорты css файлов, т.к. в node.js (при ssr) они не используются.

<details>
<summary>Стили автоматически импортируются внутри компонента, а это значит, что их использование предполагает наличие webpack с примерно такой конфигурацией</summary>

-   Стили внутри `js` бандла

```js
{
    module: {
        rules: [
            ...
            {
                test: /\.css$/,
                use: [
                    require('style-loader'),
                    {
                        loader: require('css-loader'),
                        options: {
                            importLoaders: 1,
                        },
                    },
                ],
            },
            ...
        ],
    },
}
```

-   С выносом в отдельный файл (обычно используется для production сборки)

```js
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const cssLoader = require('css-loader');
...
{
    module: {
        rules: [
            ...
            {
                test: /\.css$/,
                use: [
                    MiniCssExtractPlugin.loader,
                    cssLoader,
                ],
            },
            ...
        ],
    },
    plugins: [
        ...
        new MiniCssExtractPlugin({
            filename: '[name].bundle.css',
        }),
        ...
    ],
}
```

---

</details>

## Поддержка браузеров

Все evergreen браузеры + IE 11 :trollface:

## Тестирование :scream_cat: :umbrella:

Используется [Jest](https://h.yandex-team.ru/?https%3A%2F%2Ffacebook.github.io%2Fjest%2F), [Enzyme](http://airbnb.io/enzyme/), [ReactTestUtils из react-dom](https://reactjs.org/docs/test-utils.html)

```bash
npm run test # разовый запуск
npm run test:watch # watcher
```

Можно пробросить любые параметры в `Jest` с помощью оператора `--` из `npm`

```bash
npm run test -- --allThisString=willBePassed --to jest
```

Например, запустить тест для конкретного компонента `Header`

```bash
npm run test -- Header # разовый запуск
npm run test:watch -- Header # watcher
```

## Разработка

**Можно разрабатывать локально**

**Нужно установить Node >= 8**. Это можно легко сделать с помощью [nvm](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fcreationix%2Fnvm)

```bash
git clone git@github.yandex-team.ru:Metrika/metrika-components.git
cd metrika-components
npm i
npm run styleguide
```

Работает watcher, так что любые изменения в коде сразу же отражатся на странице.

Если используется версия из npm, нужно релизить пакет с помощью таски `npm run release -- --type=<version>`, version - любая semver валидная строка, включая major, minor, patch

## I18N

-   Ссылка на проект в танкере https://tanker.yandex-team.ru/?project=metrika-components
-   Работа в tanker-е ведётся в отдельных ветках.
-   В интерфейсе танкера создайте ветку с названием Вашей текущей ветки.
-   Внесите необходимые изменения.
-   Выгрузите изменения при помощи команды `npm run i18n:pull`.
-   После мёрджа ветки в github, смёрждите ветки в интерфейсе tanker-а.

> :pushpin: Добавить автоматический мёрдж веток после слияния

Выгрузить из ветки:

```bash
npm run i18n:pull
```

</details>
