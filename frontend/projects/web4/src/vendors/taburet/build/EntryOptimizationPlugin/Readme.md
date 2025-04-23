# EntryOptimizationPlugin

Плагин для вебпака, позволяющий уменьшить размер страницы путём удаления js-кода из сборки для неинтерактивных фич.

Такая необходимость возникает, так как вся верстка рендерится на сервере, а затем гидрируется на клиенте. Однако нам не всегда нужно гидрировать полученную верстку на клиенте. Если гидрации на клиенте нет, то и js статика нам не нужна, но нам все еще нужны стили и иногда какую то часть JS кода нам всё же необходимо оставить.

С точки зрения сборки webpackа, каждое entry выглядит как граф зависимостей:

![entry](https://jing.yandex-team.ru/files/kholstinin/entry.jpg)

После работы плагина, дерево начинает выглядеть так:

![optimized-entry](https://jing.yandex-team.ru/files/kholstinin/entry-optimized.jpg)

Мы вырезали все js модули и оставили только css и [vanilla](../../../vanillaInReact/README.md) файлы. 

К плагину прилагается лоадер, который размечает исходный код, для того чтобы плагин правильно удалил ненужные зависимости.

# Лоадер
Лоадер вызывается вебпаком на этапе чтения js файлов и обрабатывает только файлы размеченные директивой '@enable-entry-optimizer'. 

Лоадер строит AST дерево файла, после чего находит компоненты/функции которые используются внутри зарезервированных функций (в нашем случае это `withHydration` и `createComponentsExperiment`) и фильтрует все импорты/объявления переменных в файле.

Если импорт не используется в зарезервированных функциях, то он размечается специальной директивой `@entry-optimizer-import` и обрабатывается отдельно на этапе парсинга файла.

Если объявление не используется в зарезервированных функциях, то оно просто вырезается.

Если в файле нет зарезервированных слов, тогда файл состоит лишь из размеченных директивой импортов.

По сути лоадер превращает вот такой код entry:

```js
'@enable-entry-optimizer';

import { withRegistry } from '@bem-react/di';
import { organicTextRegistry } from '../OrganicText.registry/desktop';
import { OrganicText } from '../OrganicText@desktop';

export const App = withRegistry(organicTextRegistry)(OrganicText);
```

Вот в такой

```js
'@entry-optimizer-import @bem-react/di';
'@entry-optimizer-import ../OrganicText.registry/touch-phone';
'@entry-optimizer-import ../OrganicText@touch-phone';
```

Или в случае если фичу нужно частично гидрировать:

```js
'@enable-entry-optimizer';
import { createSubRoot } from '../../../../components/Root/Root@touch-phone';
import { PeoplesCardsWithFeatures } from '../../YdoWizard.components/PeoplesCardsWithFeatures/PeoplesCardsWithFeatures@touch-phone';
import { StaticMap } from '../../YdoWizard.components/StaticMap/StaticMap@touch-phone';

import '../YdoWizard_peopleServices@touch-phone';
import '../../../../components/SerpOrganic/SerpOrganic@touch-phone';

export const PeoplesCardsWithFeaturesRoot = createSubRoot('YdoWizard-PeoplesCardsWithFeatures', 'div', PeoplesCardsWithFeatures);
export const StaticMapRoot = createSubRoot('YdoWizard-StaticMapRoot', 'div', StaticMap);
```

Превращает в

```js
import { createSubRoot } from '../../../../components/Root/Root@touch-phone';
import { PeoplesCardsWithFeatures } from '../../YdoWizard.components/PeoplesCardsWithFeatures/PeoplesCardsWithFeatures@touch-phone';
import { StaticMap } from '../../YdoWizard.components/StaticMap/StaticMap@touch-phone';
'@entry-optimizer-import ../YdoWizard_peopleServices@touch-phone';
'@entry-optimizer-import ../../../../components/SerpOrganic/SerpOrganic@touch-phone';
export var PeoplesCardsWithFeaturesRoot = createSubRoot('YdoWizard-PeoplesCardsWithFeatures', 'div', PeoplesCardsWithFeatures);
export var StaticMapRoot = createSubRoot('YdoWizard-StaticMapRoot', 'div', StaticMap);
```

# Плагин

Плагин работает на нескольких этапах сборки:
1) На этапе парсинга js кода он находит ранее размеченые импорты `@entry-optimizer-import` и добавляет в граф зависимостей зависимость с новым типом - `OnlySideEffectDependency`.
2) На этапе оптимизации модулей, до того как из них чанки, плагин находит `OnlySideEffectDependecy` модули и проходясь по графу зависимостей собирает css и vanilla и добавляет их в entry как новую зависимость.

# Взаимодействие с пушмодулем

На серпе есть еще один механизм оптимизации скорости - [пушмодуль](../../../../components/PushModuleRenderer/README.md). Этот механизм позволяет выделить некоторые импорты в отдельные чанки и добавлять статику для них, только тогда, когда компонент реально присутствует на странице.

Однако для того чтобы это работало, entryOptimizer особым образом обрабатывает такие импорты.
EntryOptimizer не собирает css модули из пушмодуль импорта, а подклеивает к entry сами пушмодуль импорты и vanilla модули. После этого, модуль пушмодуля так же оптимизируется и у него убирается весь js код, оставляя в этом чанке только css.

Entry с пушмодулем:

![pushModule-entry](https://jing.yandex-team.ru/files/kholstinin/entry%20pushmodule.jpg)

После работы плагина:

![optimized-pushModule-entry](https://jing.yandex-team.ru/files/kholstinin/optimized%20entry%20pushmodule.jpg)
