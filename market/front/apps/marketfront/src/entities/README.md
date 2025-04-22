# entities

В этой директории хранятся описания сущностей, которыми мы оперируем в коде.

Также стоит ознакомиться с общими соглашениями:
[https://wiki.yandex-team.ru/market/frontend/conventions](https://wiki.yandex-team.ru/market/frontend/conventions)

## Файловая структура

Каждая сущность лежит в директории с именем в camelCase в единственном числе. В каждой такой директории могут быть следующие файлы:

### `index`

В `index.js` лежит Flow-тип сущности и вспомогательные типы.

Стоит отдельно объявить тип поля `id`, и мы не используем `opaque` для него.

Подход к именованию типов, где `SomeEntity` - это название сущности:
  * `SomeEntityCollection` - тип нормализованной коллекции;
  * `SomeEntityCollections` - тип для описания коллекции как части стейта в виджете;
  * `SomeEntityState` - тип стейта с коллекцией сущности для доступа из контейнеров;
  * `SomeEntityDenormalized` или `SomeEntityRaw` - денормализованный тип, ожидаемый в схеме, который приходит с бэкэнда;
Для создания коллекций используем тип-хелпер `Collection` из `@yandex-market/entity`, если ключом в коллекции является поле `id`


```(javascript)
// описание entity:
// @self/root/src/entities/someEntity/index.js
import type {Collection} from '@yandex-market/entities';

type SomeEntityId = number;
export type SomeEntity = {
    entity: 'someEntity',
    id: SomeEntityId,
    otherId: OtherEntityId,
    ...,
};

export type SomeEntityRaw = {
    ...$Exact<SomeEntity>,
    other: OtherEntity,
};

export type SomeEntityCollection = Collection<SomeEntity>;
export type SomeEntityCollections = {
    someEntity: SomeEntityCollection,
};
export type SomeEntityState = {
    collections: SomeEntityCollections,
};
```

Таким образом тип `Collections` в апиаривском виджете описывается пересечением типов `*Collections` из `@self/root/src/entities`
```(javascript)
// использование в виджете:
// @self/root/src/widgets/content/MyWidget/index.js
import {type SomeEntityCollections} from '@self/root/src/entities/someEntity';
import {type OtherEntityCollections} from '@self/root/src/entities/otherEntity';

type Collections = SomeEntityCollections & OtherEntityCollections;
```

```(javascript)
// использование в контейнере:
// @self/root/src/containers/MyContainer/index.js
import {type SomeEntityState} from '@self/root/src/entities/someEntity';

const mapStateToProps = (state: SomeEntityState) => ...
```

### `constants`

Релевантные константы :)

### `getters`

Геттеры - это набор функций, агрегирующих информацию о сущности, без использования стейта приложения.
Предпочтительнее каждый геттер делать отдельным атомарным модулем, а в файле index.js их реэкспортить. Для селекторов и хелперов эта логика тоже применима.
В `entities` не стоит использовать `createSelector` или делать методы типа `getPropsForView`, так как такие вещи относятся не к сущностям, а к представлению.

```(javascript)
// описание entity:
// @self/root/src/entities/someEntity/getters/getSomeField.js
import type {SomeEntity} from '..';

const getSomeField = (someEntity: SomeEntity) => someEntity.someField;

export default getSomeField;
```

```(javascript)
// @self/root/src/entities/someEntity/getters/index.js
export {default as getSomeField} from './getSomeField';
```

#### Null-safe геттеры - это зло.
Геттеры не должны быть null-safe. Пишите типы, чтобы знать когда может вернуться `undefined`. Делайте проверки перед тем, как применить геттер.

Null-safe геттеры усложняют отладку.

> Egor Bykhovtsev, [19.07.2022 13:52]
> НИКОГДА НЕ ИСПОЛЬЗУЙТЕ ВО ВЬЮ NULL_SAFE
>
> Egor Bykhovtsev, [19.07.2022 13:52]
> Это адище потом не отдебажить. Пишите код так, чтобы было понятно, к чему он готов, а к чему нет
>
> Egor Bykhovtsev, [19.07.2022 14:15]
> Короче, рассказываю, как оно выходит, когда везде поголовный null-safe
>
> 1. Если ты берёшь поле от undefined, то с вероятность 95% это уже ошибка по логике. Скорей всего ты не хотел так делать, и ожидал наличие объекта, но вот его нет, и теперь пользователь кекает с Мы вам доставим UNDEFINED в UNDEFINED в интервале UNDEFINED-UNDEFINED
>
> 2. С такого почему-то не кекают продуктологи и QA. На тебя заводят тикет на починку. Всё "смешнее", если виджет вообще упал и не появляется на странице. Особенно "весело", когда виджет так делает иногда. Т.е. обычно есть, но иногда пропадает и тикет как раз об этом
>
> 3. Ты идешь дебажить, и, допустим, быстро обнаруживаешь offer.price, у которого offer == null в моменте. "Ха, всего-то сделать проверку на наличие offer" - думаешь ты. ХРЕНА ТАМ ЛЫСОГО. offer стал  null-ом, потому что выше селектор вернул null. А селектор не простой (selectById), а золотой (selectBestFashionOfferByShadyParamsExpAndCucmberPower). Ты начинаешь смотреть, откуда null берется там, а там 30 строк и в каждой null-safe функция, которая успешно проглотила null и выплюнула null на выход. Какая падла первой выкинула null по нормальным данным ты не знаешь, и ты вынужден разбирать каждую, блин, функцию потому что нету у тебя в тестинге offer-ов  с cucumberPower, поэтому сиди и разбирайся по коду

