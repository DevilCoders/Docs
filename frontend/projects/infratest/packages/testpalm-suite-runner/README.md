# testpalm-suite-runner

> API для создания и запуска тест-ранов из заранее сконфигурированных тест-сьютов.

## Установка

```shell
npm install @yandex-int/si.ci.testpalm-suite-runner --registry=https://npm.yandex-team.ru
```

## Использование

```ts
import getRunner, { Options, ConfigSuite } from '@yandex-int/si.ci.testpalm-suite-runner';

const runner = getRunner('testpalm-project-id', {} as Options);

(async () => {
  const runningTestSuites = await runner.start([{} as ConfigSuite]);
})();
```

## API

### (projectId, [options]) => Runner

> Возвращает раннер.

#### `projectId`

* Type: `string`

Идентификатор проекта в TestPalm.

#### `options`

* Type: [`Options`](./src/types/index.ts)

### Runner

#### .start(suites) => [`RunningSuite[]`](./src/types/index.ts)

> Создаёт и запускает набор тест-ранов в соответствии с описанными тест-сьютами.

##### suites

* Type: [`ConfigSuite[]`](./src/types/index.ts)

Массив описаний запускаемых тест-сьютов.
