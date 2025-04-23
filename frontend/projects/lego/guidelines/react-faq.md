# React FAQ

Рубрика AMA с разработчиками Лего относительно React.

### Это замена текущему Лего?

Нет и еще раз нет. React в Лего  одна из технологий, реализующих блок, наравне с CSS, `i-bem`, тестами и тд. Мы считаем, что должна быть возможность использовать Лего в разных технологических стеках: именно поэтому мы занимаемся развитием React в рамках Лего. Это поможет проектам перестать создавать многочисленные клоны библиотек и думать о поддержке консистентности своих компонентов на React, а вместо этого полностью положиться на команду Лего.

### Как это работает?

Как известно, Лего и большинство сервисов в Яндексе построены согласно БЭМ-методологии, которая затрагивает не только именование селекторов в CSS, но и написание клиентского JS. Кроме того, мы используем уровни переопределения для решения разного рода задач: дифференцирования кода по платформам, проведения экспериментов, "подкладывания соломки" и тд. Этого бы нам хотелось и в работе с React — библиотека [bem-react-core](https://github.com/bem/bem-react-core) дает нам такую возможность. Библиотека реализует способ декларации React-компонентов в виде БЭМ-сущностей и позволяет доопределять их так же гибко, как в `i-bem`, а кроме того, поддерживает уровни переопределения. При этом `bem-react-core` не привносит ничего нового в сам React. Подробно почитать о том, как устроена библиотека `bem-react-core`, можно [здесь](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/guidelines/bem-react-core.md). Скоро эта документация появится и в Open Source. Мы пишем JS на чистом React без каких-либо кастомных надстроек или костылей, в соответствии с последним стандартом ES2015. Перед тем как начать разрабатывать компоненты, мы решили, что не будем насильно транслировать наружу БЭМ-методологию, уровни переопределения или требования к сборке. Поэтому мы спроектировали и проектируем API компонентов так, чтобы они ничем не отличались от любых других привычных компонентов в Open Source. Мы инкапсулировали всё про БЭМ внутри самих компонентов. У них абсолютно плоское API без модификаторов, миксов и прочего. Только нативный механизм пропсов и ничего больше.

### Там есть уровни переопределения?

Да, есть. Но по многочисленным просьбам мы предоставили возможность их не использовать. React в Лего поставляется в двух вариантах: основном, где есть уровни переопределения, и в дистрибуционном пакете `lego-on-react`, где нет ничего ни про уровни, ни про БЭМ-методологию.

### Вы переписали весь код?

Можно сказать и так. Мы повторно используем CSS и реализацию методов различных расчетов, выраженных в `VanillaJS`. Остальной код написан с нуля. Текущая реализация представляет из себя пересечение кода `BEMHTML`-шаблонов и JS на `i-bem`, но выражается в терминах React.

### Там `BEMHTML` внутри?

До недавнего времени это действительно было так. Мы разработали движок для [bem-xjst](https://github.com/bem/bem-xjst), который наравне c `BEMHTML` мог превращать шаблоны в Virtual DOM. Об этом рассказывалось, например, на [Я.Субботнике](https://events.yandex.ru/lib/talks/3687/). Мы выдвинули и даже математически доказали гипотезу об эффективности этого метода, поскольку он позволял в 10 раз ускориться на сервере относительно нативного рендеринга на React. К сожалению, мы не учли несколько нюансов, и как мы ни пытались их обойти, сделать это эффективно у нас не получилось. Как раз вовремя подоспела рабочая версия `bem-react-core` ‒ за что огромное спасибо @veged, @narqo и @dfilatov. Текущая реализация компонентов не содержит ни шаблонов на `BEMHTHML`, ни самого `bem-xjst`.

### А как же серверный рендеринг?

Сейчас рекомендуется использовать нативный серверный рендеринг React. Пока у нас не стоит задачи сильно его ускорить, но все в ваших руках.

### Там что, `i-bem` внутри?

Нет. Это не похоже на известные имплементации компонентов Лего в виде связи методов React и `i-bem`. Весь код написан с нуля, и там в принципе нет ничего лишнего либо ненужного.

### А можно один компонент?

Конечно можно. Все компоненты, как и блоки, разрабатываются и поставляются независимо. Естественно, мы подумали о коде, который будет приезжать на клиент после сборки. Один компонент из общего списка можно использовать следующим образом:

``` js
import {Link} from 'lego-on-react';
// Эквивалентный способ
import Link from 'lego-on-react/link';
```

### Что с поддержкой?

Поддержка реализуется наравне с поддержкой основных блоков Лего. В той же очереди [Startrek](https://st.yandex-team.ru/ISL), в том же канале `#support` [Slack](lego-team.slack.com), в той же рассылке lego@ и, что важно, той же командой в штатном режиме.

### Когда релизы?

Как известно, Лего выпускает минорные версии раз в 2 недели. Патчи могут выходить гораздо чаще. Мажоры ‒ раз в полгода. Ровно так же будет выпускаться и реализация на React.

### Что с тестами?

Всё хорошо. Мы тестируем как верстку компонентов, так и результат шаблонизации разных движков. Также мы [работаем](https://st.yandex-team.ru/ISL-3087) над универсальным фреймворком тестирования, который позволит нам писать общие тесты и на React API, и на `i-bem`. Кроме того, в команде Лего есть тестировщик @spiker, который тестирует все компоненты вручную. В качестве бонуса мы работаем над привлечением асессоров для тестирования всех компонентов Лего.

### Что с примерами?

Примеры для React-компонентов лежат рядом с примерами основных блоков Лего в директориях `*.examples/**/react`. Скоро они станут доступны на основном [сайте Лего](lego.yandex-team.ru). Локально примеры можно собрать одной командой `npm run react-hot-examples`. Примеры будут собираться наравне с основными, в том числе в Teamcity.

### Что с документацией?

Мы работаем над этим. На данный момент мы готовы оказывать персональные консультации по любым вопросам интеграции и использования Лего на React. Документация будет реализована рядом с основной в виде описание API и инлайновых примеров.

### Можно ли использовать в виджетах?

Можно. Есть определенный класс разработки в виде встраиваемых виджетов на страницу, и React — хороший кандидат для реализации. Изоляцию стилей можно обеспечить использованием [CSS-модулей](https://github.com/css-modules/css-modules).

### Может ещё и i18n есть?

Есть. Мы как никто другой понимаем, что сервисы Яндекса работают в других странах. React-реализация должна удовлетворять этому требованию. Следить за прогрессом разработки технологии i18n можно [здесь](https://st.yandex-team.ru/ISL-3078).

### Как собирать на проекте?

Мы собираем React-компоненты с помощью Webpack, но не навязываем этот способ. Дистрибуционный пакет `lego-on-react` может собираться любым известным (или не очень) сборщиком. Если вы хотите (а мы верим, что вы хотите) использовать уровни переопределения и БЭМ-декларации для React на своем проекте, вы можете воспользоваться [лоадером](https://github.com/bem/webpack-bem-loader) для Webpack или таким же [плагином](https://github.com/bem/babel-plugin-bem-import) для Babel в сочетании с любым сборщиком. Оба этих решения реализуют обход уровней с целью поиска наличия деклараций, обеспечивают автоматическое подключение JS и CSS, а также работают с особенным синтаксисом импортов.

### Что за особенные импорты?

Это специальный синтаксис импортов, который позволяет подключать React-компоненты в виде БЭМ-сущностей. Вся магия в том, что подключенная сущность будет обладать ровно тем набором свойств, что описаны в декларациях на уровнях переопределения. Выглядит это примерно так:

``` js
import Block from 'b:block';
import BlockWithMod from 'b:block m:modName';
import BlockWithManyMods from 'b:block m:modName=modVal1|modVal2';
import BlockElem from 'b:block e:elem';
import BlockElemWithMod from 'b:block e:elem m:modName';
import BlockElemWithManyMods from 'b:block e:elem m:modName=modVal1|modVal2';
```

Подробное описание синтаксиса импортов находится [здесь](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/guidelines/bem-react-import.md) и скоро появится в Open Source.

### А что с описанием зависимостей, надо писать?

Привычный механизм декларации зависимостей отсутствует полностью. Он реализуется автоматически.

### Зачем плагин и для Webpack, и для Babel?

Может показаться, что они делают одно и тоже. Так оно и есть. Разница заключается в следующем: плагин для Webpack позволяет во время работы сборщика добрасывать сущности, которых на файловой системе пока еще нет. Но когда они появятся, Webpack доставит их код без перезагрузки. Плагин для Babel так сделать не может, поскольку не следит за файловой системой и выполняет анализ только во время старта. Это значит, что когда вы создадите новый CSS-файл, придется перезапустить сборку, чтобы он попал в бандл. Однако важно отметить, что плагин для Babel позволяет использовать особый синтаксис импортов в серверном коде и тестах. Мы работаем над интеграцией двух решений, и в конечном счёте Webpack плагин будет предоставлять только горячую дозагрузку, а все задачи по обходу уровней и парсингу импортов будет выполнять Babel.

### Есть Starter Kit?

Конечно, есть, и там можно посмотреть, как настраивается сборка и используются блоки Лего. Мы сделали 2 варианта: простой и очень простой. Во-первых, мы сделали [обычный репозиторий](https://github.yandex-team.ru/lego/lego-on-react-stub), где все настроено. Во-вторых, [мы готовим свою реализацию](https://github.yandex-team.ru/lego/create-react-app-on-lego) популярного `create-react-app`, чтобы этим могли пользоваться и дизайнеры в том числе. В основной ветке используется дистрибуционный пакет `lego-on-react`, а настройки с использованием уровней и БЭМ-деклараций находятся в ветке `bem`.

### Как следить за разработкой?

Специально для всех неравнодушных мы сделали два фильтра по задачам в Startrek:

- [что уже сделано](https://st.yandex-team.ru/filters/filter?query=KEY%3AISL-2851%2CISL-2865%2CISL-2866%2CISL-2867%2CISL-2869%2CISL-2870%2CISL-2871%2CISL-2872%2CISL-2952%2CISL-2953%2CISL-3230%2CISL-3231%2CISL-3297%2CISL-3309%2CISL-3346%2CISL-3347%2CISL-3350%2CISL-3352%2CISL-3409%2CISL-3413)
- [что уже запланировано](https://st.yandex-team.ru/filters/filter?query=KEY%3AISL-2873%2CISL-2874%2CISL-2875%2CISL-2876%2CISL-3291%2CISL-3331%2CISL-3342%2CISL-3345%2CISL-3348%2CISL-3353%2CISL-3399%2CISL-3415%2CISL-3424%2CISL-3432%2CISL-3433%2CISL-3434%2CISL-3452%2CISL-3453%2CISL-3455%2CISL-3456)

На текущий момент готовы блоки:

- Button - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/button2/button2.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/button2/button2.examples/index.react.js)
- CheckBox - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/checkbox/checkbox.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/checkbox/checkbox.examples/index.react.js)
- Dropdown - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/dropdown2/dropdown2.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/dropdown2/dropdown2.examples/index.react.js)
- Font - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/i-font/i-font.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/i-font/i-font.examples/index.react.js)
- Icon - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/icon/icon.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/icon/icon.examples/index.react.js)
- Image - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/image/image.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/image/image.examples/index.react.js)
- Link - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/link/link.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/link/link.examples/index.react.js)
- Logo - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/logo/logo.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/logo/logo.examples/index.react.js)
- Menu - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/menu/menu.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/menu/menu.examples/index.react.js)
- Modal - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/modal/modal.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/modal/modal.examples/index.react.js)
- Popup - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/popup2/popup2.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/popup2/popup2.examples/index.react.js)
- RadioButton - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/radio-button/radio-button.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/radio-button/radio-button.examples/index.react.js)
- RadioBox - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/radiobox/radiobox.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/radiobox/radiobox.examples/index.react.js)
- Select - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/select2/select2.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/select2/select2.examples/index.react.js)
- ServiceIcon - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/service-icon/service-icon.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/service-icon/service-icon.examples/index.react.js)
- Spin - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/spin2/spin2.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/spin2/spin2.examples/index.react.js)
- TextInput - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/textinput/textinput.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/textinput/textinput.examples/index.react.js)
- Tumbler - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/tumbler/tumbler.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/tumbler/tumbler.examples/index.react.js)
- UserAccount - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/user-account/user-account.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/user-account/user-account.examples/index.react.js)
- UserPic - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/user-pic/user-pic.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/user-pic/user-pic.examples/index.react.js)
- User - [описание](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/user2/user2.ru.md) и [примеры](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/user2/user2.examples/index.react.js)

### Какие сроки?

Мы планируем закончить все основные блоки, необходимые для разработки сервисов, до следующего ревью. У вас все еще есть время повлиять на состав работ. Но самое главное — уже можно начинать планирование по внедрению Лего на своем сервисе.

### Куда писать про ошибки?

Как обычно в рассылку lego@, создавать задачи в очереди [Startrek](https://st.yandex-team.ru/ISL), кричать в канале `#support` [Slack](lego-team.slack.com) или лично @grape.

### Что-то я вам не доверяю...

Приходи к нам лично или пиши, мы всегда рады обсудить любые штуки и обязательно пойдем тебе навстречу ;)