### `helpers`

Хелперы - это почти как геттеры, но только они могут принимать какие-то дополнительные аргументы помимо самой сущности.

### `selectors`

Селекторы - набор функций, агрегирующих информацию о сущности, обращаясь при этом к стейту приложения..

```(javascript)
// описание entity:
// @self/root/src/entities/someEntity/selectors/selectById.js
import type {SomeEntityState, SomeEntityId} from '..';

const selectById = (state: SomeEntityState, {someEntityId}: {someEntityId: SomeEntityId}) =>
    state.collections.someEntity[someEntityId];

export default selectById;
```

```(javascript)
// @self/root/src/entities/someEntity/selectors/index.js
export {default as selectById} from './selectById';
```

### `reducer`

Редьюсер - это метод, который обновляет коллекцию в зависимости от экшенов.
Важно, что на одну коллекцию может быть только один редьюсер, поэтому они объявлены рядом с сущностями.
Если нет необходимости обновлять коллекцию по каким-то кастомным экшенам, то следует использовать стандартный `EMPTY_REDUCER`. А стейт в свою очередь обновлять экшеном `updateCollections` из апиари.

### `schema`

В schema описывается единственная схема для сущности. Если есть необходимость создать новую схему, значит это будет уже другая сущность, и для нее нужно создавать отдельную директорию.
Внутри схемы стоит делать преобразования к "каноническому" виду сущности, который зафиксирован как флоу-тип в index.js.
**Важно** обратить внимание на использование внешних схем. Их стоит использовать только если внутри сущности `SomeEntity` действительно приходит другая сущность `OtherEntity`.
А если в денормализованном виде приходит только айдишник, то лучше в `processStrategy` явно его положить в поле типа `OtherEntityId`.
Или если внутренняя сущность не существует без внешней (например фото), то лучше её оставить внутри и не выносить в отдельную коллекцию.

### `__mock__/someEntity.mock.js`

Типизированный криэйтор моков сущности, который удобно использовать в юнит-тестах.

## Как мы описываем сущности

1. Сущности, имеющие однозначный идентификатор, должны быть нормализованы

   **Плохо:**
   ```flow js
   export type Outlet = {
      // Данные об одинаковых регионах повторяются в каждой сущности `Outlet`.
      region: {
        id: '...',
        name: '...',
        // ...
      },
   };
   ```

   **Хорошо:**
   ```flow js
   import type {RegionId} from '@self/root/src/entities/region';

   export type Outlet = {
      // ...

      // От сущности региона остался только идентификатор,
      // по которому мы можем получить из state'а нужный регион.
      regionId: RegionId,

      // ...
   };
   ```

   Всегда стоит иметь в виду возможность выделения некоторой части полей сущности в отдельную сущность.

   **Причины:**
   https://groups.google.com/forum/#!topic/reactjs/jbh50-GJxpg

   ---

1. Сущность не должна содержать лишних данных

   **Плохо:**
   ```flow js
   export type Offer = {
      id: '...',
      // На фронте никак не используется
      classifierMagicId: string,
      meta: {
           recommendationSource: 'formula' | 'shop',
      },
      // ...
   };
   ```

   **Хорошо:**
   Описывать минимальный набор необходимых полей сущности. От бэкенда приходит 47 полей в объекте? Выдели только те, что будешь использовать и опиши их в сущности.

   **Причины:**
   Лишняя информация затрудняет чтение кода, приводит к возникновению сомнений ("а точно ли это поле мне нужно использовать?")

   ---

1. Сущность должна быть полной

   **Плохо:**
   ```flow js
   export type Order = {
     // ...
     // Чтобы компонент смог отрендерить цену, нужна связка из двух вещей:
     // значение цены (`value`) и валюта (`currency`).
     priceBeforeDiscount: number,
     price: number,
     // ...
   };
   ```

   **Хорошо:**
   ```flow js
   import type {Price} from '@self/root/src/entities/price';

   export type Order = {
     // ...
     priceBeforeDiscount: Price,
     price: Price,
     // ...
   };
   ```

   **Причины:**
   Сущности с "неполным" набором данных сложно использовать. Например, для случая с неполным ценой постоянно приходится
   думать откуда "стащить" валюту для отображения.

   ---

