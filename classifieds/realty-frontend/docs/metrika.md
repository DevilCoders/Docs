# Работа с целями метрики

## Инициализация
Для того чтобы функция `reachGoal` отправляла цели, нужно инициализировать метрику на странице с помощью вызова функции
`initializeMetrika`, передав в неё нужные параметры (эксперименты, параметры страницы и прочее).

Пример:
```javascript
import { initializeMetrika } from 'realty-core/view/common/libs/metrika';
import config from '../config';

initializeMetrika();
```

После инициализации можно использовать импортированную функцию `reachGoal`:
```javascript
import { reachGoal } from 'realty-core/view/common/libs/metrika';
...
reachGoal('button_click');
```
Если использовать её до инициализации, все цели складываются в кэш, который отправляется 
при инициализации.

## Именование цели

Создать новую цель можно по [инструкции](https://wiki.yandex-team.ru/users/emiliyamur/realty/allmetricas/metrika-events/)

## Использование
Можно вызывать функцию `reachGoal` с различными параметрами и с несколькими целями сразу:

```javascript
// одна цель без параметров
reachGoal('button_click');

// одна цель с параметрами
reachGoal('link_click', { color: 'red', location: 'header' });

// несколько целей без параметров
reachGoal([ 'goal1', 'goal2' ]);

// несколько целей с одинаковыми параметрами
reachGoal([ 'goal1', 'goal2' ], { common_param: 'yyy' });

// несколько целей с разными параметрами
reachGoal([
    [ 'goal1', { goal1Param: 'zzz' } ],
    [ 'goal2', { goal2Param: 'xxx' } ]
]);
```

## Препроцессинг параметров целей
Для чего: во многих случаях параметры цели извлекаются из различных объектов и логика их извлечения/обработки растекается по проекту.
Для частичного решения этой проблемы существует объект `{ название_цели: обработчик }`.
Он находится в `realty-core/view/common/libs/metrika/data-transformers/index.js`

При отправке цели с параметрами, функция `reachGoal` смотрит в этот объект, и если находит там название цели, то применяет
к переданным параметрам функцию, соответствующую этому ключу.

Пример:
```javascript
// 1. добавляем обработчик в data-transformers: 
// realty-core/view/common/libs/metrika/data-transformers/index.js
export default {
    my_goal_name: data1 => ({ param1: data1.zzz, param2: data1.yyy }),
    my_goal_name_2: data2 => ({ my_param1: data2.zzz, my_param2: data2.yyy })
}

// 2. вызываем функцию reachGoal с необработанными данными
import { reachGoal } from 'realty-core/view/common/libs/metrika';
...
reachGoal('my_goal_name', this.props.data);
reachGoal(['my_goal_name', 'my_goal_name_2'], this.props.data);
reachGoal([ [ 'my_goal_name', this.props.data1 ], [ 'my_goal_name_2', this.props.data2 ] ]);
...

// 3. цель отправляется с обработанными данными
```

## Location в цели метрики
Для этого есть HOC [withElementLocation](../realty-core/view/react/common/enhancers/withElementLocation.js).

Он представляет из себя обёртку для компонента, которая позволяет определять параметр `location` для его потомков
без необходимости прокидывать пропы вниз по цепочке через все элементы.
Работает через `React.createContext`.

### Для чего вообще нужен этот HOC
В параметры отправляемых целей метрики зачастую требуется передавать параметр location, обозначающий, откуда была,
например, нажата кнопка. Если в ряде случаев можно точно определить, где эта кнопка была нажата и записать этот параметр
руками, то в некоторых случаях, местоположение определяется только на этапе выполнения.

Пример: есть компонент сниппета оффера, который используется во многих местах (обычный листинг, листинг на карте, избранное, и т.д.)
и на этом компоненте есть кнопка "добавить в избранное", нажатие на которую нам нужно отследить, и отправить место,
где эта кнопка находится (листинг, листинг на карте, избранное).
Для того, чтобы такое провернуть, нужно идти вверх по дереву, найдя первый не переиспользуемый компонент (например, страница SearchPage)
и определить этот location там, после чего пробросить его через все компоненты до кнопки избранного.
Всё это выглядит так себе и трудно отлаживается.

Поэтому, это проще сделать через контекст, чтобы не прокидывать пропы через 10 компонентов и не проверять для каждого
location'a, не нарушается ли цепочка.

### Использование
1. Обернуть "определяющий" компонент в `withElementLocation({ location: 'my-location-name' })`
2. Обернуть компонент-потребитель этого `location` в `withElementLocation()`
3. Вызвать проп `getElementLocation()` в компоненте-потребителе, чтобы получить строку `'my-location-name'`

Можно также перезаписать `location` через переопределение ниже по дереву: тогда в компоненты-потребители пойдёт ближайший к
ним (по дереву) `location`.
Например:
```javascript
import OfferPage from '...';
import OfferCard from '...';
import FavoriteButton from '...';

const EnhancedOfferPage = withElementLocation({ location: 'page_offer' });
const EnhancedFavoriteButton = withElementLocation();

pseudoRender(
    <EnhancedOfferPage>
        <OfferCard>
            <EnhancedFavoriteButton />
        </OfferCard>
    </EnhancedOfferPage>
)
// в коде выше, если getElementLocation() вызвать внутри EnhancedFavoriteButton, то вернётся строка 'page_offer'
```

Оверрайтим:
```javascript
const EnhancedOfferPage = withElementLocation({ location: 'page_offer' });
const EnhancedOfferCard = withElementLocation({ location: 'card_offer' }); // добавилась эта строка
const EnhancedFavoriteButton = withElementLocation();

pseudoRender(
    <EnhancedOfferPage>
        <EnhancedOfferCard>
            <EnhancedFavoriteButton />
        </EnhancedOfferCard>
    </EnhancedOfferPage>
)
// в этом коде, при вызове getElementLocation() внутри EnhancedFavoriteButton, вернётся строка 'card_offer'

```
