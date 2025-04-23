# testpalm-united-runner

> Код раннера для объединённой схемы запуска тестирования на асессорах.

## Установка

```shell
npm install @yandex-int/si.ci.testpalm-united-runner --registry=https://npm.yandex-team.ru
```

## Использование

```js
const tpurFactory = require('@yandex-int/si.ci.testpalm-united-runner');

const runner = tpurFactory({
  hitmanToken: argv.hitmanToken,
  testPalmToken: argv.testpalmToken
});

(async () => {
  const version = await runner.prepare({ /* Версия, сформированная yml2tsv */ });

  await runner.start(version);
})();
```

## API

### .prepare(runs, options)

Создаёт версию с тест-ранами для переданного конфига.

#### runs

* Type: `Run[]`

См. [#Run](../yml2tsv/typings/formatters/united.d.ts)

### .run(version, options)

Запускает переданную версию на асессорах.

#### version

См. [#Version](./typings/index.d.ts)