1. Сущность должна использовать фронтовые бизнес-термины

   **Плохо:**
   ```flow js
   import type {RegionId} from '@self/root/src/entities/region';

   export type Outlet = {
      // ...
      // Репорт по техническим причинам в качестве названия идентификатора региона
      // использует термин `rids`.
      // Использование бекендами того или иного слова не является достаточным условием для того, чтобы это слово вошло в наш глоссарий.
      // При описании сущности Фронт должен преобразовывать (при нормализации) подобные
      // казусы к общефронтовым терминам, `rids` -> `regionId`.
      rids: RegionId,
      // ...
   };
   ```

   **Хорошо:**
   ```flow js
   import type {RegionId} from '@self/root/src/entities/region';

   export type Outlet = {
      // ...
      regionId: RegionId,
      // ...
   };
   ```

   **Причины:**
   В Яндекс.Маркете больше 20 бэкендов, которые не могут/не хотят договориться об общем формате предоставляемых данных.
   Внутри нашего приложения мы хотим использовать единые термины (так их проще поддерживать).

   ---

1. Сущность должна переиспользовать другие сущности

   **Плохо:**
   ```flow js
   export type Subscription = {
      // ...
      uid: number,
      regionId: number,
      // ...
   };
   ```


   **Хорошо:**
   ```flow js
   import type {Uid} from '@self/root/src/entities/user';
   import type {RegionId} from '@self/root/src/entities/region';

   export type Subscription = {
      // ...
      uid: Uid,
      regionId: RegionId
      // ...
   };
   ```

   **Причины:**
   Обновлять/изменять одну точку входа проще нескольких.

   ---

1. Названия полей сущности не должны быть избыточными

   Например, слово, использованное в имени сущности, скорее всего не должно попадаться в названии поля сущности.

   **Плохо:**
   ```flow js
   export type Subscription = {
      // ...
      subscriptionStatus: 'NEED_SEND_CONFIRMATION' | 'CONFIRMED',
      subscriptionType: 'ADVERTISING' | 'STORE_ADVERTISING',
      // ...
   };
   ```

   **Хорошо:**
   ```flow js
   export type Subscription = {
     // ...
     status: 'NEED_SEND_CONFIRMATION' | 'CONFIRMED',
     type: 'ADVERTISING' | 'STORE_ADVERTISING',
     // ...
   };
   ```

   ---

1. Если сущность имеет идентификатор, то он находится в поле .id

   **Плохо:**
   ```flow js
   export type WareMd5 = string;

   export type Offer = {
     // ...
     // По историческим причинам, идентификатор оффера в Репорте называется `wareMd5`
     WareMd5: WareId,
     // ...
   };
   ```

   **Хорошо:**
   ```flow js
   export type OfferId = string;

   export type Offer = {
     // ...
     // Преобразуем историческую неточность к общему виду:
     id: OfferId,
     // ...
   };
   ```

   ---

1. Сущность содержит только относящиеся к ней данные

   **Плохо:**
   ```flow js

   export type Price = {
     // ...
     // Бэкенд Репорт для удобства присылает признак "в стоимость включена доставка" вместе с ценой.
     // Если хранить в сущностях лишнюю информацию, то сущности становиться сложно переиспользовать.
     // Например, бэкенд `Чекаутер` присылает цену без каких-либо признаков доставки.
     isDeliveryIncluded: boolean,
     // ...
   };
   ```

   ---

1. Поля сущности должны быть максимально строгими

   **Плохо:**
   ```flow js

   export type Region = {
     //...
     // Бэкенды могут присылать одинаковые по смыслу сущности в разных форматах.
     id: number | string, // 213 | '213'
     // ...
   };
   ```

   **Хорошо:**
   ```flow js

   export type Region = {
     // ...
     id: number,
     // ...
   };
   ```

   **Причины:**
   Сущности с "размытыми" границами сложно использовать, поэтому на этапе нормализации
   Делаем сущность максимально строгой. number | string –> number.

   ---

1. Поля сущности должны иметь общеупотребимые названия

   **Плохо:**
   ```flow js

   export type User = {
     // ...
     // identificator: number,
     // avatarID: number,
     // ...
   };
   ```

   **Хорошо:**
   ```flow js

   export type User = {
     // ...
     id: number,
     avatarId: number,
     // ...
   };
   ```

   ---

1. Названия полей сущности должны явно указывать на содержание

   **Плохо:**
   ```flow js
   import type {RegionId} from '@self/root/src/entities/region';

   export type Outlet = {
     // ...
     // Под этим полем лежит идентификатор Outlet'а.
     region: RegionId,
     // ...
   };
   ```

   **Хорошо:**
   ```flow js
   import type {RegionId} from '@self/root/src/entities/region';

   export type Outlet = {
     // ...
     regionId: RegionId,
     // ...
   };
   ```

   **Причины:**
   Улучшает семантические связи в коде, ограничивает способы применения данных, уменьшая вероятность ошибки.
