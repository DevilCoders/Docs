# CSS-стили
Всё написанное здесь касается Реакта. В BEM-части (legacy) особых правил нет, но стараемся придерживаться таких же правил, как и в Реакте.

## Соглашение по именованию классов
На проекте для именования классов в CSS принята BEM-нотация. Ознакомиться с ней подробнее можно [здесь](https://ru.bem.info/methodology/naming-convention/).

Мы постоянно внедряем новые технологии и инструменты, но проект огромный, поэтому переписать за раз всё невозможно.
У нас много компонентов на js + обычный css с парой postcss-плюшек, но если вы пишите что-то новое - используйте typescript + [css-modules](https://github.com/css-modules/css-modules).

Пример именования при использовании обычного css:
```jsx
    // TextInput.js

    require './TextInput.css';

    modules.export = () => {
        return (
            <span className="TextInput TextInput_size_l TextInput_active">
                <span className="TextInput__box">
                    <input className="TextInput__control"/>
                </span>
            </span>
        );
    }
```
```css
    /* TextInput.css */

    .TextInput {
        /* стили самого блока */
        ...

        /* модификаторы блока */
        &_active {
            ...
        }

        /* модификаторы блока вида key_value */
        &_size_m { ... }
        &_size_l { ... }

        /* элементы блока */
        &__box {
            ...

            /* модификаторы элемента */
            &_big { ... }
        }

        /* переопределение стилей элемента */
        &_active &__box { .. }

        &__control { ... }

        ...
    }
```

Пример именования при использовании [css-modules](https://github.com/css-modules/css-modules):
```tsx
    // TextInput.tsx

    import cn from 'classnames';

    import css from './TextInput.m.css';

    export default () => {
        // мы используем classnames для склеивания классов,
        // но можно пользоваться и Array.join(' ') и шаблонными строками (``).
        return (
            <span className={ cn(css.root, css.root_size_l, css.root_active) }>
                <span className={ css.box }>
                    <input className={ css.control }/>
                </span>
            </span>
        );
    }
```
```css
    /* TextInput.m.css */

    /* стили самого блока */
    .root { ... }

    /* модификаторы блока */
    .root_active { ... }

    /* модификаторы блока вида name & value */
    .root_size_m { ... }

    .root_size_l { ... }

    /* элементы блока */
    .box { ... }

    /* модификаторы элемента */
    .box_big { ... }

    /* переопределение стилей элемента */
    .root_active .box { ... }

    .control { ... }

    ...
```

### Особенности работы с css-modules:
- при сборке `.root` будет заменен на название файла (без ".m.css" - `.root = TextInput`, `.root_mod = TextInput_mod`)
- если вам нужен класс, но для него не нужны стили, вам всё равно необходимо описать его в css с пометкой "for js"
```css
    .root {
        /* for js */
    }
```
- к сожалению, хотя css-modules поддерживают nesting (вложенность классов через `&`), ни плагин, который даёт нам автокомплит для классов, ни линтер, позволяющий отслеживать undefined/unused классы, не умеют собирать классы, описанные через `&`, поэтому __для классов__ в css-modules мы его не используем. Но вы можете использовать nesting для описания псевдо-элементов, псевдо-селекторов, вложенных тегов и т.д.
```css
    .root {
        /* ts не найдёт этот класс, линтер на pre-commit не пропустит ваш код, хотя webpack всё соберет */
        &_active { ... }
    }

    .button {
        /* всё, что не касается классов, пройдёт и отлично соберется */
        &:hover { ... }

        & span { ... }
    }
```
- плагин не позволит вам использовать генерацию для классов, поэтому их придётся описывать целиком (что в целом плюс, так как такие классы проще искать потом по проекту):
```js
    const className = cn(
        css.button,
        css[`button_type_${ props.type }`], // соответствующие классы в css будут помечены как unused
    );
```
```js
    const className = cn(
        css.button,
        {
            [css.button_type_submit]: props.type === 'submit',
            [css.button_type_button]: props.type === 'button',
        },
    );
```
- написание __скриншотных тестов__: поведение css-modules здесь аналогично проду. Так как это тесты непосредственно на верстку, здесь css-modules проходят полную обработку Webpack. Она добавляют к каждому классу уникальный hash - `.TextInput__box-[hash]`, поэтому  используйте селекторы вида `[class^="TextInput__box-"]` для нахождения нужной html-ноды. Селектор обязательно должен оканчиваться на "-", иначе под ваше правило так же попадут похожие классы (например, `.TextInput__boxIcon-[hash]`).
- написание __тестов на логику__: здесь css-modules не обрабатываются Webpack, а возвращаются через Proxy как есть (`.root = 'root'`, `.button = 'button'`), но чтобы найти условную кнопку и кликнуть по ней этого достаточно. Чтобы использовать модули, их нужно экспортнуть из файла компонента:
```js
    import css from './Banner.m.css';

    ...

    export { css };

    export default Banner;
```
Тогда в тесте их можно будет использовать как:
```js
    import Banner, { css } from './Banner';

    it('отправляет метрики на клик', () => {
        const { container } = render(
            <Context>
                <Banner/>
            </Context>,
        );

        const link = container.querySelector(`.${ css.link }`);
        link && UserEvent.click(link);

        expect(contextMock.metrika.reachGoal).toHaveBeenCalled();
    });
```
__Важно__: прямой импорт css-modules в файле с тестами (`import css from './Button.m.css';`) не будет работать, так как css не успеет пройти через Proxy.

### Основные договоренности
(код, нарушающий их, не должен пройти review)

- имена классов формируются через знак подчеркивания "_" по правилу `[block-name]__[elem-name]_[mod-name]_[mod-val]`
- класс блока `[block-name]` соответствует имени вашего компонента и он в __PascalCase__
- класс элемента `[elem-name]`, модификаторы `[mod-name]` и их значения `[mod-val]` именуются в __camelCase__
- каждый BEM-блок описывается в отдельном css-файле
- стили компонента описываются одним BEM-блоком (если вам нужно больше, лучше вынести эту часть в отдельный под-компонент со своими стилями)
- если компонент использует какие-либо стили, кроме своих, вы должны их явно импортировать в css (иначе ваши скриншотные тесты не будут соответствовать истине)
```css
    /* Пример - ваш компонент использует кастомный шрифт */
    @import '~auto-core/react/components/gerbera-font.css';

    ...

    .title {
        font-family: var(--gerbera-font);
    }
```
- мы не используем [composes](https://github.com/css-modules/css-modules#composition) в css-modules, а контролируем классы напрямую в компоненте (явное лучше неявного)
- у нас запрещено переопределять стили другого компонента, используйте [миксование](https://ru.bem.info/methodology/key-concepts/#микс) классов с помощью прокидывания props.className в нужный компонент. Но в исключительных случаях если очень-очень надо, в css-modules переопределить стили позволяет директива `:global`:
```css
    /* stylelint-disable-next-line selector-pseudo-class-disallowed-list */
    .root :global(.Button) {
        color: red;
    }
```
- если вы правите обычный css (не css-modules), вы можете использовать nesting, но при этом нельзя разбивать через `&` имена блока, элемента, модификатора (или его значение). То есть так делать __не стоит__:
```css
.BlockName {
    &__element {
        &Name1 { ... }
        &Name2 { ... }
    }
}
```
Это мешает искать стили по имени элемента и ухудшает читабельность. Стоит задуматься, почему вам захотелось сделать так и вынести этот элемент в отдельный под-компонент. Правильное написание:
```css
.BlockName {
    &__elementName1 { ... }
    &__elementName2 { ... }
}
```

### Best practices
(не обязательно, но желательно использовать)

- соблюдать последовательность описания стилей из примеров - это улучшает читабельность css
- если вы используете локальные переменные, то их лучше описывать не в глобальной области видимости, а только для вашего блока:
```css
    /* вот так писать НЕ СТОИТ */
    :root {
        --height: 34px;
    }

    .root { ... }

    .box {
        height: var(--height);
    }
```
```css
    /* вот так лучше */
    .root {
        --height: 34px;
    }

    .box {
        /* это сработает, так как элемент вложен в html-ноду с классом блока */
        height: var(--height);
    }
```
- сложные вычисления лучше обозначать говорящими переменными или сопровождать комментарием
```css
    .root {
        --width-ratio-landscape: 0.54;
        --text-width-ratio-landscape: calc(1 / var(--width-ratio-landscape) * (1 - var(--width-ratio-landscape)));
    }

    .box {
        width: calc(var(--width-ratio-landscape) * 100%);
    }

    .boxText {
        width: calc(var(--text-width-ratio-landscape) * 100% - 16px);
    }
```
- если вам нужно получить объект с классами из css-module и прокинуть в другой компонент, скорее всего линтер начнёт ругаться на классы как на unused. В этом случае не стоит отключать его через eslint-disable, а явно описать структуру объекта с классами - это позволит сохранить типизацию и линтинг стилей.
```jsx
    // TextInput.tsx with styles
    import css from './TextInput.m.css';

    const classNames = {
        root: css.root,
        box: css.box,
        control: css.control,
    };

    export default () => {
        return <TextInputDumb classNames={ classNames }>
    };
```
```tsx
    // TextInputDumb.tsx without styles
    type Props = {
        classNames: {
            root: string;
            box: string;
            control: string;
        };
    }

    export default (props: Props) => {
        const css = props.classNames;

        return (
            <span className={ css.root }>
                <span className={ css.box }>
                    <input className={ css.control }/>
                </span>
            </span>
        );
    };
```

### Возможные проблемы
- Если в VS Code у вас не работает автокомплит классов в .tsx, вероятно у вас запущено расширение для IDE, работающее с css-modules и конфликтующее c плагином typescript, установленным в проекте (например, [CSS Modules by clinyong](https://github.com/clinyong/vscode-css-modules)). Отключение расширения должно помочь.
- Если в VS Code у вас runtime отсутствует подсветка undefined/unused классов в .tsx, проверьте какую версию typescript вы используете в IDE - VS Code's version или Workspace version (предпочтительнее). Подробнее [здесь](https://code.visualstudio.com/docs/typescript/typescript-compiling#_using-the-workspace-version-of-typescript).


## Работа с типографикой
Источник правды по типографике - [гайд в фигме](https://www.figma.com/file/EPYpK2cb3mB31vRrEXgeED/Web-Auto-Library-NEW?node-id=3%3A6810)
Все переменные типографики лежат в файле [variables.css](../auto-core/react/components/variables.css)

Алгоритм работы с типографикой в новых макетах:
* выбрать в макетах Figma необходимый слой, в панели Inspect в правой части экрана найти блок Typography
* взять первое слово в названии пресета, использовать переменные: для `line-height` это `--lh-{type}`, для `font-size` это `--fs-{type}`
* если в блоке Typography что-то не то, либо использован не пресет типографики (какой-то хардкод, кастомные значения) - писать дизайнеру с просьбой исправить, он ошибся

Например, для пресета "Body • 15|20 / Regular", стоит использовать переменные --fs-body и --lh-body.
При реальной необходимости можно попросить дизайнера обновить части старых макетов.

## Работа с цветами
Источник правды в вопросах цветов - [гайд в фигме](https://www.figma.com/file/ceSbxo6MM0GUHaO3W2GRg0Un/Auto-%E2%80%A2-Colors?node-id=1%3A60).
Все переменные цветов лежат в файле [variables.css](../auto-core/react/components/variables.css)

Цвета делятся на следующие группы:
* базовые
* промо
* социальные

Элементы интерфейса, к которым применяются переменные цветов, мы делим на следующие группы:
* текст
* иконки
* блоки с заливкой
* бордеры и дивайдеры
* контролы

Наши переменные базовых цветов должны полностью соответствовать цветам в гайде. Это значит, что мы не добавляем новые переменные сами.

Все базовые цвета отражены на каждую из групп с соответствующим префиксом. Например, для базового цвета `--red`, имеются `--red`, `--red`, `--icon-red`, `--divider-red` и `--control-red`. Мы используем только такие полусемантичные цвета, соответственно, базовые цвета нельзя использовать за пределами файла `variables.css`. Социальные цвета, (например, `--social-vk`), а также промо-цвета (например, `--promo-blue-dimmed`) можно использовать напрямую.

Для удобства работы с цветами рекоммендуется поставить расширение для вашего редактора кода. Например, для [vscode](https://marketplace.visualstudio.com/items?itemName=naumovs.color-highlight) и для [vim](https://github.com/gko/vim-coloresque).

### Как не испытывать боль при работе с цветами
Мы сохраняем именование цветов дизайнеров. Это позволяет нам в большинстве случаев точно определить используемый цвет следующим образом:
* в фигме выбираем интересующий нас слой с цветом
* выбираем в правой панели вкладку Code
* ищем над значением цвета автоматически проставленный комментарий, например `/* Blue Light Extra */`
* если комментарий есть - используем цвет с таким же именем, не забывая добавить необходимый префикс, например `--tertiaryBlue`

Отсутствие комментария означает, что дизайнер использовал цвет не из списка гайдовых. Он мог сделать это намеренно. Если цвет определенно не похож на уже используемые нами - используем его напрямую, без переменной. Если имеются сомнения, стоит написать дизайнеру.
