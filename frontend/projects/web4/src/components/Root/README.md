# Root

## withHydration

Если вся фича — единый интерактивный компонент, например [переводчик](https://yandex.ru/search/?text=%D0%BA%D0%BE%D0%B4%20%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4), то корневой компонент фичи целиком заворачивается в `withHydration`. Корневой компонент в этом случае называется "рутом".

`withHydration` — изоморфный хелпер, который при серверной шаблонизации рендерит компонент в html, записывая его пропсы в data-атрибут, а на клиенте гидрирует (инициализирует) компонент:

![Схема работы](https://jing.yandex-team.ru/files/vttly/react-createApp.png)

## createSubRoot

Если интерактивной является только часть результата, то "рутом" можно сделать только часть, но называться она будет "мини-рутом". Рассмотрим пример, в котором мини-рутом будет компонент `Extralinks` - контекстное меню обычного органического сниппета (будем заворачивать его в `createSubRoot`). Сам органический сниппет гидрироваться не будет, и данные для него не будут отправлены на клиента.

1. В entry-файле импортируем сам компонент и делаем из него мини-рут
2. Мини-рут ExtralinksRoot складываем в реестр органики, заменяя обычный Extralinks

```ts
import { createSubRoot } from '@components/Root/Root';
import { Extralinks } from '@components/Extralinks/Extralinks@desktop';
import { cnSerpOrganic } from '@components/SerpOrganic/SerpOrganic.const';

// Создаем мини-рут
const ExtralinksRoot = createSubRoot('Extralinks', 'span', Extralinks);

// Складываем мини-рут в реестр органики
const organicRegistry = new Registry({ id: cnSerpOrganic() }).set('Extralinks', ExtralinksRoot);

export const App = withRegistry(organicRegistry)(FeatureComponent);
```

Подход с мини-рутами избавляет нас от отправки лишних данных и от гидрации статичных компонентов, но js-статичных компонентов по прежнему будет отправлять на клиента. Чтобы при сборке следует вырезать лишнюю статику, в entry-файл добавляем директиву `'@enable-entry-optimizer'` (см. плагин [EntryOptimizationPlugin](../../vendors/taburet/build/EntryOptimizationPlugin)).

В проекте есть [пример использования createSubRoot](../../experiments/learn_partial_hydration/features/Time).

## FAQ

### Почему не стоит передавать react-компоненты в пропсах

В компонент, который будет гидрироваться на клиенте, не стоит передавать react-компоненты в пропсах (такие как `children`), так как это очень сильно раздувает размер html.
Вся иерархия компонентов помещается в data-state, что плохо влияет на размер страницы.
Лучше обернуть всю фичу в компонент, а в него передавать только данные для формирования фичи.

### Можно вообще ничего не гидрировать на клиенте?

Необходимо убрать все `withHydration`/`createSubRoot` из entry-файла и добавить директиву `'@enable-entry-optimizer'`

### Почему enable-entry-optimizer может вырезать не все?

Алгоритм оптимизации вырезает все зависимости entry-файла, которые не используются в `withHydration`/`createSubRoot`, все что используется — вырезано не будет. Кроме прямых зависимостей оцениваются транзитивные, это может приводить к неочевидным последствиям. Например, если вы будете править реестр (как в примере правился реестра органики), то все зависимости из этого реестра по умолчанию будут доставлены на клиента. Чтобы не привозить лишнего, но сохранить возможность замены компонентов в реестре, можно разбить один реестр на несколько. И дальше работать с меньшими по размеру реестрами.

### Что делать, если мини-рут не гидрируется?

Особенностью плагина `EntryOptimizationPlugin` является обязательное сохранение мини-рута в переменную перед добавлением его в реестр. Поэтому сейчас при подобной записи гидрация мини-рута не сработает:

```ts
'@enable-entry-optimizer';

featureRegistry.set(
    'Scroller',
    createSubRoot('Scroller', 'div', withStaticChildren(Scroller))
);
```

Чтобы гидрация отработала, перед добавлением мини-рута в реестр сохраните его в переменную:

```ts
'@enable-entry-optimizer';

const ScrollerRoot = createSubRoot('Scroller', 'div', withStaticChildren(Scroller));
featureRegistry.set('Scroller', ScrollerRoot);
```

Это действие станет необязательным после выполнения [SERP-107151](https://st.yandex-team.ru/SERP-107151).
