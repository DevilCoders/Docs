# Реестр по платформам

Библиотека позволяет:
1. удобно переиспользовать компоненты, у которых отличается вёрстка и используемые ресурсы по разным платформам,
2. удобно проводить эксперименты над этими компонентами.

## Использование в компонентах

В папке компонента создаёте файл `index.tsx` со следующим содержанием.
```tsx
import { withPlatform } from 'sakhalin/src/lib/PlatformedRegistry';

import { Component as desktop } from './Component@desktop';
import { Component as phone } from './Component@touch-phone';

export const Component = withPlatform({ desktop, 'touch-phone': phone });
```

Если у компонента совпадает вёрстка для разных платформ, то нужно положить один импорт на все платформы в опциях.
```tsx
import { withPlatform } from 'sakhalin/src/lib/PlatformedRegistry';

import { Component as base } from './Component';

export const Component = withPlatform({ desktop: base, 'touch-phone': base });
```

Если компонент не реализован для какой-то из платформ, то используем заглушку `nullable`.
```tsx
import { withPlatform } from 'sakhalin/src/lib/PlatformedRegistry';
import { nullable as phone } from 'sakhalin/src/utils/functional/nullable';

import { Component as desktop } from './Component@desktop';

export const Component = withPlatform({ desktop, 'touch-phone': phone });
```


Готово!
Теперь можете использовать `Component` из только что созданного файла, библиотека сама будет подставлять актуальный компонент в зависимости от платформы.

### Примечание
Не помещайте в файл `index.tsx` ничего другого, кроме переиспользования компонента по платформам — это может ухудшить оптимизации и усложнить разработку в дальнейшем.
Размещайте константы и типы в других файлах.

## Использование с модификатором
Процесс похож на использование в компонентах, только нужно использовать `withPlatformMod`.
```tsx
import { withPlatformMod } from 'sakhalin/src/lib/PlatformedRegistry';

import { withYourMod as desktop } from './YourMod@desktop';
import { withYourMod as phone } from './YourMod@touch-phone';

export const withYourMod = withPlatformMod({ desktop, 'touch-phone': phone });
```
<!-- TODO: SAKHALIN-3285 - поддержать экспериментальные уровни
## Создание эксперимента

Для создания эксперимента необходимо создать файл с самим экспериментом.
Располагайте файл по пути `src/experiments/{expFlag}/components.entries/{Component}@{platform}.ts`, где
* `expFlag` — имя флага, под которым включается ваш эксперимент,
* `Component` — имя компонента, для которого вы проводите эксперимент,
* `platform` — платформа, для которой предназначен эксперимент.

```tsx
// Импортируем компонент из index файла — он будет ключом для создания эксперимента.
import { Component } from '@components/Component';
import { createExperiment } from 'sakhalin/src/lib/PlatformedRegistry/PlatformedRegistry';

createExperiment(Component, {
    // Для доставки статики необходимо указать файл эксперимента.
    // Всегда указывайте тут __filename - это простой способ получить путь к текущему файлу.
    filePath: __filename,

    // HOC накладывающий эксперимент.
    // Сам HOC можно вынести в другой файл для удобства.
    enhance: BaseComponent => NewComponent,

    // Возможность указать условие применение эксперимента на сервере.
    // Необязательный параметр.
    condition: (context: ISerpContext, { type, subtype }: IRegistryKey) => true;
});
```
Параметр `condition` опционален. Если его не указывать, то для применения эксперимента достаточно включения флага.
Имя флага автоматически определится из имени папки, где располагается ваш эксперимент.
`condition` принимает в себя первым параметром `context` серпа, где вы можете завязаться на дополнительные условия.
Например, на значения вашего флага или наличие другого эксперимента.
Второй параметр `{ type, subtype }` позволяет вам ограничить условие применения эксперимента по фиче.
Это позволит вам не присылать статику эксперимента, если фичи нет на странице.

После этого необходимо добавить импорт этого файла в `src/experiments/.registry/{platform}.ts`, чтобы сервер знал о вашем эксперименте
```tsx
import '../{expFlag}/components.entries/{Component}@{platform}';
```
-->
## F.A.Q.

### Использование с pushModule
Обязательно называйте файл с расширением tsx, так как другие расширения pushModule не воспринимает.

Добавьте в конце файла `default export Component`, так как pushModule работает только с импортами по умолчанию.

### Как использовать с @yandex-lego/components?
Создайте на уровне проекта папку, как если бы хотели создать этот компонент сами.
После этого создайте только файл `index.tsx`, с объявлением withPlatform и используйте.

Например вы хотите использовать `@yandex-lego/components/Button`.
Создаём файл index.tsx по пути `src/components/Button/index.tsx`.
Помещаем там следующий код:
```tsx
import { Button as desktop } from '@yandex-lego/components/Button/desktop';
import { Button as phone } from '@yandex-lego/components/Button/touch-phone';

import { withPlatform } from 'sakhalin/src/lib/PlatformedRegistry';

export const Button = withPlatform({ desktop, 'touch-phone': phone });
```

Далее в проекте используем следующим образом.
```tsx
import { Button } from '@components/Button'
```
