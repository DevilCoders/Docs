# Как именовать все в React'е

## Компоненты

(они же блоки)

Под каждый компонент заводится отдельная папка.
Как правило, она располагается в папке `*/react/components`.
Имя папки в точности совпадает с именем компонента (класса).
Имя файла с js и со стилями такие же, как и имя компонента:

    www-desktop
        react
            components
                Header
                    Header.js
                    Header.styl

Когда мы подключаем где-то этот компонент, то используем "абсолютные" пути:

    const Header = require('components/Header');

Используем [этот плагин](https://github.com/shaketbaby/directory-named-webpack-plugin/tree/v1.4.0),
чтобы `require('components/Header')` находило файл `Header.js`.

Имя основного css-класса также совпадает с именем компонента:

    require('./Header.styl')

    class Header extends React.PureComponent {
        render() {
            return (
                <div className="Header">
                    ...
                </div>
            );
        }

    }

Если нам нужно разделить css-файл на несколько файлов для удобства, то используем
суффиксы через точку:

    Header.styl
    Header.colors.styl
    Header.layout.styl

И в основном css-файле импортим их:

    @import "Header.colors.styl"
    @import "Header.layout.styl"

    .Header
        ...

При этом мы разбиваем на файлы не для того, чтобы сэкономить байтиков,
собирая "только нужное", нет. Нет смысла усложнять сборку, чтобы не собирать
в бандл лишних 100 байт.


## Префиксы имен компонентов

Часто компоненты относятся к какому-то куску сервиса или странице. Но при этом не являются "элементами"
у какого-то одного компонента. В этом случае даем им всем одинаковый префикс-неймспейс:

    ListingItem
    ListingForm
    ...

При этом компонента `Listing` может и вовсе не быть.
Нужно все это, чтобы не путаться, а что это за `Item`, к чему он относится.
И чтобы различать `ListingItem` и `MotoListingItem` (тут префиксом будет `MotoListing`) и т.д.

**Важно**. Мы не создаем папки для просто группировки. Например, вот так не нужно делать:

    Listing             <- не компонент
        ListingItem     <- не элемент компонента Listing
        ListingForm     <- не элемент компонента Listing

Либо это элементы, либо компоненты, никаких группировок.


## Компоненты-элементы

Иногда большой компонент нужно разбить на несколько подкомпонентов.
Причем эти подкомпоненты не могут ни при каких обстоятельствах быть использованы вне этого компонента.
В bem-терминологии это элементы.

Тут нужно понимать, что нет очень четкой границы между настоящими элементами и блоками.
Например, `ListingItem` мог бы быть элементом блока `Listing`. С другой стороны, `ListingItem`
мог бы в теории использоваться и внутри `MotoListingItem`, тогда лучше сделать его полноценным блоком.
Но даже если `ListingItem` никогда не используется вне `Listing` могут быть причины сделать его блоком,
а не элементом. Например, это очень большой и сложный компонент и проще держать его отдельно.

В целом посыл такой: мы не хотим загромождать основную папку с компонентами всеми мелкими подкомпонентами,
поэтому складываем их внутри папки с родительским компонентом. При необходимости может сделать элемент
самостоятельным блоком, если он начинает использовать где-то еще.

В отличие от bem мы не ограничиваем уровень вложенности двумя — у элементов могут быть свои элементы.
Но без фанатизма, конечно. Каждый уровень вложенности должен быть как-то оправдан.

Элементы устроены почти так же, как и обычные компоненты. Их название всегда начинается
с названия родительского компонента (блока).
В остальном они ничем не отличаются от компонентов. Они тоже лежат в папке,
имя которой совпадает с полным именем элемента, стилевой файл именуется так же
(если он есть, в принципе, можно стили для элемента хранить в родительском стилевом файле,
если их немного и вообще это удобнее).

    Header
        HeaderMenu
            HeaderMenu.js
            HeaderMenu.styl
        HeaderMenuItem
            HeaderMenuItem.js
        Header.js
        Header.styl

Внутри `Header.js` мы подключаем элементы используя относительные пути (???):

    //  Header.js

    require('./Header.styl');

    //  Элементы.
    const HeaderMenu = require('./HeaderMenu');
    const HeaderMenuItem = require('./HeaderMenuItem');

    //  Компоненты.
    const Dropdown = require('./Dropdown');

В `HeaderMenu.js` мы подключаем стили этого элемента. css-классы опять-таки
всегда именуются так же, как называется сам элемент:

    //  Header/HeaderMenu/HeaderMenu.js

    require('./HeaderMenu.styl');

    class HeaderMenu extends React.PureComponent {
        render() {
            return (
                <div className="HeaderMenu">
                    <div className="HeaderMenu__wrapper">
                        ...
                    </div>
                </div>
        }

    }

CSS-классы всегда пишем полностью. Не нужно, например, делать вот так:

    const base = 'Header';

        ...
        <div className={ `${ base }__wrapper` }>
            ...
        </div>

Это облегчает использование grep'а.

В этом примере `HeaderMenuItem` в теории мог бы быть элементом элемента `HeaderMenu`,
если он не используется вне `HeaderMenu`. Но это не очень оправдано. У нас нет десятков
и сотен элементов внутри `Header`, нет проблемы положить все на один уровень — так нагляднее.
В общем не нужно усложнять иерархию элементов без реальной необходимости.

Кажется, что часто удобнее все стили элементов хранить в основном файле:

    //  Header.styl

        .Header
            ...

            &Menu
                ...

                &Item
                    ...

С другой стороны, опять же удобнее грепать по `.styl` файлам и находить `.HeaderMenu`.
(???) — надо подумать.


## Публичные элементы

Как правило элементы — приватны. Их нужно использовать только внутри соответствующего компонента.
Но. Бывает так, что они при этом используются не в коде этого компонента, а где-то еще:

    //  Header.js

    const Dropdown = require('components/Dropdown');
    const DropdownSwitcher = require('components/Dropdown/DropdownSwitcher');
    const DropdownMenu = require('components/Dropdown/DropdownMenu');

    render() {
        return (
            ...
            <Dropdown className="HeaderNavigationItem">
                <DropdownSwitcher>
                    <HeaderMenuTitle url="/">Легковые</HeaderMenuTitle>
                </DropdownSwitcher>
                <DropdownMenu className="HeaderMenuItems">
                    <HeaderMenuItem url="/">С пробегом</HeaderMenuItem>
                    <HeaderMenuItem url="/">Новые</HeaderMenuItem>
                    <HeaderMenuItem url="/">Каталог</HeaderMenuItem>
                    <HeaderMenuItem url="/">Дилеры</HeaderMenuItem>
                </DropdownMenu>
            </Dropdown>
            ...
        );
    }

Здесь у компонента `Dropdown` есть два элемента: `DropdownSwitcher` и `DropdownMenu`.
Но они публичные, чтобы создать `Dropdown` в шапке, мы явно используем эти элементы.
(хорошо бы было использовать неймспейсы: `Dropdown.Switcher` — но увы, jsx не поддерживает это)


## BEM-нотация в CSS-классах
см. [css.md](./css.md)

## Специальные случаи

### Страницы

Верхние компоненты для страниц именуются `Page<RouteName>`. Т.о. все страницы лежат в одном месте и их легко найти.

### Иконки

(нужно дописать, я не помню точно)

Мы решили, что bem-нотацию для модификаторов в этом случае не используем.
Делаем базовый класс `Icon` в `components/Icon`, а сами иконки группируем в папку `components/icons`
(не `Icons`!). И уже внутри нее определяем конкретные иконки:

    Icon
        Icon.js
    icons
        IconPlus
            IconPlus.js
        IconMinus
            IconMinus.js
        ...
        index.js

В `icons/index.js` (это не компонент, так что имя этого файла `index.js`)
можем сделать (если нужно) оглавление:

    //  icons/index.js

    module.exports = {
        IconPlus: require('./IconPlus'),
        IconMinus: require('./IconMinus'),
        ...

    };

## Селекторы

Селекторы называются по схеме `domainName% + %fileName%`.
Например:
```
const bunkerGetNode = require('auto-core/react/dataDomain/bunker/selectors/getNode');
const userGetId = require('auto-core/react/dataDomain/user/selectors/getId').default;
```
