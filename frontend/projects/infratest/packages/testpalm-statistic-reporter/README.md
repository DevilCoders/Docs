# testpalm-statistic-reporter

> Инструмент для сбора статистики по данным, полученным из TestPalm.

## Установка

```shell
npm install @yandex-int/si.ci.testpalm-statistic-reporter
```

## Зачем?

У нас есть множество различных утилит, которые собирают данные из TestPalm,
анализируют их, а затем отправляют полученные данные в другое место, например,
для построения какого-либо графика.

Для того, чтобы в каждой такой утилите не писать методы получения, а также
обработки данных, предлагается использовать этот пакет, который инкапсулирует
в себе всю нужную функциональность.

## Использование

> :warning: Требуется токен в переменной окружения `TESTPALM_OAUTH_TOKEN` для
> доступа к TestPalm.

Предполагается, что пользоваться этим пакетом нужно через CLI-обёртку. Тем не
менее вот пример того, как можно использовать этот пакет:

```js
import tsr from '@yandex-int/si.ci.testpalm-statistic-reporter';

(async () => {
  const serviceId = 'serp-js';
  const projectId = 'serp-js-100500';

  await tsr([
      { id: 'first-plugin' },
      {
        id: 'second-plugin',
        options: { statboxToken: 'token' }
      }
    ], { projectId, serviceId });
})();
```

## API

### (plugins, project) => Promise

#### plugins

* Type: [`PluginDescription`](./src/index.ts)

Описание плагинов, которые требуется использовать при запуске.

#### project

##### projectId

* Type: `string`

Идентификатор проекта в TestPalm. Например, `serp-js-100500`.

##### serviceId

* Type: `string`

Идентификатор сервиса. Например, `web4`.

## Написание плагина

Каждый плагин имплементирует интерфейс [`Plugin`](./src/types/plugin.ts), поэтому
проблем с пониманием того, как написать свой плагин быть не должно.

> :book: Знайте, что данные, которые приходят первым аргументом для каждого
> плагина предварительно клонируются, чтобы исключить влияние работы одного плагина
> на другой.

Не забывайте корректно указывать значение для поля `dependencies`, так как на
его основе выбирается наименьший набор данных, который требуется всем плагинам.

> :warning: Модули пакетов должны находиться внутри директории [`plugins`](./src/plugins).

```ts
import { NSPlugin } from '../types/plugin';

const plugin: NSPlugin.Plugin = {
    id: 'my-first-task',

    dependencies: {
        definitions: true
    },

    options: {},

    execute: async (data: NSPlugin.Data) => {
      console.log(`The "${data.projectId}" has "${data.definitions.length} definitions`);
    }
};

export = plugin;
```

После того как плагин написан – его нужно подключить в `plugin/index.ts`:

```ts
import plugin from './plugin-name';

export = {
  [plugin.id]: plugin
};
```
