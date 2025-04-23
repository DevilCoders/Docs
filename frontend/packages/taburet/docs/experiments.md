## Эксперименты с адаптерами
### Создание экспериментального адаптера
Для каждого эксперимента создается папка в директории `src/experiments` с названием эксперимента, например `src/experiments/smile_reverse`.
Внутри размещается папка `features`, содержащая папку с названием базовой фичи, над которой ставится эксперимент.
В нашем случае, это фича под названием `Smile`.
Код экспериментального адаптера размещается в файле `Smile.server.ts`

Таким образом, путь до экспериментального адаптера выглядит так:

`src/experiments/smile_reverse/features/Smile/Smile.server.ts`

Экспериментальный адаптер должен экспортировать функцию, которая возвращает экспериментальный класс фичи, отнаследованный от базового адаптера `taburet/Adapter` или от неэкспериментального класса фичи:
```ts
import { AdapterSmile as AdapterBase } from '../../../../features/Smile';

export function adapterSmileReverse(Base: typeof AdapterBase) {
    return class AdapterSmile extends Base {
        transform() {
            return {
                username: this.snippet.username,
            	text: 'Reverse smile to $username'
            };
        }
    };
}
```

### Создание экспериментального реестра и добавление в него адаптера
Все эксперементальные реестры находятся в папке `src/experiments/.registry`.

Для каждой платформы создается свой реестр. Например, для платформы `desktop`, нужно создать файл `src/experiments/.registry/desktop.ts`.

> __NB:__ Платформа в этом случае — один из возможных вариантов организации кода. Если в вашем проекте их нет, то можно назвать реестр просто .registry/index.ts

Внутри файла создается экземпляр класса `AdaptersExpRegistry`, в который добавляется созданный нами адаптер.
Для добавления адаптера в реестр используется метод `set`, принимающий на вход:
* название флага, под которым проводится эксперимент
* объект, описывающий адаптер (тип и необязательное поле подтипа)
* экспериментальная реализация адаптера

```ts
import { AdapterExpRegistry } from '@yandex-int/taburet';
import { adapterSmileReverse, adapterSmileSad } from 'src/experiments/smile_reverse/Smile/Smile.server'

const experiments = new AdapterExpRegistry('desktop');

experiments.set('smile_reverse', { type: 'smile'}, adapterSmileReverse);

export default experiments;
```

### Используем рантайм для подключения адаптеров в приложение
В коде вашего приложения создаем экземпляр класса `AdaptersRuntime`, передавая в конструктор наш реестр с адаптером `adapterSmileReverse` и название платформы.
Пересоздавать экземпляр между запросами к приложению не нужно:
```ts
import { AdapterRuntime, Assets } from '@yandex-int/taburet';
import AdaptersExpRegistry as experiments from 'src/experiments/.registry/desktop.ts';

const runtime = new AdapterRuntime({
    adapters: {
        base, /* реестр базовых адаптеров, см. "Быстрый старт" */
        experiments,
        componentsExperiments /* реестр экспериментов с компонентами */
    },
    platform: 'desktop',
    assets: new Assets('desktop', new AssetsDevProvider()) /* ассеты будут рассмотрены отдельно */
});
```

### Запуск подходящего экспериментального адаптера в Runtime
Чтобы выполнить код адаптера `adapterSmileReverse`, нужно обратиться к методу `select` рантайма.
В объекте `context.expFlags` нужно указать все активные флаги.
Флаг указывается в формате "ключ-значение", где ключ это название флага, а значение это любая строка или число:
```ts
const context = { expFlags: { smile_reverse: '1' } };
const snippet = { type: 'smile', username: 'Kate' };

runtime.select({ context, snippet });
```
Отключить экспериментальный адаптер можно передав в качестве значения соответствующего ему флага строку `'null'`;

Внутри метод `select` производит поиск по экспериментальному реестру с учетом активных флагов, находит подходящий адаптер (`type`/`subtype` сниппета должны совпадать с `type`/`subtype` ключа при добавлении адаптера в реестр).

Созданный выше адаптер будет найден в реестре, если в метод `select` в классе `Runtime` передать объект `{ type: 'smile', username: 'Kate' }`

В ситуации, когда в экспериментальном реестре находится больше одного подходящего эксперимента, происходит процесс "наследования" адаптеров.
Берется базовый адаптер, на основе которого проводится эксперимент, к нему применяется адаптер эксперимента, тем самым получая класс адаптера с новым функционалом.
После применения всех экспериментов, получается единый адаптер, экземпляр которого создатется далее.
Порядок "наследования" определяется порядком добавления экспериментальных адаптеров в реестр.

Далее у созданного экземпляра адаптера вызывается метод `transform`.
Результат заворачивается в структуру `{ data, meta }`:
```ts
{
    // Результат метода transform
    data: {
        username: 'Kate',
        text: 'Smile to $username'
    },
    // Ключ адаптера в реестре
    meta: {
        type: 'smile',
        subtype: 'wide'
    }
}
```

### Работа несколько одновременных экспериментов с одним адаптером
```ts
// src/experiments/.registry/desktop.ts
registry.set('flag_smile_reverse', require('../smile_reverse/features/Smile/Smile@desktop'));
registry.set('flag_smile_sad', require('../smile_sad/features/Smile/Smile@desktop'));
```

Во время работы шаблонов рантайм находит все версии адаптеров фичи, с учетом активных флагов, и строит такую цепочку вызовов:
```ts
const { adapterSmileSad } = require('../smile_sad/features/Smile/Smile@desktop');
const { adapterSmileReverse } = require('../smile_reverse/features/Smile/Smile@desktop');

// реализация адаптера для флага flag_smile_sad
adapterSmileSad(
    // реализация адаптера для флага flag_smile_reverse
    adapterSmileReverse(
        // базовая реализация адаптера, или если ее нет, базовый адаптер (см. src/vendors/taburet/Runtime.ts)
        AdapterSmile || Adapter
    )
)
```

В результате получается цепочка наследования от базовой версии по всем активным экспериментам.
