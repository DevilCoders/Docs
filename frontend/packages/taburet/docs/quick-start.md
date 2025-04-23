## Быстрый старт
### Создание адаптера
Для каждой фичи создается папка в директории `src/features` с названием фичи, например `src/features/Smile`.

Код адаптера размещается в файле `src/features/Smile/Smile.server.ts`.

Класс обязательно должен содержать метод `transform`, который возвращает данные, необходимые для дальнейшей отрисовки блока:
```ts
import { Adapter } from '@yandex-int/taburet';

export class AdapterSmile extends Adapter {
    transform() {
        return {
            username: this.snippet.username,
            text: 'Smile to $username'
         };
    }
}
```

### Создание реестра и добавление в него адаптера
Все адаптеры хранятся в реестрах. Основные реестры находятся в папке `src/features/.registry`.

Для каждой платформы создается свой реестр. Например, для платформы `desktop` нужно создать файл `src/features/.registry/desktop.ts`

> __NB:__ Платформа в этом случае — один из возможных вариантов организации кода. Если в вашем проекте их нет, то можно назвать реестр просто .registry/index.ts

Внутри файла создается экземпляр класса `AdaptersRegistry`, в который добавляется созданный нами адаптер.
Для добавления адаптера в реестр используется метод `set`, принимающий на вход объект, описывающий адаптер (тип и необязательное поле подтипа), а также сам адаптер:
```ts
import { AdapterRegistry } from '@yandex-int/taburet';
import { AdapterSmile } from 'src/features/Smile/Smile.server'

const base = new AdapterRegistry('desktop');

base.set({ type: 'smile', subtype: 'wide' }, AdapterSmile);

export default base;
```

### Используем рантайм для подключения адаптеров в приложении
В коде вашего приложения создаем экземпляр класса `AdaptersRuntime`, передавая в конструктор наш реестр с адаптером `AdapterSmile` и название платформы.
Пересоздавать экземпляр между запросами к приложению не нужно:
```ts
import { AdapterRuntime, Assets } from '@yandex-int/taburet';
import AdaptersRegistry as base from 'src/features/.registry/desktop.ts';

const runtime = new AdapterRuntime({
    adapters: {
        base,
        experiments,  /* эксперименты будут рассмотрены отдельно */
        componentsExperiments, /* эксперименты с компонентами */
    },
    platform: 'desktop',
    assets: new Assets('desktop', new AssetsDevProvider()) /* ассеты будут рассмотрены отдельно */
});
```

### Запуск подходящего адаптера в Runtime
Чтобы выполнить код адаптера `AdapterSmile`, нужно обратиться к методу `select` рантайма:
```ts
const context = { expFlags: {} }; /* см. "Эксперементальные компоненты" */
const snippet = { type: 'smile', subtype: 'wide', username: 'Kate' };

runtime.select({ context, snippet });
```

Внутри метод `select` производит поиск по реестру, находит подходящий адаптер (`type`/`subtype` сниппета должны совпадать с `type`/`subtype` ключа при добавлении адаптера в реестр).

Созданный выше адаптер будет найден в реестре, если в метод `select` в классе `Runtime` передать объект `{ type: 'smile', subtype: 'wide', username: 'Kate' }`

Далее у созданного экземпляра адаптера вызывается метод `transform`. Результат метода `transform` заворачивается в структуру `{ data, meta }`:
```ts
return {
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
};
```

### Отладка
Чтобы увидеть отладочную информацию Табурета, используйте переменную окружения `NODE_DEBUG`:

- `taburet:*` - для всей информации
- `taburet:runtime` - только про рантайм
- `taburet:registry` - только про реестры
