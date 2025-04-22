Использование
=============

Описание модели
---------------

Параметры и возвращаемый тип модели описываются классами со специальными декораторами.

У свойств можно использовать несколько декораторов (список ниже), но не обязательно.

Сама модель описывается классе который наследуется от [`duffman.Model`](https://github.yandex-team.ru/personal-services/frontend/blob/dev/packages/duffman/lib/model.ts#L10) и должна иметь метод `action`. Так же класс может иметь **статические** свойства `noAuth`, `noCkey` (соответствуют флагам `NO_AUTH` и `NO_CKEY`) и свойство `modelParams`. Пока в нём можно описать только что некоторые поля параметров должны быть принудительно завёрнуты в `HiddenParam`. Такие поля в описании класса должны иметь тип `HiddenParam<sometype>`. Даффман автоматически добавит тип `sometype` в разрешённые типы для этого поля.

```ts
import { Model } from '@duffman-int/core';
import { Description, Tag, Pattern } from '@duffman-int/decorators';

export class CheckUserParams {
    @Description('TVM2 user ticket. String either plain or wrapped in HiddenParam class')
    userTicket: HiddenParam<string>;
}

export class CheckUserResult {
    @Description('UID — User id')
    @Pattern(/^\d+$/)
    uid: string;

    @Description('Array of additional uids')
    uids: string[];

    @Description('Parsed debug data')
    debug: string;

    @Description('Logging safe string (ticket w/o signature)')
    logging: string;
}

// где-то определён
interface TvmServiceCore { ... }

@Tag('tvm')
@Description('Validate TVM2 user ticket')
export default class CheckUser extends Model<CheckUserParams, CheckUserResult, TvmServiceCore> {
    async action(params: CheckUserParams, core: TvmServiceCore): Promise<CheckUserResult> {
        // ...
    }

    static modelParams = {
        userTicket: { hidden: true }
    } as const;

    static noAuth = true;
}
```

Сборка
------
Для сборки используется пакет `ttypescript`.

В `tsconfig.json` добавляем секцию плагинов:
```json
"plugins": [
    {
        "transform": "@ps-int/duffman-doc/transform"
    }
]
```
Вместо запуска `tsc` выполняем команду `ttsc`. Все остальные параметры командной строки не менятюся. После сборки рядом с js-файлом модели появится yaml-файл с описанием этой модели.

Сборка документации
-------------------
В пакете есть команда `build-doc-models`, она принимает два параметра: файл и имя экспорта моделей.
```sh
npx --no-install build-doc-models models/index.ts models
```

Пример:
```typescript
// models/index.ts
import vdirect from './sba/vdirect';
import staffAffiliation from './staff-api/staff-affiliation';

export const models = {
    vdirect: vdirect,
    'staff-affiliation': staffAffiliation
} as const;
```

Декораторы
----------
[src](./src/schema.ts)

Ниже `~тип` указывает к какому типу можно применять декоратор.

* `Integer(min?: number, max?: number)~number`. Задаёт тип `integer` (вместо `number`). Параметры `min`/`max` превращаются соответственно в ключевые слова `minimum` и `maximum`.
* `MinLength(min: number)~string`. Задаёт ключевое слово `minLength`.
* `Pattern(pattern: RegExp | string)~string`. Задаёт ключевое слово `pattern`.
* `Title(title: string)~any`, `Description(description: string)~any` — задают `title` и `description`. Можно задавать как отдельным свойствам, так и классам.
* `Tag(...tag: string[])`. Теги для документации. Можно задавать только классу модели.


Соответствие типов и схемы
--------------------------
* `LiteralType` → `const`
* `string`, `number`, `boolean`
* `TYPE[]`, `Array<TYPE>` → array of `TYPE`
* `const1 | const2 | ...` → `enum`
* `type1 | type2 | ...` → `oneOf`
* `Hidden<TYPE>` → `TYPE`
* `interface`, `class` → вынести в отдельные описания?
